---
layout: post
title:  "Load DLLs Power Shell"
date:   2019-01-11 18:53:51 -0200
categories: [CTF,REVERSE,eSecurity]
author: Sql3t0
event: "Esecurity"
tags: [CTF,REVERSE,eSecurity]
description: "Hoje estou aqui para falar um pouco sobre DLLs. Mais exatamente sobre alguns Desafios de CTF que envolvem reverse em DLLs."
image: "/assets/images/wtf/GH0kA7N.png"
---


**Ola caros leitores !!**

  

  

Hoje estou aqui para falar um pouco sobre **DLLs**. Mais exatamente sobre alguns Desafios de **CTF** que envolvem **reverse** em DLLs.

  

  

Tomando como Exemplo de DLL irei usar uma [DLL](https://github.com/sql3t0/shellterlabsCTF/blob/master/tools/LoadDLL/CTF-Esecurity_LaricasCriptografia.dll?raw=true) de um desafio que ocorreu no CTF da [Esecurity](https://ctf.esecurity.com.br) de 2018.

  

  

![](https://github.com/sql3t0/shellterlabsCTF/blob/master/tools/WriteupsSiteDeadlokTeam/LoadDLLsPowerShell/imgs/img_00.png?raw=true)

  

Usando o comando **file** na DLL para descobrir a qual arquitetura ela pertence, descobrimos que ela é x86.

  

--------------------------------------------------------------------------------------------------------------------------------------

  

```powershell
C:\Users\Sql3t0\Desktop> file CTF-Esecurity_LaricasCriptografia.dll
CTF-Esecurity_LaricasCriptografia.dll: PE32 executable (DLL) (console) Intel 80386 Mono/.Net assembly, for MS Windows

```

--------------------------------------------------------------------------------------------------------------------------------------

  

A partir dessa descoberta, agora podemos selecionar a versão correta do [Decompiler](https://en.wikipedia.org/wiki/Decompiler), que nesse caso e o [dnSpy x86](https://github.com/0xd4d/dnSpy), que e um decompiler opensource e que esta disponível para download no **Github**.

  

  

![](https://github.com/sql3t0/shellterlabsCTF/blob/master/tools/WriteupsSiteDeadlokTeam/LoadDLLsPowerShell/imgs/img_01.png?raw=true)

  

Como e possível perceber, utilizando o dnSpy conseguimos encontrar duas **Classes** dentro do NameSpace **Laricas**:

  

## Database

  

Olhando a **Classe**  **Database** e facil perceber que ha duas variáveis (**DB_USER**,**DB_PASS**) bem sugestivas e que parecem estar **Encriptadas**.

  

![](https://github.com/sql3t0/shellterlabsCTF/blob/master/tools/WriteupsSiteDeadlokTeam/LoadDLLsPowerShell/imgs/img_02.png?raw=true)

  

  

## Encryption

  

Olhando agora a **Classe**  **Encryption** podemos notar que existe um **método** chamado **crypt**.

  

  

![](https://github.com/sql3t0/shellterlabsCTF/blob/master/tools/WriteupsSiteDeadlokTeam/LoadDLLsPowerShell/imgs/img_03.png?raw=true)

  

Indo mais a fundo no método **crypt** é possível deduzir que ele nada mais é que **uma variação do algoritimo de [XOR](https://en.wikipedia.org/wiki/XOR_cipher)**.

  

--------------------------------------------------------------------------------------------------------------------------------------

  

```c#
byte[] array = new byte[input.Length];
for (int i = 0; i < input.Length; i++)
{
    array[i] = (byte)((int)input[i] ^ this._secret[i % this._secret.Length]);
}
return array;

```

--------------------------------------------------------------------------------------------------------------------------------------

  

A partir desse ponto pressupõe-se que os valores das variaves **DB_USER** e **DB_PASS** foram criptografados usando o método **crypt**.

  

  

Sabendo-se que a reversão para criptografia de XOR e simplismente XOR,então podemos usar o mesmo método que foi utilizado na cifragem para tentar realizar a decifragem.

  

E e nessa parte onde entra uma dica que pode lhe fazer economizar muito tempo em futuros CTFs que venham a utilizar DLLs.

  

  

Esse dica nada mais e que usar o **powershell** do Windows para **carregar** a DLL na **memoria** e utilizar ela. Tudo isso a partir da linha de comando.

  

  

### Como fazer isso **?**

  

Usando a classe **[System.Reflection.Assembly](https://docs.microsoft.com/pt-br/dotnet/api/system.reflection.assembly?view=netframework-4.7.2)** e possivel carregar o conteudo da DLL, criar objetos das classes e ainda utilizar os seus metodos contidos em cada classe.

  

--------------------------------------------------------------------------------------------------------------------------------------

  

```powershell
PS C:\Users\Sql3t0\Desktop> $DLLbytes = [System.IO.File]::ReadAllBytes("C:\Users\Sql3t0\Desktop\CTF-Esecurity_LaricasCriptografia.dll")
PS C:\Users\Sql3t0\Desktop> [System.Reflection.Assembly]::Load($DLLBytes)

GAC Version Location

--- ------- --------

False v4.0.30319

PS C:\Users\Sql3t0\Desktop>
```

  

--------------------------------------------------------------------------------------------------------------------------------------

  

Caso queira **Listar** todos o métodos contidos na DLL recém carregada basta executar o comando :

  

--------------------------------------------------------------------------------------------------------------------------------------

```powershell
PS C:\Users\Sql3t0\Desktop> [Laricas.Encryption].GetMethods()
```

--------------------------------------------------------------------------------------------------------------------------------------

  

Para criar um **Objeto** de uma Classe basta executar o comando :

  

--------------------------------------------------------------------------------------------------------------------------------------

  

```powershell
PS C:\Users\Sql3t0\Desktop>$objeto = New-Object "Laricas.Encryption"
```

  

--------------------------------------------------------------------------------------------------------------------------------------

  

Onde **Laricas** e o **Namespace** e **Encryption** o nome da **Classe**.

  

  

Olhando para os valores cifrados podemos deduzir que eles estao em Base64 e teremos que decodificar eles antes de passarmos como parâmetro no método **crypt**.

  

--------------------------------------------------------------------------------------------------------------------------------------

  
  
  
  

```c#
public class Database
{
    // Token: 0x04000001 RID: 1
    public string DB_USER = "exFzCnkMXhFxCmoMRBFWCkkM";

    // Token: 0x04000002 RID: 2
    public string DB_PASS = "UhFBCm4MVBFpCnwMUhFzCmAMaBFxCnkMThFiCn8MWBEvCnsMQBF8CjgMUxFvCg==";
}
```

  
  

--------------------------------------------------------------------------------------------------------------------------------------

  

Para isso usaremos o comando :

  

--------------------------------------------------------------------------------------------------------------------------------------

  

```powershell
PS C:\Users\Sql3t0\Desktop> $string = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("UhFBCm4MVBFpCnwMUhFzCmAMaBFxCnkMThFiCn8MWBEvCnsMQBF8CjgMUxFvCg==")
```

  
  

--------------------------------------------------------------------------------------------------------------------------------------

  

Sequencialmente codificaremos a **$string** para **UTF-8** :

  

--------------------------------------------------------------------------------------------------------------------------------------

  
  

```powershell
PS C:\Users\Sql3t0\Desktop> $enc = [system.Text.Encoding]::UTF8
PS C:\Users\Sql3t0\Desktop> $data = $enc.GetBytes($string)
```

  
  

--------------------------------------------------------------------------------------------------------------------------------------

  

E entao chamamos o método **crypt** para decodificar, salvando o resultado em uma outra variável na qual codificaremos o resultado em **ASCII** para ser finalmente impresso na tela:

  

--------------------------------------------------------------------------------------------------------------------------------------

  
  

```powershell
PS C:\Users\Sql3t0\Desktop> $array = $objeto.crypt($data)  
PS C:\Users\Sql3t0\Desktop> $enc = [System.Text.Encoding]::ASCII  
PS C:\Users\Sql3t0\Desktop> $enc.GetString($array)  
e S e c { w e a k _ c r y p t o = p w n 3 d }  
PS C:\Users\Sql3t0\Desktop>
```

  

--------------------------------------------------------------------------------------------------------------------------------------

  

![](https://github.com/sql3t0/shellterlabsCTF/blob/master/tools/WriteupsSiteDeadlokTeam/LoadDLLsPowerShell/imgs/img_04.png?raw=true)

  

  

E e isso aew pessoal !!

  

  

Espero que todos tenham gostado do conteúdo aqui repassado.E para todos aqueles que chegaram ate aqui eu deixo o meu sincero **Muito Obrigado** e ate a proxima.

  

  

\m/...**Hack_Never_Ends**...\m/

  

  

Codigo final :

  

--------------------------------------------------------------------------------------------------------------------------------------

  
  

```c#
if($args.count -eq 2){  
    $DLLName = $args[0]  
    $DLLbytes = [System.IO.File]::ReadAllBytes($DLLName)  
    [System.Reflection.Assembly]::Load($DLLBytes)  
    #lista todos os metodos na DLL  
    #[Laricas.Encryption].GetMethods()  
    $objeto = New-Object "Laricas.Encryption"  
    $string = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($args[1]))  
    $enc = [system.Text.Encoding]::UTF8  
    $data = $enc.GetBytes($string)  
    $array = $objeto.crypt($data)  
    $enc = [System.Text.Encoding]::ASCII  
    $enc.GetString($array)  
}else{  
    echo "Usage : script.ps1 DLLNameStringToDecode"  
}
```

  
  
  

--------------------------------------------------------------------------------------------------------------------------------------