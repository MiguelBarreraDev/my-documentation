# Flask aplication

## Definir una aplicación con Flask
```python
from flask import Flask
```
Objeto para definir una Flask aplication, cuyo primer parametro
le permite a Flask identificar la aplicación a ejecutar.
Flask ejecuta la aplicación proveída en la variable de entorno "FLASK_APP" , y "wsgi.py"
o "app.py" module.
```python
# Crea una instancia del objeto Flask
# __name__ :
# > Representa el nombre del paquete de la aplicacón.
# > Se usa para indicar dónde se encuentra la aplicación.
# > Flask lo utiliza para identificar recursos: plantillas, static files, instance path...
app = Flask(__name__)
```
## Configuración para flask-mysqldb module
```python
app.config["MYSQL_HOST"] = "localhost"
app.config["MYSQL_USER"] = 'root'
app.config["MYSQL_PASSWORD"] = 'password'
app.config["MYSQL_DB"] = 'my_database'
.
.
```

## Definir Rutas
Se usa el ***decorador route()*** para lograrlo, donde se vincula un URL significativa
a cada ***función de vista*** que creamos.
### route()
Es un decorador que va encima de la función de vista y toma algunos parámetros:
- rule: La URL en formato cadena
- endpoint: El nombre de la función de vista
- options: ...
```python
# Definimos la ruta principal de la pagina
@app.route('/')
def index():
	return "Welcome to my web page"
# Definimos la ruta para agregar contactos desde la pagina
@app.route('/add_contact')
def add_contact():
	return "Saved contact"
```
### Función de vista (en:View function)
Aquella función debajo del decorador ***route()*** que se ejecuta cuando llegan requests
a la ruta previamente establecida en el decorador.
La combinación entre ***route()*** y esta función se conoce comúnmente como la vista o
la ruta.
### Static routing
En este tipo de routing, especificamos una cadena de URL constante como regla para
le decorador***route()***.
```python
# Definimos una ruta constante para eliminar un contacto
@app.route('/delete_contact')
def add_contact():
	return "Deleted contact"
```
### Dinamyc routing
El parámetro ***rule*** en ***router()*** no es una cadena constante. En su lugar, se
pasa una regla variable al decorador ***route()***.
```python
# Agregar reglas (ruler parameter) variables
# Sintaxis: <varaible_name>
# Uso: @app.route('/delete_contact/<variable_name>')
# variable_name se pasará a la función de vista para ser utlizada
# Definimos una ruta constante para eliminar un contacto
@app.route('/delete_contact/<string:id_to_delete>')
def add_contact(id_to_delete):
	return f"Deleted contact with id: {id_to_delete}"
# @app.route('/delete_contact/<string:id_to_delete>')
# > regla variable ~ id_to_delete
# > convertidor ~ string (default)
# Otros convertidores
# > String
# > int
# > float
# > path
# > uuid
```

## Renderizar html desde el servidor
Enviar template(html) desde el servidor al cliente
### Estrcutura de archivos
```shell
- flask-app
- + templates			// Directory donde Flask busca templates
- - - index.html	// Template
- - App.py				// Flask aplication
```
### Flask aplication
```python
from flask import Flask, render_template
#...
@app.route('/', ['GET'])
def index():
	return render_template("index.html")
```

## Manejo de solicitudes
El objeto request contiene la información de la petición a la ruta
```python
# Caso: Datos de un formulario desde el cliente
from flask import Flask, render_template, request
#...
@app.route('/add_contact', ['POST'])
def add_contact():
	if request.method == "POST":
			fullname = request.form["fullname"]
			phone = request.form["phone"]
			email = request.form["email"]
	return "Saved contact"
```

## Redirecionar al cliente desde el servidor
```python
from flask import Flask, render_template, request, redirect, url_for , flash
# ...
@app.route('/add_contact', ['POST'])
def add_contact():
	# Manejar la solicitud con el objeto request
	return redirect(url_for("url_name"))
```

## Enviar mensajes desde el servidor
Para evidenciar una acción de exito, error, etc
```python
from flask import Flask, render_template, request, flash
# ...
@app.route('/add_contact', ['POST'])
def add_contact():
	if request.method == "POST":
			fullname = request.form["fullname"]
			phone = request.form["phone"]
			email = request.form["email"]
			# Almacenar datos en la DB con flask-mysqldb module
			flash("Contact Added successfully")
	return redirect(urlf_for("url_name"))
```
