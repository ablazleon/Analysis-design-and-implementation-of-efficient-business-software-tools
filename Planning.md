
Marzo
Sprint 2: 10 de Feb al 10 de Marzo

1- Servicio de catálogo de productos para empresas barato y parametrizable (+ posibilidad de venta online)
- Crear dos trellos, uno privbado si quieres: uso ese que ya teníamos, para poenr un poco esto, loq ue hago en cada sprint: se puede poner así mono, uno público
- Un ecommerce + una página de contacto (primero contacto + ecommerce (más barato))
a- hacerlo en odoo enterprise verison (grátis) (per no sé de qué manera nos loquea) => más rápido (enseñar la prueba)
b- odoo community version
c- saleor => coste en perosnalización
- Cómo abaratar el ecommerce
Odoo parece parametrizable => 
- a - Desplegar un eccomerce de odoo de prueba: https://piedadleon.odoo.com/
- b- Evaluar qué funcionalidades no permite esta versión gratuita de odoo que sí permita un despliegue propio => a priori la gestión de almacen y el panel de información sobre ventas
- c- Serverless paraece barato => 
realizar un depsleigue sencillo de serverless + 
despliegue con ci/cd +
un despliegue en una máquina virtual de odoo community versión +
depsleigue de este odoo en serverless
=> en serverless habría que reescribir todo para que fucnionase en lambda
- d- Evaluar performane de esta solución
Realizar un servicio web (plagio de odoo.com/wix/shopify) para orquestrar la creación de servicios

March => do an eshop

- cheaper ecommerce with serverless, and more usable
- manage invetory
- other features rpa

1. First for free in odoo.com => something left
2. Then, impelment a service with serverless containers

Impelment odoo in vbox

4. Then implement oddo in serverless

https://www.serverless.com/blog/container-support-for-lambda

1. First for free in odoo.com => something left

Using Odoo do a basic webpage. With the ecommerce plugin 

https://www.youtube.com/watch?v=dErAZbzEkh0

a. THen it is set an spreadsheet a source of truth for the ecommerce
b. Remain teh same the changes to the website

Create from my user an add to other users

https://www.odoo.com/forum/help-1/openerp-online-how-to-create-a-new-user-or-allow-an-existing-one-to-connect-827

Enterpise vs community

- csv intergation for mass iamges
- stabel for users creation
- create bills
- stock inventory
- - autoamtitation vs investment

- manage invetory:

To handle the stock of shop or every warehouse, it helps a software that tracks the wares. It can be used an spreadsheet, the problem is that the log of itneraction is lost.

It is created an odoo erp and play with it.

A way to acces it transactgfull

How to know logs

over thsi transactions

I cannot do this netiehr form the ecomemrce neutehr from  invenotry
https://www.cybrosys.com/odoo/odoo-books/odoo-book-v14/

QUIero añadir cantidad y sueprmercado desaedo, y dont knwo if i can modify the data model

BUsiness intellegnece a coste de pcoa felxibildiad en lso objetos

Ordenaqrlo por la cantidad que falta comrpar => avoid this step of having to do this each time

- other features rpa

Serverless hybrid architecture:

https://stackoverflow.com/questions/63417602/how-to-connect-an-on-premises-application-to-aws-aurora-serverless
https://neilpatel.com/blog/loading-time/

=> what would happen if aurora servelress

3.6€
vpn => se puede  bajar a 3.6€ + more delay

https://cloud.google.com/solutions/automated-network-deployment-multicloud
more cost need of an ec2
https://www.odoo.com/es_ES/forum/ayuda-1/visual-database-design-schema-for-odoo-168392

https://www.bbva.com/en/economics-of-serverless/
https://dzone.com/articles/caas-services-through-aws-azure-and-google-cloud
https://www.reddit.com/r/docker/comments/c2swqc/comparison_between_container_orchestration/
https://aws.amazon.com/fargate/pricing/
https://arv14.medium.com/a-solution-to-serverless-adoption-cloud-run-aws-fargate-3c2942cc85b5

