# 2. Análisis y diseño (identificar y probar soluciones, diseñenado una apta y más barata)
## a. Identificación del caso de estudio (what if?/what wows?))
- Los siguientes casos de estudio definen el negocio
### eBusiness para artista y eBusiness para Breadfree => Kontá como plataforma SaaS

Empresas pequeñas con los procesos de negocio comentados anteriormente. Se plantea la necesidad de un servicio SaaS para proveer odoo

Ciertas aplicaiones digitales no son accesibles para los negocios hasta que no poseen suficiente capital para permitírsela: procesos tan importantes en un negocio como el catálogo web, la automatización del proceso de inventario y producción y la newsletter. Shopify, permite estos mínimos servicios a 30€/mes, pero requiere de un sistema de gestión de producción como katana que cuesta 100€/mes. Odoo ofrce una plataforma dónde automatiza estos tres procesos, pero a 100€/mes también. Por ello, se detecta una demanda de un servicio que ofrezca estos procesos a un precio menor, por ejemplo 15€/mes el servicio de catálogo + newsletter (como wix o shoopify lite( y a 50€/mes la automatización del proceso de inventario y producción.

Misión de kontá: ofrecer estos procesos a un precio asequible para que los emprendedores se puedan concentrar en aportar valor y no en realizar tareas monótonas.

## b. Identificación de soluciones (what works?)
### Puesta a producción del servicio 
- Intento 0: Comparativa inicial y FaaS shop

Al principio tras comprar las disitntas formas de proveer con herramientas los procesos de negocios, se idnetifica iniciamnete un servicio FaaS cómo el óptimo en coste. Sin embargo, se plantea un piloto en el siguietne repositorio y se descubre que si bien FaaS es bastatne barato en cuanto al coste en función de las peticiones, obliga a rescribir todo el código.

https://github.com/ablazleon/shop-serverless

- Intento 1 1: saleor + gcp(cloud run + cloud sql)

En esta fase se esbozan disitnos casos de uso que más tarde serán expresados como procesos de negocio, y se plantea un despliegue con un coste mínimo de 10$/mes. Con el inconveniente de que saleor, si bien es muy persnalizable en cuanto al frontend, requiere de expertize para la configuración del frontend, y le falta de integraciones nativas, como con un sericio de gestión de inventarios. En esta fase dr provee el despliegue de saleor primero con heroku y luego con netlify; pero cloud runes más barato que estos servicios.

Comparación de recursos (proyectos de eccomerce (erp/crm o frontend + backend + cloud + db):
https://docs.google.com/spreadsheets/d/1Xon-1Qho6XSfOwBKpCQ4RG33cyaWvSCvdgt_JxIQYl0/edit?usp=sharing
https://medium.com/@ablazleon/my-journey-on-setting-up-an-ecommerce-learning-saleor-google-cloud-run-dns-31e7c94f4c9a

- Intento 2: odoo ce + aws(fargate+aurora serverless v1) vs odoo + gcp(crun+cloudsql)

AWS and GCP (resultado del state of the art)

## AWS

Despelgar fargate en pruebas: beta

- 1. Despelgar con copilot una app
- 2. Despelgar aurora
- 3. Despelgar faraget odoo + aurora

- 1. Despelgar un docker de ejemplo en fargate


[Desplegar un wordpress con copilot(aurora+faragete)](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/getting-started-aws-copilot-cli.html)

## GCP

Estrategia: sacrificar que la bbdd pueda tener muchas conexiones porque los créditos sean grátis en gcp. Se despliega una bbdd, y se intenta ajustar a que este coste tenga lo que costaría con shopify (30€), pero con gestión de impuestos e inventarios.

Se plantea:

7-17 jun: plantear estrategia
17-25: ejecutarla
25 decidir si se puede desplegar odoo o mejor shopify

-------------

COger el de bookstore

comprar el dominio de piedadleon

ponerlo como kontá

hago esas dos, y cofngiro las cosas

Estrategia de backup:
diariamente

https://www.odoo.com/es_ES/forum/ayuda-1/domain-name-for-website-in-odoo-community-edition-152627



```
Error: Request Entity Too Large
Your client issued a request that was too large.
```



```
Database restore error: Postgres subprocess ('/usr/bin/pg_restore', '--dbname=breadfree', '--no-owner', '/tmp/tmplkjmgika') error 1
```
```
Internal Server Error
The server encountered an internal error and was unable to complete your request. Either the server is overloaded or there is an error in the application.
```



Borrar las tablas

```
gcloud sql connect db4 --user=odoo --database=breadfree --quiet
```

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

---------------

Un trello con errores centor de atenicón al usuario

quién se entere que llame

erroreres comunes

el límite es 52 cómo hagfo para hacer bakcups

sino lo puedo ahcer a tarves de la web o migro a http2

newsletter el 8 va a estar y el ivenntaroo también, eso me ralla y es cierto que .

S´ñigueme ptrutnagnto per sí que es ceirto llevo este mes he parpendido

Te lo dejo motnado esta semana, decidir con tiempo, darle caña a eso: temo lo de la beca,t elo digo con tiempo
100% no voy a estar, 8 h con lo de bvakcup, 2-4h a la smeana cosas putnaules Adir he itnetando mucho esto y no me funciona. 

Por ejemplo, inventario d eproductos lo esoty autnamizanod, paln d eproduccion ym naudfatutra, en casa de pasta no van las cosas bien. Ya vendéis y ya os podéis permitir a alguien incluso a una cosnutlora, esoty ivnlocrado, pero ya me ahn lalamdao la atneiconen csa de que tengo que ganar pasta

os hago el cambio 3 meses si querési con una cuenta mía que se ahce g´ratis. Háblalo con Miguel

SI quieres create una cuenta en gcp y te lo desplñegio en tí, me mola mazo ofrecerlso gra´tis y he pdpido contiuair, pero síq ue es cierot que a tope no puedo estar

1- backup
2- esta smeana caña a eso

31 junio
operación Manu
ahcer un software, compras hasta pagar 100€, 2 meses grátis  a partir de ahí parte va par ala saca
7 julio

buscar en oca, oye he hecho esto
no tenog nignuan ventaja diferneical, soy otro más co nmenos conocieminto
tengo conomeitnos de seguridad
coentarle un splunk

15 de julio
misnait 
aws

------------


Estrategia cada caso de uso

SItio web

Marketing

Inventario

Crear productos, con referencia y precio, cada estrategia de precio

https://www.postgresqltutorial.com/postgresql-show-tables/
https://dba.stackexchange.com/questions/10142/how-to-make-it-impossible-for-a-postgres-user-to-delete-databases


---------------

Mejor método de pago:

https://www.xataka.com/basics/6-alternativas-bizum-para-enviar-dinero-al-momento



Can i change acocunt , oepnbank works

como orgnaizco los pagos https://www.bbvaapimarket.com/es/banking-apis/es-api-pagos-payments-psd2/
pero parece que no es grátis

https://www.unnax.com/blog/9-ways-psd2-is-fundamentally-changing-e-commerce-payments/
https://www.unnax.com/products/payments/

https://jaychapel.medium.com/4-ways-to-get-google-cloud-credits-c4b7256ff862
https://www.joinffl.com/program

Hasta que punto es mala idea lo de pedir creidtos de cloud? QUñe procentaje de la empresa se queddan?

https://bonbillo.com/?cat=-1

Ask this for breadfree and for kontá

https://www.bunnyshell.com/blog/easily-deploy-odoo-cloud/

bunnyshell

Flanks

DIrect payments

Fargate
NEwsletter
Tienda
hacer ceunta en n26


### Mejora continua: análisis de riesgos
