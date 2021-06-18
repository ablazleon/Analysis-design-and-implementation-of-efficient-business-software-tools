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

AWS and GCP

## AWS

Despelgar fargate en pruebas: beta

- 1. Despelgar con copilot una app
- 2. Despelgar aurora
- 3. Despelgar faraget odoo + aurora

- 1. Despelgar un docekr de ejemplo en fargate


Then teh wordpress thing, https://docs.aws.amazon.com/AmazonECS/latest/developerguide/getting-started-aws-copilot-cli.html
Need not a root acount, https://docs.aws.amazon.com/IAM/latest/UserGuide/console.html

couse: AWS OTP-AWSD7
AWS: Getting Started with Cloud Security

Con copilot un multi az

https://aws.amazon.com/blogs/containers/introducing-aws-copilot/
Cost of the stack: https://stackoverflow.com/questions/65337280/how-to-get-budget-estimate-for-copilot

https://community.bitnami.com/t/help-on-architecture-for-odoo-deployment-with-multiple-sites-1-db/93346

with steps: https://aws.amazon.com/blogs/compute/building-deploying-and-operating-containerized-applications-with-aws-fargate/

with cli: https://aws.amazon.com/blogs/containers/running-wordpress-amazon-ecs-fargate-ecs/

Temproary managed credneitals
```
✘ execute "env upgrade --app demo --name test": get template version of environment test in app demo: get metadata for stack demo-test: get template summary: InvalidClientTokenId: The security token included in the request is invalid
        status code: 403, request id: f2dd98e8-f84c-4ef0-acc5-2a78d7c2aab5
        
        
admin:~/environment/demo-app (master) $ aws sts get-session-token --serial-number arn:aws:iam::764217278004:mfa/admin --token-code 273414

An error occurred (InvalidClientTokenId) when calling the GetSessionToken operation: The security token included in the request is invalid        
```

```
sudo curl -Lo /usr/local/bin/copilot https://github.com/aws/copilot-cli/releases/latest/download/copilot-linux \
   && sudo chmod +x /usr/local/bin/copilot \
   && copilot --help
```

no puedo isntalar docker en cloud shell y en cloud9 da problemas de iam.

aws cli 2 for copilot init

Then the wordpress https://github.com/bvtujo/copilot-wordpress

It seems it needs aws cofnigure after disabling it, it continue not working

Addons aurora

https://aws.github.io/copilot-cli/docs/developing/additional-aws-resources/
https://www.reddit.com/r/aws/comments/adre7w/is_anyone_using_aurora_serverless_in_production/
https://ecsworkshop.com/microservices/
https://aws.amazon.com/rds/aurora/serverless/
https://aws.amazon.com/blogs/database/best-practices-for-working-with-amazon-aurora-serverless/

https://medium.com/adobetech/deploy-microservices-using-aws-ecs-fargate-and-api-gateway-1b5e71129338, https://pereliksoft.com/index.php/2020/11/19/aws-fargate-vs-google-cloud-run/, https://thenewstack.io/comparison-aws-fargate-vs-google-cloud-run-vs-azure-container-instances/, https://medium.com/@jonah.jones/things-to-love-about-aws-fargate-part-1-deployments-c2a8a8349057, https://blog.codecentric.de/en/2021/03/fargate-with-efs-and-aurora-serverless-using-aws-cdk/, https://aws.amazon.com/blogs/compute/building-deploying-and-operating-containerized-applications-with-aws-fargate/, https://www.youtube.com/watch?v=Nv7s-N8ZxQA, https://cloudacademy.com/course/course-automatically-created-2018-10-02-113135226141/c3l4-terraform1/

https://www.youtube.com/watch?v=YCCFK2RRm7U


https://www.reddit.com/r/aws/comments/adre7w/is_anyone_using_aurora_serverless_in_production/
Better to manage cloud run

https://www.jeremydaly.com/aurora-serverless-the-good-the-bad-and-the-scalable/

https://www.reddit.com/r/aws/comments/n2ts9r/aurora_serverless_v2_approximate_release_date/

https://cloud.google.com/sql/docs/quotas#:~:text=Cloud%20Run%20services%20are%20limited,connections%20per%20deployment%20can%20grow.

o create eksctl vs autopilot for database

odoo saas, ask them how to do this

Try the differnet configruations

## GCP

Primero, en al cuenta de extra teleco: depsleigo grun + cluodsql

One odoo, and tehn one database and how to connect them. I will write the commands

CUando esto funcione, pruebo la perforamnce, y digo que ya está en prueba

Intentñe hacer backup pero no lo cosneguí. Hacer un ambiente de prueba y otro de proucción

