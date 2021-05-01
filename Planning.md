
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
 
 






