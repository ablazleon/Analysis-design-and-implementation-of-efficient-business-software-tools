# Análisis, diseño e implementación de un servicio de comercio electrónico en la nube

- En este documento describo mi propuesta de anteproyecto. 

Índice:

# Introducción
# 1. [Estudio del estado del arte (what is?)](https://github.com/ablazleon/Analysis-design-and-implementation-of-efficient-business-software-tools/blob/main/1-State%20of%20the%20art.md)
## 1. Relación entre procesos de negocio (3 casos de uso identificados) y herramientas habilitadoras
## 2. Relación entre la estrucutra de coste del despliegue y las herramientas habilitadoras
# 2. [Análisis y diseño (identificar y probar soluciones, diseñenado una apta y más barata)](https://github.com/ablazleon/Analysis-design-and-implementation-of-efficient-business-software-tools/blob/main/2-Analysis%20and%20design.md)
## a. Identificación del caso de estudio (what if?/what wows?))
- Los siguientes casos de estudio definen el negocio
### eBusiness para artista y eBusiness para Breadfree => Kontá como plataforma SaaS
## b. Identificación de soluciones (what works?)
### Puesta a producción del servicio 
- Fase 0: FaaS shop
- Fase 1: comparativa despliegues: jenkinsX(eks, gke), cloudformation
- Fase 2: saleor + gcp (cloud run + cloud sql)
- Fase 3: odoo ce + aws (fargate + auroraserverless)
- Fase 4: odoo ce + gcp (cloud run + cloud sql)
- Fase 5: (wp + wc  + plugins) + namecheap 
### Mejora continua: análisis de riesgos
- Fase 5
## 3. Discusión sobre la implementación (what works?). Conclusión
# Líneas futuras
# Anexo
## Organización del tiempo
## [Retos a los que me enfrenté](https://github.com/ablazleon/Analysis-design-and-implementation-of-efficient-business-software-tools/blob/main/RetosALosQueMeEnfrente.md)
## Procedimientos

# 1- Anteproyecto

## Autor

Raúl Adrián Blázquez León

## Tutor

## Introducción

El software permite automatizar tareas, facilitando el acceso a información o evitando tareas repetitivas. En el contexto actual, se han identificado, por un lado, ciertas iniciativas que manifiestan que el software en el contexto empresarial no es accesible para todas las empresas en particular para aquellas pequeñas (por planes estatales de inversión como AceleraPyme). Por otro lado, que ciertas tecnologías, sobre todo el despliegue en la nube, permiten crear servicios baratos y eficientes. Así, dado una pyme, el objetivo de este proyecto es analizar, diseñar e implementar un servicio de comercio electrónico en la nube.

 Se ha identificado demanda de tres funcionalidades:

1. Catálogo de productos (+ posibilidad de venta online) => aumento de la demanda de venta online
2. Registrar productos para analizar datos sobre el uso del almacen
3. NFR: disponibilidad y seguridad

Existen soluciones que permitan estan fucnionalidades desde Wix/Shopify/Odoo.com o Salesforce o SAP a software a medida. En el caso de una pequeña empresa o un autónomo, bsucaría solcuiones baratas, por ejemplo, el primer bloque de soluciones Wix/Shopify/Oddo.com como mínimo cuesta al mes de 15 a 30€ o solciones de ecommerce a medidas hosteadas en MrDomain 3€/mes de hosting (pero que sólo ofrecen la funcionalidad de catálogo ecommerce). En este proyecto se implementan distinto del prototipo: una tienda con un backend basado en lambda, otra basará en salero en cloud run y cloud SQL, odoo en va y gke, y Woocommerce en namecheap. se plantea cómo poder desplegar un servicio que ofrezca estas fucnionalidades de forma más eficiente económicamente: valorando esquemas pay as you go en la nube. Si odoo con estas tres funcionalidades costaría entorno a los 90-120€/mes, se trata de buscar una solución en torno a los 60€/mes comparando caldiades de servicio frente a odoo saas.

https://www.odoo.com/es_ES/pricing#pl=77&version_id=32&num_users=3&app_account=on&app_sale_management=on&app_website=on&app_website_sale=on&app_account_accountant=on&app_stock=on&app_mass_mailing=on&num_iot_boxes=1&hosting=online&odoosh_workers=1&odoosh_storage=2&odoosh_staging=1&implementation_service=self&pack=100&force_country=ES&integrating_partner_id=0&price_by=monthly

## Resumen de objetivos

En este estudio se propone:

1. Hacer un estudio del estado del arte de estas 3 funcionalidades
2. Identificación de un caso de estudio
3. Realizar un análsis (identificar y probar) soluciones
4. Diseñar un solución más barata
5. Implementarlo y probarla

## Organización y planificación previstas




1 ects -> 27h => 30 ects 810

- Sprint 1: cheap ecommerce (15th August 2020 - 15th September 2020 => 8h/day) [80 de saleor] and  (15th September 2020 -15th October 2020 => 4h/week) [20 de comentar] + 40x4 [160 de la prueba de los cursos] = [260 h]

- Sprint 2: efficient software (15th October 2020 - 7th Feb 2021 => 1h/week) and ( 7th Feb 2021 - x => 20h/week) (June)- Sprint 2: efficient software) [30] + [100] h = [130 h]

- [400 h]

- Sprint 3: odoo. junio


---------------

# Draft

## Organización y planificación previstas

1. Catálogo de productos para empresas barato (+ posibilidad de venta online)
2. Registar productos para analizar daots sobre el uso del almacen
3. Automatizar trámites (puede que con RPA)/ o hacer un plan de operación de ciberseguridad / o hacer los pagos con PSD2 para que sean grátis en vez de pagar a una pasarela

- Sprint 1: cheap ecommerce (15th August 2020 - 15th September 2020 => 8h/day) and  (15th September 2020 -15th October 2020 => 4h/week)
Comparación de recursos (proyectos de eccomerce (erp/crm o frontend + backend + cloud + db):
https://docs.google.com/spreadsheets/d/1Xon-1Qho6XSfOwBKpCQ4RG33cyaWvSCvdgt_JxIQYl0/edit?usp=sharing
- spending of 10€ per month becasue of the db => turn into less (I am with the free plan)

- much time perosnalizing saleor => maybe odoo website creator

https://medium.com/@ablazleon/my-journey-on-setting-up-an-ecommerce-learning-saleor-google-cloud-run-dns-31e7c94f4c9a

- Sprint 2: efficient software (15th October 2020 - 7th Feb 2021 => 1h/week) and ( 7th Feb 2021 - x => 20h/week) (June)

- cheaper ecommerce with serverless, and more usable => so difficult to rewrite everythign in serverless
- manage invetory
- other features rpa
