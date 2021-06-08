
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
- [x] 6 preguntar a Víctor Facic mejor manera para desplgieues en lanube baratos (clodu run + cloud sql vs fargate + aurora serverless vs linode) => en youtbe: su solución es que no sabe => preguntar en stckovf como ven alicloud en cuanto a costes, ibm code engine vs cloud run: en caas => alicloudsólo preio por hora pero se apagan sólos 
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
- [ ] 7 desplegar en vbox odoo: https://www.cybrosys.com/blog/how-to-install-odoo-14-on-ubuntu-20-04-lts
- [ ] 8 desplegar en gcloud 
- [x] 9 para evaluar necisto saber cómo usarlo: más que en concreto en abstracto: pedir aputnes del itirnerario de gestión o hay n profe que oferta un tfm, oye estoy intentando impelemantr uno, como que no tengo la parte de invenstairos, más adleante le improta hablar. COIT mentorizado
- [x] 10. Cómo formatear el texto: ppt + un texto explicativo + un jupyer con text abierto por si se quiere en plan awesome list y traducirla (inglés) 

=>

- General
- [x] Tiempo, bajar a 8h entas, S, D, L
- [x] Hacer una slides con la idea general =>solución propeusta se basa en datos, dudo esta ahí la justifiación
- Caso de uso de breadfree => email marketing
- [ ] Vbox, funciona
- [ ] de la talba probar las cosas que se quiere que funcioneen ahí, y parece que no fucnioana en el toro lado
- [ ] Solución pay as you : google vs alibaba => pay as you go vs falt rate. Horas en funcioanmeitno dle serivico
- [ ] Solución Pay as you go: preguntar => hacer un esquema de cómo va a escalar esta estrucutra de coste
- Caso de uso de breadfree => ecommerce
- [ ] Pasos de autoamtización del servicio: seguimietno de pagos
- [ ] Campaña de lanzmaienot

- [ ] Integrar con un dominio personalizado
- [ ] configurar la web: (decir que se aceptan encargos + biografía)
- [ ] Cuántos usuairos visitan la página al mes? Integrar google analytics
- [ ] COnfigurar precios y detalles de cada producto: con un excel de una
- [ ] odoo self hosted vs odoo saas => cuánto tiene que csotar? Hacer planes
- [ ] preguntar en stack ovf si ven algún probelma con alicloud: qué stack mejor => hacer un curso en alicloud => depslegar alicloud
- [ ] Plan general, pues siugiente paso, seguimeitno de pagquetes y oferta de distninos precios
- [ ] Configurar correo con mi propio dominio: https://thedigitalnonprofit.com/use-gmail-own-domain-free/ 

1,2,3,4 => junio 15

Estructura de coste: otros facotres, en relaiad son las hsitorias de usuairo, pulir algunas, no son tan ortogoanles => amazon 
- [ ] pq estrucura de costes si no lo van a usar y en qué sentido? un plan de negocio para vender arte online. custoemr journey: shopify has inveotory things, amazon has a logistic advantage, but only allows for low product ammount https://sell.amazon.com/pricing.html?ref_=sdus_soa_begin_plans_n#selling-plans => not scale, and if scale 40€ month, dificil encontrar seo para cuadros apar decorar, cómo decorar la csas: dónde esta la necesidad, en vez de un kofi una copia de un cuadro. EL referral fee de amazon
squarespace, hay un monton y más en arte => tenog una hipótesis y es que o el marketplace se lleva un 30%  por enviar y por gestioanr la manufactura => cómog esitoanr la manufactura, aún así hay que gestioanrlo
- tengo una ceirta idea de que tiene pinta que de las muchas opciones que hay, marketplaces, una página personal es la que menos fees tienen para uno mismo, y odoo permite hacer bundles de uno mismo. AUnque pagas el referral fee: MVP kofi => odoo colaboración con printers, automatizar la tarea de manfuactura, ahorrar un sueldo.
- tengo una hipótesis, y es que la ofrma en que gestioanr la oepracioens auotamtizadas, en vez de hacerlo manual puede haorra más timepo => RPA o por el propio programa => o si quiere trabajr en concjunto, lo que he investigado puede que le sirva.
- => sólo voy a jugar a ser barato o a tener lo mismo, lo que diferencia son las ditnstas vistas parcialkes

- [ ] si el pain parece que el rival aprece ser shopify, que ceuste lo mismo, pero que tenga una visión de mrp mejor en vez de costando 100€ costando lo que shopify, o shopify + katana => quiero imitar odoo.sh. quiero depslegar odoo.sh y ofrcerlo a aselcis

