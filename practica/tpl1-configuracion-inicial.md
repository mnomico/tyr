## [Volver atrás](../readme.md)

<div align="center">
<h1>TPL 1 - Configuración inicial de la red del laboratorio</h1>
</div>

### Segunda parte: Configuración de hosts en una red - prueba de conectividad - análisis de captura

**Consignas**

Los comandos necesarios para llevar adelante la práctica se encuentran listados en el apunte respectivo de la asignatura, disponible en la web de la misma. En todos los casos, el informe a entregar debe mostrar los comandos ejecutados y las salidas obtenidas (en caso de ser una salida extensa, resaltar la parte importante). Además, se debe explicar lo que se interpreta de dicha salida y si es lo esperado en cada caso.

1. Verificar la/s interfaces de red (comúnmente llamada placa de red o NIC) que el sistema operativo haya detectado en pc1 y pc2, y listar su información en pantalla.

    ¿Que comando utilizó? ¿Cual es el nombre de las interfaces? ¿Que parte de la salida le indicó cual es la interfaz que se encuentra conectada? ¿Cual es el nombre de la interfaz que se encuentra conectada a la red?

```
root@pc1:/# ip link show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
5: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 1e:72:ca:9b:4a:44 brd ff:ff:ff:ff:ff:ff
```

Se utilizó el comando **ip link show** para identificar las interfaces de red. Los nombres de las interfaces son ```lo``` y ```eth0```. La parte de la salida que indica cuál es la interfaz que se encuentra conectada es el valor de ```state```, que en el caso de ```eth0``` es ```UP``` (activa), mientras que en el caso de ```lo``` es ```UNKNOWN``` (desconocida).

```
root@pc2:/# ip link show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
4: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 3a:b4:85:44:f1:71 brd ff:ff:ff:ff:ff:ff
```

Lo anterior aplica también en ```pc2```.

2. Configuración de interfaces de red para utilizar el protocolo TCP/IP. El paso siguiente es asignar las direcciones IP 10.4.11.11 y 10.4.11.12 a pc1 y pc2 respectivamente (la máscara de red es /24 o 255.255.255.0).

3. Verificar que es posible contactar ambos equipos de la red.

4. Cambiar la configuración de los nombres de los equipos asignandoles tyr11 y tyr12 a pc1 y pc2 respectivamente.

5. Resolución de nombres de hosts a direcciones IP.

    a. Configurar la resolución de nombres locales en ambos host con la información contenida en el punto 4.

    b. Verificar que es posible contactar ambos equipos de la red utilizando nombres de host.

6. Ver la tabla de ruteo definida en el equipo. ¿Cuáles son las redes accesibles?

7. Agregar la dirección 10.4.11.30 como ruta por defecto para acceder a otras redes. Verificar nuevamente la tabla de ruteo.

8. Realizar una captura de las PDU intercambiadas mientras se utiliza el comando ping para verificar conectividad con el otro equipo. Las acciones que debe realizar son:

    a. En el dispositivo capturador inicie la captura utilizando el comando tcpdump o tshark sobre la interfaz eth0 y redirigir la salida a un archivo en el directorio /shared para su posterior análisis.

    b. En pc1 ejecutar el comando ping para enviar a pc2 exactamente 3 mensajes ICMP Echo Request (consulte el manual de ping).

    c. Una vez obtenida la respuesta del comando ping (deberán recibirse tres respuestas), detener la captura (finalizar el proceso tcpdump o tshark presionando Ctrl+C)

    d. Analizar el volcado del programa de captura utilizando la aplicación wireshark (o cualquier otro analizador de tráfico que permita leer archivos en formato pcap), representando en un gráfico ideado por usted el intercambio de mensajes. Indicar cuál es la función de cada uno identificando los datos de encabezados mas relevantes.

9. Escribir los comandos de configuración que ejecutó en los puntos 2, 4, 5 y 7 en pc1 y pc2 a los archivos pc1.startup y pc2.startup respectivamente, que están dentro del directorio del laboratorio, de manera tal que los nodos se configuren automáticamente al reiniciar el laboratorio.