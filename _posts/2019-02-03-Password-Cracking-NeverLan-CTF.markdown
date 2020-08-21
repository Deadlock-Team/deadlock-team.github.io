---
layout: post
title:  "Password Cracking"
date:   2019-02-03 00:00:01 -0300
categories: [CTF,CRYPTO,NeverLAN CTF]
author: andersongomes001
event: "NeverLAN CTF 2019"
tags: [CTF,CRYPTO,NeverLAN CTF]
description: "Writeup Password Cracking."
image: ""
---
___
## Desafios
[PW 3](#title-pw-3) - [PW 5](#title-pw-5) - [PW 6](#title-pw-6) - [PW 8](#title-pw-8) - [PW 11](#title-pw-11) - [PW 13](#title-pw-13) - [PW 15](#title-pw-15) - [PW 16](#title-pw-16)

___

Execute:

```bash
john --wordlist=rockyou.txt passwords.txt
```

Resultado:

```bash

$1$3EWs3fw8$lXtCH8R38PUZbtLhoCw.d/:viking
$1$d8qBkGme$gNZFeDbg20rDdQw/ap3Zh/:darthvader
$1$8Xzzo2Un$4RCP.BvWE7GNJ/QIRnMmE1:indianajones
$1$tIDzBW38$Io93.ZnYWv1HaBbSKW8hM.:zevlag
$1$66dlQFzj$dFDKADbdgd/7Hs9iLM7WG1:123456seven
$1$VXpHmtKC$rtvIjzeg3QtBpfgEsJo/N.:pwned
$1$DsNwIwCB$GJtdNZe.zC9/CfCLkIU5L.:n30

```

Execute:

```bash
john --wordlist=10-million-password-list-top-1000000.txt passwords.txt
```

Resultado:

```bash
$1$RVgjU0zp$alpNzFXw/jc8/V/HkXNga.:neverlan
```

[SecList wordlist](https://github.com/danielmiessler/SecLists)

___


## Title: PW 13

### Points: 30

Oh no. We did it. We're releasing password cracking challenges on the  **last**  day of the CTF. WHAT ARE YOU GOING TO DO!?!? You don't have a  _ton_  of time to brute force these.

This is our little way of saving the planet by saving your graphics cards from sucking all its' energy.

Enjoy!

Hash:  `$1$3EWs3fw8$lXtCH8R38PUZbtLhoCw.d/`

Note: These challenges aren't in any order of difficulty or anything. They're just here.

FLAG: **viking**

___


## Title: PW 5

### Points: 30

Oh no. We did it. We're releasing password cracking challenges on the  **last**  day of the CTF. WHAT ARE YOU GOING TO DO!?!? You don't have a  _ton_  of time to brute force these.

This is our little way of saving the planet by saving your graphics cards from sucking all its' energy.

Enjoy!

Hash:  `$1$d8qBkGme$gNZFeDbg20rDdQw/ap3Zh/`

Note: These challenges aren't in any order of difficulty or anything. They're just here.

FLAG: **darthvader**

___


## Title: PW 3

### Points: 30

Oh no. We did it. We're releasing password cracking challenges on the  **last**  day of the CTF. WHAT ARE YOU GOING TO DO!?!? You don't have a  _ton_  of time to brute force these.

This is our little way of saving the planet by saving your graphics cards from sucking all its' energy.

Enjoy!

Hash:  `$1$8Xzzo2Un$4RCP.BvWE7GNJ/QIRnMmE1`

Note: These challenges aren't in any order of difficulty or anything. They're just here.

FLAG: **indianajones**

___

## Title: PW 15

### Points: 30

Oh no. We did it. We're releasing password cracking challenges on the  **last**  day of the CTF. WHAT ARE YOU GOING TO DO!?!? You don't have a  _ton_  of time to brute force these.

This is our little way of saving the planet by saving your graphics cards from sucking all its' energy.

Enjoy!

Hash:  `$1$tIDzBW38$Io93.ZnYWv1HaBbSKW8hM.`

Note: These challenges aren't in any order of difficulty or anything. They're just here.


FLAG: **zevlag**

___


## Title: PW 8

### Points: 30

Oh no. We did it. We're releasing password cracking challenges on the  **last**  day of the CTF. WHAT ARE YOU GOING TO DO!?!? You don't have a  _ton_  of time to brute force these.

This is our little way of saving the planet by saving your graphics cards from sucking all its' energy.

Enjoy!

Hash:  `$1$66dlQFzj$dFDKADbdgd/7Hs9iLM7WG1`

Note: These challenges aren't in any order of difficulty or anything. They're just here.

FLAG: **123456seven**

___


## Title: PW 6

### Points: 30

Oh no. We did it. We're releasing password cracking challenges on the  **last**  day of the CTF. WHAT ARE YOU GOING TO DO!?!? You don't have a  _ton_  of time to brute force these.

This is our little way of saving the planet by saving your graphics cards from sucking all its' energy.

Enjoy!

Hash:  `$1$VXpHmtKC$rtvIjzeg3QtBpfgEsJo/N.`

Note: These challenges aren't in any order of difficulty or anything. They're just here.

FLAG: **pwned**

___


## Title: PW 11

### Points: 30

Oh no. We did it. We're releasing password cracking challenges on the  **last**  day of the CTF. WHAT ARE YOU GOING TO DO!?!? You don't have a  _ton_  of time to brute force these.

This is our little way of saving the planet by saving your graphics cards from sucking all its' energy.

Enjoy!

Hash:  `$1$DsNwIwCB$GJtdNZe.zC9/CfCLkIU5L.`

Note: These challenges aren't in any order of difficulty or anything. They're just here.


FLAG: **n30**

___


## Title: PW 16

### Points: 30

Oh no. We did it. We're releasing password cracking challenges on the  **last**  day of the CTF. WHAT ARE YOU GOING TO DO!?!? You don't have a  _ton_  of time to brute force these.

This is our little way of saving the planet by saving your graphics cards from sucking all its' energy.

Enjoy!

Hash:  `$1$RVgjU0zp$alpNzFXw/jc8/V/HkXNga.`

Note: These challenges aren't in any order of difficulty or anything. They're just here.

FLAG: **neverlan**


