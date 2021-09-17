# S4

Qué he hecho, qué tengo pensado hacer y qué problemas he tenido?

QUé tengo pensado hacer para el sigueitne sprint: hito es para el 25 de junio es necesario que haya un servicio de dnewsletter en produción para que se peuda aprender ausarlo para el 8 de julio sacar la capmapaña. Pureba a depslegar en gcp odoo ce con el ojetivo de que ceusta 30 en vez de 70

- [ ] 1 Desplegado un entorno de pruebas 20
- [ ] 2 20 de junio llevalro a producion -25 hacerle laod tesitng
- [ ] 3 25 probar y enseñar


- [ ] 1 Desplegado un entorno de pruebas 20

stateless copilot => 70€/mes

La estrategia de parar reducir coste, la opció mejor aprece en gcp con cloudsql. app runner + aurora svl 70$ pero escla más

Una grande y en ella varias, menos latencia

witha ntoehr account, pass this data to the otehr

depwsslegar eso probar:

perforamce
backup
hacer un konta, grátis para siempre. Para pedir créditos, de aws, gcp


1- cloud run 
2- cloudsql
3-how to connect


## procedimeinto de despleigue
## procidimeinto de backup
## procedimeinto de http2
como hacer pruebas?
---------

## procedimeinto de despleigue
## procidimeinto de backup

addons como montarlo en un contenedor

gituhb actions para que coja eso

crear otro contenedor, cómo hacer que aneje los secretos la bbdd y el fichero de conf

Para bakup hay que isntalar eso, lo pruebo en la máquina. dónde guardo el backup?

## procedimeinto de http2

para ahcer eso

## problema con las sessiones

migracion a la version 13


actulizar la tabla de herramientas

cloud run + cloud sql 30€/mes => 360€/año => no funciona
problema con el backup que se puede solucioanr exportando

tiene que ser en la nube?

hacer algo que cuimpla los procesos en paln consultor

15 de julio, 20

ofrcer eso que haga a más


rescribir la tabla de herramietnas: poniedno herramietnas como stack, y añadir seuridad y disponibldiad. En dos horas mr domian puede ocsta 60+120 =180€/año vs 360€/mes. Merece la pena?


por 180 € algo mejor que shopify => ventas
 
 por 600 €
 
 más tengo el protfolio de servicios
 
 

- [ ] 2 20 de junio llevalro a producion -25 hacerle laod tesitng
- [ ] 3 25 probar y enseñar

----------

Hola Santiago, hola Dani, cómo va vuestor verano?

pues en este video os reusmo como siempre, qué he hecho este mes, qué problemas he tenido y que tenog planteado para el siguietne mes

1- Qué he hecho este mes?

Lo que dije que iba a hacer 

- [ ] 1 Desplegado un entorno de pruebas 20
- [ ] 2 20 de junio llevalro a producion -25 hacerle laod tesitng
- [ ] 3 25 probar y enseñar

el resutlado ah sido que lo eh hecho pero que en clodu run csql sienod la opcion más barata no vale porque clodu run no persite el estado de form que se peudrn lso css tneog las cpautras qu elo dmeuestran


Todo esto para el itento de odoo ce, si quieres hago zoom para poenr en contexto

en el rpo actualicé el estado del arte, la jugada era que se han idnetifaicado cierto srequsitos  de tienda onlein+ gesiton d eintecatio gesiton de marketing, iterivamtene s eproponeen sw y depsleigeus

primer itneot pensaba el el qurisot era un minimo ahcer un ecocemrce desde cero, desde serverless incluso hice una demo,a hsta deposlegue un cluter como aumtaizar cd ocn jenkins x o ahora mas adetna con corplace y con argo, auotmaicar con vm awen aws. Quizá hablé pco de esto pero bueno est rabjao que hcie, y el resutlado era que si el objetivo es tener un shopify o wix  o un hstoign con wordpress, iba a ser muy barato hosterlo en le kuebrntes servleerss que iba a ser cloud run

primer inteot saelro, la peroisnalizacion no er acmomoq eureiamos

a busar odoo pareica uan solcuion itnegrada masd carac que un hsoting qu epuede ser como 10€/mes, con cloud run bajar preioc

parece que no y admeas en las purebas con loader que cae la solcuon de vm + csql que fue la sigueiten opcion

una dmeo de que funcioanldiad tenia

