---
layout: post
title:  "epic mount"
date:   2019-01-16 00:00:00 -0200
categories: [CTF,FORENSIC,35C3 CTF]
author: glfms
event: "35C3 CTF"
tags: [CTF,FORENSIC,35C3 CTF]
description: "Ao inspecionar o binário, descobrimos que, assim como no desafio rare mount, se trata de um JFFS2 filesystem."
image: "/assets/images/writeups/inspection.png"
---


# 35C3 CTF - Junior

## Nome: epic mount

### Descrição:

>A little bit of stego. Not every header field looks like the other.

[ffbde7acedff79aa36f0f5518aad92d3-rare-fs.bin](/download/f9be7cb88a778615216f212d58f62ea3-epic-fs.bin)

### Solução:

Ao inspecionar o binário, descobrimos que, assim como no desafio `rare mount`, se trata de um JFFS2 filesystem.

![](/assets/images/writeups/inspection.png)

Tentei rodar a *tool* `jefferson` para extrair os arquivos do binário. Com isso, o mesmo vídeo obtido no *challenge* anterior foi obtido. Entretanto, nenhum arquivo contendo a flag apareceu e o seguinte erro foi reportado diversas vezes: `hdr_crc does not match!`

```bash
jefferson f9be7cb88a778615216f212d58f62ea3-epic-fs.bin -d outdir
```

![](/assets/images/writeups/error.png)

Como a *tool* não ajudou muito dessa vez, eu resolvi seguir a parte da descrição que falava sobre *stego* e buscar por alguma mensagem ou arquivo esteganografado. Confesso que, com isso, gastei algumas horas em pesquisas e tentativas frustrantes de extrair a flag do vídeo encontrado, mas, obviamente, sem sucesso. Após conversar com outro integrante do time, decidimos comparar esse binário com o do *challenge* anterior, com finalidade de encontrar as diferenças e corrigir os erros reportados. Visto que, parecia se tratar do mesmo arquivo, porém corrompido.
Pesquisando por algum utilitário que comparasse os dois arquivos byte a byte, eu encontrei o [cmp](http://man7.org/linux/man-pages/man1/cmp.1.html).

Comparando as diferenças entre os arquivos, obtemos a flag:

```bash
cmp -b -l f9be7cb88a778615216f212d58f62ea3-epic-fs.bin ffbde7acedff79aa36f0f5518aad92d3-rare-fs.bin
```

![](/assets/images/writeups/flag.png)

¯\\\_(ツ)\_/¯

Achei esse *challenge* bem interessante, pois foi a primeira vez que encontrei estaganografia em algum arquivo que não fosse mídia.

FLAG: 35C3_hide_me_baby_one_more_time
