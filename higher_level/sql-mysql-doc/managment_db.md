# Managment of MySQL database
MySQL es un software de administración de base de datos, que ayuda
a almacenar, organizar y luego recuperar datos.

## Components
### Validate password
- Permite mejorar la seguridad al momento de requerir contraseñas
- Brinda pruebas de seguridad de contraseñas potenciales
- Expone variables del sistema para configurar la política de contraseñas
- Expone variables de estado para la supervisión del componente
- Implementa tres niveles de contraseña: Low, Mediun (default) y Strong.
```mysql
/**
 * Low: Solo prueba la longitud de la contraseña
 * - Al menos 8 caracteres (default)
 * Medium: Almenos un caracter
 * - numérico
 * - minúscula
 * - mayúscula
 * - especial
 * Strong: No deben coincidir con palabras en el archivo de diccionario
 */
```
#### Comandos relacionados
- Variables de configuración
```mysql
-- Command: Mostrar configuración actual del componente
SHOW VARIABLES LIKE 'validate_password%'
-- Output
+--------------------------------------+--------+
| Variable_name                        | Value  |
+--------------------------------------+--------+
| validate_password.check_user_name    | ON     |
| validate_password.dictionary_file    |        |
| validate_password.length             | 8      |
| validate_password.mixed_case_count   | 1      |
| validate_password.number_count       | 1      |
| validate_password.policy             | MEDIUM |
| validate_password.special_char_count | 1      |
+--------------------------------------+--------+
-- Command: Modificar valores de las variables arriba
mysql> SET GLOBAL validate_password.policy=LOW;
```
- Implementa una una función para evaluar la seguridad de contraseñas potenciales,
	que retorna una valor entre 0 (debil) a 100 (fuerte)
```mysql
-- Function: VALIDATE_PASSWORD_STRENGTH()
mysql> SELECT VALIDATE_PASSWORD_STRENGTH('Weak')
-- output
+------------------------------------+
| VALIDATE_PASSWORD_STRENGTH('weak') |
+------------------------------------+
|                                 25 |
+------------------------------------+
```
- Produce un error si la contraseña no cumple con la política de contraseñas
```mysql
-- Command
mysql> ALTER USER USER() IDENTIFIED BY 'abc';
-- Output
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements
```
- Modificar los niveles de seguridad
```mysql
-- Comand: Cambiar el nivel de verificación a bajo
mysql> SET GLOBAL validate_password.policy=LOW;
-- Comand: Cambiar el nivel de verificación a intermedio
mysql> SET GLOBAL validate_password.policy=MEDIUM;
-- Comand: Cambiar el nivel de verificación a fuerte
mysql> SET GLOBAL validate_password.policy=STRONG;
```


## Usuarios
### Create new user
```mysql
-- Se crea sin permisos
mysql> CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
/**
 * localhost: Hostname que significa "esta computadora"
 * Cuando se inicie sesión con este host, la conexión se dará mediante un 
 * archivo de scoket Unix
 */
```

### Otorgando permisos
```mysql
-- Se otorga todos los permisos(leer, editar, ejecutar, ...) en la database
mysql> GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
/**
 * *(1): Hace referencia a todas las databases
 * *(2): Hace referencia a la tabla
 */
-- Siempre volver a cargar todos los privilegios luego de configurar
mysql> FLUSH PRIVILEGES;
```

### Permisos específicos
```mysql
mysql> GRANT 'type_of_permission' ON 'database_name'.'table_name' TO 'username'@'localhost';
/**
 * Lista de permisos comunes
 * ALL PRIVILEGES: Todos los permisos
 * CREATE: Crear nuevas tablas o databases
 * DROP: Eliminar tablas o databases
 * DELETE: Eliminar records de una tabla
 * INSERT: Insert records into tables
 * SELECT: Use 'SELECT' command to read en una databases
 * UPDATE: Actualizar records en una tabla
 * GRANT OPTION: Conceder o remover permisos a otros usuarios
 * REPLICATION MASTER: Verificar el estado principal/replica de sus bases de datos
 * REPLICATION SLAVE: Habilita la cuenta para replicar databases from source server
 */
-- Siempre volver a cargar todos los privilegios luego de configurar
mysql> FLUSH PRIVILEGES;
```

### Revoke permissions
```mysql
mysql> REVOKE 'type_of_permission' ON 'database_name'.'table_name' FROM 'username'@'localhost';
```

### Revisar permisos de un usuario
```mysql
mysql> SHOW GRANTS FOR 'username'@'localhost';
```

### Delete a user altogether
```mysql
mysql> DROP USER 'username'@'localhost';
```
