---
layout: post
title:  "level 13"
date:   2018-12-14 18:00:51 -0200
categories: [CTF,Hackaflag]
author: andersongomes001
event: Hackaflag challengeweek
tags: [CTF,Hackaflag]
description: "Está na hora de verificar quais foram os passos tomados, a base para se entender como algo funciona é entender como aquilo é montado..."
image: "/assets/images/writeups/48360195102098451191639464176715524807327744.jpg"
---
## Desafio:

Está na hora de verificar quais foram os passos tomados, a base para se entender como algo funciona é entender como aquilo é montado.

{:refdef: style="text-align: center;"}
![Branching](/assets/images/writeups/20181224161940.png)
{:refdef}

[arquivo][1]


## Solução:

Olhando bem para o arquivo percebemos que se trata um dump,e verificando o Hex signature `ffd8 ffe0 0010 4a46 4946 0001` descobrimos que se trata de um arquivo `jpg` ou `jpeg`.

```python
#!/usr/bin/env python3

#abre o arquivo para leitura
flag = open("flag",'r')

hexdump = ""
#pega somente os hexa do arquivo
for linha in flag.readlines():
    hexdump += str(linha[10:50]).replace("\n","").replace(" ","")
data = bytes.fromhex(hexdump)

#gera uma imagen
with open('image.png', 'wb') as file:
    file.write(data)
```
E o resultado é a imagem abaixo.

{:refdef: style="text-align: center;"}
![Branching](/assets/images/writeups/48360195102098451191639464176715524807327744.jpg)
{:refdef}

Flag: HACKAFLAG{AsBasesPrimeiro}

Fontes:

[wikipedia - List of file signatures][List_of_file_signatures]

[1]:{{ site.url }}/download/challengeweek13.txt
[List_of_file_signatures]: https://en.wikipedia.org/wiki/List_of_file_signatures
