# SSH (Secure Shell or Secure Socket Shell)
## Qué es SSH
- SSH se refiere tanto al protocolo de red criptográfico
- Conjunto de utilidades que implementan ese protocolo
- Un servidor SSH escucha en el puerto 22 de forma predeterminada

## Ventajas
- Brinda una forma segura de acceder a una computadora a través de una red
	abierta
```zsh
# Conectarse a un servidor remoto
ssh username@hostname 
#> Options:
# -i <identity_file>
# -p <port>
# -4 Forzar ssh a usar IPv4
# -6 Forzar ssh a usar IPv6
# -l <login_name>
# -q <Quit_mode> suprime la mayoría de mensajes de advertencia
# -v <Verbose_mode>
```
- Proporciona una fuerte autenticación (contraseña y llave pública)
- Comunicación de datos encriptados entre dos computadoras
- Ejecución remota de comandos
```zsh
#> Without options
ssh username@hostname pwd # /home/username
#> With option -t
# -t: emula una terminal para el comando
ssh -t usename@hostname irssi
```
- Entrega de parches de software y actualizaciones...

## Cómo funciona
- SSH permite iniciar sesión y ejecutar sesiones de terminal en sistemas remotos, tal como
Telnet y rsh, pero de forma segura.
- Reemplaza a programas de transferencia de archivos como FTP y rcp (copia remota).
- La primera vez que negocia una conexión entre un host local y un servidor, se le 
	solictará al usuario la huella dactilar de la clave pública del host remoto.
	La clave de host se almacenará en el archivo known_hosts para posteriores conexiones.

## Otros comandos ejecutables SSH
### sshd
Inicia el servidor SSH, que espera solicitudes SSH entrantes y permite que los
sistemas autorizados se conecten al host local
### ssh-keygen
Permite crear un par de claves de autenticación para SSH, que permite automatizar el
inicio de sesión
### ssh-copy-id
Permite copiar, instalar y configurar una clave SSH en un servidor para automatizar
inicios de sesión
```zsh
ssh-copy-id username@hostname:
# Nos pedirá la contraseña para poder copiar la key
# Copia la llave al archivo .ssh/authorized_keys del servidor
```
### ssh-agent
Programa de ayuda que rastrea las claves de identidad y sus frases de contraseña
### ssh-add
Agrega una clave al agente de autenticación SSH
### scp
Programa que se usa para copiar archivos de una computadora a otra
### sftp
Programa para copiar archivos de una computadora a otra. Es una version segura de SSH en comparación con ftp, el Protocolo de transferencia de archivos original

## Tunelización SSH
Conocida como reenvío de puertos SSH, es una técnica que permite a un usuario abrir un
túnel seguro entre un host local y un host remoto