Sprint 3:

Abril 1,2,3,4,5

- [x] 1 quitar de gcloud la versión de saleor
- [ ] 2 revisar los videos sobre ecommerce e inventario: hasta qué aputno añade valor isntalar la versión community:
  -  integrar la subscripción a la newslettter en la web => ¿cómo añadir una newsletter en odoo? https://www.youtube.com/watch?v=LmG-yxxFmPc
  -  cambiar de una el nombre de los productos
- [x] 3 estudiar lo de meter en un excel las urls de lso productos apra tenr una especie de backup de los productos https://www.youtube.com/watch?v=ThRUxHCndDs => use community
- [ ] 4 estudiar lo de productos con distintos tamaños
- [ ] 5 estudiar lo de meter en un excel las urls de lso productos apra tenr una especie de backup de los productos
- [ ] 6 preguntar a Víctor Facic mejor manera para desplgieues en lanube baratos (clodu run + cloud sql vs fargate + aurora serverless vs linode) => en youtbe: su solución es que no sabe => preguntar en stckovf como ven alicloud en cuanto a costes, ibm code engine vs cloud run: en caas => alicloudsólo preio por hora pero se apagan sólos 
  - budget comparasion
  - https://www.quora.com/How-does-Amazon-compare-to-Alibaba-Cloud-Service => maybe its chaeaper, 
  - ibm has contianer as a service, but not database serverless
  - https://www.alibabacloud.com/help/doc-detail/194524.htm?spm=a2c63.p38356.b99.136.10f62388NoQio6#section-p74-zs8-s6z, it seems to be billed by hour
  - difficult to find isntances with pay as you go https://www.parkmycloud.com/blog/aws-vs-alibaba-cloud-pricing/
  - https://www.alibabacloud.com/blog/alibaba-cloud-free-trial-how-to-sign-up-and-get-started_595840?spm=a3c0i.8276372.5363776690.1.56b26ed6l1U9db
  - https://www.alibabacloud.com/blog/getting-started-with-container-service_595870?spm=a3c0i.8276372.5363776690.213.56b26ed6l1U9db
  - https://www.alibabacloud.com/blog/devsecops-best-practices-on-alibaba-cloud-%E2%80%93-building-an-e-commerce-application_593846?spm=a3c0i.8276372.5363776690.225.56b26ed6l1U9db
  - db: only 60 days free => it's not worth it, what it is worth it is ine year of use
  - how to deploy odoo: stateless + state
  - => can give me advice:  based on tehir experince what is cheaper: teh 5 of them
- [ ] 7 desplegar en vbox odoo
- [ ] 8 desplegar en gcloud 
- [x] 9 para evaluar necisto saber cómo usarlo: más que en concreto en abstracto: pedir aputnes del itirnerario de gestión o hay n profe que oferta un tfm, oye estoy intentando impelemantr uno, como que no tengo la parte de invenstairos, más adleante le improta hablar. COIT mentorizado
- [ ] 10. Cómo formatear el texto: ppt + un texto explicativo + un jupyer con text abierto por si se quiere en plan awesome list y traducirla (inglés) 

1,2,3,4
=> auditar el despleigue: Aselcis o a quién pregunto para auditar ese despliegue
=> meter plataforma de pagos
=> evlauar lo del portencaje que se llevan las pasarelas de pagos (preguntar a Alex que hizo su TFG de eso si la pasaerla de apgos de caixa que estudió es segura)
=> meter lo de google analytics para saber cuántas visitas llegan
=> (leenversefashion) el despliegue de odoo: y el conector para itnergarlo con shopify


=> estudiar cómo se va a gestioanr stock (directamente decir que en una semana puede llegar)
=> método de trasnporte (correos o portefy)
=> compartir la página
=> cómo integrar facturas
