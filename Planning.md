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


--------------

vidoe ppt


  
  
