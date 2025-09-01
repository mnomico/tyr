## [Volver atrás](../readme.md)

<div align="center">
<h1>TPL 3 - Domain Name System</h1>
</div>

### Indice

✍️ [Consignas](#consignas)

❓ [Guía de preguntas](#guia-de-preguntas)

📝 [Resumen](#resumen)

📖 [Bibliografía](#bibliografia)

---

### Consignas

1. Utilizando la herramienta dig (o nslookup ) realice consultas al servidor DNS indicado por el docente, (o desde su hogar al provisto por su ISP, o bien alguno de acceso público tal como 8.8.8.8 o 1.1.1.1) para obtener la siguiente información:
    
    a. ¿Cuál es la dirección IP del host platdig.unlu.edu.ar ?

    b. ¿Cuál es la dirección IP del host educativa.unlu.edu.ar ? ¿Qué diferencia nota en la respuesta respecto al punto anterior?

    c. ¿Cuáles son los intercambiadores de mail (mnemónico y dirección IP) del dominio unsa.edu.ar ?

    d. ¿Cuál es el nombre del host cuya dirección IP es 190.104.80.12 ?

    e. ¿Cuáles son los servidores de nombres (mnemónicos y dirección IP) para el dominio ripe.net ?

    f. ¿Cuál es la dirección IPv6 del host debian.org ?

2. Utilice la herramienta DNS BAJAJ disponible en http://www.zonecut.net/dns/ para obtener información en forma de grafo acerca del dominio cruzroja.org.ar . ¿Cuáles son los servidores (nombre y dirección IP) para dicho dominio?

3. ¿En dónde se encuentra la copia mas cercana de un servidor dns raíz? ¿Cuál es el nombre del servidor replicado (o servidores)?
4. Defina cómo estará compuesta la base de datos de un servidor DNS administrado por Ud., de manera tal que sea el servidor primario del dominio SU-NRO-LEGAJO.tyr.example ( .example es un TLD reservado para uso en documentación y ejemplos). De acuerdo al diagrama de la Figura 1, defina:

    a. El nombre de todos los hosts en el nuevo dominio, y su respectivo puntero reverso.

    b. Los hosts pc1 y ns1 como name servers del dominio.

    c. www.SU-NRO-LEGAJO.tyr.example y ftp.SU-NRO-LEGAJO.tyr.example como alias de server1.
    
    Complete la planilla adjunta a partir de las definiciones previas.

<div align='center'>

![](./archivos/tpl3.4.png)

Figura 1: Host en la red a definir en DNS

</div>

5. Instale e inicie en el entorno kathara el laboratorio de dns provisto por los docentes disponible en https://github.com/redesunlu/kathara-labs/blob/main/tarballs/kathara-lab_dns.tar.gz y realice las siguientes actividades:

    a. En el dispositivo capturador inicie la captura utilizando el comando tcpdump o tshark sobre la interfaz eth0 y redirigir la salida a un archivo en el directorio /shared para su posterior análisis. (Ej. “tshark -i eth0 -w - > /shared/captura_dns.pcap”)

    b. Desde pc1.lugroma3.org, ejecute el comando ping -c 4 pc2.nanoinside.net

    c. Una vez recibidas las 4 respuestas ICMP, detenga la captura.

    d. Analice la captura y describa cómo es el proceso de resolución de nombres para determinar la dirección ip de pc2.nanoinside.net, representando gráficamente el intercambio de mensajes dns, e indicando el propósito de cada uno.

    e. Identifique el host que realiza una consulta recursiva y cuál consultas iterarivas.

6. Analice la captura captura_ejemplo_dns.pcap y represente el intercambio de mensajes. ¿Puede indicar alguna particularidad que observe en la misma?

7. ¿Cómo un desarrollador de aplicaciones puede acceder al servicio DNS? (Por ej. si es necesario resolver, en una aplicación de software, mnemónicos a direcciones IP o viceversa)

---

### Guia de preguntas

¿Cuál es el objetivo del sistema DNS?

¿Porqué es un sistema y no solamente un protocolo? Descríbalo indicando estructura, elementos que intervienen y tipos de datos (Resource Records) típicos que se pueden consultar.

El protocolo DNS puede utilizar como protocolo de transporte tanto UDP como TCP. ¿En qué casos se utiliza cada uno y cuál es la razón?

¿Quién tiene a su cargo la administración de los nombres de dominio bajo el dominio .ar ? ¿Qué y cuáles son las zonas especiales? ¿Qué requisito especial se requiere para solicitar un dominio .org.ar ?

---

### Resumen

#### 25.0 Domain Name System

Hay varias aplicaciones en la capa de aplicación que siguen el paradigma cliente/servidor. Los programas cliente/servidor se pueden dividir en dos categorías: los que pueder ser usados directamente por el usuario, y los que dan soporte a otros programas de aplicación. El Domain Name System (DNS) es un programa de soporte que es usado por otros programas, como el e-mail.

<div align='center'>

![](./archivos/tpl3/25_ejemplo_dns.png)

</div>

La imagen anterior muestra como un programa cliente/servidor DNS puede dar soporte a un programa de correo para encontrar la dirección IP de un receptor. Un usuario de un programa de correo puede saber la dirección de correo del receptor, pero el protocolo IP necesita la dirección IP. El cliente DNS envía una solicitud a un servidor DNS para encontrar la dirección IP correspondiente a esa dirección de correo.

Para identificar una identidad, los protocolos TCP/IP usan la dirección IP. Pero las personas prefieren usar nombres en lugar de direcciones numéricas, entonces se necesita un sistema que pueda mapear un nombre a una dirección o viceversa.

Con el tiempo fueron surgiendo varias soluciones, pero la que se utiliza hoy en día es dividir la enorme cantidad de información en partes más pequeñas y almacenar cada parte en una computadora diferente. El host que necesita encontrar una dirección se puede contactar con la computadora más cercana que contiene la información necesaria. Este método es el que utiliza el **Domain Name Service (DNS)**.

#### 25.1 Espacio de nombres

Para no ser ambiguos, los nombres asignados a las máquinas deben ser seleccionados con cuidado a partir de un espacio de nombres con control total sobre la asociación de nombres y direcciones IP. En otras palabras, los nombres deben ser únicos porque las direcciones son únicas. Un espacio de nombres que mapea cada dirección a un nombre único puede ser organizado de dos maneras: plana o jerárquica.

**Espacio de nombres plano**

En un espacio de nombres plano, un nombre se asigna a una dirección. Un nombre en este espacio es una secuencia de caracteres sin estructura. Los nombres pueden o no tener una sección en común, y si la tienen, no tiene significado. La principal desventaja de un espacio de nombres plano es que no puede ser usado en un sistema grande como el Internet porque debe ser controlado de manera centralizada para evitar la ambiguedad y duplicación.

**Espacio de nombres jerárquico**

En un espacio de nombres jerárquico, cada nombre se compone de varias partes. La primera parte puede definir la naturaleza de una organización, la segunda parte puede definir el nombre de una organización, la tercera puede definir departamentos dentro de la organización, etc. 

La autoridad que asigna y controla el espacio de nombres puede ser descentralizada. Una autoridad central puede asignar la parte del nombre que define la naturaleza de la organización y el nombre de la organización, mientras que se puede dar la responsabilidad sobre el resto del nombre a la organización misma. La organización puede agregar sufijos o prefijos al nombre que define su host o sus recursos. 

#### 25.2 Espacio de nombres de dominio

El espacio de nombres es un espacio de nombres jerárquico. Para lograr esto, se diseñó un **espacio de nombres de dominio**. Los nombres se definen con una estructura de árbol invertida con una raíz en la parte superior. El árbol solo puede tener 128 niveles, del nivel 0 (raíz) al nivel 127.

<div align='center'>

![](./archivos/tpl3/25_espacio_de_nombres.png)

</div>

**Etiqueta**

Cada nodo en el árbol tiene una etiqueta, una cadena de caracteres con un tamaño de 63 caracteres como máximo. El nodo raíz es una cadena vacía. 

**Nombres de dominio**

Cada nodo en el árbol tiene un nombre de dominio. Un **nombre de dominio** completo es una secuencia de etiquetas separadas por puntos. La última etiqueta es la etiqueta raíz (nulo). 

<div align='center'>

![](./archivos/tpl3/25_nombres_y_etiquetas.png)

</div>

Si la etiqueta finaliza con una cadena nula, entonces el nombre de dominio se denomina **nombre de dominio completamente cualificado (FQDN)**. Un FQDN es un nombre de dominio que contiene el nombre completo de una estación. Contiene todas las etiquetas que definen únicamente el nombre del host. Por ejemplo, el nombre de dominio ```challenger.atc.fhda.edu.``` es el FQDN de una computadora llamada ```challenger``` instalada en el Centro de Tecnología Avanzada (Advanced Technology Center) en De Anza College. Un servidor DNS solo puede unir un FQDN a una dirección.


Si la etiqueta no finaliza con una cadena nula, entonces se tiene un **nombre de dominio parcialmente cualificado (PQDN)**. Un PQDN empieza desde un nodo, pero no llega a la raíz. Se usa cuando el nombre a resolver pertenece al mismo sitio que el cliente. En este caso el resolver puede brindar la parte faltante, llamada sufijo, para crear un FQDN. Por ejemplo, si un usuario en el sitio de ```fhda.edu.``` necesita la dirección IP de la computadora challenger, el usuario puede definir el nombre parcial ```challenger```. El cliente DNS agrega el sufijo ```atc.fhda.edu.``` antes de pasarle la dirección al servidor DNS.

**Dominio**

Un **dominio** es un subárbol del espacio de nombres de dominio. El nombre del dominio es el nombre del dominio del nodo que se encuentra en la parte superior del subárbol. Acá se pueden ver un par de ejemplos:

<div align='center'>

![](./archivos/tpl3/25_dominios.png)

</div>

#### 25.3 Distribución del espacio de nombres

La información contenida en un espacio de nombres de dominio debe ser almacenada, pero es muy ineficiente almacenar tanta información en una sola computadora, debido al tráfico que ocasiona la multitud de solicitudes que puede recibir dicha computadora. Tampoco es fiable porque cualquier fallo puede hacer que la información quede inaccesible.

**Jerarquía de servidores de nombre**



---

### Bibliografia

➤ [**FOR07**] - [Data Communications and Networking](https://github.com/mnomico/tyr/raw/main/libros/FOR07.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 25: “Domain Name System”

</div>