----------

9
- [ ] hoy o mañana => hsitorias de usairo con un what wows? quiero hacer un poc, es un shopify con el poder de odoo: qué MVP
- [ ] preguntar esas dudas sobrwe estrucutra de coste: algo que escale a 0 ypueda ocnsturir un saas que cueste 0 para el cliente y como el cloud provider, sólo se tnega beneficios, si se vende 10% por cada compra, una cosas muy de mínimos
- [ ] el bitname ese depsñgarlo y ver cómo funciona

https://www.shopify.com/blog/211990409-how-to-sell-art-online

16

- [ ] qué es lo que quiero ser de mayor: ofrcer un saas un software como servicio, ceirtos serivicos de oddo qye ya he jsutificado, para autónomos, de que paguen 30€ cada mes, como shopify, con más funcionalidades, y un máximo de 50 en función dle uso.  quiero ser: auitonomos llegan con ideas, le doy un plan de negocio
- [ ] lo suyo sería que pagasen 0.
- [ ] dscutir en cuanto a estructura de costes: kubenrtes vs aplcaicineos de servicio: precio, frente a evitar  esté corriendo toda la noche => 
- [ ] un despliegue de odoo en kuberntes gcloud +linode + alicloud

deploy this in cloud run  + cloud sql => 10€
autopilot => 0€ to 40€ => i have a question, so if i want to deploy a cluster. its gonna be alive all the time or not?
fargate + aurora serverless => 0 to 5€
alicloud?

=> cuanto cobro a mis clientes: odoo saas 50€/mes, sólo si vendes, sino vendes te cuesto 0. En función de lo que usen tu plataforma

- [ ] 

https://cloud.google.com/architecture/best-practices-for-running-cost-effective-kubernetes-applications-on-gke
https://www.youtube.com/watch?v=goZFUy4uHVg
https://www.youtube.com/watch?v=Zztufl4mFQ4
https://www.youtube.com/watch?v=-59KDnNrIfc
https://techbeacon.com/enterprise-it/5-open-source-apm-tools-compared
https://techbeacon.com/enterprise-it/top-5-open-source-rpa-frameworks-how-choose
https://www.youtube.com/watch?v=eVeafIoZcXA&t=2s
https://aws.amazon.com/blogs/apn/building-a-multi-tenant-saas-solution-using-amazon-eks/
autopilot => 13€/mes: autopilot shutdown your databases if they are not used?
=> migrating to cloud spanner
or fargate and auroraserverless

=> cloud run or autopilot
autopilot keeps alive the database

kubernetes
specific solutions

kubenretes => autopilot 13€/month
cloud run + cloud sql

alibaba: pay as you go

https://www.reddit.com/r/aws/comments/j84h22/why_doesnt_aws_have_a_cloud_run_equivalent/
http://fargate-pricing-calculator.site.s3-website-us-east-1.amazonaws.com/
https://www.reddit.com/r/aws/comments/i01whu/eks_w_fargate_pricing/

23
30





- shopify manage inventory, but has not different form which to send => datos para el seguimeitno del pedido. Es decir, no avisa de cuántos productos pedir, ni de irle haciendo el traqueo del pedido al cleinte
- el cusotemr jorney: publico un catálogo de productos, el cliente lo elige, cuando se relaiza la compra le llega la petición al proveedor, cuando esté el pedido, se recoge en tienda y se envía, cuál es la mejor opción de tranpsorte
- first year, shopify for free

- catalogo: all the same (with the plus of images from an url)
- inventario: visualizar stock sí, alerat a proveedor => SIGE, estoy haciendo esto, reflexión para depslegar una web, no ´se hasta qué punto estará bien las hipótesis, pasar lo que es´tais haciendo cunaod lo termiéis, cogerme sige & preguntar cómo es el proceso, o algún libro en generla de cómo funciona esto
- marketing basic 0> shopify y otros

=> why beacuse it has more fucnitonalities, not
it's cheaper (price of a cluster) + same func, plus some tips => freemium, bundle, same as shopify => entocnes el problema cuál es? que cunaod piden productos  quieres saber los que están hehcos y los que no, o sea que no es´ta integrado con la producción
100 kitana essential plan, automazar producción

