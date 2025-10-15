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

---

### Bibliografia

➤ [**FOR07**] - [Data Communications and Networking](https://github.com/mnomico/tyr/raw/main/libros/FOR07.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 8: “Switching” (hasta 8.3)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 20: “Network Layer:
Internet Protocol” (hasta 20.2 inclusive)

➤ [**STE11**] - [TCP/IP Illustrated Vol I](https://github.com/mnomico/tyr/raw/main/libros/STE11.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 2: “The Internet Address Architecture” (hasta 2.3)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 5: “The Internet Protocol (IP)” (hasta 5.3)