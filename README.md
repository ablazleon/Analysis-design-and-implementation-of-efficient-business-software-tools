# Analysis-design-and-implementation-of-efficient-business-software-tools

Análisis, diseño e implementación de un servicio de comercio electrónico en la nube

Desarrollo de un servicio de software para empresa competitivo

En este docuemnto describo mi propuesta de anteproyecto y realizo un borrador sbore la estrucutra del documento del proyecto.

# 0- Propuesta de requisitos para este sprint

# 1- Anteproyecto

# 2- Memoria (índice)

-----------

# 0- Propuesta de requisitos para este sprint ( de entre el esquema general de objetivos)

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

2. Registar productos para analizar daots sobre el uso del almacen

3. Automatizar trámites (puede que con RPA)/ o hacer un plan de operación de ciberseguridad / o hacer los pagos con PSD2 para que sean grátis en vez de pagar a una pasarela

# 1- Anteproyecto

## Autor

Raúl Adrián Blázquez León

## Tutor

## Introducción

El software permite automatizar tareas. Automatizar tareas regala tiempo a las personas: facilitar el acceso a información o evitar treas repetitivas. En el contexto actual, se han identificado ciertas iniciativas que manifiestan que el software en el contexto empresarial no es accesible para todas las empresas en particular para aquellas pequeñas (por planes estateales de inversión como AcelraPyme). Se ha identificado demanda de tres fucnionaldiades:

1. Catálogo de productos para empresas baratos (+ posibilidad de venta online) => aumento de la demanda de venta online
2. Registar productos para analizar datos sobre el uso del almacen
3. Automatizar trámites (puede que con RPA)/ o hacer un plan de operación de ciberseguridad / o hacer los pagos con PSD2

Existen soluciones que permitan estan fucnionalidades desde Wix/Shopify/Odoo.com o Salesforce o SAP a software a medida (Woocomerce. . .) . En el caso de una pequeña empresa o un autónomo, bsucaría solcuiones baratas, por ejemplo, el primer bloque de soluciones Wix/Shopify/Oddo.com como mínimo cuesta al mes de 15 a 30€ o solciones de ecommerce a medidas hosteadas en MrDomain 3€/mes de hosting (pero que sólo ofrecen la funcionalidad de catálogo ecommerce). En este estudio se plantea cómo poder desplegar un servicio que ofrezca estas fucnionaldiad de fomra más barata, usando serverless.

## Resumen de objetivos

En este estudio se propone:

1. Hacer un estudio del estado del arte de estas 3 funcionalidades
2. Identificación de un caso de estudio
3. Realizar un análsis (identificar y probar) soluciones
4. Diseñar un solución más barata
5. Implementarlo y probarla

## Organización y planificación previstas



- Sprint 1: cheap ecommerce (15th August 2020 - 15th September 2020 => 8h/day) and  (15th September 2020 -15th October 2020 => 4h/week)

- Sprint 2: efficient software (15th October 2020 - 7th Feb 2021 => 1h/week) and ( 7th Feb 2021 - x => 20h/week) (June)- Sprint 2: efficient software

- + 4 horas pregutnadno precios
- +2 horas PReguntando sobre el producto

March => do an eshop

- cheaper ecommerce with serverless, and more usable
- manage invetory
- other features rpa

1- anteproyecto por correo
2- explicar 



# 2- Memoria

## Index

## Intro and objectives => requirments detected

## Enabling technologies

## Analysis

## Design and implementation

## Conclusion

## Future lines

## Annex

### Time management

### Challenges that I faced

# Draft

## Intro and objectives => requirments detected

## Enabling technologies

## Analysis

1. Catálogo de productos para empresas barato (+ posibilidad de venta online)
2. Registar productos para analizar daots sobre el uso del almacen
3. Automatizar trámites (puede que con RPA)/ o hacer un plan de operación de ciberseguridad / o hacer los pagos con PSD2 para que sean grátis en vez de pagar a una pasarela

## Design and implementation

- Sprint 1: cheap ecommerce (15th August 2020 - 15th September 2020 => 8h/day) and  (15th September 2020 -15th October 2020 => 4h/week)

Comparación de recursos (proyectos de eccomerce (erp/crm o frontend + backend + cloud + db):

https://docs.google.com/spreadsheets/d/1Xon-1Qho6XSfOwBKpCQ4RG33cyaWvSCvdgt_JxIQYl0/edit?usp=sharing

Using Saleor + Cloud: www.breadfree.es

- spending of 10€ per month becasue of the db => turn into less (I am with the free plan)

- much time perosnalizing saleor => maybe odoo website creator

https://medium.com/@ablazleon/my-journey-on-setting-up-an-ecommerce-learning-saleor-google-cloud-run-dns-31e7c94f4c9a

- Sprint 2: efficient software (15th October 2020 - 7th Feb 2021 => 1h/week) and ( 7th Feb 2021 - x => 20h/week) (June)

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

## Conclusion

## Future lines

## Annex

### Time management

### Challenges that I faced

1- How to publish the summaries that I am creating how to make them accesible

word => pdf (depend on an office 365 licencse?) 70€/year
markdown => difficult to update citations
https://www.freecodecamp.org/news/taking-off-the-successful-launch-of-an-open-source-book-7553a2262898/
https://leanpub.medium.com/why-dont-i-use-leanpub-4ad2a77f5744
https://geocompr.github.io/user_19/presentation/#18
blog (like medium) => easier to be found difficult to update citations
latex (with overleaf) =>
PS: not with meister mind beacuse colalboartion is only allowed in paid plan

2- Sql vs Nosql for eccomerce with Saleor

https://medium.com/@ablazleon/nosql-vs-sql-para-ecommerce-con-saleor-707bc5851407

