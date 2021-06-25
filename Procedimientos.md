# Procedimientos

## 1. Creación manual de un servicio odoo ce (crun+csql)

## 2. Procedimiento de backup

## 3. Procedimiento de actualización

## 4. Mejora. Usar http2 parapermitir backups mayores de 32 MB.

## 5. Procedimiento de control de acceso autorizado

-------------------

## 1. Creación manual de un servicio odoo ce (crun+csql)

### Código de odoo
### Crun
### Csql 
### Configurar

-----------

### Código de odoo
Fork de odoo/docker y configurar cloudbuild para que caundo cambie el repo (con las actualizaciones) se cree otra vez la imagen.

Es mejor que coger un contenedor de bitnami, pues bitnami isntal postgres en la misma docker network.

[1](https://github.com/bitnami/bitnami-docker-odoo/blob/14.0.20210610-debian-10-r7/14/debian-10/Dockerfile)
[2](https://www.cloudbooklet.com/install-odoo-13-on-ubuntu-18-04-with-nginx-google-cloud/)

COnfigurar una github acción para que se haga pull del docker maestro.

[1](https://mathieu.carbou.me/post/649318432483033088/automatic-fork-syncing-with-github)
[2](https://gist.github.com/mathieucarbou/96ab30024f0d3fb44cac970219d23efc)

Poner como default la branch master.

### Crun
Se elige la región con menos latencia, Beligum (gcping) y los valores del contenedor.

[1](https://kinsta.com/blog/google-cloud-network/)
[2](https://gcping.com/)
[3](https://www.youtube.com/watch?v=PSyGrZZOd3Q)

Se configuran dos variables de entorno: host con la ip de la ddbb y dbport con el puerto de posgres. Nótese que se debe cambiar el valor port pro dbport en entrypoint.sh para que no colisione con el valor or defecto del port que expone cloud run

Si se configura http2 aparece este error:

```
upstream connect error or disconnect/reset before headers. reset reason: protocol error
```

entreypoint.sh y odoo.conf => dbport = 5432

Puede ser que este error sea debido a llamr una revision con un nombre ya usado o ha llamar uno repo en mayúscula.

```
Your build failed to run: generic::invalid_argument: invalid build: invalid image name "eu.gcr.io/breadfree/myOdoo/bf-test:a93ef07e1398c76d1c8bf55ae6e59cd73db3b4d0": could not parse reference: eu.gcr.io/breadfree/myOdoo/bf-test:a93ef07e1398c76d1c8bf55ae6e59cd73db3b4d0
```

### Csql 

Primero se reflexiona sobre qué instancia es mejor coger.
Luego sobre cómo conectar cloudsql con odoo, básicamente exponiendo parámetros como variables de entorno y cambiando parámetros del fichero de configuración. Como la clave maestra
Después se reflexiona sobre cómo posibilitar más conexiones al servicio.

[1](https://blog.doit-intl.com/how-does-a-cloud-sql-database-scale-and-what-to-know-when-setting-one-up-c23c52fc9947)
[2](https://www.cybrosys.com/blog/odoo-14-deployment-using-docker)
[3](https://cloud.google.com/sql/docs/quotas)
[4](https://cloud.google.com/sql/docs/mysql/operational-guidelines)
[5](https://cloud.google.com/sql/docs/mysql/replication/create-replica)
[6](https://www.jhanley.com/google-cloud-sql-for-mysql-connection-security-high-availability-and-failover/)


Con la configración en multiaz se espera 42.5€/m. No se configura backup pues se realiza este de forma externa. Se elige shared-core 1.7 GB

Primero, se descomenta la línea admin_password, escriebiendo una de tal forma que esta password coincida con la password de odoo.conf.

Además se elige el Docekrfile como ./14.0/Dockerfile y la rama como master.

```
Database connection failure: could not connect to server: Connection timed out
```

Después de reflexionar se crea un usuario odoo con contraseña odoo, para permtir que la aplicación se conecte a la bbdd. Como mediante cloudsehll con ip privada dice que error, se da una ip pública para crear el usuario.

````
ERROR: (gcloud.sql.connect) It seems your client does not have ipv6 connectivity and the database instance does not have an ipv4 address. Please request an ipv4 address for this database instance.
````

[1](https://www.postgresql.org/docs/8.0/sql-createuser.html)


Se cambian el puerto a 8069, y se introduce la variable de entorno PORTDB.

La password ppuede ser odoo u otra más grande



```
 \du
 create user odoo with password 'J2Gpv74A5yGPk735FstW9aBwEKGPetneCkCXADG6wFD8hh2BY7rUrVVuZwvqZ4ds';
 \du
 ALTER USER odoo WITH CREATEDB;
 \du
```

```
postgres=> create user odoo with password 'odoo';
CREATE ROLE
postgres=> \du 
                                                List of roles
         Role name         |                         Attributes                         |      Member of
---------------------------+------------------------------------------------------------+---------------------
 cloudsqladmin             | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 cloudsqlagent             | Create role, Create DB                                     | {cloudsqlsuperuser}
 cloudsqliamserviceaccount | Cannot login                                               | {}
 cloudsqliamuser           | Cannot login                                               | {}
 cloudsqlimportexport      | Create role, Create DB                                     | {cloudsqlsuperuser}
 cloudsqlreplica           | Replication                                                | {pg_monitor}
 cloudsqlsuperuser         | Create role, Create DB                                     | {pg_monitor}
 odoo                      |                                                            | {}
 postgres                  | Create role, Create DB                                     | {cloudsqlsuperuser}
 
 create user odoo with password 'odoo';
 \du
 ALTER USER odoo WITH CREATEDB;
```

Se pone accesible la bbdd. Se hace primero exponiéndola públicamente creando una red a la que acceden todos (0.0.0.0/0). Luego, se mejora la privacidad del diseño configurando la bbdd como privada, creando un conector vpc serverless.

Después de esto, como mejora de seguridad, se vuelve a hacer un fork de odoo/docker, ahora privado. Después se configura github actions para que haga pull del repo. Así se deben crear dos servicios en cloud run: uno de test con una github action automática y uno de prod con una github action manual. Luego se reflexiona que si lso cambios pasan los tests de odoo, parece razoanble sólo ahcer una action y que esta sea automática. Se debe disponer de una manera de comprobar que una actulización ha hecho caer el servicio. Por ejemplo para culaquier incidencia consultar a un correo.

Nos percatamos de que al crear una bd aparece el siguiente error, que se subsana dotando de ciertos privilegios al usuario odoo.

```
Database creation error: permission denied to create database
```

[1](https://www.odoo.com/es_ES/forum/ayuda-1/programmingerror-permission-denied-to-create-database-64086)

```
ALTER USER odoo WITH CREATEDB;
```

Se quita finalmente el acceso público para comprobar que fucniona con este servicio privado.

Cambiar password odoo en el conf por una autogenerada

Para borrar una database: 

- 1 se le da el role de postgres al usuario odoo que posee la database, desde el role posgres
- 2 se hace a postgres owner de la db. Porque si no odoo conectado a breadfree no prodía borrarlo
- 3 postgres borra la db breadfree

```
postgres=> grant postgres to odoo;
GRANT ROLE

breadfree=> alter database breadfree owner to postgres;
ALTER DATABASE

postgres=> drop database breadfree;
DROP DATABASE
```


https://stackoverflow.com/questions/26684643/error-must-be-member-of-role-when-creating-schema-in-postgresql

```
postgres=> drop database breadfree;
```

### Configurar


```
Error de usuario:

Odoo is currently processing a scheduled action.
Module operations are not possible at this time, please try again later or contact your system administrator.
```

Se reinicia y funciona.

```
postgres=> SELECT pg_terminate_backend (pid)
FROM pg_stat_activity
WHERE pg_stat_activity.datname = 'breadfree';
ERROR:  must be a member of the role whose process is being terminated or member of pg_signal_backend
```


------------

## 2. Procedimiento de backup


 ?De qué forma autoamtizar el bakup de la bbd y del filestore?
 
 - Hacerlo 
 - BUscar un addon

-----------

- Hacerlo

Con un scheduler ejecutar cloud run. Peor puede que el script dependa de la versión

[1](https://cloud.google.com/run/docs/triggering/using-scheduler)
[2](https://linuxize.com/post/how-to-setup-automatic-odoo-backup/)

- Addons

Existen addons compatibles gratuitos

[1](https://apps.odoo.com/apps/modules/14.0/odoo_backup_sh/)
[2](https://apps.odoo.com/apps/modules/14.0/ir_attachment_s3/)

Montarlos sobrer el Dockerfile. Hacer un Dockerfile con este. Crear una db6 de pruebas inyectándola la password.
Añadirle a este Dockerfile el addon de backup. Meter las credenciales de aws en ello. Configurarla cómo funciona.

Aparece el siguiente error:
```
Skipping database bf-dev because of modules to install/upgrade/remove.
```

Se propone arranca la db, y entocnes instalar y darle a udpate.

No hay bd, no hay ningún error, todo puede ser por haber clikado dos veces en crear bd. Se crea un bd8 y se borra esta.

Luego el addon de attachment a s3.

-------------

## 3. Procedimiento de actualización

Cómo activar la actualizacion autoamtica con github actions

Un DOckerfile más serio con un github actions para hacer pulling


Probar con un Dockerfile: un ockerfile público sin la contraseña, sino tenog que ahcer una github action, y eso no escala
Hay que ahcerlo no se hace sólo

https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions

https://subscription.packtpub.com/book/business_and_other/9781800200319/1/ch01lvl1sec07/updating-the-add-on-modules-list

-------------

## 4. Mejora. Usar http2 parapermitir backups mayores de 32 MB.

https://stackoverflow.com/questions/68130278/how-to-set-in-a-dockerfile-an-nginx-in-front-of-the-same-container-google-cloud
------------

## 5. Procedimiento de control de acceso autorizado


cómo mangjar la clave maestra e cloud sql

migarar a un bbdd privada, 

db2 migarr a una bbdd privada

https://cloud.google.com/sql/docs/postgres/connect-run

cuanto improta la seguridad: si me borran la bbdd, no tenog nada

qué hacer con las contraseñas, en un repo privado

https://www.odoo.com/es_ES/security
https://www.odoo.com/es_ES/forum/ayuda-1/warning-your-odoo-database-manager-is-not-protected-please-set-a-master-password-to-secure-it-109951

Cómo gestioanr las cotnraseñas de una forma que la master password sólo sea concoida por el usuario

Crear un nuevo service account

crear un string muy largo, y ponerlo en los dos lados, poner esa copia en privado
se puede poner ese fichero de configuración en privado

harcoded password in config files => send password as env

github actiosn apra actualziarlo

porqué despue´s de usar lighhouse no se ven los estilos

3- craer la bbdd uy probar en una de ejemplo que puedo hacer backup y pasarlo allí: por ejemplo el peidad leon con lo básico sin fotos

--------
4- conseguir dominio
5- configurar peidad leon con los cuadros en un prod
6- garantía me parece chancullo
7- enviar emsnaje al de saas


como lo de amrjketing lo usas y sólo cuadno veas beneficios entonces te cesta, no te cuesta sino que parte se va a eso

