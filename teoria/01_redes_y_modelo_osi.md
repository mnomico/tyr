## [Volver atrás](../readme.md)

<div align="center">
<h1>Introducción, Redes y Modelo OSI</h1>
</div>

### Indice

❓ [Guía de preguntas](#guia-de-preguntas)

📖 [Bibliografía](#bibliografia)

---

### Guia de preguntas

1. **¿Qué es una red de datos y cuáles son sus objetivos y características principales?**

    Una red es un conjunto de dispositivos autónomos interconectados, permanentemente o no, que tienen por objetivo compartir recursos y permitir la comunicación.

    Otra definición, que se encuentra en STA04 Capítulo 16.4:

    Una red es un conjunto de puntos de acceso interconectados con una estructura software de
    protocolos que posibilita la comunicación.

    Sus características principales son:
    - **Fiabilidad**: los datos transmitidos deben llegar al destino, y además deben llegar en el orden en el que fueron enviados.


2. **¿Qué es un enlace? Brinde ejemplos.**

    Un enlace es el medio de comunicación físico por el cual dos dispositivos conectados entre sí se comunican simultáneamente y transfieren datos.

3. **¿Qué es un protocolo de comunicaciones y qué define?**

    Una arquitectura de protocolos es una estructura en capas de elementos hardware y software que facilita el intercambio de datos entre sistemas y posibilita aplicaciones distribuidas, como el comercio electrónico y la transferencia de archivos.

    En los sistemas de comunicación, en cada una de las capas de la arquitectura de protocolos se implementa uno o más protocolos comunes. Cada protocolo proporciona un conjunto de reglas para el intercambio de datos entre sistemas.

    La comunicación se consigue haciendo que las capas correspondientes, o pares, intercambien información. Las capas pares se comunican intercambiando bloques de datos que verifican una serie de reglas o convenciones denominadas **protocolo**. Los aspectos clave que definen o caracterizan a un protocolo son:

    - La **sintaxis**: establece cuestiones relacionadas con el formato de los bloques de datos.
    - La **semántica**: incluye información de control para la coordinación y la gestión de errores.
    - La **temporización**: considera aspectos relativos a la sintonización de velocidades y secuenciación.

4. **¿Cuáles son los “Tipos de Servicio” ofrecidos por los protocolos? ¿En qué se diferencian?**

    Si el que inicia la transferencia recibe una confirmación de que el servicio solicitado ha tenido el efecto deseado en el otro extremo, esta secuencia de eventos se conoce como **servicio confirmado**. Si solamente se invocan las primitivas de solicitud e indicación, entonces se denomina **servicio no confirmado**: la entidad que inicia la transferencia no recibe confirmación de que la acción solicitada haya tenido lugar.

    En la capa de transporte se especifican dos protocolos, el **orientado a conexión**, TCP (Protocolo de Control de la Transmisión, Transmission Control Protocol) y el **no orientado a conexión** UDP (Protocolo de Datagrama de Usuario, User Datagram Protocol).

    TCP proporciona una conexión fiable para transferir los datos entre las aplicaciones, mientras que UDP no garantiza la entrega, la conservación del orden secuencial, ni la protección frente duplicado, pero posibilita el envío de mensajes entre aplicaciones con la complejidad mínima.

    La capa de sesión proporciona los siguientes servicios:
    - **Control del diálogo**: éste puede ser simultáneo en los dos sentidos (full-duplex) o alternado en ambos sentidos (half-duplex).
    - **Agrupamiento**: el flujo de datos se puede marcar para definir grupos de datos. 
    - **Recuperación**: la capa de sesión puede proporcionar un procedimiento de puntos de comprobación, de forma que si ocurre algún tipo de fallo entre puntos de comprobación, la entidad de sesión puede retransmitir todos los datos desde el último punto de comprobación.

5. **¿Qué es el modelo de referencia OSI y qué define?**

    El modelo **OSI** (Open System Interconnection) es un modelo de referencia que fue desarrollado para la normalización, es decir permitir la comunicación entre sistemas distintos sin que sea necesario cambiar el hardware o el software.

    Dentro del modelo, en cada capa se pueden desarrollar uno o más protocolos. El modelo define en términos generales las funciones que se deben realizar en cada capa.

6. **Enuncie ventajas y desventajas del modelo OSI.**

    Simplifica el procedimiento de la normalización ya que:
    - Como las funciones de cada capa están bien definidas, para cada una de ellas, el establecimiento de normas o estándares se puede desarrollar independiente y simultáneamente. Esto acelera el proceso de normalización.
    - Como los límites entre capas están bien definidos, los cambios que se realicen en los estándares para una capa dada no afectan al software de las otras. Esto hace que sea más fácil introducir nuevas normalizaciones.

7. **Indique la función de cada capa del modelo OSI.**

    - **Capa de aplicación**: proporciona el acceso al entorno OSI para los usuarios y, también, proporciona servicios de información distribuida.
    - **Capa de presentación**: proporciona a los procesos de aplicación independencia respecto a las diferencias en la representación de los datos (sintaxis).
    - **Capa de sesión**: proporciona el control de la comunicación entre las aplicaciones; establece, gestiona y cierra las conexiones (sesiones) entre las aplicaciones cooperadoras.
    - **Capa de transporte**: proporciona una transferencia transparente y fiable de datos entre los puntos finales; además, proporciona procedimientos de recuperación de errores y control de flujo origen-destino.
    - **Capa de red**: proporciona independencia a los niveles superiores respecto a las técnicas de comunicación y de transmisión utilizadas para conectar los sistemas; es responsable del establecimiento, mantenimiento y cierre de las conexiones.
    - **Capa de enlace**: proporciona un servicio de transferencia de datos fiable a través del enlace físico; envía bloques de datos (tramas) llevando a cabo la sincronización, el control de errores y el flujo.
    - **Capa física**: se encarga de la transmisión de cadenas de bits no estructurados sobre el medio físico; está relacionada con las características mecánicas, eléctricas, funcionales y de procedimiento para acceder al medio físico.

8. ¿Qué capa define la “red”?

9. ¿Cuántos protocolos hay en la capa de aplicación de una pila? ¿Y en la de transporte? ¿Y en la de red? Justifique en cada caso.

10. **¿Qué es una PDU? Brinde un ejemplo.**

    La unión de los datos generados por la capa superior, junto con la información de control de la capa actual, se denomina unidad de datos del protocolo (**PDU**, Protocol Data Unit). 

    **PDU de transporte**

    La cabecera en cada PDU de transporte contiene información de control que será usada por el protocolo de transporte en la computadora destino. La información que se debe incluir en la cabecera puede ser, por ejemplo:
    - **SAP destino**: cuando la capa de transporte destino recibe la PDU de transporte, deberá saber a quién van destinados los datos.
    - **Número de secuencia**: ya que el protocolo de transporte está enviando una secuencia de PDUs, éstas se numerarán secuencialmente para que, si llegan desordenadas, la capa de transporte destino sea capaz de ordenarlas.
    - **Código de detección de error**: la capa de transporte emisora debe incluir un código obtenido en función del resto de la PDU. El protocolo de transporte receptor realiza el mismo cálculo y compara los resultados con el código recibido. Si hay discrepancia se concluye que hubo un error en la transmisión, el receptor puede descartar la PDU y tomar las acciones necesarias para su corrección.

    **PDU de red**

    El protocolo de acceso a la red añade la cabecera de acceso a la red a los datos provenientes de la capa de transporte, creando así la PDU de acceso a la red. La cabecera debe contener la siguiente información:
    - **La dirección del destino**: la red debe conocer a quién debe entregar los datos.
    - **Solicitud de recursos**: el protocolo de acceso a la red puede pedir a la red que realice algunas funciones, como por ejemplo, gestionar prioridades.

11. **Explique qué se define con el término “Encapsulamiento”.**

    Prácticamente en todos los protocolos, los datos son transferidos en PDUs. Cada PDU contiene no solo datos, sino también información de control.

    La adición de información de control a los datos es lo que se conoce como **encapsulamiento**. Los datos son aceptados o generados por una entidad y encapsulados dentro de una PDU que contiene los datos más información de control.

12. **Defina SAP, SDU e ICI en el contexto del Modelo OSI (y la función de encapsulamiento)**

    <div align="center">

    ![01_sap.png](/teoria/imagenes/01_sap.png)

    </div>

    **SAP** (Service Access Point) es una dirección única dentro de una computadora, que permite a la capa de transporte proporcionar los datos a la aplicación apropiada. También se los conoce como **puertos**.

13. Indique similitudes y diferencias entre el Modelo OSI y la pila de protocolos TCP/IP.

14. En el contexto del modelo OSI ¿Qué es un “Sistema Intermedio” y “Sistema Final”? ¿Cuáles son los equivalentes en el contexto de TCP/IP?

    Un **sistema final** es un sistema el cual transmite o recibe paquetes de datos. Un encaminador, procesador que conecta dos redes y cuya función principal es retransmitir datos desde una red a otra siguiendo la ruta adecuada para alcanzar al destino, es un **sistema intermedio**.

15. A partir de la lectura de la “Breve Historia de Internet”

    a. ¿Qué es justamente “Internet”?

    b. ¿En qué desarrollo se basa?

    c. ¿Qué reglas plantearon para las redes?

    d. ¿Qué problemas debían resolver? Relacione cada uno con la capa del Modelo OSI adecuada para resolverlo.

---

### Bibliografia

<div>

➤ [**STA04**] - [Comunicaciones y redes de computadores](https://github.com/mnomico/tyr/raw/main/libros/STA04.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 1: “Introducción”<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 2: “Protocolos y Arquitectura”

</div>


➤ [**Online**] - [Breve historia de Internet](https://www.internetsociety.org/es/internet/history-internet/brief-history-internet/)