- [ ] Odoo puede permitir un Shopify + gestor de stock + newsletter + estado de las imágnees en un csv => despleigue propio: cuál es el mejor mecanismo pay as you go escalable => IaaS, PaaS, SaaS
=> SaaS no, PaaS => donDOminio  muy barato pero como Shopify. IaaS => AWS vs Azure vs GCP vs AliCloud vs IBM => alicloud barato no free tier vs GCP autopilot
=> what is? what if? ahorro de tiempo, quiero comrparlo y hostearlo, reducir coste
=> preguntar, oye, cuál renta más
- [ ] deplegar odoo, para ver estas funcionalidades, primero en local y luego en cloud => definri el happy path a patir de los requisitos, tanto en compra como en gestión de inventarios, como en marketing => en la nube; 
=> what if? user stories (use cases) + con ciad
=> mejor forma de despelgarlo => ver el video de clusters de k8s
=> el cómo vs en dónde => a la larga, pq debe tener un precio u otro: esobzar un plan econcomico financiero =>bbva, a paritr de un cierto uso, uno cuesta más barato
=> fases 1 mes de depslegarlo en los tres sitios? primera incursión => instead of a video, why not an awsome repo that anyubody can modify?
- [ ] documentar esto: en las slides, incluir saleor
- [ ] quiero ver si cómo hago yo las cosas es como se hace en general: puedo cursar esas asignaturas a falta de 6 créditos
- [ ] ya están definidos esos path, y despelgado eso en la nube => hacer planes de negocio sobre cuál es el mejor precio
- [ ] cómo copiar un odoo saas; los script que presento son abiertos, lo que cuesta es la oepraicón de seguirdad, que esté bastante disponible. Ask Aselcis and CYbrosis what they think about that

- [ ] hacer un curso para despelgarlo en alicloud
- [ ] auditar el despleigue: Aselcis o a quién pregunto para auditar ese despliegue => hacer un saas, payg
- [ ] meter plataforma de pagos
- [ ] evlauar lo del portencaje que se llevan las pasarelas de pagos (preguntar a Alex que hizo su TFG de eso si la pasaerla de apgos de caixa que estudió es segura)
- [ ] meter lo de google analytics para saber cuántas visitas llegan
- [ ] (leenversefashion) el despliegue de odoo: y el conector para itnergarlo con shopify


=> estudiar cómo se va a gestioanr stock (directamente decir que en una semana puede llegar)
=> método de trasnporte (correos o portefy)
=> compartir la página
=> cómo integrar facturas

---------

- [ ] estructura de coste, como otra caracteristica más a la hora de jsutifica rel producto
- [ ] prototipar la de odoo a pelo, y luego tres más, con lighthouse
- [ ] describir conclusiones


----------------------

Spitn 2.2

Hola Santiago y Dani, ¿cómo va todo? Bueno pues en estos poco minutos quiero compartir con vosotros qué he hecho en estas semanas qué tengo pensado hacer en el próximo mes y qué problemas he tenido

 Primero, disculapd mi demora en este sprint en cuanto al plan, a principios de abril tenía que entregar y entrego hoy 21 de abril. Con Dani ya l ohablétodavía no Sanitago, te le intenté dedicar 40 horas semanales que quería dedicar al proyecto, le decdica tantas hroas en marzo que el emxane de ciberseguridiad no le dediqué mucho. Así que me centré en los 4 proyectos que tenía para semana santa y este finde he retomado el proyecto, como se puede ver en las horas que me registro en toogl con pomodone.  Así que propongo un cambio de estrategia; si de las 700 horas que son un TFM llevaba 300 horas,  quería deidcarle 20 por semana, para cada mes hacer 100 y hasta antes de verano hacer 300 horas, para tener el verano más libre para prácticas, y así convalidar esos 6 créditos que me faltan en verano. Propongo, reducir a 8 horas smeanles en este mes que falta, por no suspender nignuan asignatura, y desplzar esta carga de trabajo a junio y julio, a 40 horas cada mes, compeltando como 300, a falta de ehcar 100 restantes en el primer semestre del curso 2021-2022. Con el fnd de dejar más o menos paltneado un servicio de ecommerce en producción para verano y djear horas de mantemeinto evolutivo para el sigueiten semestre. Entonces, en vez de conseguir esos 6 cvréidtos a´si, he pensado que como me flata background en las limitaciones de lso servicios de gestión de la empresa, en vez de ahcer prácticas, cursar el sigueitne semestre un par de asignuas del itironrao de gestión, de 4.5 y 4.5, una sobre sistema de información para el mundo empresarial y puede que una de admisntiarción de dempresas. Y así, bueno itnetnar para septeimbre un tfm completo, para resentarlo en febrero. Y en adleante seguir con el mantenimiento del servicio por un lado y preparar la opiscion del cuerpo tic de a1 de la AGE de febrero  a febrero con el dienro ahorarado, pagando una academia. Y caudno se me acabe, significa que este sericio que he desarrollado en el tfm no me es suficiente para ser autónomo, así que itennar aplciar a un puesto relacionado con la epxerienceia que he aprendido en el TFM, algo de site relaibility engineer, consutltor de servicios de gestión y cloud, algo así

