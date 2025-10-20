## [Volver atrás](../readme.md)

<div align="center">
<h1>Conmutación, Capa de Red y Protocolo IPv4</h1>
</div>

### Indice

💡 [Conceptos a tener en cuenta](#conceptos-a-tener-en-cuenta)

❓ [Guía de preguntas](#lans---guia-de-preguntas)

📝 [Resumen](#resumen)

📖 [Bibliografía](#bibliografia)

---

### Conceptos a tener en cuenta

- Concepto sobre conmutación 
    - Circuitos	
    - Datagramas
    - Circuitos Virtuales
- Necesidad de una capa de red
- Funciones de la capa de red según el Modelo OSI
    - Cuestiones particulares de IP
- Protocolo IP
    - Características/Tipo de Servicio
    - Header
    - Esquema de direcciones
    - Fragmentación y ensamblado
    - Time-to-Live (TTL)
- Protocolo auxiliar ICMP
    - Ejemplos básicos

---

### Guia de Preguntas

1. Defina “conmutación” en el ámbito de una red de datos.
2. Compare los métodos de conmutación vistos.
3. ¿Cuál es la función de la capa de red?
4. ¿Cuál es la diferencia en el envío de mensajes (PDU) en capa 3 respecto de tramas en capa 2?
5. ¿Qué tipo de servicio ofrece el protocolo IP? ¿Es confiable? Justifique.
6. ¿La capa de red en Internet implementa control de congestión? Justifique.
7. En IPv4, ¿Qué es la fragmentación, por qué ocurre y cómo se realiza?
8. ¿Qué campos del header de IPv4 cambian su valor a medida que “pasan” de ruteador a ruteador?
9. A partir de las siguientes direcciones IP con máscara 255.255.255.224 indique dirección de red y host y dirección de broadcast de la subred.

    a. 10.1.1.216 

    b. 10.1.1.184 

    c. 201.202.203.204 

    d. 156.14.45.129

10. ¿Qué son los bloque de direcciones privadas? ¿Cuáles son?
11. Indicar cuáles direcciones pertenecen a las mismas redes usando las máscaras: 255.255.255.192 - 255.255.192.0 - 255.255.248.0

    140.128.200.1 , 150.128.30.3 , 140.128.200.255 , 140.129.250.1 , 140.128.190.221 , 140.128.30.30 , 140.128.120.120 , 140.128.60.1

12. Si se cuenta con la dirección 170.210.96.0/24, y 200 hosts separados en 3 redes, cual seria una máscara apropiada. Determine la asignación de IP para cada subred, indicando IP inicial y final, máscara y dirección de broadcast. Repita la operación de 4 y 7 redes.
13. Si se cuenta con la dirección 170.210.0.0/24 y 200 hosts separados en 3 redes, cual seria una máscara apropiada. Determine la asignación de IP para cada subred, indicando IP inicial y final, máscara y dirección de broadcast. Repita la operación de 4 y 7 redes.
14. ¿Para qué se utiliza el protocolo ARP? Capture datos de una red y muestre los mensajes correspondientes.
15. ¿Qué partes de un datagrama IP son controladas por el campo checksum?
16. ¿Cúal es la utilidad de la dirección de loopback?
17. ¿Cuál es la finalidad del protocolo ICMP y cómo se implementa?
18. ¿Qué información se obtiene con el comando ping? ¿Qué mensajes ICMP utiliza?

---

### Resumen

### 8 Switching

Una red es un conjunto de dispositivos conectados. Una red conmutada consiste de una serie de nodos entrelazados llamados **switches**. Los switches (o conmutadores) crean conexiones temporales entre dos o más dispositivos conectados al switch. 

Los tres métodos de conmutación más importantes son **conmutación de circuitos**, **conmutación de paquetes**, y **conmutación de mensajes**. Los primeros dos son usados actualmente, mientras que el último ya no se utiliza demasiado. Las redes actuales se pueden dividir en tres categorías: redes de conmutación de circuitos, redes de conmutación de paquetes, y redes de conmutación de mensajes. Las redes de conmutación de paquetes se pueden dividir en redes de circuitos virtuales y redes de datagramas.

<div align='center'>

![](./imagenes/05_taxonomia_conmutacion.png)

</div>

#### 8.1 Circuit-Switched Networks

Una red de conmutación de circuitos es una serie de switches conectados por enlaces físicos. La conexión entre dos estaciones es un camino dedicado formado por uno o más enlaces. Sin embargo cada conexión usa sólo un canal dedicado en cada enlace.

Los sistemas finales se conectan directamente a un switch. Cuando un sistema final A necesita comunicarse con un sistema final B, el A necesita enviar una solicitud de conexión a B que debe ser aceptada tanto por todos los switches como por B. Para esto se debe realizar primero la fase de establecimiento: se reserva un circuito (un canal) en cada enlace. Esta combinación de circuitos define el camino que va a usarse para la transferencia de datos. Una vez finalizada la transferencia, los circuitos se desarman.

La conmutación de circuitos tiene las siguientes características:
- La conmutación de circuitos se realiza en la capa física.
- Antes de comenzar la comunicación, se deben reservar los recursos que se van a utilizar. Estos recursos pueden ser canales (ancho de banda en FDM y ranuras de tiempo en TDM), buffers en switches, tiempo de procesamiento de los switches, y los puertos de entrada/salida de los switches, que deben mantenerse exclusivamente dedicados a la transferencia de datos hasta la fase de desarmado.
- Los datos que se transfieren entre las estaciones no se empaquetan, es decir que los datos son un flujo continuo enviados desde la estación origen y recibidos por la estación destino.
- No hay direccionamiento durante la transferencia de datos, solamente para la fase de establecimiento de la conexión.

La comunicación en una red de conmutación de circuitos requiere tres fases: **fase de establecimiento de conexión**, **fase de transferencia de datos**, y **fase de desarmado de conexión**.

**Fase de establecimiento de conexión**

Para que dos o más entidades se puedan comunicar, se debe establecer un circuito dedicado. Los sistemas finales normalmente están conectados por líneas dedicadas a los switches, entonces la fase de establecimiento significa crear canales dedicados entre los switches.

<div align='center'>

![](./imagenes/05_ej_conmutacion_circuitos.png)

</div>

Cuando el sistema A necesita conectarse al sistema M, envía al switch I una solicitud de establecimiento que incluye la dirección del sistema M. El switch I encuentra un canal entre si mismo y el switch IV, entonces el switch I envía la solicitud al switch IV, y este encuentraun canal dedicado entre si mismo y el switch III. El switch III le entrega la solicitud al sistema M.

El sistema M envía una confirmación al sistema A mediante el mismo camino de manera inversa.

**Fase de transferencia de datos**

Luego de establecer el circuito dedicado, las dos entidades pueden transferir datos.

**Fase de desarmado de conexión**

Cuando una de las entidades solicite el fin de la conexión, se envía una señal a cada switch para que libere sus recursos.

En cuanto a **eficiencia**, las redes de conmutación de circuitos no son tan eficientes como los otros dos tipos de redes porque los recursos se asignan durante toda la conexión, y estos recursos no se pueden utilizar para otras conexiones.

Si bien las redes de conmutación de circuitos tienen baja eficiencia, el **delay** en este tipo de redes es mínimo. Gracias a que los recursos para la conexión son dedicados, el flujo de datos es continuo, por lo tanto no hay tiempos de espera en los switches. El único delay que ocurre es durante el establecimiento de la conexión, la transferencia de datos, y el desarmado del circuito.

#### 8.2 Datagram Networks

En las comunicaciones de datos, se necesita enviar mensajes de un sistema final a otro. Si un mensaje pasa por una red de conmutación de paquetes, necesita ser dividido en paquetes.

En la conmutación de paquetes, no se reservan recursos. Los recursos se asignan bajo demanda. La asignación se hace de manera FCFS (First Come, First Served). Cuando un switch recibe un paquete, el paquete debe esperar si hay otros paquetes siendo procesados. 

En una red de datagramas, cada paquete se trata independientemente del resto. En estos casos, los paquetes son llamados **datagramas**.

A comparación de la conmutación de circuitos, que se realiza en la capa física, la conmutación de datagramas se realiza en la capa de red.

<div align='center'>

![](./imagenes/05_ej_conmutacion_datagramas.png)

</div>

En este ejemplo, los cuatro datagramas pertenecen al mismo mensaje, pero pueden viajar por diferentes caminos para llegar al destino. Debido a esto, los datagramas pueden llegar al destino desordenados. También se pueden perder los paquetes o pueden ser descartados debido a la falta de recursos. La responsabilidad de solicitar la retransmisión de paquetes o de reordenarlos recae en un protocolo de capa superior.

Las redes de datagramas a veces se las conoce como redes sin conexión, es decir que el switch no almacena información sobre el estado de la conexión, no hay fases de establecimiento o desarmado. Cada paquete se trata igual sin importar su origen o destino.

Para que los paquetes puedan llegar a destino en una red de datagramas, se utilizan las **tablas de ruteo**. Cada switch contiene una tabla de ruteo, basadas en direcciones de destino. Las tablas de ruteo son dinámicas y se actualizan periódicamente. Las direcciones de destino y los puertos de salida correspondientes se almacenan en las tablas.

<div align='center'>

![](./imagenes/05_tabla_ruteo.png)

</div>

Cada paquete en una red de datagramas tiene un encabezado con la dirección de destino del paquete. Cuando el switch recibe el paquete, examina la dirección de destino y consulta la tabla de ruteo para encontrar el puerto por el cual debe reenviar el paquete.

En cuanto a **eficiencia**, la red de datagramas es más eficiente que una red de conmutación de circuitos, ya que los recursos son asignados solamente cuando se necesita transferir paquetes.

Pueden existir **delays** más grandes en una red de datagramas. Si bien no hay fases de establecimiento o desarmado, cada paquete puede tener que esperar en un switch antes de ser reenviado. Además, como cada paquete puede viajar por medio de diferentes switches, el delay entre los paquetes puede ser muy diferente.

### 20 Network Layer: Internet Protocol

En Internet, el protocolo de red principal es el **Internet Protocol (IP)**. 

#### 20.1 Internetworking

Para poder solucionar el problema de enviar por varios enlaces, se diseñó la capa de red. La capa de red es responsable de la entrega host a host y para rutear (o encaminar) los paquetes por los routers o switches.

<div align='center'>

![](./imagenes/05_capa_de_red.png)

</div>

La capa de red en el origen es responsable de crear un paquete de los datos que provienen de otro protocolo (como el protocolo de capa de transporte). El encabezado del paquete contiene las direcciones lógicas de origen y de destino. La capa de red es responsable de verificar su tabla de ruteo para encontrar información sobre el ruteo, como la interaz por la que debe salir el paquete o la dirección física del siguiente nodo. Si el paquete es muy grande, se fragmenta.

La capa de red en el switch o router es responsable de rutear el paquete. Cuando llega un paquete, el router o switch consulta su tabla de ruteo y encuentra la interfaz por la cual debe enviar el paquete. El paquete, luego de sufrir algunos cambios en su encabezado, se pasa nuevamente a la capa de enlace.

La capa de red en el destino es responsable de verificar direcciones, es decir que se asegura que la dirección destino en el paquete es la misma que la dirección del host. Si el paquete es un fragmento, la capa de red espera hasta que lleguen todos los fragmentos, y luego los reensambla y pasa a la capa de transporte.

<div align='center'>

![](./imagenes/05_capa_de_red_2.png)

</div>

El Internet, en la capa de red, es una red de conmutación de paquetes. Se eligió la conmutación de datagramas para la capa de red. Utiliza direcciones universales que se definen en la capa de red para rutear paquetes desde un origen hacia un destino.

La entrega de un paquete se puede lograr utilizando un servicio de red **orientado a la conexión** o **no orientado a la conexión**. En un servicio orientado a la conexión, el origen primero establece una conexión con el destino antes de enviar un paquete. Cuando se establece la conexión, una secuencia de paquetes del mismo origen hacia el mismo destino pueden ser enviados uno tras otro. Cuando todos los paquetes de un mensaje se entregaron, se termina la conexión.

En un protocolo orientado a la conexión, la decisión sobre la ruta de una secuencia de paquetes con el mismo origen y destino sólo se puede hacer una vez, cuando se establece la conexión. Los switches no recalculan la ruta de cada paquete. 

En un servicio no orientado a la conexión, el protocolo de capa de red trata cada paquete independientemente. Los paquetes en un mensaje pueden o no viajar por el mismo camino hacia su destino. Este tipo de servicio se utiliza en las redes de datagramas, y es el que utiliza el Internet.

La razón de esto es que el Internet está formado de varias redes heterogéneas, haciendo imposible la conexión desde un destino hacia un origen sin saber la naturaleza de las redes de antemano.

#### 20.2 IPv4




---

### Bibliografia

➤ [**FOR07**] - [Data Communications and Networking](https://github.com/mnomico/tyr/raw/main/libros/FOR07.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 8: “Switching” (hasta 8.3)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 20: “Network Layer:
Internet Protocol” (hasta 20.2 inclusive)

➤ [**STE11**] - [TCP/IP Illustrated Vol I](https://github.com/mnomico/tyr/raw/main/libros/STE11.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 2: “The Internet Address Architecture” (hasta 2.3)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 5: “The Internet Protocol (IP)” (hasta 5.3)