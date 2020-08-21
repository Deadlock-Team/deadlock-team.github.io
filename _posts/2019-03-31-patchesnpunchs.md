---
layout: post
title:  "Patches' Punches"
date:   2019-03-31 12:00:01 -0300
categories: [CTF,REVERSE,Sunshine CTF 2019]
author: andersongomes001
event: "Sunshine CTF 2019"
tags: [CTF,REVERSE,Sunshine CTF 2019]
description: "Writeup Patches' Punches"
image: ""
---

gdb patches 

``` bash
GNU gdb (Ubuntu 7.11.1-0ubuntu1~16.5) 7.11.1
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000051d <+0>: lea    0x4(%esp),%ecx
   0x00000521 <+4>: and    $0xfffffff0,%esp
   0x00000524 <+7>: pushl  -0x4(%ecx)
   0x00000527 <+10>:    push   %ebp
   0x00000528 <+11>:    mov    %esp,%ebp
   0x0000052a <+13>:    push   %ebx
   0x0000052b <+14>:    push   %ecx
   0x0000052c <+15>:    sub    $0x10,%esp
   0x0000052f <+18>:    call   0x5c6 <__x86.get_pc_thunk.ax>
   0x00000534 <+23>:    add    $0x1aa4,%eax
   0x00000539 <+28>:    movl   $0x1,-0x10(%ebp)
   0x00000540 <+35>:    cmpl   $0x0,-0x10(%ebp)
   0x00000544 <+39>:    jne    0x5a3 <main+134>
   0x00000546 <+41>:    movl   $0x0,-0xc(%ebp)
   0x0000054d <+48>:    jmp    0x580 <main+99>
   0x0000054f <+50>:    lea    0xc8(%eax),%ecx
   0x00000555 <+56>:    mov    -0xc(%ebp),%edx
   0x00000558 <+59>:    add    %ecx,%edx
   0x0000055a <+61>:    movzbl (%edx),%edx
   0x0000055d <+64>:    mov    %edx,%ecx
   0x0000055f <+66>:    mov    -0xc(%ebp),%edx
   0x00000562 <+69>:    mov    0x48(%eax,%edx,4),%edx
   0x00000569 <+76>:    sub    %edx,%ecx
   0x0000056b <+78>:    mov    %ecx,%edx
   0x0000056d <+80>:    mov    %edx,%ebx
   0x0000056f <+82>:    lea    0xc8(%eax),%ecx
   0x00000575 <+88>:    mov    -0xc(%ebp),%edx
   0x00000578 <+91>:    add    %ecx,%edx
   0x0000057a <+93>:    mov    %bl,(%edx)
   0x0000057c <+95>:    addl   $0x1,-0xc(%ebp)
   0x00000580 <+99>:    cmpl   $0x1e,-0xc(%ebp)
   0x00000584 <+103>:   jle    0x54f <main+50>
   0x00000586 <+105>:   sub    $0x8,%esp
   0x00000589 <+108>:   lea    0xc8(%eax),%edx
   0x0000058f <+114>:   push   %edx
   0x00000590 <+115>:   lea    -0x1988(%eax),%edx
   0x00000596 <+121>:   push   %edx
   0x00000597 <+122>:   mov    %eax,%ebx
   0x00000599 <+124>:   call   0x3b0 <printf@plt>
   0x0000059e <+129>:   add    $0x10,%esp
   0x000005a1 <+132>:   jmp    0x5b7 <main+154>
   0x000005a3 <+134>:   sub    $0xc,%esp
   0x000005a6 <+137>:   lea    -0x1970(%eax),%edx
   0x000005ac <+143>:   push   %edx
   0x000005ad <+144>:   mov    %eax,%ebx
   0x000005af <+146>:   call   0x3b0 <printf@plt>
   0x000005b4 <+151>:   add    $0x10,%esp
   0x000005b7 <+154>:   mov    $0x0,%eax
   0x000005bc <+159>:   lea    -0x8(%ebp),%esp
   0x000005bf <+162>:   pop    %ecx
   0x000005c0 <+163>:   pop    %ebx
   0x000005c1 <+164>:   pop    %ebp
   0x000005c2 <+165>:   lea    -0x4(%ecx),%esp
   0x000005c5 <+168>:   ret    
End of assembler dump.
(gdb) b *main+39
Ponto de parada 1 at 0x544
(gdb) r
Starting program: /home/andersongomes001/patches 

Breakpoint 1, 0x56555544 in main ()
(gdb) jump *main+41
Continuando em 0x56555546.
Hurray the flag is sun{To0HotToHanDleTo0C0ldToH0ld!}
[Inferior 1 (process 10863) exited normally]
(gdb) q
```

flag => sun{To0HotToHanDleTo0C0ldToH0ld!}
