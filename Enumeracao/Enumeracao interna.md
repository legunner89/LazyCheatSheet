### Windows

```shell
wpscan --url http://192.168.50.244 --enumerate p --plugins-detection aggressive -o websrv1/wpscan

# Busca de arquivos
## Windows

## CMD
dir /s /b
dir /s /b flag.txt
dir /s /b *.txt

### Ver arquivos ocultos
dir /a:h

### Para ignorar a pasra AppData que trás muitos resultados:
dir /s /b | findstr /v /i /c:"AppData"

## Powershell

### Procurando arquivos por extensões
Get-ChildItem -Path C:\Users\celia.almeda\ -Include *.txt,*.pdf,*.xls,*.xlsx,*.doc,*.docx,*.php,*.htm,*.html -File -Recurse -ErrorAction SilentlyContinue

### Procurando arquivo .kdbx
Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue

### Buscar arquivos com a palavra alvo
Get-ChildItem -Recurse | Select-String -Pattern "password"

### Tentar visualizar historico do usuário
Get-History

(Get-PSReadlineOption).HistorySavePath

## serviços
wmic service get name,pathname,displayname,startmode | findstr /i auto | findstr /i /v "C:\Windows\" | findstr /i /v """
```




### Linux

#### Enum4Linux-ng

- https://github.com/cddmp/enum4linux-ng

```shell
python3 ./enum4linux-ng.py -A 192.168.161.100 -oA enum_dc.txt
```
```bash
## Buscar aquivo pelo nome
find . -name "foo*"

## Que contenha a palavra
grep -r -a  "password" ./

## Que contenha a palavra mas exclua certa extensão
grep -r --exclude="*.js" "password" /caminho/da/pasta

## Ler historico do usuário
history
cat ~/.bash_history

## SUID/SGID
find / -perm -u=s -type f 2>/dev/null
find / -perm -g=s -o -perm -u=s -type f 2>/dev/null
```


# wfuzz
- service: http
- tactics: enumeration

## bruteforce web parameter
- `wfuzz -u http://target-ip/path/index.php?param=FUZZ -w /usr/share/wordlists/rockyou.txt`