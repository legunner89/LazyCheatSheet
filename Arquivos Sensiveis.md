```
/etc/issue (A message or system identification to be printed before the login prompt.)
/etc/motd (Message of the day banner content. Can contain information about the system owners or use of the system.)
/etc/passwd 
/etc/group 
/etc/resolv.conf (might be better than /etc/passwd for triggering IDS sigs)
/etc/shadow
/home/[USERNAME]/.bash_history or .profile
~/.bash_history or .profile
$USER/.bash_history or .profile
/root/.bash_history or .profile
```

**Web server files**

```
# Usually found in the root of the website
.htaccess
config.php
```

**SSH**

```
authorized_keys
id_rsa
id_rsa.keystore
id_rsa.pub
known_hosts
```

**Logs**

```
/etc/httpd/logs/acces_log 
/etc/httpd/logs/error_log 
/var/www/logs/access_log 
/var/www/logs/access.log 
/usr/local/apache/logs/access_ log 
/usr/local/apache/logs/access. log 
/var/log/apache/access_log 
/var/log/apache2/access_log 
/var/log/apache/access.log 
/var/log/apache2/access.log
/var/log/access_log
```

**User specific files**

Found in the home-directory

```
.bash_history
.mysql_history
.my.cnf
```

## WINDOWS

**Fingerprinting**

```
c:\WINDOWS\system32\eula.txt
c:\boot.ini  
c:\WINDOWS\win.ini  
c:\WINNT\win.ini  
c:\WINDOWS\Repair\SAM  
c:\WINDOWS\php.ini  
c:\WINNT\php.ini  
c:\Program Files\Apache Group\Apache\conf\httpd.conf  
c:\Program Files\Apache Group\Apache2\conf\httpd.conf  
c:\Program Files\xampp\apache\conf\httpd.conf  
c:\php\php.ini  
c:\php5\php.ini  
c:\php4\php.ini  
c:\apache\php\php.ini  
c:\xampp\apache\bin\php.ini  
c:\home2\bin\stable\apache\php.ini  
c:\home\bin\stable\apache\php.ini
```

**Logs**

Common path for apache log files on windows:

```
c:\Program Files\Apache Group\Apache\logs\access.log  
c:\Program Files\Apache Group\Apache\logs\error.log
```