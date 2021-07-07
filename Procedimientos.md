# Procedimientos

## 1. Creación manual de un servicio odoo ce (crun+csql)

## 2. Procedimiento de backup

## 3. Procedimiento de actualización

## 4. Bug/mejora. Usar http2 parapermitir backups mayores de 32 MB.

## 5. Procedimiento de control de acceso autorizado

## 6. Bug/mejora. Cloud run es stateless, no persiste los VOLUMEs.

## 7. Saber cuántas visitas. Conectar google analytics

Oca vs saas
https://www.youtube.com/watch?v=XqND6_PITio

-------------------

## 1. Creación manual de un servicio odoo ce (crun+csql)

# CE 14

### Código de odoo
### Crun
### Csql 
### Configurar

# CE 13 + session store (redis) + s3 (backup and images)

### Código de odoo
### Crun
### Csql 
### Redis
### Images 
### Backup
### Configurar

-----------

# CE 14

### Código de odoo
Fork de odoo/docker y configurar cloudbuild para que cuando cambie el repo (con las actualizaciones) se cree otra vez la imagen. Es mejor que coger un contenedor de bitnami, pues bitnami isntal postgres en la misma docker network.

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

La password puede ser odoo u otra

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

 gcloud sql connect db9 --user=odoo --database=breadfree --quiet

breadfree=> alter database breadfree owner to postgres;
ALTER DATABASE

