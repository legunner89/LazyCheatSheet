
- Aspectos do Usuario

   → Qual o ID do usuario e de quais grupos ele faz parte?

        id

   → Posso ler algum arquivo sensivel?

        cat /etc/passwd
        cat /etc/shadow

   → Em quais diretorios tenho permissao de escrita?

        find / -writable 2> /dev/null

   → Posso utilizar o sudo para alguma atividade privilegiada?

        sudo -l
	
   → Tenho algum historico de comandos anteriores?

        history
        cat ~/.bash_history
   
   → Exite algum arquivo com SUIG/SGID habilitado que tenho acesso?

        find / -perm -u=s -type f 2>/dev/null
        find / -perm -g=s -o -perm -u=s -type f 2>/dev/null
    
   → No home do usuario existe alguma chave SSH?

        ls -lha

- Aspectos do Sistema

   → Qual a versao do SO?

        cat /etc/issue
        cat /etc/lsb-release
	
   → Qual a versao do Kernel?

        uname -a
	
   → Quais processos estao executando com permissao de root?

        ps -aux | grep root
	
   → Quais servicos de rede estao rodando?

        netstat -tunap
        ss -tunap
	
   → Existem tarefas agendadas?

        ls -lahR /var/spool/cron
        cat /etc/cron*
        atq
        cat /etc/at.allow
        cat /etc/at.deny
        cat /etc/anacron