suponiia o deplgar un clsuter de juebtes 50 al mes, de priemras no ofrecia mas ventaja que un hstoign

me aplentae apenrder owrpdress y woocmerce, itnear imitar todos los requistos y lso rpoeceso de negocio de odoo itnegrados con plugins de woocmerce, tengo un reusmen de ocampraitva de plguiins , que peude que custe como 30 € al año

- qué es lo que tenog pensado?

si llevo como 600 hen spetiembreen y lo que le pueda deidcar en agosto 100 horas, tener ese mínimo por un lado teinda + newsletter tnaot prar dani como para mi madre y si el tf tfm son 800, en la sotras 50 intear hacer aele anlidas de riesgos de loq ue quede , toamndo como paltneialla elqui hice en una asignaturas

y para finales de septiembre pricniois de otubreescribrlo entero,a sigque para fianles de octubteew te diga este es el word que he hecho qué te parece


- problema he tindo

camio









  Me gustaría sobre el 25 de julio proponérosla, pero me falta todavía  En resumen: odoo pareció la solución integrada definitiva frente a WordPress, Spotify (360€ al año )o wix (200€ al año) y con cloud run iba a costar 120€ al año. Pero tras un mes, como te conté, no conseguí que funcionara por el estado efímero de su disco. Probé la forma clásica de servidor en gcp con la tienda de mi madre (https://piedadleon.art), funciona, pero a priori parece que cuesta entre 500 y 700 pavos mensuales. A largo plan, es una solución muy personalizada y se comparte coste entre empresas,se podría asumir, pero en principio,no way. De forma que volvemos a la cooperación inicial. Aunque ya tengamos una web en odoo pq no replantearnos wp? Estoy trabajando en un despliegue con woo
  
  
  --------------------------------
  
  Hola Santiago, qué tal la vuelta de las vacaciones?
  
  oye, comparto esta actualziación contigo y no con Dani porque sé que está muy liado estos días, luego te ocmento al fianl  lo que he hablado con él
  
  yo bien, muy contento salí en agosto
  
  qué he hecho qué tenog pensado hacer en el próximo mes y qué problemas he tneido
  
 - qué he hecho desd eifnales de julio que te cometné
  
 -  básciamente lo que hacía falta para temrinar habiendo realizado ya esas 650 hroas es ese último empujón que quería darale para llegar a las 810h, y además el poder enseñar un producto que encajer con el lceitne. Hasta ahora he impelenmtando 4 pero ninguno parece que no concenvece al cleitne al 100%.

4 cosas

-  wp +wc + namecheap: más estudio previo de cómo hacer que por 20€ al año  es decir menos de 2€ al mes se tenga toda la funcioanldiad de odoo. y piedad leon art, con una demo

- análsisi de reisgos usando pilar

- ppt presnetaicón aprox en 10 min de lo que propongo decir en enero a ver qué te parece

- meoria en la que palnteo todas esta dieas en word; sigo editando; cosas como cometnario y las voy viendo


qué tengo pensado hacer, 28 de seopteimbre

octubre, noviembre,r evisar lo que me propognas

qué probelmas he tneido, nignuo destacable.


-----------------------

video demo:


Hola, soy Adrián Blázquez, y en este video muestro los caminos del usaior que se han impelmetnado en este prototipo de tienda en woocommerce + namecheap En este último sprint del preycto, los casos de uso que se han analizado se podrían proponer como el sigueitne diagrama de casos de uso. Dos casos de uso relfejados como epic, tienda online y gestor de inventarios. Dos grandes actores, el comrpado r y el gestor de la tienda, y casos de uso secundarios derivados de los casos de uso principaes: de tienda online se se identifica uno relacionado con que el comrpador visaulzie los productos del catálogo y pueda realizar el pago bajo la introducción de su domicilio. Además se necesita que llguen correos que informen al suairo del sigueitnemiento del pedido. SObre este caso de uso principal el gestor de la teinda puede consturir la web, es decir añadir o quitar uno u otro producto añadir algún mensjae de oferta. Respecto al caso de uso de gestor de oepracone se resalta el poder visualizar el stock. Esto es muy improntate en el caso de la tienda online de la artista, en el que se prevee gran rotación de stock de embalaje y poco spacio de alamcén, así que se propone como forma de autoamzitar la detección de flata de stock. Por último, el caso de uso de calculador de csote, en caunto a que se necestia que en los peiddos se refelje tanto el casote dle propio producto para relaizar una estimación dle coste, como dle propio coste del envío en función del peso de los productos.

Por último, se desa señalar que se cntempla como improtantes los requisitos no funcionales de disponibilidad y seguridad, que serán analizados en otro video

Vale, primer caso de uso secundario

Visualización de catálogo. El usuario llega a piedadleon.art. consulta la landing Page, le informa de una oferta. Decide leer sobre la artista. Decide consultar el catálogo. Puede ver distintos cuadros y además elegir distintos tamaños y si lo desea impreso o original.

Sobre esta funcionalidad, nótese que primero se planteó un modelo de datos en el que se desglosaban las variantes tamaño e impreso u original. Pero más adelante, se identificó el problema de seguir el stock de productos secundarios como el embalaje, de forma que se vuelve necesario encontrar una forma de expresar el producto dibujo 1 tamaño a2 para que cuando se compre se descuente no sólo el lienzo, sino los otros elementos que lo componen, del stock. Como el tubo, el sello identificativo o la etiqueta de envío. Entonces se plantea usar el plugin wpc clever bundle expresando los productos así.

Vale, por otro lado una vez se ha añadido al carrito se puede proceder a la compra. 
Primero se comprueba el stock por ejemplo del dibujo 1 con la herramienta smart manager, se observa que sale en backorder, y con stock de tubo 1

Para el caso de dibujos impresos se ponen los elementos como sin límite, pq imprimir un dibujo apenas toma tiempo en comparación con pintarlo. Se finaliza compra, se observa que en woocommerce pagos se ha configurado tres, tarjeta PayPal y stripe, habiendo previamente creado una cuenta bancaria aislada en un banco. Para no pagar cuotas adicionales se opta por el pago en mano para el ejemplo. Se compra, se comprueba que la orden aparece y que llega un correo. Luego se comprueba como el stock de tubo ha disminuido en 1

Por otro lado, para lienzos originales agotados como el 3 se compra y se observa como no se deja comprar 

Segundo caso de uso seguimiento, 
Se ha configurado la cuenta de email de cliente y la del gestor
ha llegado el mensaje  se procesa la orden llega otro mensaje tanto a cliente como a gestor. Se procesa el pedido y llega otro

Constructor. Cómo se ha visto se ha creado un usuario gestor de tienda

Por último, se desa señalar que se cntempla como improtantes los requisitos no funcionales de disponibilidad y seguridad, 

FR:
- Tienda online: 
- 1.1. Constructor de sitios web (CMS) + catálogo + plataforma de pago
- 1.2. Seguimiento de paquetes: avisar que se ha realizado el envío
- Gestión de operaciones
- 2.1. Integración pedido tienda/Visualización de stock: poner en los originales que el stock es uno. Si quieres otro, escribir al email
- 2.2. Calculador de coste: tanto de producto como de de envío: Opciones de envío para nacional e internacional
- NFR:
- Disponibilidad: cuantos usuarios o conexiones a la vez se pueden servir
- Seguridad: cuán fácil es actualizar el sw

En un pr9mer punto se ocmpreuba como woocmerce pemrite editar web, con elmetnor
Ver un catlolo, y comprar, s eockpra y lelva el mensaje

Primeor conv ariaciones, psoibidalid de ahcer pedidos de llevar un conteo del stock

Se ha visto cómo se ha ocmprado el origianl, y se desucento uno del stock

Genración de pedios para comrpa a proveedores, se piden y se guradan
se observa como envío naciaonl e itnernacioanl

Se gnerna las disinta partes y a tra´ves del cmapo low stock del excel se peude, Se ha ocnfiurado con ese plugin

jem talbe rate, en base a pesos

Aceso rápido, dipsonibildiad con la versión ba´sica hasta cdn con el otro fallaban

No se ha relaizado un anañsis de riesgos en proufniddad plugin siem, accesoy 2fa

disponible y segruo


--------------

vidoe ppt


--------------------

despue´s de camri el número de products a mostrar no se pueen ver

https://www.storeapps.org/woocommerce-delete-all-products/
  
https://stackoverflow.com/questions/47247512/any-way-to-set-screen-options-wordpress-via-the-database

https://wpfluent.com/how-to-delete-all-woocommerce-products/
