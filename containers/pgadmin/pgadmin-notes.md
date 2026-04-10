# Notas sobre la instalación de PgAdmin

Registro de problemas encontrados durante la ejecución del contenedor y las soluciones aplicadas para cada caso. 

## Problema los permisos del volumen _queries_

Si llega a presentar el error:

```
werkzeug.exceptions.InternalServerError: 500 Internal Server Error: The user does not have permission to read and write to the specified storage directory.
```

Se debe garantizar que el usuario `pgadmin` del contenedor tenga acceso al directorio `./volumenes/queries/`.

*Ejemplo:*

```
# Esto no es recomendado en ambiente de producción
chmod 777 -R volumes/queries
```

Una vez que has iniciado por primera vez tu sesión en _*pgAdmin*_ y haz creado la conexión al contenedor de _*PostgreSQL*_ deberás darle acceso al host al directorio con el comando siguiente:

```
# Desde el contenedor de pgAdmin
chmod 707 sotelo.enrique_gmail.com/
```

Esto no es necesario si deseas ejecutar las consultas desde el contenedor de _*PostgreSQL*_ ya que este último se ejecuta como usuario `root`.

*Ejemplo:*

```
# Desde el contenedor de postgresql
psql -h localhost -U postgres -d postgres -f /queries/sotelo.enrique_gmail.com/funcion_now.sql 
```

Al cambiar los permisos de lectura, escritura y ejecución del directorio ya será posible escribir las consultas desde el host y ejecutarlas en el contenedor de _*pgAdmin*_.
