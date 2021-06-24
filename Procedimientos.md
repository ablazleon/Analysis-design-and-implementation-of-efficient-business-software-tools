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
- 2 se hace a postgres owner de  la db. Porque si no odoo conectado a breadfree no prodía borrarlo
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
Añadirle a este Dockerfile el addon de backup. Meter las credenciales de aws en ello. COnfigurarla cómo funciona.

Luego el addon de attachment a s3.


-------------

## 3. Procedimiento de actualización

Cómo activar la actualizacion autoamtica con github actions

Un DOckerfile más serio con un github actions para hacer pulling


Probar ocn un docekrfile: un ockerfile público sin la contraseña, sino tenog que ahcer una github action, y eso no escala
Hay que ahcerlo no se hace sólo

https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions

-------------

## 4. Mejora. Usar http2 parapermitir backups mayores de 23 MB.

No peude exceder de 32MB la request. 

https://support.websoft9.com/docs/odoo/zh/else-troubleshooting.html#odoo-related
https://cloud.google.com/run/quotas

Necesidad de hacer un cambio, que no es fácil a prioir https://cloud.google.com/blog/products/serverless/cloud-run-gets-websockets-http-2-and-grpc-bidirectional-streams

https://stackoverflow.com/questions/61231930/can-i-have-my-cloudrun-server-receive-http-2-requests

Se pdoría intentar un script que rellenaes la bbdd.

```
upstream connect error or disconnect/reset before headers. reset reason: protocol error
```

Cómo hacer bvackup si no se peude hacer a travñes de ahí

Hya dos partes: filestore y sql. Parece que si sólo hago backup de eso, falla

en el dump he pdoido saber la verisón de la bbdd, es necesario los filesotre? sí

probarlo con ese posgres 13, puede que la versión o sea la misma

en odoo qué está en filestore y qué en la bbdd. QUé pasa si no restauro el filestore y sólo el dumping en sql? algo tiene que spar proque pesa abastante

cómo lo restauro entonces?

https://firebase.google.com/docs/firestore/quickstart#python_1

tocar c´doigo lo que impclairá hacer tests
https://apps.odoo.com/apps/modules/12.0/auto_backup/
https://stackoverflow.com/questions/348363/what-is-the-best-place-for-storing-uploaded-images-sql-database-or-disk-file-sy
https://portcities.net/blog/tech-blog-6/post/why-companies-should-host-odoo-on-cloud-and-advantages-of-google-cloud-platform-29


https://kyoukai.readthedocs.io/en/latest/adv/http2.html
https://www.tunetheweb.com/performance/http2/
https://www.odoo.com/es_ES/forum/ayuda-1/v-14-recommendation-for-web-server-for-odoo-183087
https://developers.google.com/web/fundamentals/performance/http2
https://cloud.google.com/blog/products/serverless/cloud-run-gets-websockets-http-2-and-grpc-bidirectional-streams

Vamos a ver tenemos un problema

EN hacer bakup para pasar eso de ahí, al otro si fuera necesario, el problema es que el límtie están en 32 megas,
parece uqe no se peude más y no s epeude hacer backup de otra forma, porque tiene lso fiels een filesystem. Lo suyo se´ria usar un servico de filesystem para que cuest menos lso coentendores no necesitan tanta memoruia, y pro otro lado s epuede haecer backup. pero impclia cambiar c´dogio y eso impclai tiempo y mcuhas purebas.

Solcuioens que se me ocurren, hay un m´doulo que hacee autobackup puedio rpobar con él, aún a´si nada
o reducrilo para que lelgue a 32 o activar http2. Parace que els ervidor web que usa odoo (wekzeug, osea como apcah nginx) no pemrite http2, hombre pdoría poner en esa misma imagen un coentendor nginx para que encapsulara en http2, hombre pdrá funcionar

qué permiti´ria sobre todo no dpeneder de cauntas iamgens pognamso, ese cloud autoamtion no vale para iamgens

https://serverfault.com/questions/966408/google-cloud-run-how-to-mount-filestore-nfs

