---
layout: post
title:  "Hacking N' Roll Wallpaper"
date:   2018-12-24 15:21:51 -0200
categories: [CTF,STEGO,ShellterLabs]
author: andersongomes001
event: ShellterLabs
tags: [CTF,STEGO,ShellterLabs]
description: "Pegamos ‘emprestado’ o notebook pessoal de Fábio Jebb, consiglere de Don Jebb e homem de negócios da família. Analisamos seu notebook adquirindo evidências. Baixe o documento e descubra algo interessante..."
image: "/assets/images/writeups/690524d5-3808-49e3-a84b-a8b45b8f0052.png"
---
## Desafio:

Pegamos ‘emprestado’ o notebook pessoal de Fábio Jebb, consiglere de Don Jebb e homem de negócios da família. Analisamos seu notebook adquirindo evidências. Baixe o documento e descubra algo interessante.

{:refdef: style="text-align: center;"}
![Branching](/assets/images/writeups/690524d5-3808-49e3-a84b-a8b45b8f0052.png)
{:refdef}

##  Solução:

Usando o [stegsolve][stegsolve] e mudando a colour map da imagen rapidamente obetemos a flag.
{:refdef: style="text-align: center;"}
![Branching](/assets/images/writeups/20181224154733.png)
{:refdef}

Flag: hnrv{an_easy_secret_with_michael}

[stegsolve]: https://raw.githubusercontent.com/andersongomes001/ctf-tools/master/stegsolve/install

