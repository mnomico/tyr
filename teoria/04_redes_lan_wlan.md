## [Volver atrás](../readme.md)

<div align="center">
<h1>Redes Locales y WLANs</h1>
</div>

### Indice

💡 [Conceptos a tener en cuenta](#conceptos-a-tener-en-cuenta)

❓ [LANs - Guía de preguntas](#lans---guia-de-preguntas)

❔ [WLANs - Guía de preguntas](#wlans---guia-de-preguntas)

📝 [Resumen](#resumen)

📖 [Bibliografía](#bibliografia)

---

### Conceptos a tener en cuenta

- Características generales de las Redes de Área Local
- Identificar propiedades de los diferentes tipo de acceso al medio:
    - Dinámico/Aleatorio (con contienda)
    - Dinámico/Controlado (sin contienda)
    - Estático
- Acceso al medio CSMA/CD
- Protocolo Ethernet y su sucesor, el IEEE 802.3
- Algoritmo de un bridge/switch
- Hub, Bridge y Switch Ethernet.
- Alcances y limitaciones de las WLANs
- Acceso al medio CSMA/CA
- Problema del nodo oculto

---

### LANs - Guia de Preguntas

1. Describa las principales características de una red LAN.

2. ¿Qué es un método de acceso al medio? ¿Cómo se clasifican?

3. Describa cómo opera el método de acceso al medio CSMA/CD.

4. ¿Qué es una colisión? ¿En qué casos pueden ocurrir?

5. ¿De qué forma se enteran los nodos que transmiten que ha sucedido una colisión? ¿Y los restantes?

6. ¿Qué es una colisión tardía? ¿Qué problema podría ocurrir si sucede? ¿Por qué ocurren?

7. ¿Cómo opera y cúal es el objetivo de la técnica de Backoff?

8. ¿Qué es un hub y un conmutador (switch)? ¿Cuáles son sus diferencias funcionales principales?

9. Enuncie las características básicas de una red Token Ring y una basada en bus.

10. ¿Qué es Ethernet? Describa sus características principales.

11. Describa sintéticamente las normas 802.x.

12. Explique el modo full duplex en Ethernet.

13. Describa las similitudes y diferencias entre Ethernet, Fast Ethernet y Gigabit Ethernet.

14. ¿Sobre qué topologías se puede desplegar una red Ethernet?

15. ¿A qué se denomina modo promiscuo de operación en Ethernet? ¿Cúal es su utilidad y cuál su peligrosidad?

16. ¿Qué son las direcciones MACs? ¿Cómo se asignan?

17. ¿Cúal es el objetivo de los puentes en LANs? ¿Qué es un puente transparentes?

18. ¿Cúal es la diferencia entre un dominio de colisión y un dominio de broadcast?

19. ¿Qué objetivos se persiguen con la implementación de puentes (switches) (conmutadores) en las redes locales?

20. ¿Qué diferencias existen entre Ethernet e IEEE 802.3? (detalle los formatos de trama en cada caso).

---

### WLANs - Guia de Preguntas

1. Elabore una comparativa entre los diferentes tipos de servicios Wireless: Celular, Microondas, WiMax, Bluetooth, WiFi, Satelital, etc. en los siguientes aspectos:

    a. Frecuencia de Trabajo

    b. Ancho de Banda

    c. Velocidad Nominal

    d. Ventajas/Desventajas de cada una respecto al resto.

2. Explique cuáles son las similitudes y diferencias entre los métodos de acceso CSMA/CA y CSMA/CD, y justifique los motivos.

3. La capa de acceso MAC permite utilizar el medio en dos modos de coordinación. Explique brevemente en qué consiste cada uno de estos modos de trabajo.

4. ¿Cuál es la solución al problema del Nodo Oculto?

5. ¿En qué casos es mejor usar el esquema CSMA/CA y en cuáles usar RTS/CTS? Justifique y desarrolle posibles entornos.

6. Si se configura la red como "oculta" en un AP, ¿qué sucede con los beacon frames? ¿Realmente produce un ocultamiento de la red? 
¿Cómo se produce la asociación a la red? Justifique.

7. ¿En qué caso se utilizan los 4 campos de dirección de una trama?

---

### Resumen

### 12 Multiple Access

Podemos considerar que la capa de enlace de datos tiene dos subcapas. La capa superior que es responsable del control de flujo y de error se llama **capa de control de enlace lógico (LLC, Logical Link Control)**, la capa inferior que es responsable de la resolución de múltiple acceso se llama **capa de control de acceso al medio (MAC, Media Access Control)**

Cuando los nodos o estaciones están conectados mediante un mismo enlace, llamado **enlace multipoint** o **broadcast**, se necesita un protocolo de múltiple acceso para coordinar el acceso al enlace.

### 12.1 Random Access

En los métodos de acceso o contención aleatoria, ninguna estación es superior al resto y a ninguna se le asigna el control sobre otra. Ninguna estación permite o bloquea a otra estación a transmitir. Cuando una estación necesita transmitir, usa un procedimiento definido por el protocolo para decidir si transmitir o no transmitir. Esta decisión depende el estado del medio, es decir si está desocupado u ocupado. Las estaciones compiten entre sí para acceder al medio.

Si más de una estación trata de transmitir, puede haber una colisión y las tramas van a ser destruidas o modificadas. Para evitar esto, se utilizan métodos que evolucionaron de un protocolo conocido como **ALOHA**.

El protocolo ALOHA original se llama **ALOHA puro**. Cada estación transmite una trama cuando tiene datos para transmitir. Como hay un solo canal compartido, existe la posibilidad de colisión. El ALOHA puro depende de los ACKs del destino, si no se recibe el ACK luego de un período de tiempo (conocido como **time-out**), la estación asume que la trama o el ACK fueron destruídas y retransmite la trama.

<div asign='center'>

![](./imagenes/04_aloha_puro.png)

</div>

Para evitar que varias estaciones, al retransmitir sus tramas colisionen, cada estación espera un período de tiempo aleatorio antes de retransmitir su trama. A este tiempo se lo llama **tiempo back-off (Tb)**.

Luego de un número máximo de retransmisiones Kmax, la estación debe darse por vencida e intentar más tarde.

El período de time-out es igual al máximo valor posible de **delay de propagación de ida y vuelta** (RTPD, round-trip propagation delay), el cual es el doble del tiempo requerido para enviar una trama: 2Tprop. El tiempo back-off es un valor aleatorio que depende de K (el número de intento de transmisiones). Se toma un valor entre 0 y 2^k - 1 y se multiplica por Tprop o Ttrama para encontrar Tb. El valor de Kmax en general es 15.

<div asign='center'>

![](./imagenes/04_procedimiento_aloha_puro.png)

</div>

El **período vulnerable** es el tiempo en el que existe una posibilidad de colisión. El período vulnerable de ALOHA puro es 2 veces el tiempo de trama.

Este tiempo de vulnerabilidad en ALOHA puro se da porque no hay reglas definidas sobre cuando una estación puede transmitir. **ALOHA con ranuras** fue inventado para mejorar la eficiencia del ALOHA puro.

En ALOHA con ranuras se divide el tiempo en ranuras de Ttrama y obliga a las estaciones a transmitir sólo al comienzo de una ranura.

<div asign='center'>

![](./imagenes/04_aloha_con_ranuras.png)

</div>

El período vulnerable de ALOHA con ranuras se reduce a la mitad, es decir que es igual a Ttrama.

Para minimizar las probabilidades de colisión e incrementar el rendimiento, se desarrolló el método **CSMA (Carrier Sense Multiple Access)**. La probabilidad de colisión se puede reducir si la estación sensa el medio antes de transmitir.

La probabilidad de colisión todavía existe debido al delay de propagación, cuando una estación envía una trama, le toma un tiempo al primer bit para llegar a cada estación. Una estación puede sensar el medio y verlo desocupado porque el primer bit de otra estación todavía no llegó.

<div asign='center'>

![](./imagenes/04_colisiones_csma.png)

</div>

El período vulnerable de CSMA es el tiempo de propagación Tp, el tiempo que necesita la señal para propagarse desde un extremo del medio al otro.

**Métodos de persistencia**

Para saber que hacer cuando un canal está ocupado o desocupado, se desarrollaron tres métodos.

<div asign='center'>

![](./imagenes/04_metodos_de_persistencia.png)

</div>

El método de **persistencia 1** consiste en que cuando la estación encuentra el medio desocupado, transmite una trama inmediatamente. Tiene la mayor probabilidad de colisión.

En el método de **no persistencia**, una estación que tiene datos para transmitir sensa el medio. Si el medio está desocupado, transmite. Sino, espera un período de tiempo aleatorio y sensa el medio de nuevo. Reduce la probabilidad de colisión debido a que es poco probable que dos o más estaciones esperen la misma cantidad de tiempo para transmitir, sin embargo reduce la eficiencia ya que puede dejar al medio desocupado.

El método de **persistencia p** se usa si el medio tiene ranuras de tiempo con una duración igual o mayor que el tiempo de propagación. Combina las ventajas de los otros dos métodos, reduciendo la probabilidad de colisión y mejorando la eficiencia. En este método, luego de que la estación vea al medio desocupado, sigue estos pasos:
1. Con probabilidad p, la estación transmite su trama.
2. Con probabilidad q = 1 - p, la estación espera a la próxima ranura y sensa el medio de nuevo.
    
    a. Si el medio está desocupado, vuelve al paso 1.

    b. Si el medio está ocupado, asume que ocurrió una colisión y usa el procedimiento back-off. 

<div asign='center'>

![](./imagenes/04_diagrama_de_flujo_persistencia.png)

</div>

El método **CSMA/CD (Carrier Sense Multiple Access with Collision Detection)** implementa que hacer dada una colisión, cosa que CSMA por si sola no especifica.

En este método, una estación sensa el medio al transmitir una trama para ver si la transmisión fue exitosa. Si no lo fue, ocurrió una colisión, y se retransmite la trama.

<div asign='center'>

![](./imagenes/04_colision_csma_cd.png)

</div>

Para que CSMA/CD funcione, se necesita restringir el tamaño de trama. Antes de transmitir el último bit de la trama, la estación emisora debe detectar una colisión, si es que hay alguna, y abortar la transmisión. Esto se debe a que la estación, una vez que transmite su trama, no guarda una copia de la trama y no sensa el medio para detectar colisiones. Entonces el tiempo de transmisión de trama Ttrama debe ser al menos dos veces el tiempo de propagación Tprop.

Para decidir cuando transmitir, se utiliza uno de los métodos de persistencia. La estación transmite la trama y al mismo tiempo sensa su propia señal (si es igual, es porque no hubo colisión) en puertos diferentes para detectar si hubo una colisión o si la transferencia fue exitosa. Si se detecta una colisión, se envía una **señal jamming** para que las otras estaciones se enteren de la colisión.

<div asign='center'>

![](./imagenes/04_diagrama_de_flujo_csma_cd.png)

</div>

El nivel de energía de un canal puede tener tres valores: cero, normal, y anormal. En el nivel cero, el medio está desocupado. En el nivel normal, una estación está transmitiendo una trama por el medio. En un nivel anormal, hay una colisión y el nivel de energía es el doble que el del nivel normal. Una estación que quiere transmitir una trama debe sensar el nivel de energía del medio para determinar si el canal está ocupado, desocupado, o en modo colisión.

<div asign='center'>

![](./imagenes/04_nivel_de_energia.png)

</div>

En una red inalámbrica, la mayoría de la energía enviada es perdida durante la transmisión. Una colisión solo agrega entre un 5 y 10 porciento de energía a la señal, lo cual complica la detección de colisiones.

Como no se pueden detectar las colisiones, se deben evitar. **CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)** fue creado para las redes inalámbricas. Las colisiones se evitan mediante tres estrategias: el espacio entre tramas, la ventana de contención, y acknowledgements.

<div asign='center'>

![](./imagenes/04_csma_ca.png)

</div>

Las colisiones se evitan retrasando la transmisión incluso si el medio está desocupado. Cuando el medio se ve desocupado, la estación espera un período de tiempo llamado **espacio entre tramas (IFS, InterFrame Space)**. Si bien parece que el medio está desocupado, una estación puede haber comenzado su transmisión, y su señal todavía no alcanzó la estación que quiere transmitir. Una vez pasado el IFS, la estación sensa el medio nuevamente, y si está libre, puede transmitir, pero debe esperar un tiempo igual al tiempo de contención. El IFS se puede usar para dar prioridad a estaciones o tipos de tramas.

La **ventana de contención** es una cantidad de tiempo dividida en ranuras. La estación que quiere transmitir elige una cantidad aleatoria de ranuras como tiempo de espera. Por cada intento de transmisión, se incrementa la cantidad de ranuras a esperar, similar a la persistencia p. Luego de cada ranura, la estación debe sensar el medio. Si lo encuentra ocupado, detiene el timer y lo reanuda cuando el canal se encuentre desocupado. Esto da prioridad a la estación que estuvo esperando por más tiempo.

Incluso con estas precauciones, puede haber una colisión y se pueden corromper los datos. Para verificar esto, se utilizan las **confirmaciones** o acknowledgements y el timer de time-out para saber si el receptor recibió la trama.

<div asign='center'>

![](./imagenes/04_diagrama_de_flujo_csma_ca.png)

</div>

### 12.2 Controlled Access

En el acceso controlado, las estaciones se consultan para saber que estación tiene el derecho de transmitir. Una estación no puede transmitir a no ser que haya sido autorizada por otras estaciones.

En el método de **reserva**, una estación debe realizar una reserva antes de transmitir. El tiempo se divide en intervalos, y en cada intervalo, una trama de reserva precede las tramas de datos enviadas en ese intervalo.

Por cada estación en el sistema hay una ranura de reserva en la trama de reserva. Cada ranura pertenece a una estación, y cuando una estación necesita transmitir datos, hace una reserva en su ranura. 

<div asign='center'>

![](./imagenes/04_reservas.png)

</div>

El **muestreo** funciona con topologías en las que un dispositivo se designa como estación primaria y el resto de los dispositivos como estaciones secundarias. Todas las transferencias se deben realizar por la estación primaria. La estación primaria controla el enlace, y las estaciones secundarias siguen sus instrucciones. La estación primaria es siempre la que inicia una sesión.

Si la estación primaria quiere recibir datos, le pregunta a las estaciones secundarias si tienen algo para transmitir; esto se conoce como **muestreo**. Si la estación primaria quiere enviar datos, le avisa a las estaciones secundarias que los reciba; esto se conoce como **selección**.

<div asign='center'>

![](./imagenes/04_muestreo.png)

</div>

Si la estación primaria tiene que enviar datos, los envía, porque sabe que el medio esta desocupado, ya que él es el que decide sobre la transferencia de datos. Lo que no sabe es si el destino está preparado para recibir, entonces avisa al destino sobre la transmisión mediante una trama **SEL (select)** y espera una confirmación. 

Cuando la estación primaria está lista para recibir datos, le pregunta (o muestrea) cada estación si tiene algo que transmitir. La estación secundaria responde con una trama **NAK** si no tiene nada que transmitir o con datos. Cuando pasa esto último, la estación primaria responde con una trama ACK.

En el método **token-passing** o **paso de testigo**, las estaciones se organizan en un anillo lógico. Para cada estación, hay un predecesor y un sucesor. El derecho de acceso se pasa del predecesor a su sucesor. El derecho va a ser pasado al sucesor de este último cuando la estación no tenga datos para transmitir.

Para que el derecho de acceso al medio se transmita de una estación a otra, un paquete especial llamado **token** circula por el anillo. Este token da derecho de acceso al medio a quien lo posea.

El tiempo que las estaciones poseen el token debe ser limitado, y el token debe ser sensado para asegurar que no se haya perdido o destruido. También se puede asignar prioridades a las estaciones y a los tipos de datos a transmitir.

Las estaciones no tienen que estar físicamente conectadas a un anillo, este puede ser lógico.

<div asign='center'>

![](./imagenes/04_token_passing.png)

</div>

```
Acá podría explicar las diferentes topologías, pero con la imagen creo que es suficiente
```

### 12.3 Channelization

La canalización es un método de acceso múltiple en el cual el ancho de banda disponible de un enlace es compartido en tiempo, frecuencia, o mediante código, entre diferentes estaciones.

En el **acceso múltiple por division de frecuencia (FDMA)** el ancho de banda se divide en bandas de frecuencia. A cada estación se le asigna una banda para transmitir datos. Cada estación también usa un filtro de pasabanda para confinar las frequencias que transmite. Para prevenir interferencias entre las estaciones, las bandas se separan por pequeñas bandas de guarda.

<div asign='center'>

![](./imagenes/04_fdma.png)

</div>

FDMA define una banda de frecuencia default para la comunicación, lo cual significa que se puede utilizar un flujo de datos continuo con FDMA.

En el **acceso múltiple por división de tiempo (TDMA)**, las estaciones comparten el ancho de banda del canal en el tiempo. A cada estación se le asigna una ranura de tiempo en la cual puede transmitir datos.

<div asign='center'>

![](./imagenes/04_tdma.png)

</div>

El problema principal de TDMA es la sincronización de las diferentes estaciones. Cada estación debe saber el comienzo y la ubicación de su ranura, lo cual puede ser difícil por los delays de propagación que se introducen si las estaciones estan muy separadas. Para compensar los delays, se pueden insertar tiempos de guarda.

En el **acceso múltiple por división de código (CDMA)**, sólo un canal ocupa el ancho de banda entero, y todas las estaciones pueden transmitir al mismo tiempo.

CDMA se basa en la teoría de la codificación, a cada estación se le asigna un código, el cual es una secuencia de números llamada **chips**.

<div asign='center'>

![](./imagenes/04_chips.png)

</div>

Los chips tienen las siguientes propiedades:
1. Cada secuencia está hecha de N elementos, dónde N es el número de estaciones.
2. Si se multiplica una secuencia por un número, cada elemento de la secuencia se multiplica por ese número (multiplicación escalar).
3. Si se multiplican dos secuencias iguales, elemento por elemento, y se suman los resultados, se consigue N, dónde N es el número de elementos de cada secuencia (producto interno de dos secuencias iguales).
4. Si se multiplican dos secuencias diferentes, elemento por elemento, y se suman los resultados, se obtiene 0.
5. Sumar dos secuencias da como resultado otra secuencia.

Si una estación necesita enviar un bit 0, lo codifica como -1, y si necesita enviar un bit 1, lo codifica como +1. Cuando una estación está desocupada, no envía ninguna señal, lo cual se interpreta como 0.

---

### Bibliografia

➤ [**FOR07**] - [Comunicaciones y redes de computadores](https://github.com/mnomico/tyr/raw/main/libros/FOR07.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 12: “Multiple Access”

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 13: “Wired LANs: Ethernet”

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 14: “Wireless LANs”

[**KUR12**] - [Computer Networking: A Top-Down Approach](https://github.com/mnomico/tyr/raw/main/libros/KUR12.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Sección 5.4.3: "Link-Layer Switches"

➤ [**STA04**] - [Comunicaciones y redes de computadores](https://github.com/mnomico/tyr/raw/main/libros/STA04.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Sección 15.4: "Bridges"

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Sección 15.5: "Layer 2 and Layer 3 Switches"
