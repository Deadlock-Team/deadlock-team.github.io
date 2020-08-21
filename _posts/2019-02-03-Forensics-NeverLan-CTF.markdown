---
layout: post
title:  "Forensics"
date:   2019-02-03 00:00:01 -0300
categories: [CTF,FORENSIC,NeverLAN CTF]
author: andersongomes001
event: "NeverLAN CTF 2019"
tags: [CTF,FORENSIC,NeverLAN CTF]
description: "Writeup Forensics."
image: "/assets/images/writeups/ISxr9xi.png"
---

___
## Desafios
[Return of the Sith - Part 1](#title-return-of-the-sith---part-1)
[Return of the Sith - Part 2](#title-return-of-the-sith---part-2)
[Return of the Sith - Part 3](#title-return-of-the-sith---part-3)
___

## Title: Return of the Sith - Part 1

### Points: 100

We've been given a specific forensics case by a really grumpy customer. He starting smashing consoles and stuff when he found out what happened ([video](https://www.youtube.com/watch?v=6ZrdPMU-Ofw)).

Looks like he was hacked. Here's the VM Download you'll use:

[maquina virtual](https://files.utahcon.org/file/neverlan/NeverLAN%20CTF%2064-bit%2018.04.1.7z)

7z md5 hash:  `cfb95b3d837602f1932fa309aafd8aff`

Password to uncompress:  `the_path_to_the_dark_side`

User's Password:  `ikilledmydad`

Challenge:

After a quick gander, we realized the user installed VNC with a crappy password. Can you get the password he used so we can prove to him it was bad?

Note: The password is the flag, it is not in the flag{} format.

### *Resolução:*

```bash
$ git clone https://github.com/jeroennijhof/vncpwd.git
Cloning into 'vncpwd'...
remote: Enumerating objects: 28, done.
remote: Total 28 (delta 0), reused 0 (delta 0), pack-reused 28
Unpacking objects: 100% (28/28), done.
$ cd vncpwd/
$ gcc -o vncpwd vncpwd.c d3des.c
$ scp kyloren@192.168.1.7:~/.vnc/passwd ./
kyloren@192.168.1.7's password: 
passwd                                                                                                             100%    8     1.7KB/s   00:00    
$ ./vncpwd passwd 
Password: darthvad

```
FLAG: **darthvad**

___

## Title: Return of the Sith - Part 2

### Points: 100

We've been given a specific forensics case by a really grumpy customer. He starting smashing consoles and stuff when he found out what happened ([video](https://www.youtube.com/watch?v=6ZrdPMU-Ofw)).

Looks like he was hacked. Use the VM provided in Part 1.

Challenge:

Since they got in with VNC, they were locked into his user account, without any root access.  _The user used SUDO for 'protection' so that means he’s safe from the attacker getting his password, right?_  The goal here is to figure out if the user was able to escalate to root without having the user's password. DO BE CAREFUL since messing with a VM has the ability to remove traces of what you’re looking for. This IS a forensics challenge.

_Edit_: the point value was posted wrong. Droping it to 100 like it should have been.


### *Resolução:*

```bash
$ history | grep sudo
...
vim .xd/sudo 
cat .xd/sudo 
...
```

RUN:
```bash
vim .xd/sudo
```

![](/assets/images/writeups/ISxr9xi.png)

****flag{check-out-my-sudo-stealer}****

___

## Title: Return of the Sith - Part 3

### Points: 100

We've been given a specific forensics case by a really grumpy customer. He starting smashing consoles and stuff when he found out what happened ([video](https://www.youtube.com/watch?v=6ZrdPMU-Ofw)).

Looks like he was hacked. Use the VM provided in Part 1.

Challenge:

Ok, great. They had full root access, did they leave anything else behind? Any other backdoor?

Notes: This one is also not in the flag format, but the flag will be the 'identifer' of the back door. If you think you've found it, but it's not accepting your challenge, you can message bashNinja on the  [NeverLAN Slack](https://neverlanctfpublic.slack.com/join/shared_invite/enQtNTQwMDQzMTM5OTkwLWE4NThlODNkNTdjNGFhODkyZTdlYzliOGI4MzBiZDFkMDJlNjg3MjdkNDQ2MTRmOGM3NzVmZDE3ZTFhNjAzMzU)  and he will verify if you've gotten it correct or not.

### *Resolução:*

Usuário `mysql` com poderes de superusuário e banco de dados mysql não instalado na máquina.

```bash
$ history | grep mysql

...
/usr/bin/sudo usermod -a -G sudo mysql
/usr/bin/sudo passwd mysql
...
```
FLAG: **mysql**
