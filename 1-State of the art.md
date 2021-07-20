
Automatizar tareas regala tiempo a las personas: facilitar el acceso a información o evitar tareas repetitivas. En el contexto actual, se han identificado ciertas iniciativas que manifiestan que el software en el contexto empresarial no es accesible para todas las empresas, en particular, para aquellas pequeñas (por planes estatales de inversión como AceleraPyme). A continuación, se analiza en base a datos la fase "what is?" del ciclo de "Design Thinking": se investigan las necesidades del usuario. Para ello se realizan tres discusiones. 
- 1- Primero se discute, presentando en una tabla, la relación entre procesos de negocio, herramientas y precios ¿Qué procesos de negocio se han identificado? ¿Qué herramientas se han encontrado en el mercado (español, en concreto en Madrid) que implementen estos procesos de negocio? ¿Y qué precio tienen? Nótese que en cuanto a "herramienta" se entiende el servicio software entero, detallando su infrastuctura con el fin de comprar costes.
- 2- A continuación, se discute una segunda dimensión en el debate sobre la relación entre procesos de negocio y herramientas: de estas herramientas, cuál es la relación entre el uso de cada herrmienta y su estructura de coste.


# 1. Relación entre procesos y herramientas
## 1.1. Herramientas
## 1.2. Procesos
# 2. Estructura de coste y herramientas
## 2.1. Estructura de coste y créditos de proveedores de nube
## 2.2. Estructura de coste y tipo de despliegue

-----------

# 1. Relación entre procesos y herramientas
## 1.1. Herramientas

Primero se discute, presentando en una tabla, la relación entre procesos de negocio, que primero se listan y herramientas y precios ¿Qué procesos de negocio se han identificado? ¿Qué herramientas se han encontrado en el mercado (español, en concreto en Madrid) que implementen estos procesos de negocio? ¿Y qué precio tienen? 

Primero se esbozan los procesos de negocio del ciclo de producción para el ejemplo de pequeño negocio en #2., y a continuación se identifican ciertos procesos genéricos que engloban estos del proceso de producción:

- I.	Se crea arte
- II.	Se inventaria: asigna un código y precio y se publica en la web (1)
- III.	Un usuario realiza una compra
- a.	Comprueba qué producto quiere, con qué precio y para cuándo, y acepta tasa de envío
- b.	Realiza el pago y el trámite de compra rellenando la dirección
- c.	Aparece un pedido con una dirección.
- d.	Dependiendo de si es original o glicé. 
- i.	Si es original: se enmarca y se envía
- ii.	Si es impreso 
- 1.	cada dos días se cogen los pedidos y enviamos un correo con los productos. 
- 2.	Previamente escaneamos los cuadros con un número, enviamos un correo con cada número cada día y que nos confirmen para recogerlo
- 3.	Se firma el cuadro y se pone el cuadro en el tubo
- 4. En un correo de atención al usuario se atienden las devoluciones.
- 5. Se gestionan descuentos para próximas compras

--------

Estos procesos genéricos son los que se comparan para cada herramienta. Así se eligirá la herrramienta que automatice más procesos a menor precio:

- 1. Tienda online
- 1.1. Constructor de sitios web (CMS) + catálogo + plataforma de pago
- 1.2. Seguimiento de paquetes: avisar que se ha realizado el envío
- 1.3. Subscripción a la newsletter
- 2. Gestión de operaciones
- 2.1. Integración pedido tienda/Visualización de stock: poner en los originales que el stock es uno. Si quieres otro, escribir a cotnactaconleon
- 2.2. Generación de pedidios para comprar a proveedores: enviar los códigos de los impresos y las cantidades al correo de la impresora
- 2.3. Opciones de envío para nacional e internacional
- Disponibilidad: cuantos usuarios o conexiones a la vez se pueden servir
- Seguridad: cuán fácil es actualizar el sw

Se presentan 4 tablas:

- 1. Herramientas de tienda online SaaS
- 1. Herramientas de tienda online Open Source desplegadas
- 2. Herramientas de gestión de inventarios
- 3. Herramientas de marketing

-----------

- 1. Herramientas de tienda online SaaS
 
 Procesos vs tool 
