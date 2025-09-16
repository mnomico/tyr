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
