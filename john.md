
## ZIP

Tirar um hash do arquivo zip com senha:

```
zip2john backup.zip > backup.hash
```

Quebrar o hash:

```
john --format=ZiP backup.hash --wordlist=/usr/share/wordlists/rockyou.txt
```



## Chave privada cracking

Seguindo a metodologia de cracking, nosso próximo passo é transformar o chave privada em formato hash para nossas ferramentas de cracking. Usaremos o **ssh2john** script de transformação do conjunto JtR e salve o hash resultante para **ssh.hash**.

```shell
kali@kali:~/passwordattacks$ ssh2john id_rsa > ssh.hash

kali@kali:~/passwordattacks$ cat ssh.hash
id_rsa:$sshng$6$16$7059e78a8d3764ea1e883fcdf592feb7$1894$6f70656e7373682d6b65792d7631000000000a6165733235362d6374720000000662637279707400000018000000107059e78a8d3764ea1e883fcdf592feb7000000100000000100000197000000077373682...
```

Dentro desta saída, "$6$" significa _SHA-512_.[1](https://portal.offsec.com/courses/pen-200/books-and-videos/modal/modules/password-attacks/password-cracking-fundamentals/ssh-private-key-passphrase#fn1) Como antes, removeremos o nome do arquivo antes dos primeiros dois pontos. Então, vamos determine o modo Hashcat correto.

```shell
kali@kali:~/passwordattacks$ hashcat -h | grep -i "ssh" 
...
  10300 | SAP CODVN H (PWDSALTEDHASH) iSSHA-1                 | Enterprise Application Software (EAS)
  22911 | RSA/DSA/EC/OpenSSH Private Keys ($0$)               | Private Key
  22921 | RSA/DSA/EC/OpenSSH Private Keys ($6$)               | Private Key
  22931 | RSA/DSA/EC/OpenSSH Private Keys ($1, $3$)           | Private Key
  22941 | RSA/DSA/EC/OpenSSH Private Keys ($4$)               | Private Key
  22951 | RSA/DSA/EC/OpenSSH Private Keys ($5$)               | Private Key
```
