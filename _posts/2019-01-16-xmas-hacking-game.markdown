---
layout: post
title:  "Suspicious Hacking Game"
date:   2019-01-16 00:00:00 -0200
categories: [CTF,STEGO,X-MAS CTF]
author: glfms
event: "X-MAS CTF 2018"
tags: [CTF,STEGO,X-MAS CTF]
description: "Novamente um challenge com imagem, o que nos leva a suspeitar de mensagens e arquivos escondidas, principalmente pelo fato da imagem ter 43MB (grande demais para um simples PNG)."
image: "/assets/images/writeups/x-mas/suspicious.png"
---


# X-MAS CTF 2018

## Nome: Suspicious Hacking Game

### Descrição:

>You woke up on Christmas Day only to find this lame hacking game cartridge laying under the Christmas tree. You are certain that you were an ethical hacker this year, though, and you deserve something better. Maybe Santa has left you another present you aren't yet aware of?

{:refdef: style="text-align: center;"}
![suspicious.png](/assets/images/writeups/x-mas/suspicious.png)
{:refdef}

[download](https://drive.google.com/file/d/1HRBkXzI_RtJIpWP1F7Gz-1p7rbTUHkM3/edit){:target="_blank"}

### Solução:

Novamente um challenge com imagem, o que nos leva a suspeitar de mensagens e arquivos escondidas, principalmente pelo fato da imagem ter 43MB (grande demais para um simples PNG).

Em busca de algum sinal da flag, eu utilizei o comando `strings`, mas nada útil surgiu a princípio. Contudo, buscando mais a fundo por algum arquivo esteganografado com a ferramenta `zsteg`, é possível notar que existe um ZIP escondido na imagem.

```bash
ztseg -a suspicious.png
```

![](/assets/images/writeups/x-mas/zsteg.png)

Podemos extrair o ZIP com o seguinte comando:

```bash
zsteg -E b8,bgr,lsb,xY suspicious.png > file.zip
```

Ao abrir o ZIP, é possível notar que ele contém um APK, o qual tudo indica ser um jogo para android.

![](/assets/images/writeups/x-mas/zip_content.png)

A princípio, eu pensei em rodar o jogo ou decompilar para ver ser encontrava a flag, mas ao compartilhar o arquivo econtrado com os outros integrantes do time, eu notei que o ZIP pesa 125,5 MB e o APK apenas 24,4 MB. O que não fez sentido nenhum para mim, visto que, se o arquivo estava comprimido, ele deveria pesar mais que o ZIP após a extração. Resolvi então utilizar a tool `binwalk` para fazer um *carving* e recuperar aquivos no ZIP.

```bash
binwalk -ze suspicious.png
```

Confirmei minhas suspeitas ao observar os resultados do scan e ver mais alguns arquivos sendo encontrados. A ferramenta gerou uma pasta contendo um único arquivo ZIP com nome genérico (23.zip). Entretanto, ao tentar extrair o arquivo, um erro surgiu na tela.

![](/assets/images/writeups/x-mas/error.png)

*Shit!*

Resolvi reparar o ZIP com o seguinte comando:

```bash
zip -FF 23.zip --out repaired.zip
```

E funcionou! Um novo arquivo foi gerado e dessa vez foi possível realizar a extração.

Em seu conteúdo, encontra-se um diretório com uma única DLL no final: `Assembly-CSharp.dll`

Admito que isso me desanimou um pouco, pois não parecia ser algo que pudesse conter a flag. Mas, por desencargo de consciência, eu resolvi ler o conteúdo utilizando o comando `cat`:

![](/assets/images/writeups/x-mas/flag.png)

E *Voilà!* A flag surgiu para minha surpresa.

FLAG: X-MAS{S4v3_Th1s_1m4g3_4nd_g3t_4_fr33_g4m3}
