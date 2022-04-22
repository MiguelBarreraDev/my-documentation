# Commands

### SSH como un proxy para el navegador
```zsh
ssh -D <puerto> username@host
# Crea un proxy SOCKS en el servidor ssh para poder usarlo como proxy en el navegador
```
### Ejecutar aplicaciones UI que están en el servidor en nuestra máquina
```zsh
# Linux
ssh -X username@hostname
# Mac or Window
#> Instalar un servidor X y luego ejecutar el comando 
```
### Tunel con ssh
```zsh
#> Caso en el que se quiera acceder a un servidor que no está abierto a internet
# pero sí desde otro servidor en la misma red local
ssh -L 2020:host2:22 username@host1
# Se crea/habilita el puerto 2020 en mi máquina que apunta al puerto 22 del host2
# a través del host1
```
### Tunel ssh reverso
```zsh
ssh -R 2020:localhost:22 root@externo
# Crea/habilita un puerto en el servidor externo que apunte al puerto 22 del
# server2 (localhost)
```
