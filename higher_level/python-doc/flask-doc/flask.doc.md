# Flask
***Es un framework de desarrollo web desarrollado en python***
- Proporciona un servidor de desarrollo y un depurador
- Utiliza lantillas Jinja2
- Compatible con WSGI 1.0
- Soporte integrado para pruebas unitarias
- Muchas extensiones disponibles para flask
## Por qué Flask es un micro-framework?
Porque solo proporciona los componentes esenciales para el desarrollo web:
- Enrutamiento
- Manejo de solicitudes
- Sesiones, etc
Opuesto a los full-stack frameworks, que ofrecen modulos para autenticar, orm, etc.
## Dónde está mi flask app?
En el modelo arquitectónico cliente-servidor, una **Flask app** está del
lado del servidor, esperando **requests** desde un cliente como el navegador.
## Patrones de arquitectura de software ¿?
### MVC (Model-View-Controller)
Patrón de arquitectura de software en el que la lógica de la aplicación se
divide en tres componentes en base a la funcionalidad.
- **Modelos**
Representan cómo se almacenan los datos en la base de datos, dado que,
contienen todas las definiciones de datos para su aplicación (el esquema)
- **Vistas**
Componentes visibles para el usuario, como una salida o interfaz gráfica de
usuario (GUI)
- **Controladores**
Actúan como interfaz entre los modelos y las vistas, interpretando entradas
o interaciones del usuario, para realizar tareas en los modelos antes de
devolver los datos apropiados a través de las vistas
### MTV (Model-Template-View)
Es una ligera variación de la arquitectura MVC, introducido por el framework
Django.
## WSGI y Jinja2
### WSGI (Web Server Gateway Interface)
Es un estandar que describe las especificaciones relativas a la comunicación
entre un servidor web y una aplicación cliente.
- **Flexibilidad** con los componentes de la aplicación
- **Interoperabilidad** dentro de diferentes frameworks de python
- **Escalabilidad** de la aplicación con aumento de usuarios
- **Eficiencia** en términos de velocidad de desarrollo
### Jinja2
Es un motor de plantillas usado en python/Flask, usado dentro de HTML para
que el contenido de la pagína HTML se vuelva dinámico.
