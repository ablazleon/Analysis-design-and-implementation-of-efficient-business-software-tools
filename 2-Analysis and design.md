# 2. Análisis y diseño (identificar y probar soluciones, diseñanado una apta y más barata)
## a. Identificación del caso de estudio (what if?/what wows?))
- Los siguientes casos de estudio definen el negocio
### eBusiness para artista y eBusiness para Breadfree => Kontá como plataforma SaaS

Empresas pequeñas con los procesos de negocio comentados anteriormente. Se plantea la necesidad de un servicio SaaS para proveer odoo

Ciertas aplicaiones digitales no son accesibles para los negocios hasta que no poseen suficiente capital para permitírsela: procesos tan importantes en un negocio como el catálogo web, la automatización del proceso de inventario y producción y la newsletter. Shopify, permite estos mínimos servicios a 30€/mes, pero requiere de un sistema de gestión de producción como katana que cuesta 100€/mes. Odoo ofrce una plataforma dónde automatiza estos tres procesos, pero a 100€/mes también. Por ello, se detecta una demanda de un servicio que ofrezca estos procesos a un precio menor, por ejemplo 15€/mes el servicio de catálogo + newsletter (como wix o shoopify lite( y a 50€/mes la automatización del proceso de inventario y producción.

- Misión de kontá: ofrecer estos procesos a un precio asequible para que los emprendedores se puedan concentrar en aportar valor y no en realizar tareas monótonas.

## b. Identificación de soluciones (what works?)
### Puesta a producción del servicio 
- Intento 0: Comparativa inicial: coste de vms con IaC en AWS, FaaS shop and GKE

Al principio tras comprar las disitntas formas de proveer con herramientas los procesos de negocios, se idnetifica iniciamnete un servicio FaaS cómo el óptimo en coste. Sin embargo, se plantea un piloto en el siguietne repositorio y se descubre que si bien FaaS es bastatne barato en cuanto al coste en función de las peticiones, obliga a rescribir todo el código.

https://github.com/ablazleon/shop-serverless

Más adletna se plantea una forma mejroada de gke + jenkins X [1](https://www.youtube.com/watch?v=eEcgn_gU3SM)

- Intento 1 1: saleor + gcp(cloud run + cloud sql)

En esta fase se esbozan disitnos casos de uso que más tarde serán expresados como procesos de negocio, y se plantea un despliegue con un coste mínimo de 10$/mes. Con el inconveniente de que saleor, si bien es muy persnalizable en cuanto al frontend, requiere de expertize para la configuración del frontend, y le falta de integraciones nativas, como con un sericio de gestión de inventarios. En esta fase dr provee el despliegue de saleor primero con heroku y luego con netlify; pero cloud runes más barato que estos servicios.

Comparación de recursos (proyectos de eccomerce (erp/crm o frontend + backend + cloud + db):
https://docs.google.com/spreadsheets/d/1Xon-1Qho6XSfOwBKpCQ4RG33cyaWvSCvdgt_JxIQYl0/edit?usp=sharing
https://medium.com/@ablazleon/my-journey-on-setting-up-an-ecommerce-learning-saleor-google-cloud-run-dns-31e7c94f4c9a

- Intento 2: odoo ce + aws(fargate+aurora serverless v1) vs odoo + gcp(crun+cloudsql)

No valen porque on preservan el estado

- Intento 3: odoo ce + vm + cloud sql (60€/mes)

Parece que todas estas soluciones alojadas en la nube son bastante costosas para pequeñas empresas

- Intento 4: Wordpress + WooCommerce + MrDomain (60€/año)

Si con eso es necesario, ¿para qué un despliegue en k8s? ¿Da odoo más valor que Wp+WC+inventario?

3 días ese depsleigue

he hecho un análsisi

25 qué hago Santiago?



## AWS

Despelgar fargate en pruebas: beta

- 1. Despelgar con copilot una app
- 2. Despelgar aurora
- 3. Despelgar faraget odoo + aurora

- 1. Despelgar un docker de ejemplo en fargate


[Desplegar un wordpress con copilot(aurora+faragete)](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/getting-started-aws-copilot-cli.html)

## GCP

Estrategia: sacrificar que la bbdd pueda tener muchas conexiones porque los créditos sean grátis en gcp. Se despliega una bbdd, y se intenta ajustar a que este coste tenga lo que costaría con shopify (30€), pero con gestión de impuestos e inventarios.

- Intento 3: odoo ce + gcp (vm+cloudsql)

- Intento 4: odoo ce + gcp (gke+cloudsql)

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




---------------


https://wikiprot.protaapp.com/11_vulnerabilities/#herramientas-para-gestion-de-vulnerabilidades

----------------

https://stackoverflow.com/questions/19948149/can-i-run-multiple-programs-in-a-docker-container

https://github.com/jbfink/docker-wordpress/blob/master/Dockerfile


-----------

activar la autenticación en dos apsos
crear un posgres12 e intentarlo allí


-----------

problema cuando credo dos bbdd en una

------------

si pongo el repo en privado no se auto actuliza, tengo que hacer las actions

ponerlo en público pero poner las amster password como un parámetro

--------
https://apps.odoo.com/apps/modules/14.0/delivery_sendcloud_official/

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


--------------

WARNING ? odoo.addons.base.models.ir_cron: Skipping database bf-dev because of modules to install/upgrade/remove.

------------


Estrategia cada caso de uso

SItio web

Marketing

Inventario

Crear productos, con referencia y precio, cada estrategia de precio

https://www.postgresqltutorial.com/postgresql-show-tables/
https://dba.stackexchange.com/questions/10142/how-to-make-it-impossible-for-a-postgres-user-to-delete-databases


------------

https://www.aselcis.com/en_US/jobs
https://www.aeodoo.org/forum/aeodoo-1


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
