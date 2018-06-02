# Acceso al servidor y transferencia de datos

El usuario deberá iniciar sesión en el cluster a través de un cliente ssh mediante el servidor de login utilizando usuario y contraseña o un par llave pública-llave privada. El software que necesitará usar en su sistema cliente depende de su sistema operativo:

### Acceso desde window

Se puede abrir una sesión modo texto utilizando un cliente ssh como putty: [ftp uci](ftp://10.0.0.22/software/Tools/Network/Putty/),[web oficial](https://www.putty.org/).

Para enviar datos y recibir datos desde el cluster se pueden utilizar:

* WinSCP: [ftp uci](ftp://10.0.0.22/software/Tools/Network/Winscp/), [web oficial](https://winscp.net/eng/download.php)

* FileZilla: [ftp uci](ftp://10.0.0.22/software/Tools/Network/FileZilla/), [web oficial](https://filezilla-project.org/)

### Acceso desde linux modo texto utilizando OpenSSH

___Requisitos:OpenSSH___

En la mayoría de los casos un enlace en modo texto es suficiente para la ejecución de las tareas. Para esto, se utiliza el comando `ssh`:

	$ ssh <usuario>@<ip_nodo_login>

La primera vez que se conecte al servidor de login, usted deberá autenticar el nodo login, ejemplo: 

	The authenticity of host 'hostname (ip)' can't be established.ECDSA key fingerprint is SHA256:+795v7FnFcMGcwlok8eHxJN27XEVqg94Y0ROxZNz/Gs.Are you sure you want to continue connecting (yes/no)?
	
Para enviar y recibir datos desde el cluster se puede auxiliar del comando `scp`:

	$ scp fichero_a_enviar usuario_remoto@hostremoto:/some/remote/directory/


### Enlaces de interés

* `man scp`
* `man ssh` 
* [Ayuda scp](https://www.garron.me/en/articles/scp.html)
* [Ayuda ssh](https://www.ssh.com/ssh/command/)
* [Ayuda winscp](https://winscp.net/eng/docs/guides)
* [Ayuda putty](https://www.ssh.com/ssh/putty/)