Hoy: montar los dos, y hacer backup entre ese y uno de 40. Hacer video. Definri ese procidieminteo

CUando ese proceidmeinto funciona, mañana depseligo en la otra cuenta, con el scirpt los dos, sobre la configuración de las cuentas

De ese contendor a cloud run, no puedo tiene que estar dnetro

CLoudbuild: del repo creo en gcr una imagen, y caundo cambien el repo puedo cambiar la iamgen.

https://kinsta.com/blog/google-cloud-network/
https://gcping.com/
https://www.bunnyshell.com/blog/easily-deploy-odoo-cloud/

bunnyshell

Belgium

No hay dockerfile, qué ficheor confirugrar para que se conecte la bbdd

https://www.cloudbooklet.com/install-odoo-13-on-ubuntu-18-04-with-nginx-google-cloud/

cambiar en el odoo conf la ip publica a pincho

o con un dockerfile o directamtne desde bintami

Configurar una bbdd con las crdeniclaes

dos repos:

prod y dev, con 

- Despliegue odoo: https://www.youtube.com/watch?v=PSyGrZZOd3Q

https://aws.amazon.com/premiumsupport/knowledge-center/tags-billing-cost-center-project/

https://blog.doit-intl.com/how-does-a-cloud-sql-database-scale-and-what-to-know-when-setting-one-up-c23c52fc9947

Cómo hacer que cloud run coja las imágenes?

EN gcr de binami o direcatmenete

https://github.com/bitnami/bitnami-docker-odoo/blob/14.0.20210610-debian-10-r7/14/debian-10/Dockerfile

bitnami me isntala psogresql y no me vale

https://www.cloudbooklet.com/install-odoo-13-on-ubuntu-18-04-with-nginx-google-cloud/

cloudsql
https://www.cybrosys.com/blog/odoo-14-deployment-using-docker
y con docker

EL proceso de actualziar, hacer un fork, eso obliga a cloud build a ejecturase

como hacer que github actualice un fork autoamticametne

version en producción

vesion en prueba, cada mes actualizo, esta ligado a un repo que se actualiza siempre
la de produccion a uno que solo se actualiza cada mes

como con rpuebas comrpboar que funciona
load testing autaotmizar un camino

dos fork uno test y otro prod

Action of github to autoamtically chagne this

https://mathieu.carbou.me/post/649318432483033088/automatic-fork-syncing-with-github
https://gist.github.com/mathieucarbou/96ab30024f0d3fb44cac970219d23efc

Make this repo private, but with githu bactions

version en dev

cloudsql

https://cloud.google.com/sql/docs/quotas
https://blog.doit-intl.com/how-does-a-cloud-sql-database-scale-and-what-to-know-when-setting-one-up-c23c52fc9947

Es mejro una istnancia psotgrsql por cada db, o todas als dbs en una?


https://cloud.google.com/sql/docs/mysql/operational-guidelines
https://cloud.google.com/sql/docs/mysql/replication/create-replica

qué datos tampoco tan necesarios, el adress pero se puede borrar

no hace falta ha

probar distnais configuraciones:

superpotetne: distitnas

5 días, en una grande todo

creo una de cada, con lo mínimo

csot of backup

42.9€/m
automate backups daily, puede que haya perdido una comrpa
y puedo perder cleitnes suscritos

como hago backup, no hay para odoo 14

buena idea activar backup

la más abrata y luego otra

https://github.com/odoo/docker/blob/master/14.0/entrypoint.sh

HOST 1

How to creaet an user called odoo

------------

Can i change acocunt , oepnbank works

como orgnaizco los pagos https://www.bbvaapimarket.com/es/banking-apis/es-api-pagos-payments-psd2/
pero parece que no es grátis

https://www.unnax.com/blog/9-ways-psd2-is-fundamentally-changing-e-commerce-payments/
https://www.unnax.com/products/payments/

- 1. En la cuenta extra
- Subir el contenedor de odoo: cómo coenctar la bbdd sin url?
https://www.cloudbooklet.com/install-odoo-13-on-ubuntu-18-04-with-nginx-google-cloud/
crar la bbdd y conectarla con la máuqina virtual, dejar este ordena encendido por si acaso
script que cree un bbdd
- 1. Crear facturación con la cuenta extra

De qué manera escala cloud sql? CUántas conexiones permite?
https://cloud.google.com/sql/docs/quotas#postgresql

concurrent connections

cloudsql vs aurora serverless

having to allcoate a big thing for using it litlte times
https://www.jeremydaly.com/aurora-serverless-v2-preview/




------------

Flanks

DIrect payments

Fargate
NEwsletter
Tienda
hacer ceunta en n26


### Mejora continua: análisis de riesgos
