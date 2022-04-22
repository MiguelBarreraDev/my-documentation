# Commands Docker

### Construir una imagen
```zsh
docker built -t <tag_name> .
#> Options
# -t - Etiqueta nuesta imagen. Para darle un nombre legible por humanos
# . - Indica que Docker debe buscar Dockerfile en el directorio actual
```
### Listar imagenes
```zsh
# image ls - Muestra todas las imagenes descargadas en nuestro equipo
docker image ls # or
docker images
# -a - Muestra tambien las imágenes intermedias
docker image ls -a # or
docker images -a
# -q - Si solo se quiere ver los números de identificación
docker image ls -q # or
docker images -q
```
### Limpiar cualquier recurso (imágenes, contenedores, volúmenes...)
```zsh
# Recursos que esten colgando (no etiquetados o asociados con un contenedor)
docker system prune
# Elminar contenedores detenidos e imagenes no utilizadas (no solo colgadas)
docker system prune -a
```
### Eliminar imágenes de Docker
```zsh
# Eliminar una o más imágenes específicas
docker rmi <ImageID | tag> <ImageID | tag>
```
### Ejecutar un contenedor
```zsh
docker run -d -p 80:80 docker/getting-started
#> Options
# -d - ejecuta el contenedor en segundo plano
# -p 80:80 - asigna el puerto 80 del host al puerto 80 del contenedor
# docker/getting-started - imagen a utilizar
```

