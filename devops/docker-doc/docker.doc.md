# Docker
- Marco de software (Conjunto de productos de plataforma como servicio) para contruir,
	ejecutar y administrar contenedores en servidores y la nube.
- Utilizan la "virtualización a nivel del sistema operativo" para entregar software en 
	paquetes denominados contenedores
- Pemite desarrollar aplicaciones que puedan ejecutarse y funcionar uniformemente en
	cualquier entorno
- El concepto de un servidor pudo eliminarse de las limitaciones del hardware, y se
	convirtio, esencialmente, en una pieza de software.

## Imagen de contenedor
- Esta imagen contiene el sistema de archivos del contenedor, por lo que debe contener
	todo lo necesario para ejecutar una aplicación
	- Dependencias, configuración, scripts, archivos binarios, etc)
- Así como configuración para el contenedor
	- Variables de entorno, comando predeterminado para ejecutar, y otros metadatos

## Comprender los contenedores
| "Los contenedores pueden ser liberadores, siempre que estén liberados"
Son procesos aislados de todos los demás procesos en la maquina host. Que aprovechan los
espacios de nombres del kernel y cgroups.
- Un contenedor es una instancia ejecutable de una imagen
- Los contenedores están aislados entre sí y ejecutan su propio software, archivos
	binarios y configuraciones
La tecnología de contenedores se puede considerar como tres categorías diferentes:
- Builder: una herramienta o serie de herramientas utilizadass para construir un
	contenedor (distrobuilder, Dockerfile)
- Motor: una aplicación utilizada para ejecutar un contenedor (docker)
- Orquestación: tecnología utilizada para administrar muchos contenedores (Kubernetes)

## Ventajas de los contenedores
### Versátiles
- En el orden de los MB
- Tienen todas las dependencias que necesitan para funcionar correctamente
- Funcionan igual en cualquier lado
### Eficientes
- Comparten archivos inmutables con otros contenedores
- Solo se ejecutan procesos, no un SS.OO. completo
### Aislados
- Lo que pasa en el container queda en el container
- No pueden alterar su entorno de ejecución (a menos que explícitamente se indique lo
	contrario)

## Diferencia entre contenedor y VM
Las maquinas virtuales virtualizan una maquina completa hasta las capas de hardware
y los contenedores solo virtualizan las capas de software por encima del nivel del
sistema operativo.
Los contenedores no tienen un sistema operativo dentro. Simplemente comparte el kernel
subyacente con los otros contenedores.
