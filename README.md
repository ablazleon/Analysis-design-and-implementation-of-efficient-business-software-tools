# Analysis-design-and-implementation-of-efficient-business-software-tools

Análisis, diseño e implementación de un servicio de comercio electrónico en la nube/Desarrollo de un servicio de software para empresa competitivo/En este docuemnto describo mi propuesta de anteproyecto y realizo un borrador sbore la estrucutra del documento del proyecto.


1. Hacer un estudio del estado del arte de estas 3 funcionalidades 
2. Identificación de un caso de estudio
3. Realizar un análsis (identificar y probar) soluciones
4. Diseñar un solución más barata
5. Implementarlo y probarla

1. Hacer un estudio del estado del arte de estas 3 funcionalidades 
=> se definen los procesos de negocio/funcionalidades, se proponen algunos y se agrupan
2. Identificación de un caso de estudio
3. Realizar un análsis (identificar y probar) soluciones
4. Diseñar un solución más barata
5. Implementarlo y probarla

# 1- Anteproyecto
# 2- Memoria (índice)

-----------

# 1- Anteproyecto

## Autor

Raúl Adrián Blázquez León

## Tutor

## Introducción

El software permite automatizar tareas. Automatizar tareas regala tiempo a las personas: facilitar el acceso a información o evitar treas repetitivas. En el contexto actual, se han identificado ciertas iniciativas que manifiestan que el software en el contexto empresarial no es accesible para todas las empresas en particular para aquellas pequeñas (por planes estateales de inversión como AceleraPyme). Se ha identificado demanda de tres fucnionaldiades que los negocios demandan:

1. Catálogo de productos para empresas baratos (+ posibilidad de venta online) => aumento de la demanda de venta online
2. Registar productos para analizar datos sobre el uso del almacen
3. Automatizar trámites (puede que con RPA)/ o hacer un plan de operación de ciberseguridad / o hacer los pagos con PSD2/email marketing

Existen soluciones que permitan estan fucnionalidades desde Wix/Shopify/Odoo.com o Salesforce o SAP a software a medida (Woocomerce. . .) . En el caso de una pequeña empresa o un autónomo, bsucaría solcuiones baratas, por ejemplo, el primer bloque de soluciones Wix/Shopify/Oddo.com como mínimo cuesta al mes de 15 a 30€ o solciones de ecommerce a medidas hosteadas en MrDomain 3€/mes de hosting (pero que sólo ofrecen la funcionalidad de catálogo ecommerce). En este estudio se plantea cómo poder desplegar un servicio que ofrezca estas fucnionalidades de forma más eficiente económicamente: valorando esquemas pay as you go en la nube de un desplieuge de odoo. Si odoo con estas tres funcionalidades costaría entorno a los 90-120€/mes, se trata de buscar una solución en torno a los 60€/mes comparando caldiades de servicio frente a odoo saas.

https://www.odoo.com/es_ES/pricing#pl=77&version_id=32&num_users=3&app_account=on&app_sale_management=on&app_website=on&app_website_sale=on&app_account_accountant=on&app_stock=on&app_mass_mailing=on&num_iot_boxes=1&hosting=online&odoosh_workers=1&odoosh_storage=2&odoosh_staging=1&implementation_service=self&pack=100&force_country=ES&integrating_partner_id=0&price_by=monthly

## Resumen de objetivos

En este estudio se propone:

1. Hacer un estudio del estado del arte de estas 3 funcionalidades
2. Identificación de un caso de estudio
3. Realizar un análsis (identificar y probar) soluciones
4. Diseñar un solución más barata
5. Implementarlo y probarla

## Organización y planificación previstas

- Sprint 1: cheap ecommerce (15th August 2020 - 15th September 2020 => 8h/day) and  (15th September 2020 -15th October 2020 => 4h/week) [200 h]

- Sprint 2: efficient software (15th October 2020 - 7th Feb 2021 => 1h/week) and ( 7th Feb 2021 - x => 20h/week) (June)- Sprint 2: efficient software

- Sprint 3: odoo

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

- cheaper ecommerce with serverless, and more usable => so difficult to rewrite everythign in serverless
- manage invetory
- other features rpa


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
latex (with overleaf) => general thing I have to present. HO w to facilitate reviews => althoug github and markwond is cool
PS: not with meister mind beacuse colalboartion is only allowed in paid plan

Why I want it to be public? => beacuse i Want people to share their experiences. I share some state based on effort, and otehr people can:
- mantain the state so is easier to justify the decision: let's take some more effort and deploy it yourself. In which way? In the way that it is useful?
- => I submitted it, but this rasteator idea of how to support teh digital transofmraotin of a business, I dont want to be fixed it can continue
-  ¿Cómo web apra comparar algo apra ver cuál es el mejor?
-  No, tiene que ser en plan orgnaización: en cualuqier momento se puede hacer un fork, los que ocntribuyen. Awsoeme
- Overleaf, pq word está bien, vetnajas pero el ivnocnenivente de para mantener esa lsita online es difícil
- cómo es la coalboración en latex? Se me va de las manos con overleaf. En word voy aescribiendo eso y se lo voy mandando
- lo bueno ahora de owrd, es que en rela time pod´ria verlo
- en latex también: con comentarios, versión de una cosas versión de otra
- con word autoría, tiempo real y concocimiento previo vs mejor formato

2- Sql vs Nosql for eccomerce with Saleor

https://medium.com/@ablazleon/nosql-vs-sql-para-ecommerce-con-saleor-707bc5851407

3- Design thinking 
https://www.salesforce.com/uk/blog/2017/10/design-thinking-questions-to-help-you-embrace-innovation.html
