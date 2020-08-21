---
layout: post
title:  "BoJack Horseman's Sad Christmas"
date:   2019-01-16 00:00:00 -0200
categories: [CTF,STEGO,X-MAS CTF]
author: glfms
event: "X-MAS CTF 2018"
tags: [CTF,STEGO,X-MAS CTF]
description: "Pelo fato da chall nos trazer uma imagem, é de se imaginar que tenha algum arquivo ou mensagem escondida."
image: "/assets/images/writeups/x-mas/bojack.png"
---

# X-MAS CTF 2018

## Nome: BoJack Horseman's Sad Christmas

### Descrição:

>BoJack recieved a Christmas card from Diane but Princess Carolyn shredded it to bits. It looks like festive barf now! Can you help BoJack read the card?

![](/assets/images/writeups/x-mas/bojack.png)

### Solução:

Pelo fato da chall nos trazer uma imagem, é de se imaginar que tenha algum arquivo ou mensagem escondida. Para verificar se ela contém algum conteúdo suspeito, utilizei as tools `strings` e `binwalk`, mas nada de relevante foi encontrado. Parti então para a análise de esteganografia e, como a imagem se trata de um PNG, utilizei o `zsteg` para fazer um scan em busca de alguma pista da flag. 

![](/assets/images/writeups/x-mas/zsteg_results.png)

Observando os resultados, a ferramenta parece ter encotrado uma outra imagem (JPEG) escondida dentro da imagem principal. Para conferir, podemos extrair com o seguinte comando:

```bash
zsteg -E b1,g,lsb,xy boJack.png > file
```

De fato, o arquivo encontrado é uma imagem válida e nos trás a flag!

![](/assets/images/writeups/x-mas/file)

FLAG: X-MAS{1_L0V3_B0J4ckH0rs3m4n}