|      |1 Shopify    | Wix   | Wordpress.com | Magento|Gumroad| Salesforce| Sap   |Odoo Saas |Etsy 1|
|:---: | :---:       | :---: | :---:         | :---:  | :---: |  :---:    | :---: | :---:    | :---: |
|1.1.  | x           | x     |               |     x  |     x |   x       |     x | x        |   x   |    
|1.2.  | x(aftership)| x     |               |     x  |     x |   x       | x     |x         |       |  
|1.3.  | x           | x     |  x            |     x  |     x |    x      | x     | x        |x      |  
|2.1.  |             |      x|               |     x  |       |  x        |      x|x         |       | 
|2.2.  |             |       |               |      x |       |        x  |      x|          |       |        
| €/mes| 30          |17.5   |  8            | 2000   | 10    | 25        | 16.000€| 100     | 0.2€/producto/mes.1 | 
|Disp  | alta        | alta  |  alta         |   alta | alta  |   alta    |  alta |alta      | alta  |   
|Segu  |   alta      | alta  | alta          |  alta  | alta  |   alta    |  alta | alta     | alta  |   
|      |1 [Shopify](https://www.shopify.com/pricing)    | [Wix](https://www.wix.com/upgrade/website)   | [Wordpress.com](https://wordpress.com/pricing/) | [Magento](https://magento.com/products/magento-commerce) |[Gumroad](https://gumroad.com/features/pricing)| [Salesforce](https://www.g2.com/products/salesforce-crm/pricing)| [Sap](https://www.aimprosoft.com/blog/much-cost-develop-e-commerce-b2b-website-sap-hybris-platform/)   | [Odoo](https://www.odoo.com/es_ES/pricing#pl=77&version_id=32&num_users=2&app_account=on&app_sale_management=on&app_website=on&app_website_sale=on&app_account_accountant=on&app_stock=on&app_purchase=on&app_mass_mailing=on&app_hr_appraisal=on&num_iot_boxes=1&hosting=online&odoosh_workers=1&odoosh_storage=1&odoosh_staging=1&implementation_service=self&pack=100&force_country=ES&integrating_partner_id=0&price_by=yearly)  |[Etsy](https://www.etsy.com/es/legal/fees/) 1|
|      |1 [No hay peticiones de compra conjunta](https://www.youtube.com/watch?v=do01YIxEVKk)    | [No hay peticiones de compra conjunta](https://www.youtube.com/watch?v=CXUsaMnpN-w)   | Necesita Woocommerce | Demasiado caro |[No hay peticiones de compra conjunta](https://www.youtube.com/watch?v=FWxu08-TsS0)| Demasiado caro| Demasiado caro |

- 1. Herramientas de tienda online Open Source desplegadas

 Procesos vs tool 
|     |1 Saleor(crun+csql)| OddoCE(VM+csql)    | WP+WC+MRDomain+Jetpack 1|WP+WC+NC+Updraft+subscribeEmail+MarketingAutomation+Etsy(autoamte.io)  1|
|:---:| :---:             | :---:              | :---:                   | :---:                   | 
|1.1. | x                 | x                  |  x                      |  x                      |      
|1.2. | x                 | x                  |  x                      | x                      |     
|1.3. | x                 | x                  |  x                      |  x                      |     
|2.1. | x                 |                   x|   x                     |  x                      |       
|2.2. | x                 |x                   |    x                    | x                      |         
|2.3. | x                 | x                  |     x                   | x                      |       
|€/mes| 15€/mes           | [40$/mes => 480$](https://cloud.google.com/products/calculator/#id=a2a1ffa9-7c7b-4e41-bd53-2c1e86aa9f79) [mail after ship](https://www.odoo.com/documentation/13.0/applications/inventory_and_mrp/inventory/management/misc/email_delivery.html) [integrado con dhl](https://www.youtube.com/watch?v=W4wmGfHwkEc)   | 350$ anuales, [WC](https://woocommerce.com/hosting-solutions/), [Mr, 60$](https://www.mrdomain.com/products/hosting/basic/) [120$/anual](https://cloud.jetpack.com/pricing) [custom emails](https://woocommerce.com/posts/how-to-customize-emails-in-woocommerce/) [Integrado con dhl](https://docs.woocommerce.com/document/woocommerce-shipping-and-tax/woocommerce-shipping/) + [50$](https://woocommerce.com/products/woocommerce-gateway-purchase-order/) + [120$ mailchimp para newsltter, si más de 200 contactos](https://mailchimp.com/pricing/marketing/)|  350$ anuales, [WC](https://woocommerce.com/hosting-solutions/), [Mr, 60$](https://www.mrdomain.com/products/hosting/basic/) [120$/anual](https://cloud.jetpack.com/pricing) [custom emails](https://woocommerce.com/posts/how-to-customize-emails-in-woocommerce/) [Integrado con dhl](https://docs.woocommerce.com/document/woocommerce-shipping-and-tax/woocommerce-shipping/) + [50$](https://woocommerce.com/products/woocommerce-gateway-purchase-order/) + [120$ mailchimp para newsltter, si más de 200 contactos](https://mailchimp.com/pricing/marketing/)|

CRM and email?

[1](https://es.wordpress.org/plugins/email-subscribe/)
[2](https://www.sendcloud.es/vender-en-etsy/)

Hay hosting para wordpress muy pbaratos [1](https://miposicionamientoweb.es/cual-es-el-hosting-mas-barato-y-de-calidad/) [2](https://www.hostinger.es/tutoriales/que-es-un-vps)

[1](https://www.namecheap.com/wordpress/pricing/)

30€/año vs hostinger que es más 45 o más

Woocomcer tiene plugin de correos, ¿es tan necesario? Parece que no. Pero no genera alertas de ivnentario cuando quedne pocos tubos, y llevar las cuentas de las ventas.

Se preuba odoo por 2: porque se puede comrpar varios productos a la vez y por la gestión de ivnentarios. Si en woocommerce se encuentran plugins para hacer backup y gestionar inventarios como se han encontrado en odoo, qué problema habría? [1](https://wordpress.org/plugins/stock-tracking-reporting-for-woocommerce/), [2](https://www.storeapps.org/woocommerce-inventory-management/)

WC [1 Backup](https://litextension.com/blog/backup-woocommerce/), [2 backup](https://themegrill.com/blog/best-wordpress-backup-plugins/), [3 updraft plus](https://wordpress.org/plugins/updraftplus/#description) [4 comprasion](https://updraftplus.com/comparison-updraftplus-free-updraftplus-premium/)


|     |2 Amazon| Glovo | G sheet| Katana 2|3 ConvertKit| MailChimp |Klaviyo | Hootsuite 3|
|:---:| :---: | :---: | :---:  | :---: |  :---:       | :---:      | :---: | :---: |
|1.1. |      x|       |        |       |    x         |     x      |       |       |
|1.2. |       |      x|       |        |              |     x       |     x |       |      
|2.1. |              x|       |        |               |            |       |       |      
|2.2. |       |       |       |      x|               |            |      x|      x|            
|2.3. |       |       |       |     x |              |             |      x|      x|    
|3.1. |       |       |       |     x |              |             |     x |     x |      
|3.2. |       |       |       |     x |              |             |     x |     x |    
|  Precio del servicio|  2. [0 hasta 40 artículos 40€/mes](https://services.amazon.es/servicios/vender-por-internet/faq.html#:~:text=%C2%BFCu%C3%A1nto%20cuesta%20vender%20en%20Amazon,sin%20IVA%20en%20distintas%20categor%C3%ADas.) | [200€/mes](https://miracomosehace.com/cuanto-cobra-glovo-restaurantes-como-poner-restaurante-glovo/#:~:text=Es%20importante%20mencionar%20que%20la,50%20euros%20a%20la%20semana.)   | 0€/mes   | [100€/mes](https://katanamrp.com/pricing/) .2|3. [30€/mes](https://convertkit.com/pricing) | [15€/mes](https://mailchimp.com/pricing/) | [30€/mes](https://www.klaviyo.com/pricing) | [40€/mes](https://www.hootsuite.com/plans) .3|
| Comentario|  2. Completo, alto precio a largo | Completo, alto precio a corto  |  2 | 2 .2|3. Falta 2 | 3 | 3 | 3 .3|

[1](https://www.techradar.com/news/best-wordpress-hosting-providers)
[2](https://www.websitebuilderexpert.com/web-hosting/comparisons/bluehost-vs-godaddy)
[3](https://themeisle.com/blog/managed-wordpress-hosting-cheap/)
[4](https://www.softrending.com/blog/diseno-web/diferencias-woocommerce-prestashop-odoo)
[5](https://www.scaleway.com/en/docs/odoo-on-kubernetes-via-easy-deploy/)


opción de la vm + cloud sql => x usuarios, no sé compatir el disco para hacer autoescalado => comprobar ucnátos en loader
kubernetes => despelgar 10 y comprobar que los rpecios salen a menos, pq mejor que namecheap + woocommerce?

| Hosting WP       | namecheap (dominio hasta septiembre)   |  hostinger | bluehost |
| :---:          |    :----:   |    :---:   |  :---:   |
| Precio 1y simple |   40      | 86         | 150       |
| SSL              |   0   |    0       |  x       |  


Qué hosting usar?

[1](https://hostingvictory.com/es/opiniones/namecheap/)
[2](https://hostingvictory.com/es/opiniones/namecheap/)
[3](https://miposicionamientoweb.es/cual-es-el-mejor-hosting-espanol/)
[4](https://www.dondominio.com/products/hosting/basic/)

Dbees pagar por más?

10 GB de ssd



Cömo comrpobar que el certificado de google es mejor que el de namecheap? GCP las tiene dv no ov.

Los autogestionados por google son DV. Elijo el free plan de namecheap [1](https://www.ssl.com/article/when-not-use-a-dv-ssl-certificate-for-e-commerce/)
[2](https://security.stackexchange.com/questions/35076/how-does-an-end-user-differentiate-between-ov-and-dv-certificates)
[3](https://www.websecurity.digicert.com/security-topics/dangers-of-domain-validated-ssl)

los ov son mejroes pero para la organización. No puedo ov porque hab´ria que estar dado de alta en el registro [1](https://comodosslstore.com/ssl-validation-process/ov) rnefe sólo tieen ov. DV hasta que seamos una empresa

Atum invenotry[1](https://stockmanagementlabs.com/addons/atum-action-logs/)

Como conclusión de esta compración se puede sacar que shopify o wix son soluciones para vender ideales, pero a las que les falta, tanto una mayor autoamtización en 2.1 (integración de pedido y visualización de stock, los llamados mrp, como katana, pero que añaden 100€ más de coste). Entonces, se concluye que una propuesta de valor puede consistir en ofrecer las bondades de este conjunto Shopify + Katana (175€/mes) por menos coste y así menos precio.

- Referencias: 
[1](https://www.repricerexpress.com/amazon-fba-vs-shopify/), 
[2](https://www.websitebuilderexpert.com/ecommerce-website-builders/comparisons/shopify-vs-etsy/), 
[3](https://www.odoo.com/forum/marketing-16/how-can-i-link-an-instagram-account-to-the-social-marketing-app-164541), 
[4](https://www.salesforce.com/editions-pricing/small-business/), 
[5](https://docs.google.com/spreadsheets/d/1Xon-1Qho6XSfOwBKpCQ4RG33cyaWvSCvdgt_JxIQYl0/edit#gid=1476303528=), 
[6](https://www.correos.es/content/dam/correos/documentos/atc/tarifas/Tarifas_2021_Peninsula_y_Baleares.pdf), 
[7](https://docs.google.com/spreadsheets/d/1Xon-1Qho6XSfOwBKpCQ4RG33cyaWvSCvdgt_JxIQYl0/edit?usp=sharing),
[8](https://www.doofinder.com/es/blog/cuanto-cuesta-crear-ecommerce),
[9](https://www.godaddy.com/es-es/paginas-web/creador-paginas-web/planes-precios),
[10](https://www.wix.com/upgrade/website),
[11 Etsy easy to start but expensive](https://www.youtube.com/watch?v=JtjcEJqmAnE)
[12 wix/squarespace is faster to setup but it will take me longer to migrate or set this up](https://www.websitetooltester.com/en/ecommerce-platforms/)
[13 order management in wix](https://www.youtube.com/watch?v=CXUsaMnpN-w)

La forma que se plantea de implementar esta propuesta de valor es mediante el despliegue en la nube de un proyecto open source que provea de estos procesos. Se encuentran disitnos proyectos, y en la tabla básicamnete se ha comparado Saleor y Odoo CE. Como se observa que Saleor es sólo una plantilla para realizar la función 1, y que no plantea el resto de soluciones, se propone desplegar odoo CE. En el apartado de procesos se detallan los procesos de negocio, y se observa que para automatizar la realización de pedidos, es econoómeicamtne rentable esta opción más que la opción wix o Shopify.

[1](https://itsfoss.com/open-source-ecommerce/)

Ahora bien, se plantea la necesidad de ciertos addons. Buscando soluciones se destacan dos paquetes de soluciones [camp2camp](https://github.com/camptocamp/odoo-cloud-platform/tree/14.0) y [itpp-labs](https://github.com/itpp-labs/misc-addons/tree/14.0)


| v14       | camp2camp   |  itpp-labs |
| :---:          |    :----:   |    :---:   |
| Auto backup    | (pero sí gcp) |  x         |
| Más estrellas gh|            |    x       |  
| Guardar sesiones|     x       |            |  

Se plantea montar la solución de c2c, pues aunque tenga menos estrellas en gh, al estar estos addons funcionando en v14 será más fácil migrar a la v15, para seguir con los parcehs de seguridad. Sin embargo, habría que ocmprobar si es más fácil realizar importaciones del backup en v14 que en v13.


| v13       | camp2camp   |  itpp-labs |
| :---:          |    :----:   |    :---:   |
| Auto backup    | x           |  x         |
| Más estrellas gh|            |    x       |  
| Guardar sesiones|     x       |    x        | 

Finalmente como nota se compara qué proveddor de nombre de dominio es mejor:


A la larga más barato

https://cloud.google.com/domains/pricing?hl=es-419 => 12$/año
https://www.websiteplanet.com/blog/google-domains-vs-godaddy-crowned-king/

## 1.2. Procesos

A continuación se listan los procesos de negocio, para concluir cómo orquestrar cada tarea.

- 1. Tienda online
- 1.1. Constructor de sitios web (CMS) + catálogo + paltaforma de pago: 
- [ ] se crea un sitio web de forma fácil
- [ ] con un catálogo con fotos desde un csv para cambiar los precios de forma automática
- [ ] los clientes llegan a un dominio específico
- [ ] eligen un producto de un cierto tamaño
- [ ] elgien un producto con unas variantes específcas, con o sin marco y paspartu
- [ ] se puede elegir entre varias plataforma de pago (paypal, stripe)
- 1.2. Seguimiento de paquetes
- ([ ] a un cliente se le ofrecen distintos medios de transporte, con precios distitnos en función de días)
- [ ] el cliente puede saber cuánto le falta al paquete para llegar
- [ ] o se puede informar en la web de cómo contactar al proveedor si hay algún problema
- [ ] o contactar si desea comprarlo y recogerlo
- 2. Gestión de operaciones
- 2.1. Integración pedido tienda/Visualización de stock
- [ ] Cada pedido recoge una creación limitada (descuentos como variantes) => ninguna de los dos lo tiene
- 2.2. Generación de alertas para comprar a proveedores => si se imprime una a una no hace falta
- [ ] una petición de compra genera un mensaje al manufacturero [necesidad de integración, pro ejemplo con katana](https://apps.shopify.com/katana-mrp-manufacturing-and-inventory-management) => también se puede hacer por correo
- [ ] cuando el manufacturero termina el proceso de fabricación avisa para que se pueda recoger y enviar el pedido => con odoo manufactura puede ver esto y generar las encesarias?
- 3. Automatización de marketing
- 3.1. Generación y envío de correos, como newsletter
- [ ] se permite suscrbir a una newsletter
- 3.2. Integración con instagram 
- [ ] se puede automatizar las campañas de marketing en más de una plataforma

- Así, tanto wix/shopify (17/30) serán una buena apuesta en comparación con odoo ce, sobre todo si se pueden realizar estos procesos definidos en 2., para lo que se suele necesitar de un sistema de inventario que ceusta en 30(stock&buy) a 100(katana). Es decir, se apuesta por desarrollar 3 semanas odoo ce 

https://multiorders.com/pricing/

multichannel caro en wix caro en odoo, no hay app:

[1](https://www.etsy.com/shop/GaryAsatrianArt?ref=l2-about-shopname)

Por qué odoo me gusta?

Mr Domain 5€/mes un ecommerce

woocommerce

- shopify/wix => cms 
- + automatiza la compra, puedo crear una quote y mandarla por correo 
- + el inventario: necesito saber cuántas tengo? La vd es que no, los glicés se hacen al momento y los originales se peudne vender con marco (poner out of stock)
- + automatización de correos
- + generar las etiquetas para los paquetes en correos
- + precio

wordpress/prestashop/magento


# 2. Estructura de coste y herramientas

A continuación, se discute una segunda dimensión en el debate sobre la relación entre procesos de negocio y herramientas: de estas herramientas, cuál es la relación entre el uso de cada herrmienta y su estructura de coste.

Se realizan dos reflexiones:

## 2.1. Estructura de coste y créditos de proveedores de nube

Una interesante reflexión es presentar los créditos que por alumno puedo conseguir a junio de 2021, pues en parte a esto dependerá la elección del servicio de despliegue. Tras este estudio los proveedores en la nube

Azure => 100$/12 months
AWS => creédtios de alumno upm 50$ 4/30/2022 => 5 meses
Google=> 40$ 15 Oct 21, 50$ 1 Oct 21 => 5 meses
Alibaba => [?](https://www.alibabacloud.com/campaign/education?spm=a3c0i.217264.1159678.1.60966d6fUFbooN)

## 2.2. Estructura de coste y tipo de despliegue

En esta sección se discute la relación que existen entre distintos tipos posibles de despliegues en la nube en función de paradigma y porveddores de estas herrmaientas que habilitan los procesos de negocio. Primero se comparan tipos de ***despleigue genéricos***, después ciertos ***stacks*** y finalmente ****formas de implementar estos stacks***.

### Comparación de tipos de despliegue

Primero se evalúan los despliegues teóricos. Generalmente, se realiza la clasificación entre tipos de despliegue: On premise IaaS PaaS SaaS. De la reflexión realizada en la sección 1, se concluye que el coste puede ser de 20€/month/client, la solución on premise sale deamsiado cara, así como las SaaS discutidas en secciones anteriores. Se plantean a continuación comaprar las soluciones que se englobarían en el rango IaaS/PaaS, en Iaas, incluyendo Vm, Kuberntes as a service (KaaS), Contianer as a service, Fucntion as a service y PaaS. Báscamente la conclusión de la siguiente comaprativa, es que son las soluciones Kubernetes as a Service o CaaS, las que ofrecen escalabilidad a un coste razonable. Sin embargo, las soluciones de kubernetes exige una operación complicada a priori de los servicios. GKE el servicio de google, parece el mejor servicio de cloud de KaaS, con autopilot se pueden gestionar los recursos pero exige gestionar dbs.


| type/prop   | Scalability | Cost          | Comment      |
| :---:       |    :----:   |         :---: |      :---:   |
| Vm          | Not scalable| Depends       |              |
| KaaS        | Y        | ?             | [hay que estudar qué opción pemirte que se apague durante la noche, más coste de operación](https://www.stackrox.com/post/2021/01/eks-vs-gke-vs-aks-jan2021/)             |
| CaaS        | Y        |   ?            |   [depende de qué opción, cloud run, fargate o eci están bien, el problema está con la bbdd](https://www.youtube.com/watch?v=-59KDnNrIfchgh)           |
| FaaS        | Y        | 0             |  El método más barato para adaptar el coste a la demanda, pero ncesita de reescribir el código enteor para usar las funciones       |
| PaaS        | N        | 0             |  PaaS como DonDominio o Heroku son ampliamente usadas pero restringen a la plataforma: Heroku unos costes altos y DonDominioo usar un sistema en PHP       |

### Comparación de stacks

Finalmente, se comparan distintos stacks de soluciones. Básicamente las soluciones Caas, sobre los proveedores de los que se disponen créditos (Azure, GCP y AWS). COmpatible se refiere a compatible con que sea serverless, es decir que sólo se pague por los recuross que se empleeen.

|CaaSstack/prop     |Compatibility       | Cost          | References | Comment   |
| :---:             |    :----:          |         :---: |    :---:   |   :---:   |
| Azure:ACI+AzPGSQL | No psql svless     | ?             | [1 cost of azure psgql](https://www.reddit.com/r/AZURE/comments/kz93ot/any_real_world_cost_comparison_between_azure_sql/) [2 psg scaling](https://azure.microsoft.com/en-us/pricing/details/postgresql/hyperscale-citus/)  [3 performance](https://docs.microsoft.com/en-us/azure/postgresql/concepts-performance-recommendations) [4 flexible server psg does not turned off when not in use](https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Flexible-Server-in-Azure-Database-for-PostgreSQL-and-MySQL)     | Sin servicio posgres serverless y con un ACI más dif´cil de depslegar que gcrun, este stack no compite|
| AWS:Fargate+AuroraSvl| Y               | min 7€        | [1 FargatevsGKE](https://blog.iron.io/aws-fargate-vs-gke/#:~:text=GKE,-By%20Nick%20%7C%20August&text=Both%20services%20are%20backed%20by,part%20of%20Google%20Cloud%20Platform.)  [2 AWS Aurora Svless](https://labrlearning.medium.com/interacting-with-aws-aurora-serverless-1398c9de329a) [3 fargate cepoyments](https://medium.com/@jonah.jones/things-to-love-about-aws-fargate-part-1-deployments-c2a8a8349057)  [4 ALB cost estimation](https://cloudsoft.io/blog/aws-alb-cost-estimation) [5 fargate pricing vs ec2](https://www.trek10.com/blog/fargate-pricing-vs-ec2#:~:text=As%20you%20can%20see%2C%20around,to%20cost%20about%2035%25%20more.)   [6 Aurora svl v1, v2 seems no tto be compatible with pg](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-2.html)  [7 aurora can scale](https://aws.amazon.com/blogs/database/best-practices-for-working-with-amazon-aurora-serverless/) | Más difícil desplegar que gcrun, pero coste no es proporcional al número de usuarios |
| GCP:CloudRun+CloudSql| Y               | min 10€       | [1 CloudSql](https://medium.com/google-cloud/save-money-by-scheduling-cloud-sql-7981e1b65ea3) [2 Scheduling cloudsql](https://medium.com/google-cloud/save-money-by-scheduling-cloud-sql-7981e1b65ea3) [3 cloudrun vs lambda](https://iamondemand.com/blog/google-cloud-run-vs-aws-lambda-performance-benchmarks-part-2/)  [4 cloud run vs fargate](https://keepler.io/en/2019/10/serverless-services-for-containers-aws-vs-google-cloud/) [5 cloud run vs fargate vs aci](https://thenewstack.io/comparison-aws-fargate-vs-google-cloud-run-vs-azure-container-instances/#:~:text=AWS%20Fargate%2FEKS%20is%20comparable,can%20accept%20a%20pod%20definition.)  [6 crun cold starts](https://github.com/ahmetb/cloud-run-faq#does-cloud-run-have-cold-starts), [7 ehre a max number of concurrent users with one instance](https://blog.doit-intl.com/how-does-a-cloud-sql-database-scale-and-what-to-know-when-setting-one-up-c23c52fc9947)     | Opción más fácil desplegar. Pero bbdd es necesario también pagarla por las noches|
| Alicloud:ECI+AsparaDB| Y               | ?             |            | Pay as you go tiene sentido, aunque carece de créditos grátis con lo que agilizar la prueba del stack |
| IBM                  | No psql svless  | ?             |            | Sin servicio posgres serverless y con un ACI más difícil de depslegar que gcrun, este stack no compite |
| CRun+AuroraSvl       | Y               | ?             |            | Sin servicio posgres serverless y con un ACI más dif´cil de depslegar que gcrun, este stack no compite |
| Clouding       | N               | ?             | [1](https://clouding.io/)           | Sin servicio posgres serverless y con un servicio de computación más dif´cil de depslegar que gcrun, este stack no compite |
| Digital Ocean      | Y               | ?             | [1](https://www.digitalocean.com/pricing/#app-platform)           | 50#/month 4GB 2CPU + db, it also has kubernetes, but this needs and overhead of operation |
| Linode      | Y               | ?             | [1](https://www.linode.com/pricing/#row--compare)           | only k8s |
| AWS:AppRunner+AuroraSvl | Y               | ?             | [1](https://www.theregister.com/2021/05/19/aws_introduces_app_runner_google/#:~:text=js%2012.&text=Pricing%20is%20dependent%20on%20resources,if%20it%20is%20always%20running.),[2](https://www.youtube.com/c/ContainersfromtheCouch/videos)  [3 problems with cloud mapping](https://dev.to/aws-builders/aws-app-runner-initial-thoughts-1pl8)        | 56€, as it cannot be sale down to zero. So, firstly it was explored beacuse it mught be cheaper that having to provision an lb, but it seems it's not |

Alicloud no es tan barato
https://www.alibabacloud.com/pricing-calculator#/

### Comparación de implementación de stacks

Finalmente, se comparan dos opciones razonables. Se opta por despelgar la primera, pues auqnue a priori parezca más difícil de depslegar, posee menos coste en el escalado.

| type/prop              | Facilidad   | Créditos      | Comment      |
| :---:                  |    :----:   |         :---: |      :---:   |
| AWS:Fargate+AuroraSvl  | N           | 40€ + ?       |  20€+10€+10€/m=> 40€/m/c one lb per env to separeete billings -mas caro, en lso primeros 7 meses +a largo plazo este método salvará de quedarse sin servicio en días espeiclaes -+ can get more credits, but they run out quicklier, +- dbs can be created and does not cost, but one fargate up always             |
| GCP:CloudRun+CloudSql  | Y           | 300€/3m + cambio| 20€/m/c, +i safe three months - puede que àrte del tráfico no se curse -por el dns en cada cambio, un día sin mantenemiento -crear disitnos  +- easier to deploy, pero si tengo que hacer scripting me llevará tiempo también - cloud sql si no atienda tráfico, hay que scalarlo a una bbdd con más ram            |

Referencias, sobre la comparacion de ambos servicios:

[6](https://www.bigcommerce.com/articles/ecommerce/ecommerce-hosting/#faqs-about-ecommerce-hosting)
[7](https://learning.oreilly.com/library/view/ecommerce-in-the/9781491946626/ch04.html)
[8](https://www.artifakt.com/pricing/)

Cloud sql vs aurora serverless v1

[1](https://www.jeremydaly.com/aurora-serverless-the-good-the-bad-and-the-scalable/#:~:text=Aurora%20Serverless%20is%20designed%20to,of%20connections%20are%20being%20used)
[2](https://www.reddit.com/r/aws/comments/bew37h/help_me_understand_aurora_serverless_pricing/)
[3](https://www.percona.com/blog/2020/10/27/a-first-glance-at-amazon-aurora-serverless-rds/)
[4](https://www.reddit.com/r/aws/comments/adre7w/is_anyone_using_aurora_serverless_in_production/)
[5](https://forums.aws.amazon.com/thread.jspa?threadID=288043)
[6](https://aws.amazon.com/rds/aurora/serverless/)
[7](https://aws.github.io/copilot-cli/docs/developing/additional-aws-resources/)
[8](https://www.artifakt.com/pricing/)
[9](https://www.2ndwatch.com/blog/serverless-aurora-production-ready-yet/)
[10](https://www.reddit.com/r/aws/comments/gh1nqw/rds_vs_aurora_big_price_difference/)
[11](https://aws.amazon.com/blogs/database/best-practices-for-working-with-amazon-aurora-serverless/)
[12](https://www.reddit.com/r/aws/comments/n2ts9r/aurora_serverless_v2_approximate_release_date/)
[13](https://cloud.google.com/sql/docs/quotas#:~:text=Cloud%20Run%20services%20are%20limited,connections%20per%20deployment%20can%20grow.)

Fargate vs cloud run

[1](https://ecsworkshop.com/microservices/)
[2](https://medium.com/adobetech/deploy-microservices-using-aws-ecs-fargate-and-api-gateway-1b5e71129338)
[3](https://pereliksoft.com/index.php/2020/11/19/aws-fargate-vs-google-cloud-run/)
[4](https://thenewstack.io/comparison-aws-fargate-vs-google-cloud-run-vs-azure-container-instances/)
[5](https://medium.com/@jonah.jones/things-to-love-about-aws-fargate-part-1-deployments-c2a8a8349057)
[6](https://blog.codecentric.de/en/2021/03/fargate-with-efs-and-aurora-serverless-using-aws-cdk/)
[7](https://aws.amazon.com/blogs/compute/building-deploying-and-operating-containerized-applications-with-aws-fargate/)
[8](https://www.youtube.com/watch?v=Nv7s-N8ZxQA)
[9](https://www.youtube.com/watch?v=YCCFK2RRm7U)

Se propone la siguiente estrategia:

- option 1: despliegue en gcp: 3 meses o 6, y puede que el servelress v2 ya haya salido a GA,y app runner decrementando el precio
- option 2: desplegar en aws: va a costar más caro pero puede escalar si llegna muchas peticiones? Depende más de 20 s el escalar

A continuación se comparan métodos de despligue del stack planteado en AWS:

| type/prop      | Facilidad   |  Comment   |
| :---:          |    :----:   |    :---:   |
| Copilot        | 3           |            |
| CDK            | 2           |            |  
| CLI            | 1           |            |  

Tras un primer despliegue se observa que

https://cloud.google.com/products/calculator/#id=9cd9c839-6297-4892-a6b0-a64134593c24

35€

https://www.digitalocean.com/pricing#managed-databases

for vm digital ocean can be cehaper

15 + 10 +10

linode 

20 1 4GB + 20 db + 10 lb =50

precios kubenrnetes

https://www.digitalocean.com/pricing/#kubernetes

https://www.linode.com/pricing/

gcp preemptible

https://cloud.google.com/compute/docs/instances/preemptible

seems no to be possible

for having https 10 + 10 + 20 + 10 vs 2, differneces

