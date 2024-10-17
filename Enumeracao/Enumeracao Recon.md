
### Dominio / ip

- https://who.is/
- https://www.whois.com/whois/

Geolocalização:

- https://www.iplocation.net/ip-lookup
- https://www.geolocation.com/pt/index

### NMAP

```
nmap -sC -sV 10.10.10.10 -p- 
```

### WEB

```shell
## Comom
gobuster dir -u http://192.168.214.73/ -w /usr/share/wordlists/dirb/common.txt 

##Gobuster quick directory busting
gobuster -u 10.10.10.10 -w /usr/share/seclists/Discovery/Web_Content/common.txt -t 80 -a Linux

##Gobuster comprehensive directory busting
gobuster -s 200,204,301,302,307,403 -u 10.10.10.10 -w /usr/share/seclists/Discovery/Web_Content/
big.txt -t 80 -a 'Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0'

##Gobuster search with le extension
gobuster -u 10.10.10.10 -w /usr/share/seclists/Discovery/Web_Content/common.txt -t 80 -a Linux -x .txt,.php

gobuster dir -u http://192.168.50.242 -w /usr/share/wordlists/dirb/common.txt -o mailsrv1/gobuster -x txt,pdf,config

gobuster dir -u http://192.168.208.147:8000 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 32

##Nikto web server scan
nikto -h 10.10.10.10

##Wordpress scan
wpscan -u 10.10.10.10/wp/


## Listas
-w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
-w /usr/share/wordlists/dirb/common.txt

## Palavras
Adicionar nas listas!!

cms
cmsms
elFinder
seclab
```

### SMB

- porta 445
- Possibilidade de acessar com o usuário "Anonymous"
- Possibilidade de subir um payload de acessar via página web do servidor

```shell
## SMB Vulnerability Scan
nmap -p 445 -vv --script=smb-vuln-cve2009-3103.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10-054.nse,smb-vuln-ms10-061.nse,smb-vuln-ms17-010.nse 10.10.10.10

## SMB Users & Shares Scan
nmap -p 445 -vv --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.10.10

## Enum4linux
enum4linux -a 10.10.10.10

## Null connect
rpcclient -U "" 10.10.10.10

## Connect to SMB share
smbclient //MOUNT/share
```



### EntryPoints

Senha Padrão

- Mesmo nome do usuário
- 123456
- admin
- root
- Case Sencitive 

#### RCE

- Execução de comando concatenando função web que executa algum comando
```
http://teste.com/index.php?cmd=ping 8.8.8.8;whoami
```

#### Robots

- robots.txt

#### FTP

- Ftp pode ser vulnerável a Directory transversal