## [Volver atrás](../readme.md)

<div align="center">
<h1>Capa de Enlace</h1>
</div>

### Indice

💡 [Conceptos a tener en cuenta](#conceptos-a-tener-en-cuenta)

❓ [Guía de preguntas](#guia-de-preguntas)

✍️ [Ejercicios](#ejercicios)

📝 [Resumen](#resumen)

📖 [Bibliografía](#bibliografia)

---

### Conceptos a tener en cuenta

➤ Funciones de la capa de enlace

➤ Trama (Frame)

➤ Control de Flujo (S&W, Sliding Windows)

➤ Control de Errores (ARQ)

➤ Tasa de Error

➤ Tiempo de Trama

➤ Tiempo de Transmisión

➤ Eficiencia en enlace (U)

➤ Producto Retardo x Ancho de Banda

➤ Throughput

---

### Guia de preguntas

1. Describa las funciones del Nivel de Enlace ¿Qué similitudes y diferencias existen con las funciones propuestas por el Modelo OSI para la capa de transporte?

2. ¿Por qué es necesario contar con las funciones que provee la capa 2?

3. ¿Cuáles son las técnicas típicas para realizar dichas funciones? Compare cada una indicando ventajas y desventajas.

4. ¿Cuáles son los requisitos para una comunicación efectiva a nivel de enlace?

5. Describa la técnica de ventanas deslizantes para control de flujo. ¿En qué situaciones es altamente recomendable su uso? Justifique.

6. ¿Por qué los datos a enviar se dividen en tramas? ¿Qué estructura tienen?

7. ¿Por qué es necesaria la utilización del número de secuencia dentro de la estructura de la trama?

8. Explique el concepto de piggyback. ¿En qué casos se utilizaría y en cuáles no?

9. ¿Qué mecanismos se utilizan para la detección de errores? ¿Cuál es el fundamento del CRC? ¿Qué polinomio usa HDLC y qué prestaciones le brinda?

10. Realice un diagrama de tiempo para el intercambio de tramas entre dos equipos (A y B) utilizando un protocolo con ventana deslizante (con W = 5) para el control de flujo y un ARQ-adelante-atrás para control de errores. En el ejemplo, el equipo A debe enviar 6 tramas y el B solamente 3.

11. Indique y ejemplifique por qué hay que modificar el tamaño máximo de ventana cuando se utilizan ARQ-Adelante-Atrás-N y ARQ con Retransmisión Selectiva.

12. Se cuenta con un enlace digital para transmitir música por radio. ¿Qué técnica para tratar los errores es la más adecuada y por qué? 

    a) Ninguna técnica 

    b) Sólo detección de errores 

    c) Detección y recuperación (ARQ).

13. Describa brevemente las características del protocolo HDLC y cómo implementa las funciones de enlace.

14. ¿Qué significa que HDLC puede utilizar una configuración no-balanceada? Mencione un ejemplo propio donde se muestre dicha situación y justifique.

15. HDLC, ¿Es un protocolo orientado a la conexión ó no? ¿Con qué primitivas cuenta (según respuesta a la primera pregunta)?

16. ¿Cuáles son los 3 tipos de trama que define HDLC? ¿Para qué es cada una y durante qué etapa de la comunicación se utilizan?

17. ¿Qué configuración de HDLC utilizaría para un enlace satelital? Justifique.

18. Explique la técnica de bit stuffing y su uso ¿Cuál sería una alternativa?

19. ¿Qué es el throughput de un enlace? ¿De qué variables depende?

20. ¿Qué parámetros se consideran al evaluar la eficiencia de un protocolo de enlace?

---

### Ejercicios

1. ¿Cuál es el producto retardo x ancho de banda de un enlace de 256 Kbps y RTT = 30 ms? ¿Cómo se modifica si el RTT sube a 500 ms? ¿Cómo afecta al rendimiento de los protocolos?

2. Suponga que se requiere transmitir información desde un satélite de comunicaciones hasta una base en la luna (distancia 4 x 105 km). Para ello se tiene un canal de 1024 Kbps. Calcule el RTT del enlace y el producto retardo x ancho de banda. Y si quisiera transmitir desde una estación terrestre: ¿Qué valores toman tales parámetros? ¿Qué utilización (U) se obtendrían con un protocolo S&W y uno con SW (con W = 128)? Suponga tramas de 2000 bytes.

3. Un enlace de 50km de longitud y un ancho de banda de 1 Mbps se gestiona utilizando un protocolo con control de flujo por S&W. Calcule el tamaño de trama necesario para obtener la mayor utilización (U) si el retardo es de 50 ms.

4. Calcular el throughput para un enlace que utiliza un protocolo de ventana deslizante cuyo tamaño de trama es de 100 bytes y la ventana es 8. La tasa del enlace es de 1.45 Mbps y el RTT = 50 ms. ¿Cuál es el rendimiento (U) del enlace?

5. Un canal tiene una velocidad de transmisión de 4 Kbps y un retardo de 20 ms. ¿Para qué tamaño de trama se conseguirá un esquema de parada y espera con una eficiencia (U) del 50%?

6. Dos estaciones se comunican a través de un enlace de 1 Mbps con un retardo de propagación de 270 ms. Si se usan tramas HDLC de 1024 bits con números de secuencia de 3 bits ¿Cuál será el rendimiento máximo posible considerando sólo los datos transportados?

7. Analizar para qué tamaño de ventana resulta el throughput óptimo si se cuenta con un enlace de 512 Kbps y RTT = 500 ms y el tamaño de trama es de 800 bytes.

8. Calcule la utilización de un enlace de fibra óptica de 500 metros cuya tasa de transferencia es de 500 Mbps si se utiliza un protocolo con control de flujo mediante parada y espera cuyas tramas son de 1000 bytes. ¿Cómo se modifica la situación si se utilizan ventanas? ¿Qué tamaño de W brinda la mayor utilización?

9. ¿Qué ocurre en el caso anterior si se tiene una probabilidad P=0.2 de error y se utiliza ARQ con: 
    
    a) S&W

    b) retransmisión selectiva?

10. ¿Con qué parámetros se puede obtener una utilización superior al 50% para un enlace con tramas de 53 bytes, de 100 Kms y 30 Mbps si la probabilidad de error es P=0.35?

---

### Resumen

---

### Bibliografia

➤ [**STA04**] - [Comunicaciones y redes de computadores](https://github.com/mnomico/tyr/raw/main/libros/STA04.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 7: “Protocolos de control del enlace de datos”