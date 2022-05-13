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
#	> Se usa para indicar dónde se encuentra la aplicación.
#	> Flask lo utiliza para identificar recursos: plantillas, static files, instance path...
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
Se usa decoradores para lograrlo, donde se definen la ruta, el metodo, etc
```python
# Define la ruta.
# Define el método que acepta la ruta en cuestión.
# La función debajo de los decoradores es la que se ejecuta cuando llega una petición
#	a dicha ruta.
@app.route('/', ['GET'])
def index():
	return "Welcome to my web page"

@app.route('/add_contact', ['POST'])
def add_contact():
	return "Saved contact"	
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
