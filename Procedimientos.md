# Procedimientos

## 1. Creación manual de un servicio odoo ce (crun+csql)

## 2. Procedimiento de backup

## 3. Procedimiento de actualización

## 4. Bug/mejora. Usar http2 parapermitir backups mayores de 32 MB.

## 5. Procedimiento de control de acceso autorizado

## 6. Bug/mejora. Cloud run es stateless, no persiste los VOLUMEs.

## 7. Saber cuántas visitas. Conectar google analytics

## 8. Desplegar odoo ce vm+cloudsql

## 9. Configurar productos: variantes, estrategia de precios y descuentos

## 10. Maquetar el diseño

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

Se añade el código de camptocamp. Se añade al script las dependencias necesarias. Lo instalo pero con el requirement no sale. bdist wheel en el camp2camp
[1](https://github.com/aws/aws-cli/issues/4243), [2](https://stackoverflow.com/questions/34819221/why-is-python-setup-py-saying-invalid-command-bdist-wheel-on-travis-ci/49426845). [3](https://realpython.com/python-redis/) The requirment says it is needed redis 2.10.5, why it cannot be used a redis higher? WHich si the redis version that mathces? Hay un pyaml there. Se itnetna con un redis 4. Sino se va montando un 13 [4](https://cloud.google.com/memorystore/docs/redis/scaling-instances) Scaling is a bit hard 
[5](https://cloud.google.com/memorystore/docs/redis/pricing) +32€. ¿Por qué no se ven los módulos, sólo si los ahgo uno a uno sí? no aparecen los módulos aunque la db sea nueva => nos módulos extra. 

bfdev3 cobn todos los módulos
bfdev4 con 13
bfdev5 con un sólo módulo


```
Could not get content for /website/static/src/scss/options/user_values.custom.web.assets_common.scss defined in bundle 'web.assets_common'.
```

style compilation
say there's a problem with redis

poner un issue: hay un problema con redis

put an issue this does not wo

falla la compilación: será porque cloud run no alberga la sesión o porqué?

repeat this anotehr time and check why this happen

### Images 

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

[Esto lleva a problemas de visualización de js y css](https://stackoverflow.com/questions/68334528/have-you-found-a-way-of-persisting-the-odoo-core-modules-in-v14-different-form-a). [No se muestra css](https://www.odoo.com/es_ES/forum/ayuda-1/no-css-no-images-after-user-logout-from-website-127642)

```
Failed to load resource: the server responded with a status of 404 () web.ssets frontend.css:1
```

[si cloud run no persite los volúmenes, los addons se van](https://www.odoo.com/es_ES/forum/ayuda-1/how-to-configure-the-filestore-in-high-availability-172440)
[Con attachments](https://github.com/itpp-labs/misc-addons/tree/11.0/ir_attachment_s3)
[Otros casos](https://www.odoo.com/es_ES/forum/ayuda-1/css-and-js-files-are-not-loading-96868)

```
GET4041.04 KB24 msChrome 91 https://bf-dev3-u7raxlu3nq-ew.a.run.app/web/content/290-f328144/1/website.assets_editor.css
```


[Parece que sí es posible con autoscaling groups](https://dokumen.tips/business/simple-odoo-erp-auto-scaling-on-aws.html) [2](https://www.slideshare.net/lecadoujr/simple-odoo-erp-auto-scaling-on-aws)

Se elige París como localización de bucket: [1](https://www.cloudping.info/), [2](https://aws.amazon.com/s3/pricing/)

```
eb/content/258-3d5e37d/web.assets_common.css:1 Failed to load resource: the server responded with a status of 404 
```

```
Bad Request
Session expired (invalid CSRF token)
```




-------------

Regenerate the keys

https://ask.streamsets.com/question/9775/unable-to-write-object-to-amazon-s3-the-request-signature-we-calculated-does-not-match-the-signature-you-provided-check-your-key-and-signing-method/

https://github.com/OCA/server-env/tree/14.0

Intenta instalar el módulo 'cloud_platform' que depende del módulo 'server_environment'.
Este último módulo no está disponible en su sistema.



## 7. Saber cuántas visitas. Conectar google analytics


https://analytics.google.com/analytics/academy/course/6/unit/1/lesson/1


We weren't able to verify your property: www.breadfree.es

## 8. Desplegar odoo ce vm+cloudsql

[Tutorial](https://www.youtube.com/watch?v=UAamkipG8R8) + [csql integration](https://www.cloudbooklet.com/how-to-install-odoo-14-on-ubuntu-20-04-google-cloud/)

Se elige esta opción por ser más fácil de despelgar al principio y poder prototipar si odoo ce es válido o no.

- 1. Desplegar el contenedor desde el creado en cloud run.

- 2. Lo bueno de usar odoo 14 con psotgres 12 es que se peude migrar breadfree.

- 3. Odoo git en minúsculas

- 4. Pirmero se conecta a una red pública, luego se prueba con una privada

- 5. Crear el usuario odoo

- 6. Cambiar la versión de la vm sin borrarla, temrina borrando el disco

- 7. [Cómo conectar la vm y cloud sql](https://timtech4u.medium.com/connecting-to-cloud-sql-from-vm-instances-on-google-cloud-platform-f43166716346#:~:text=On%20your%20GCP%20Console%2C%20click,ahead%20and%20select%20Create%20Instance.&text=Go%20ahead%20and%20input%20your,ID%2C%20Root%20Password%20and%20Zone.)

- 8. [Set the primary internal ip as allowed connections](https://www.odoo.com/es_ES/forum/ayuda-1/hardware-requirements-for-odoo-11-138936)

- 9. FUnciona aun concetada a una red itenrna, pq está en dafult

- Si tengo que activar un balanceador de carga para tener https, cada una tendrá un filestore distitno. [1](https://cloud.google.com/load-balancing/docs/https)

Parece que lo que se debe proponer es craer un cluster, o un scaling group

https://docs.cloudbees.com/docs/cloudbees-ci/latest/cloud-setup-guide/gke-https-setup


en autoscaling group la memoria de una vm puede ser accedida por otra

https://www.todobravo.es/que-dominio-elegir-para-tus-paginas-web-com-es-eu/

instance group

https://www.namecheap.com/domains/registration/results/?domain=piedadleon
https://domains.google.com/registrar/search?searchTerm=piedadleon&hl=en#
https://www.reddit.com/r/webhosting/comments/j7f5tv/premiumdns_with_namecheap_is_it_worth_it_or_give/

https://www.cloudflare.com/learning/dns/what-is-cloudflare-registrar/

https://www.gregoryvarghese.com/why-im-switching-from-namecheap-to-cloudflare/

piedad elon .art y cambari en 60 días

```
The requested URL / was not found on this server. That’s all we know.
```

CUidado con lso puertos 8069 en el helathcheck

Por qué dice el health check que no está healthy?

```
psycopg2.OperationalError: FATAL:  remaining connection slots are reserved for non-replication superuser connections
```

Se feurza a reiniciar

Cómo saber cuándo hay un error para reniciar?

bbdd más memoria par que quepan otros plugins

COmo coenctar el banco a strupe

https://odoo-community.org/groups/contributors-15/contributors-66571

Muchas conexiones abiertas

https://cloud.google.com/load-balancing/docs/https/setting-up-https

añadir una regla de firewall

https://stackoverflow.com/questions/30419407/google-compute-engine-http-load-balancer-not-working-after-vm-restart

si da ssl protocol error se le quita la s

cuidado en s3 da problema de signatura, pero se peude descargar con un comando parecido a través de aws cli

```
aws s3api get-object --bucket odoo-backup-dev --key ./breadfree.2021-07-12_19-33-18.info /mnt/c/Users/ablaz/PycharmProjects/breadfree.2021-07-12_19-33-18.info
```

Se desnicripta con la clave, en mi caso la master y gpg, o estas instructs https://github.com/itpp-labs/misc-addons/blob/14.0/odoo_backup_sh/doc/index.rst

AL hacer más grnade la vm se pierde el volumen

https://piedadleon.art

THe oauth client was not found

o es impresión o es original, precios y sotcks disntios para cada producto

## 9. Configurar productos: variantes, estrategia de precios y descuentos

como crear la opcion metodo de entrega

no s epued esubir iamgénes da igaul como lo ahga

preserved state size

S3 attachemnt lead to this

```
The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "/usr/lib/python3/dist-packages/odoo/http.py", line 639, in _handle_exception
    return super(JsonRequest, self)._handle_exception(exception)
  File "/usr/lib/python3/dist-packages/odoo/http.py", line 315, in _handle_exception
    raise exception.with_traceback(None) from new_cause
binascii.Error: Incorrect padding
```

https://www.packlink.es/elegir-servicio?hash=1gr61z

https://www.puntopack.es/espacio-pro/ofertas-y-servicios/oferta-a-medida/modos-y-pais-de-envio/

puntopack

no se puecde exprota r a xls las variantes

cuando le doy al carrito desaprarece

[admitting to http](https://cloud.google.com/load-balancing/docs/https/setting-up-http-https-redirect#console_6)


redirects

```
gcloud compute forwarding-rules create http-content-rule \
   --address=35.227.243.117 \
   --global \
   --target-http-proxy=http-lb-proxy \
   --ports=80
   ```

Adding a cutom header

  ```
gcloud compute backend-services update odoo-dev-backend \
    --global \
    --custom-response-header='Strict-Transport-Security:max-age=31536000; includeSubDomains; preload'
  ```

discounts

cuando crean muchas vairantes empeiza a djear d efuncioanr la db

migro a una db mayor

https://www.odoo.com/forum/inventory-11/can-t-import-variants-due-to-error-on-attribute-186407

https://cloud.google.com/products/calculator/#id=fcb44e5e-252b-4deb-88e3-90f9750e9944

montarlo varias veces una para cada

Plan para que salga más barata la tienda:

- 1. Migrar la vm a una ucenta con un carné, siendo esta la cuenta principal. Así aguanto 3 meses, luego 3 ceuntas más, ahorrando como 800€  

- 2. En el mientras, despelgar en k8s o con autoscaling para reducir coste. Por qué no se conecta con las orgnaizaicones de las que soy partícipe?

- 0. Sobre el código crear un container

- a. Crear vm: con 4Gb y 2 de CPU con una regla de fw pemrition el puerto 8069

- b. crear sql, 1 y 1.7

- c. [crear lb.](https://cloud.google.com/load-balancing/docs/https/setting-up-http-https-redirect#console_6) y [admitting to http](https://cloud.google.com/load-balancing/docs/https/setting-up-http-https-redirect#console_6)

- d. [Setup domain](https://www.youtube.com/watch?v=245ZJLm1AV4&t=1464s)

En una ceunta se crea un cluster de gke  con una tamaño mínimo, dos uno de autopilot y otro de normal

```
Region "us-central1" for subnet "default" does not match cluster's region "us-west2"
```

https://stackoverflow.com/questions/62362051/gcp-kubernetes-engine-my-first-cluster-config-when-i-change-the-zone-cluster

healthc cheak en el puerto correpoenidnete

Cambienado el tiempo de drianing

https://kinsta.com/knowledgebase/err_ssl_version_or_cipher_mismatch/

Porque el certiifcado es´ta asoicado a varios dominios

```
ERR_SSL_VERSION_OR_CIPHER_MISMATCH
```

Psa un itempo y caindo sólo está asociado a uno se va solcionando

Se ocnfigura un primer setup para hacer el siege y ver cuántos usuairos siporta

cómo escala?

- 1. Hacerlo con vm, cuántos usuarios permite? Qué hacer si me quedo sin servicio? Parece que es la bbdd la que tiene el límite, como en la iamgen salía no puede hacer más coenxiones. AUtoescalado de la bbdd en k8s

- 2. Hacerlo con autoscaling groups: de qué es lo que se queda con poco primero. Como ligar el disco

- 3. Probar con k8s


## 9. Configurar productos: variantes, estrategia de precios y descuentos

Prodcutso > configurar vairantes

Alamacenable

Hace el serivio cuan alguien pide 1 se crea y ya está

Pago seguro a tra´ves de bbva

https://www.gestoriaonlinesapientia.com/consejos-fiscales-tienda-online/

https://getquipu.com/blog/abrir-tienda-online-sin-ser-autonomo/

darse de alta como autónomo

https://www.elabogadodigital.com/obtengo-unos-ingresos-reducidos-debo-darme-de-alta-como-autonomo/

Que sea habitual cuando llegue al SMI a lso 400 habrá que darse de alta y tener menos benficios

https://www.infoautonomos.com/seguridad-social/tarifa-plana-autonomos/

9 meses ganando eso 

https://pro.packlink.es/becommerce/vender-en-etsy-sin-ser-autonomo/#:~:text=Etsy%20es%20una%20plataforma%20internacional,para%20vender%20en%20la%20misma.&text=Aunque%20circula%20un%20falso%20mito,existe%20esta%20norma%20como%20tal.


https://www.odoo.com/forum/help-1/importing-products-with-variants-including-internal-reference-and-barcode-per-variant-160219

https://www.odoo.com/es_ES/forum/ayuda-1/importing-products-with-without-product-variants-146115

Crear un product de cada tipo

https://debitoor.es/blog/iva-artistas-autonomos

cómo añadir el iva

footer con la ceunta bnacaria

https://www.europapress.es/estar-donde-estes/noticia-impuesto-sociedades-cuando-toca-presentarlo-20190702173125.html#:~:text=El%20impuesto%20sobre%20sociedades%20es%20un%20tributo%20competencia%20del%20estado,1%20de%20enero%20de%202016.

https://www.bankia.es/es/bankademia/pymes-y-autonomos/autonomos/iva-autonomos

Cómo hacer facturas

https://ayudatpymes.com/gestron/vender-por-internet-sin-ser-autonomo/

https://www.shopify.es/blog/113361733-tengo-que-hacerme-autonomo-si-tengo-una-tienda-online

EMpezar a vender ocnsistiría en impuestos + cuota de autonomos

Poco probable si poco 

no hago facturas: pero cobro impuestos

no cobro impuestos, tienda online 3 meses

o a través d einstagram directmatne, a través de biuzm o de paypal

la teinda onlien no la publqucamos sólo usamos para hacer el proceso más fácil

creo un cliente

o primero instagram y en 6 meses si funciona pago

o no pago, en 6 meses in facutra y que la gente compra directmatne desde ahí y desde etsy

y a partir de 6 meses hacienda impuestos y cuota praece esporádica

que lo grandes sean a través de ella

que los orgiainels sean a través y así puede el que envíe los pagos a mí a ella o a Marta en el peor de los casos

para los originales a2 contacr con la ertista

de alta vale lo cerramos sólo da ese poco

eso sin iva y se va viendo

1- hacer un instagram profesional para los encargaos (acepto ideas)
2- tienda onnline y etsy para los pequeños

https://www.tiendanube.com/blog/como-vender-por-instagram/

https://www.infoautonomos.com/blog/autonomo-varias-actividades-obligaciones/


https://www.youtube.com/watch?v=CW4hQ32C1ZQ

estado del arte esporádica: bot de email vs eccommerce

https://mailytica.com/en/pricing/

https://www.youtube.com/watch?v=xfj7X-rA4_I

https://www.creativebloq.com/wordpress/free-wordpress-backup-plugins-101517335

## 10. Maquetar el diseño

En intentos previos en este proyecto usé figme para maquetar el diseño. En un segundo intento se crea un proyecto en google sites que se ofrece al cleitne para que edite el texto y las imágenes.


-----------------

woocmerce different shoippings
promotions
jem woocommerce