postgres=> drop database breadfree;
DROP DATABASE
```

Aun así no funciona, se usa otra db y ya está

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

Desde breadfree


# CE 13 + session store (redis) + s3 (backup and images)

### Código de odoo

- 1. Fork de odoo/docker y configurar cloudbuild para que cuando cambie el repo (con las actualizaciones) se cree otra vez la imagen. Es mejor que coger un contenedor de bitnami, pues bitnami isntal postgres en la misma docker network.

- 2. Configurar una github acción para que se haga pull del docker maestro.

- 3. Poner como default la branch master.

### Crun

- 1. Se elige la región con menos latencia, Beligum (gcping) y los valores del contenedor.

- 2. Se configuran dos variables de entorno: host con la ip de la ddbb y dbport con el puerto de posgres. Nótese que se debe cambiar el valor port pro dbport en entrypoint.sh para que no colisione con el valor or defecto del port que expone cloud run


### Csql

- 1. Primero se reflexiona sobre qué instancia es mejor coger.
- 2. Luego sobre cómo conectar cloudsql con odoo, básicamente exponiendo parámetros como variables de entorno y cambiando parámetros del fichero de configuración. Como la clave maestra
- 3. Después se reflexiona sobre cómo posibilitar más conexiones al servicio.

- 4. Con la configración en multiaz se espera 42.5€/m. No se configura backup pues se realiza este de forma externa. Se elige shared-core 1.7 GB

- 5. Primero, se descomenta la línea admin_password, escriebiendo una de tal forma que esta password coincida con la password de odoo.conf.

- 6. Además se elige el Docekrfile como ./13.0/Dockerfile y la rama como master.

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

### Redis

Se añade el código de camptocamp.

Se añade al script las dependencias necesarias.

Lo instalo pero con el requirement no sale

bdist wheel en el camp2camp

https://github.com/aws/aws-cli/issues/4243
https://stackoverflow.com/questions/34819221/why-is-python-setup-py-saying-invalid-command-bdist-wheel-on-travis-ci/49426845

que salgan lso módulos

puede qaue sea necesario borrar la db

falta el resu tom,cilaer, para un reuqirment nuevo iamgino

Cree un rqeuirment habiendo un requirment para el addon

Se configura el cloud platform

redis version problem

Eso significa que no soporta redis superiores?

Intentar con la 13 que parece que sí que guraa sesiones

Pregutnar eso

usar la versión 13 de campto camp

redis version of redispy

sesion in 13

https://realpython.com/python-redis/

The requirment says it is needed redis 2.10.5, why it cannot be used a redis higher? WHich si the redis version that mathces?

Hay un pyaml there

Se itnetna con un redis 4

Sino se va montando un 13

https://cloud.google.com/memorystore/docs/redis/scaling-instances

Scaling is a bit hard 

https://cloud.google.com/memorystore/docs/redis/pricing

+32€

Crear otro servicio

añadirle ese addon

no hacer upgrad pero isntalr el compiler de rust

ese 13

en my odooesa revision con esa bbdd y ese plugin

pq no se ven los módulos, sólo si los ahgo uno a uno sí

no aparecen los módulos aunque la db sea nueva

si se añade un git dentor de otro no se ve

todos de una no funciona, una a una

sóloel de redis

wix invenotry vs this

bfdev3 cobn todos los módulos
bfdev4 con 13
bfdev5 con un sólo módulo

instalar otro modlo

comprobar si tienen los mismo modulos

instalar ese

en bfdev3o paaprecen los mdolos que se añaden depsues de crear la bd

en dev4

porque no sale para isntalar es la version 13

no seale el modulo como app sino como extra

Aunque actulize se sigue sin ver

### Images 

comprobar que se poneen las ima´genes

bfdev3
bfdev4 these things are set



https://www.odoo.com/es_ES/forum/ayuda-1/what-exactly-is-needed-to-load-a-module-as-server-wide-73152

### Backup
### Configurar

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


```
Imposible instalar el módulo "odoo_backup_sh" porqué hay una dependencia externa no resuelta: Python library not installed: boto3
```

Se intenta hacer run de pip install. En la documentation se dice que se debe elegir un bucket un un folder. Se intenta crear un folder en el bucket, pero no se sabe si se refiere a un folder en el bucket o en el contenedor de odoo.

https://www.concurrencylabs.com/blog/choose-your-aws-region-wisely/

Parece que la región más barata es us-east-1, N Virginia. Además no tiene gran latencia.

Cuando descargo el zip dice que no tiene permiso.

```
The request signature we calculated does not match the signature you provided. Check your key and signing method.
```


https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html
https://github.com/aws/aws-sdk-go/issues/3110
https://stackoverflow.com/questions/7116450/what-are-valid-s3-key-names-that-can-be-accessed-via-the-s3-rest-api

Aún con las dos cuentas da este error.




Luego el addon de attachment a s3.

-------------

## 3. Procedimiento de actualización

Cómo activar la actualizacion autoamtica con github actions

Un DOckerfile más serio con un github actions para hacer pulling


Probar con un Dockerfile: un ockerfile público sin la contraseña, sino tenog que ahcer una github action, y eso no escala
Hay que ahcerlo no se hace sólo

https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions

https://subscription.packtpub.com/book/business_and_other/9781800200319/1/ch01lvl1sec07/updating-the-add-on-modules-list

Creating a rpeo composing several repos

-------------

## 4. Mejora. Usar http2 para permitir backups mayores de 32 MB.

https://stackoverflow.com/questions/68130278/how-to-set-in-a-dockerfile-an-nginx-in-front-of-the-same-container-google-cloud

https://docs.docker.com/config/containers/multi-service_container/
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

----------------

## 6. Bug/mejora. Cloud run es stateless, no persiste los VOLUMEs.

No se meustra css

https://www.odoo.com/es_ES/forum/ayuda-1/no-css-no-images-after-user-logout-from-website-127642
```
Failed to load resource: the server responded with a status of 404 () web.ssets frontend.css:1
```

si cloud run no persite los volúmenes, los addons se van 

puede ser porque pirde los filestore.

QUé guarda odoo en filestore?

Los themes, que se pierden, y las imágenes

Cuando pongo un theme se pierde

Por eso paarece sin css.

O persisto el theme

odoo cómo guardas el filestore en la nube

cloud run no hay integración con el filestore, no se persiste

https://www.odoo.com/es_ES/forum/ayuda-1/how-to-configure-the-filestore-in-high-availability-172440

https://github.com/itpp-labs/misc-addons/tree/11.0/ir_attachment_s3

precio de redis

https://github.com/diogocduarte/odoo_s3/tree/12.0

https://github.com/itpp-labs/misc-addons

session sotre modules

https://apps.odoo.com/apps/modules/12.0/base_session_store_psql/
https://stackoverflow.com/questions/64228967/how-to-mount-persistent-storage-to-google-cloud-run
https://www.odoo.com/es_ES/forum/ayuda-1/css-and-js-files-are-not-loading-96868

https://apps.openerp.com/apps/modules/13.0/muk_fields_file/
v13

https://apps.odoo.com/apps/modules/13.0/muk_session_store/

Hacer otro odoo, y habilitar ahí con redis la session

CHoose the modules for the same provider

v14, there's no sesion storage there

v13
https://github.com/itpp-labs/misc-addons/tree/13.0/base_session_store_psql
https://github.com/itpp-labs/misc-addons/tree/13.0/ir_attachment_url

https://github.com/Smile-SA/odoo_addons/tree/13.0
muk

itpp labs

https://github.com/it-projects-llc/saas-addons/tree/13.0/saas

=> para hacer un saas muhco curro

incluso los propios volúmenes cuando meto el addon están en el filestore

Crear otro servicio bf-dev2 en db9

Probar desde el principio con redis y esas 2

https://github.com/camptocamp/odoo-cloud-platform

borrar la db e intentarlo

sino borro no salen los módulos

sólo lo coge si esta vacia

https://www.odoo.com/es_ES/forum/ayuda-1/how-to-install-addon-modules-127246

it is needed restarting

create a service add this one by one

quiero ver si con un sólo modulo tmabien sa,le como extra o como app

s3 backup

pero el oposgres parece que no se isntala que viene como dado

se comprueba si conserva la sesion el debv6 no tendría que ocnservarloa

eso

```
GET4041.04 KB24 msChrome 91 https://bf-dev3-u7raxlu3nq-ew.a.run.app/web/content/290-f328144/1/website.assets_editor.css
```

said the guys of camptocamp i tried doing this
iptpp the aame i did that and it didn't work

linkedin

https://www.odoo.com/es_ES/forum/ayuda-1/replace-session-store-of-odoo-werkzeug-86843

bfdev3 falla el css
bfdev4 parece que funciona

ir_attachment_s3
ir_attachment_url
odoo_backup_sh

specify this
write ok this is not working

ese s3 no se puede actulizar

have a shower



-------------

Regenerate the keys

https://ask.streamsets.com/question/9775/unable-to-write-object-to-amazon-s3-the-request-signature-we-calculated-does-not-match-the-signature-you-provided-check-your-key-and-signing-method/

https://github.com/OCA/server-env/tree/14.0

Intenta instalar el módulo 'cloud_platform' que depende del módulo 'server_environment'.
Este último módulo no está disponible en su sistema.



## 7. Saber cuántas visitas. Conectar google analytics


https://analytics.google.com/analytics/academy/course/6/unit/1/lesson/1


We weren't able to verify your property: www.breadfree.es
