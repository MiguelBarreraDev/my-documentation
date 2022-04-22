# Managment of MySQL database
MySQL es un software de administración de base de datos, que ayuda
a almacenar, organizar y luego recuperar datos.

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
 * *(1): Hace referencia a la database
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
 */
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