Bueno depsués de esta expclaicón mía en genrral de cómo veo la jugada, comparto con vosotros qué he hecho en estas semanas qué tengo pensado hacer en el próximo mes y qué problemas he tenido

qué he hehco pues lo que hablamos

el obejtivo etra para mayo depslegar el servicio en gogole cloud, sobre todo para tener el servioc de newsletter, quitaé el saleor investigué, para luego a fianles de mayo pedir una auditora del depsleigeu

Peor snetí que no tenía clara la jugada en cuanto a porqué elegir odoo, a largo palzo qué precio tiene que tener y que fucnoinalidades en comapració con tros servicios para que se útil? Es decir, el tiempo en depslegar un servicio con este servicio oepn soruce hasta qué punto merece la pena

Enotnces lo que hice fue, tres cosas
 primero una slide para orgnaizarme las ideas en lso spirnt, 
luego ivnesitgar sobre cómo ocmaprtir la ifnormación (word, o latex con overlefa)
 y leugo hace una comapración basada en procesos de negocio
COn el fin de hacer otra compración basda en servioc open soruce y cloud, para hacer un depsliegue como muy tarde el 15 de junio
Investigar otra opcione scomo alicloud pay as you go, de forma que se peude reoslver la pricnipal infeicenie de google cloud que era el coste de tener la bbdd encendia siempre cuando el servico eccomerce está muy centrada en la franja hraorio de unos usuarios

EN cuanto a las slide, las peude comrpatir algo así con 4 pasos pbasado en deisng thinking

EN cuanto a como comrpatir ifnormacion, me familiarizae con verleaf y owrd, así que en el futro puedo usar cualqueira

Cómo coamprtar rpocesso de negocio y herraminetas saas
a largo palzo qué precio tiene que tener y que fucnoinalidades en comapració con tros servicios para que se útil? 
Tere sufncioanldiades crear el commerce, gestaonr oepracioens y marketing
En reusmen tras la ivnesitcaión ya esta basad en datos, algo pay as you go para no pagar los primeros meses, o si es así pagar pero poco e tientar que aumetne este precio en funcion del uso

Esto he ehco en estas msenas, que tengo pensado ahcer
Pues lo primtedio para el anteriro, para el 15 de junio, el servioc de amrketing
prpond´ria:
pregunatr sobre alicloud, si hay algun gasto ocultoen stack overflow
Hacer un comarpacion de estrucutra de coste: mejro  kuebrntes u otro servico
Con la repsuta de alicloud o mientras depslgar en virutal box odoo communtiy ya 

iamigno que esto ya será en julio
sabiendo que procesos de engocio comrpobar
Hacer un tutorial de ali cloud y depslgearlo
Entonces, depslgear la pa´gina, el email + crm+ invenatior
y auditoria

Prolbemas
 
 
 -----------------

Spitn 2.3

Sprint 2, tercera iteración

Hola Santiago y Dani, ¿cómo va todo? Bueno pues en estos poco minutos quiero compartir con vosotros, pues lo de siempre, qué he hecho, qué tengo pensado hacer y qué problemas he tenido.

Qué he hecho en este mes?

Pues a parte de examenes jeje he planteado las tres tareas que hablamos:

- [ ] 1 Primero explroar la estructura de coste, a raiz de pensar a priori dónde es mejor despelgar
- [ ] 2 prototipar la de odoo en vbox, comprobando que se pueden ejecutar sobre él los procesos de negocio, y luego en más opciones, comparando con lighthouse la performance
- [ ] 3 describir conclusiones, sobre todo, cuál es el más idóneo llevar a producción

- 1- EN cuanto a 1 Primero explroar la estructura de coste, a raiz de pensar a priori dónde es mejor despelgar. Otra vez pensé, y me di cuenta de que claro esta estructura de costes es una propuesta de valor del servicio, por eso es tan improtante

