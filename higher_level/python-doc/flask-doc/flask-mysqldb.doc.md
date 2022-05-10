# flask-mysqldb
Este modulo te permite establecer una conexión con MySQL
```bash
pip install flask-mysqldb
```

## Use
### Añade una instancia de MySQL a nuestro aplicación
```python
from flask_mysqldb import MySQL
# app:
#		Instancia de Flask class, que define nuestra Flask aplication.
#		Objeto que posee la configuración con respecto a la base de datos
mysql = MySQL(app)
```
### Conexión e interacción con la base de datos
- Petición para obtener datos de una tabla
```python
# Obtener un cursor para posicionarnos en la base de datos
cur = mysql.connection.cursor()
# Con cur variable podemos ejecutar consultas sql
cur.execute("SELECT %s, %s FROM mysql.user", ("user", "host"))
# Recuperar todos los datos devuelto por la consulta
cur.fetchall()
```
- Petición para almacenar datos en una tabla
```python
# Obtener un cursor para posicionarnos en la base de datos
cur = mysql.connection.cursor()
# Con cur variable podemos ejecutar consultas sql
cur.execute(
	"INSERT INTO contacs (fullname, phone, email) VALUES (%s, %s, %s)",
	("Pepito", "1122458", "elpepe@gmail.com")
);
# Confirmar cambios
mysql.connection.commit();
```
