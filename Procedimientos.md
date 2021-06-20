# Procedimientos

## 1. Creación manual de un servicio odoo ce (crun+csql)


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


Con la configración en multiaz y backup se espera 42.5€/m

Primero, se desconecta la línea admin_password para que esta password coincida con la password de odoo.conf

```
Database connection failure: could not connect to server: Connection timed out
```

Después de reflexionar se crea un usuario odoo con contraseña odoo, para permtir que la aplicación se conecte a la bbdd. Como mediante cloudsehll con ip privada dice que error, se da una ip pública para crear el usuario.

````
ERROR: (gcloud.sql.connect) It seems your client does not have ipv6 connectivity and the database instance does not have an ipv4 address. Please request an ipv4 address for this database instance.
````

[1](https://www.postgresql.org/docs/8.0/sql-createuser.html)


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
```

Se pone accesible la bbdd. Se hace primero exponiéndola públicamente creando una red a la que acceden todos (0.0.0.0/0). Luego, se mejora la privacidad del diseño configurando la bbdd como privada, creando un conector vpc serverless.

Después de esto, como mejora de seguridad, se vuelve a hacer un fork de odoo/docker, ahora privado. Después se configura github actions para que haga pull del repo. Así se deben crear dos servicios en cloud run: uno de test con una github action automática y uno de prod con una github action manual. Luego se reflexiona que si lso cambios pasan los tests de odoo, parece razoanble sólo ahcer una action y que esta sea automática. Se debe disponer de una manera de comprobar que una actulización ha hecho caer el servicio. Por ejemplo para culaquier incidencia consultar a un correo.

### Configurar

Primero, nos percatamos de que al crear una bd aparece el siguiente error, que se subsana dotando de ciertos privilegios al usuario odoo.

```
Database creation error: permission denied to create database
```

[1](https://www.odoo.com/es_ES/forum/ayuda-1/programmingerror-permission-denied-to-create-database-64086)

```
ALTER USER odoo WITH CREATEDB;
```

Se quita finalmente el acceso público para comprobar que fucniona con este servicio privado.

------------


Cómo activar la actualizacion autoamtica con github actions

Conexión perdida. Intentando reconectar...

Crear ese en prod, e itnetnar coenctar ese otro

1- Conseguir el backup y probarlo
2- poenrlo seguro, pasarle el link

proteger los correo sy cotnraseñas

Para desplegar la bbdd privada es encesario un vpc conector

que pasa cuando realizo una atulziacion

cómo mangjar la clave maestra e cloud sql

migarar a un bbdd privada, 

db2 migarr a una bbdd privada

https://cloud.google.com/sql/docs/postgres/connect-run

cuanto improta la seguridad: si me borran la bbdd, no tenog nada

qué hacer con las contraseñas, en un repo privado

https://www.odoo.com/es_ES/security
https://www.odoo.com/es_ES/forum/ayuda-1/warning-your-odoo-database-manager-is-not-protected-please-set-a-master-password-to-secure-it-109951

Cómo gestioanr las cotnraseñas de una forma que la master password sólo sea concoida por el usuario


crear un string muy largo, y ponerlo en los dos lados, poner esa copia en privado
se puede poner ese fichero de configuración en privado

github actiosn apra actualziarlo

porqué despue´s de usar lighhouse no se ven los estilos

3- craer la bbdd uy probar en una de ejemplo que puedo hacer backup y pasarlo allí: por ejemplo el peidad leon con lo básico sin fotos

less tahn 10% of memory, soi pick 2GB

Mañana

4- conseguir dominio
5- configurar peidad leon con los cuadros en un prod
6- garantía me parece chancullo
7- enviar emsnaje al de saas


como lo de amrjketing lo usas y sólo cuadno veas beneficios entonces te cesta, no te cuesta sino que parte se va a eso

------------

### Crun
### Csql 