Me dediqué a dos subtareas:

a. recomparar las hipótesis referida a los procesos de negocio
b. comparar  qué estructura de coste aporta más valor

a. Por qué quería recomparar las hipótesis referidas a los procesos de negocio? Porque de la tabla anterior (que por cierto he hecho más chiquitita para que se peuda ver) es la clave, es la propuesta de valor: la conlusión del otro sprint era que desplegar un odoo community era una opción imbatible frente al resto de ocpioens. Pero en realidad, más que imbatible, es que es más completa que la competencia a largo plazo: permite ofrecer un shopify a precio de etsy con katana. Nótese que se estudian dos opciones más, katana, una mrp, para visualizar y autoamtizar pedidos integraado con shopify que cuesta 100€/mes y Etsy un marketpalce. De forma que la conclusión cambia ligeramente: tanto amazon como shoppify/wix/odoo saas como doo community en la nube, son buenas opciones, quizá lo más eficiente sigue siendo un odoo en la nube porque pemrite la autoamtización de la petición de la manufactura (ese mrp, katana), pero claro, depende del precio al que esto se consiga. Lo suyo sería a precio de Etsy o a precio de amazon, es decir, un cierto porcentaje de la compra.

AHora bien, con esta hipótesis en mente, de que tatno etsy como amazon como shoipify o wix son opcioens válidas pero que la jugada es que, sólo si se pagan 100€/mes es posible automatizar el stock del catálogo con la producción, es entonces cuando aparece el valor de un odoo en la nube: es al fin un katana con shopify.

b. Entonces, ahora se comparar  qué estructura de coste aporta más valor. VAlor en qué sentido? Para qué cleinte?

Se plantea ese primer usairo de breadfree o los cuadros de mi madre y luego en un futuro otras posible tiendas. De forma que se destaca que a largo plazo es buena idea optimizar costes, pero a corto lo que se desea es una solución con la performance de odoo saas pero grátis un cierto tiempo, el tiempo de prueba, teimpo en el que se puedan testear lso procesos de negocio.

Ahora en vez hacer 1.b se realzia la tarea 2, me refiero cronológicamente

Pero en resumen la idea es que si kitana cuesta 100€/mes

se plantean soluiones escalables como 

kubenretes => autopilot 13€/month
cloud run + cloud sql
alibaba: pay as you go
fargate and aurora
https://www.reddit.com/r/aws/comments/h96nhe/access_aurora_serverless_instance_from_local/

de forma que se puede despelgar odoo community para ofercer shopify + katana por la mitad de dinero

cloud vs on premise => cloud
saas, paas, iaas => ofrcer un saas

vmaas, k8saas, caas, faas

=> 40€/mes

7 al 15 de jun =>
prototipar odoo
preguntar cual de los 4 propeustas es mejor/más barata

tengo: tantos créidtos grátis: 5 casos de prueba de dónde mejor

kubenretes => autopilot 13€/month y azure, se puedne apagar si no se usan
cloud run + cloud sql => 10 a 20
alibaba: pay as you go
fargate and aurora, fargate necesita lb?


- [ ] 2 prototipar odoo en vbox, comprobando que se pueden ejecutar sobre él los procesos de negocio, y luego en más opciones, comparando con lighthouse la performance

cuáles son los procesos de negocio?

Las tareas o casos de uso que se comparan => estrategia de odoo en la nube para llevar inventarios, y luego posibildiad de conexión con etsy o amazon

Se plantean unos ciertos casos de uso con historias de usuario específicas, que definene los procesos de negocio. Y a continaución se comparan si se puedne realizar con las sigueitnes herramientas: básciamente todas se prueban con un odoo en vbox, etsy y amazon permiten vender pero no automatizar lso pedidos con la manufactura.

Para desplegar el odoo community, se plantea o usar un stack de bitnami que exige configurar ips o instalar cada elemento. Instalar cada elemento ayuda a tener concienia de cómo luego operacionalro en microservicios.

Se crea una vm para luego pasar el despliegue y que sea fácil

Jun
1
2 check odoo and compare clouds
3 deploy and newsletter and eshop
4 writing plans
5
Julio
2
3
4
5



----------------

Strategia coste autonomo
https://ayudatpymes.com/gestron/vender-por-internet-sin-ser-autonomo/
https://www.lamoncloa.gob.es/presidente/actividades/Documents/2021/270121-PlanDigitalizacionPYME01Optimizado.pdf
