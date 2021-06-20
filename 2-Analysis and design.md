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

---------------

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
