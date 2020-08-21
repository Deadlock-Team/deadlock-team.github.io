---
layout: post
title:  "BashNinjas Bash Games"
date:   2019-02-03 00:00:01 -0300
categories: [CTF,BASH,NeverLAN CTF]
author: andersongomes001
event: "NeverLAN CTF 2019"
tags: [CTF,BASH,NeverLAN CTF]
description: "O BashNinjas Bash Games são 10 desafios para testar as habilidades dos players ctf com o bash."
image: "/assets/images/writeups/gsGBQnd.png"
---

![](/assets/images/writeups/gsGBQnd.png)

___
## Desafios
[Bash 1](#title-bash-1) - [Bash 3](#title-bash-2) - [Bash 3](#title-bash-3) - [Bash 4](#title-bash-4) - [Bash 5](#title-bash-5) - [Bash 6](#title-bash-6) - [Bash 7](#title-bash-7) - [Bash 8](#title-bash-8) - [Bash 9](#title-bash-9) - [Bash 10](#title-bash-10)

___


## Title: Bash 1
### Points: 25
ssh -p 3333 neverlan@157.230.73.80
password:neverlan

## Resolução:

```bash
Level: neverlan

Instructions
═════════════════════════════════════════════════════════════════════════════════
For this challenge you need to get the contents of Welcome.txt

cat Welcome.txt
----------------------------------------------------------------------------
                  __          __  _
                  \ \        / / | |
                   \ \  /\  / /__| | ___ ___  _ __ ___   ___
                    \ \/  \/ / _ \ |/ __/ _ \| '_ ` _ \ / _ \
                     \  /\  /  __/ | (_| (_) | | | | | |  __/
                      \/  \/ \___|_|\___\___/|_| |_| |_|\___|

----------------------------------------------------------------------------

      .m.                                                          .m.
      (;)                                                          (;)
      (;)                                                          (;)
      (;)                                                          (;)
   .  (;)  .                                                    .  (;)  .
   |\_(;)_/|                                                    |\_(;)_/|
    )     (                                                      )     (
   |/ )|( \|                                                    |/ )|( \|
     ( o )                 You have entered the                   ( o )
      )8(                     Path of Honor                        )8(
     ( o )                                                        ( o )
      )8(             We're going to start our adventure           )8(
     ;|S|;          talking about the neverlan honor code.        ;|S|;
     ||S||                                                        ||S||
     ||S||                   level1 password:                     ||S||
     ||S|<          act-with-honor-and-honor-will-aid-you         ||S|<
     ||S||                                                        ||S||
     ||S||                                                        ||S||
     ||S||                                                        ||S||
     ||S||                                                        ||S||
     >|S||                                                        >|S||
     ||S||                                                        ||S||
     ||S||                                                        ||S||
     \\ //                                                        \\ //
      \V/                                                          \V/
       V                                                            V

```
___
## Title: Bash 2
### Points: 50
ssh -p 3333 level1@157.230.73.80

Use Bash 1 password

## Resolução:

```bash
Level: level1

Instructions
═════════════════════════════════════════════════════════════════════════════════
We're going to play hide and seek. I'll hide a file and you seek for it.


cat .honor-code.txt
# our honor code

 What are you best at? What is your passion? How can you provide the most good to the world? These are some of the questions that you should ask yourself.

Our Code of Conduct is based on the R00tz Asylum's Honor Code: https://r00tz.org/honor-code

# PRINCIPLES

neverlan kids focuses on these fundamental truths about the universe:

- The world is one. We are all connected.
- These connections are growing stronger and faster everyday.
- Chaos controls the connections.
- Focus controls the chaos.
- You control the focus.


# VALUES

Please remember these values in everything you do:

- Only do good
- Always do your best
- Constantly improve
- Innovate
- Think long-term
- Be positive
- Visualize it
- Inspire others
- Go big & have fun!  


# RULES

The Internet is a small place. Word gets around, fast.

Follow these rules at all times:

- Only hack things you own
- Do not hack anything you rely on
- Respect the rights of others
- Know the law, the possible risk, and the consequences for breaking it
- Find a safe playground

level2 password: the-only-path-to-honor-is-to-stick-to-your-chosen-code
```

___
## Title: Bash 3

### Points: 75

ssh -p 3333 level2@157.230.73.80

Use Bash 2 password

## Resolução:

```bash
Level: level2

Instructions
═════════════════════════════════════════════════════════════════════════════════
Ok. So you found the hidden file. How about trying to find the password in plain
sight? You'll have to figure out how to sift through the muck though...

cat canyoufindme.txt | grep 'level3'
level3:child-of-honor

```
___

## Title: Bash 4

### Points: 100

ssh -p 3333 level3@157.230.73.80

Use Bash 3 password

## Resolução:

```bash
Level: level3

Instructions
═════════════════════════════════════════════════════════════════════════════════
So you know how to use grep or some other similar program. Good for you. Now can
you do the same thing with a binary file?


strings random | grep 'level4'
level4:only*hack^things%you$own
```

___

## Title: Bash 5

### Points: 125

ssh -p 3333 level4@157.230.73.80

Use Bash 4 password

## Resolução:

```bash
Level: level4

Instructions
═════════════════════════════════════════════════════════════════════════════════
Nice job on that last level. I'll have to step it up. Alright here is a file,
but I won't tell you what it is. You'll have to figure that out on your own.

gzip -dc nextlevel > flag.txt; cat flag.txt
PRINCIPLES

r00tz kids focuses on these fundamental truths about the universe:

- The world is one. We are all connected.

- These connections are growing stronger and faster everyday.

- Chaos controls the connections.

- Focus controls the chaos.

- You control the focus.

level5:on-my-honor-i-will-do-my-best
```
___
## Title: Bash 6

### Points: 150

ssh -p 3333 level5@157.230.73.80

Use Bash 5 password

## Resolução:

```bash
Level: level5

Instructions
═════════════════════════════════════════════════════════════════════════════════
Look around for more guidance.


cat values.txt 
VALUES

Please remember these values in everything you do:

- Only do good

- Always do your best

- Constantly improve

- Innovate

- Think long-term

- Be positive

- Visualize it

- Inspire others

- Go big & have fun! 

Oh... and you probably want to pull the image file to your computer and look at it.
You don't know how to do that? Google is your friend. 
Something like "Transfer files over SSH" might do the trick.


scp -P 3333 level5@157.230.73.80:/home/level5/Syl.jpg ./
```

open the image and see the flag

![](https://i.imgur.com/F1gwojk.jpg)

level5:have-you-memorized-the-code-yet


___

## Title: Bash 7

### Points: 175

ssh -p 3333 level6@157.230.73.80

Use Bash 6 password

## Resolução:

```bash
Level: level6

Instructions
═════════════════════════════════════════════════════════════════════════════════
Look in level7.txt. You'll have to figure out what to do with that on your own.

level6@son-of-honor:~$ strings level7.txt 
UlVMRVMKClRoZSBJbnRlcm5ldCBpcyBhIHNtYWxsIHBsYWNlLiBXb3JkIGdldHMgYXJvdW5kLCBmYXN0LgoKRm9sbG93IHRoZXNlIHJ1bGVzIGF0IGFsbCB0aW1lczoKCi0gT25seSBoYWNrIHRoaW5ncyB5b3Ugb3duCgotIERvIG5vdCBoYWNrIGFueXRoaW5nIHlvdSByZWx5IG9uCgotIFJlc3BlY3QgdGhlIHJpZ2h0cyBvZiBvdGhlcnMKCi0gS25vdyB0aGUgbGF3LCB0aGUgcG9zc2libGUgcmlzaywgYW5kIHRoZSBjb25zZXF1ZW5jZXMgZm9yIGJyZWFraW5nIGl0CgotIEZpbmQgYSBzYWZlIHBsYXlncm91bmQKCmxldmVsNzp3aGl0ZS1oYXRzLWhhdmUtdmFsdWVzLWFuZC1ydWxlcwo=

level6@son-of-honor:~$ strings level7.txt | base64 -d
RULES

The Internet is a small place. Word gets around, fast.

Follow these rules at all times:

- Only hack things you own

- Do not hack anything you rely on

- Respect the rights of others

- Know the law, the possible risk, and the consequences for breaking it

- Find a safe playground

level7:white-hats-have-values-and-rules
```
___

## Title: Bash 8

### Points: 200

ssh -p 3333 level7@157.230.73.80

Use Bash 7 password

## Resolução:

```bash
Level: level7

Instructions
═════════════════════════════════════════════════════════════════════════════════
This is almost the same thing as the last level, just gotta do one more step.


strings level8.txt | base64 -d > flag
gzip -dc flag 
manifesto.txt000644 000765 000024 00000007276 13257360563 015320 0ustar00miketweaverstaff000000 000000                                ==Phrack Inc.==

                    Volume One, Issue 7, Phile 3 of 10

=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
The following was written shortly after my arrest...

                       \/\The Conscience of a Hacker/\/

                                      by

                               +++The Mentor+++

                          Written on January 8, 1986
=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=

        Another one got caught today, it's all over the papers.  "Teenager
Arrested in Computer Crime Scandal", "Hacker Arrested after Bank Tampering"...
        Damn kids.  They're all alike.

        But did you, in your three-piece psychology and 1950's technobrain,
ever take a look behind the eyes of the hacker?  Did you ever wonder what
made him tick, what forces shaped him, what may have molded him?
        I am a hacker, enter my world...
        Mine is a world that begins with school... I'm smarter than most of
the other kids, this crap they teach us bores me...
        Damn underachiever.  They're all alike.

        I'm in junior high or high school.  I've listened to teachers explain
for the fifteenth time how to reduce a fraction.  I understand it.  "No, Ms.
Smith, I didn't show my work.  I did it in my head..."
        Damn kid.  Probably copied it.  They're all alike.

        I made a discovery today.  I found a computer.  Wait a second, this is
cool.  It does what I want it to.  If it makes a mistake, it's because I
screwed it up.  Not because it doesn't like me...
                Or feels threatened by me...
                Or thinks I'm a smart ass...
                Or doesn't like teaching and shouldn't be here...
        Damn kid.  All he does is play games.  They're all alike.

        And then it happened... a door opened to a world... rushing through
the phone line like heroin through an addict's veins, an electronic pulse is
sent out, a refuge from the day-to-day incompetencies is sought... a board is
found.
        "This is it... this is where I belong..."
        I know everyone here... even if I've never met them, never talked to
them, may never hear from them again... I know you all...
        Damn kid.  Tying up the phone line again.  They're all alike...

        You bet your ass we're all alike... we've been spoon-fed baby food at
school when we hungered for steak... the bits of meat that you did let slip
through were pre-chewed and tasteless.  We've been dominated by sadists, or
ignored by the apathetic.  The few that had something to teach found us will-
ing pupils, but those few are like drops of water in the desert.

        This is our world now... the world of the electron and the switch, the
beauty of the baud.  We make use of a service already existing without paying
for what could be dirt-cheap if it wasn't run by profiteering gluttons, and
you call us criminals.  We explore... and you call us criminals.  We seek
after knowledge... and you call us criminals.  We exist without skin color,
without nationality, without religious bias... and you call us criminals.
You build atomic bombs, you wage wars, you murder, cheat, and lie to us
and try to make us believe it's for our own good, yet we're the criminals.

        Yes, I am a criminal.  My crime is that of curiosity.  My crime is
that of judging people by what they say and think, not what they look like.
My crime is that of outsmarting you, something that you will never forgive me
for.

        I am a hacker, and this is my manifesto.  You may stop this individual,
but you can't stop us all... after all, we're all alike.

                               +++The Mentor+++

level8:my-wit-ran-out-5-levels-ago

```
___
## Title: Bash 9

### Points: 225

ssh -p 3333 level8@157.230.73.80

Use Bash 8 password

## Resolução:

```bash
Level: level8

Instructions
═════════════════════════════════════════════════════════════════════════════════
Your goal here is to decrypt `level9.enc`. There's a clue around here somewhere.

cat .clue 
aes-256-cbc encryption password: level9please

openssl aes-256-cbc -d -a -in level9.enc -out flag
enter aes-256-cbc decryption password: 

cat flag 
level9:please-someone-help

```
___
## Title: Bash 10

### Points: 250

ssh -p 3333 level9@157.230.73.80

Use Bash 9 password

## Resolução:

```bash
Level: level9

Instructions
═════════════════════════════════════════════════════════════════════════════════
Congrats. You win. Almost... You've just got to get the flag in final.txt

-----------------------------------------------------------------
You didn't say the magic word
Goodbye
Connection to 157.230.73.80 closed.


ssh -tv -p 3333 level9@157.230.73.80 cat /home/level9/final.txt
...
...
/home/level9/.bashrc: line 4: logout: not login shell: use `exit'
Congratulations. You are a Child of Honor.

Final Flag: i-am-now-a-child-of-honor
...
...

```