no soprota filestore

alguna psoiblidad de http2, sino backup, no

Poner un nginx, pero no hace falta tiene su propio blacneador

https://stackoverflow.com/questions/38878880/serving-python-flask-rest-api-over-http2

quart

conactenar un gninx, no sé qué configuraicion

https://stackoverflow.com/questions/61794069/cloud-run-needs-nginx-or-not
https://stackoverflow.com/questions/37004983/what-exactly-is-werkzeug
https://www.odoo.com/documentation/12.0/administration/deployment/deploy.html#https
https://softwareengineering.stackexchange.com/questions/382777/clearing-up-misconceptions-about-a-flask-backend-and-client-side-rendering

no hace falta poner un nginx, ya tien uno gcrun

SI pongo un lb tengo que manejar ssl, y además, va a salir muy caro

https://www.novixys.com/blog/python-web-application-docker-nginx-uwsgi/

cómo poner para que odoo sea ejecutado por nginx en un container, ejecutarlo en el puerto 80. Quizá poner un issue

Hcaer una demo, probar con eso y sino, pero dónde lo dejo?

How to set in a Dockerfile an nginx in front of a container? I tried making odoo handle http/2(on gcloud run) through running an nginx in front of it

Hi! Thanks in advance :)  My question is, how to set in a Dockerfile an nginx in front of a container? I saw examples like this [0], but they all use docker compose to run the nginx in front of it. The only example I saw that runs both in the same container is this [5], but I don't understand the steps. Can you give me any documentation that I can understand? Because according to this example I should modify the Dockerfile adding in the last lines a RUN:

They are tow processes I cannot run two processes in one container

The rest of the Dockerfile is in here [4]:




```
... more

COPY wait-for-psql.py /usr/local/bin/wait-for-psql.py

# Set default user when running the container
USER odoo

=> Here
# After setting proxy-mode in odoo-conf
docker run --link odoo:odoo --name nginx -v /nginx/nginx.conf:/etc/nginx/nginx.conf:ro -d -p 80:80 nginx
=>

ENTRYPOINT ["/entrypoint.sh"]
CMD ["odoo"]
```

```

```


 I'm deploying an odoo ce on google cloud run + cloud sql. I configured one odoo as a demo with 5 blogposts and when I tried to download it, it says that the request was too large. Then, I imagined this was because of the 32MB of cloud run request quota [1]. Then, I saw that the quota for http/2 connections was unlimited, so I activated http/2 button in cloud run. Next, when I accessed the service an error relating "connection failure appeared". So, my first question is, **anyone that has been able to make automate backups in odoo with cloud run, have you been able to make odoo handle http/2 connections (on google cloud run)? Can you give me any advice of how have you done it?**

To do so I thought of two ways: one, was upgrading the odoo http server to one that can handle http/2 like Quark. This first way seems impossible to me, because it would force me to rewrite many pieces of odoo, maybe. Then, the second option that I thought of was running in front of the odoo container (that runs a python web server on a Werkzeug), an nginx. I read in the web that nginx could upgrade connections to http/2. But, I also read that cloud run was running its internal load balancer [2]. So, my second question: **would it be possible to run in the same odoo container an nginx that exposes this service on cloud run?** 

I read some documentation about running an nginx in front of an odoo service in a vm [3]. So it would be just adding this code to the odoo Dockerfile?




However, as cloud run needs containers, I think if I setup the nginx entrypoint and also the run entrypoint.sh in the Dockerfile these both may crash [4]. I'm googling a lot if 


[0] https://github.com/Verisage/docker-nginx-letsencrypt-odoo/blob/master/docker-compose.yml
[1] https://cloud.google.com/run/quotas
[2] https://stackoverflow.com/questions/61794069/cloud-run-needs-nginx-or-not
[3] https://linuxize.com/post/configure-odoo-with-nginx-as-a-reverse-proxy/
[4] https://github.com/odoo/docker/tree/master/14.0
[5] https://github.com/swoldanski/odoo-nginx-docker-multitenant

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

