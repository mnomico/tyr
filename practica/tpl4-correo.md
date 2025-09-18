## [Volver atrás](../readme.md)

<div align="center">
<h1>TPL 4 - Correo Electrónico SMTP - POP3 - IMAP4 - MIME</h1>
</div>

### Indice

✍️ [Consignas](#consignas)

❓ [Guía de preguntas](#guia-de-preguntas)

📝 [Resumen](#resumen)

📖 [Bibliografía](#bibliografia)

---

### Consignas

1. Un usuario redacta un mensaje destinado a consultas@empresax.example.com en su cliente de correo y lo envía mediante su propio MTA. Detalle paso a paso el procedimiento que debe seguir el MTA del usuario para entregar el mensaje al destinatario.

    Cuando el usuario desea enviar un mensaje, ejecuta un programa ```user agent``` para preparar el mensaje. El mensaje contiene las direcciones de correo del emisor y del receptor. Para poder enviar el mensaje, se debe enviar por Internet: el ```MTA``` del cliente debe establecer una conexión con el ```MTA``` del servidor para transmitir el mail. 

    Para que el MTA cliente pueda establecer una conexión con el MTA servidor, primero necesita saber su dirección IP. A partir de la dirección de mail destino, extrae el dominio, en este caso ```empresax.example.com``` y le solicita al resolver DNS que obtenga los registros ```MX``` de ese dominio. Luego de obtener la dirección IP, establece una conexión TCP con el MTA servidor, y utilizan el protocolo ```Simple Mail Transfer Protocol (SMTP)``` para la transferencia del mensaje. 
    
    Para establecer la conexión SMTP, el servidor envía el código 220 (service ready) para decirle al cliente que está listo para recibir mails. Luego el MTA cliente envía el mensaje ```HELO``` para identificarse usando su nombre de dominio. El servidor responde con el código 250 (request command completed) o con otro código dependiendo de la situación.

    Luego de que la conexión se estableció entre el cliente y servidor SMTP, se pueden intercambiar mensajes. El cliente envía el mensaje ```MAIL FROM``` para enviar la dirección de mail del emisor. El servidor responde con el código 250. El cliente envía el mensaje ```RCPT TO``` para enviar la dirección de mail del destinatario. El servidor responde con el código 250. El cliente envía el mensaje ```DATA``` para iniciar la transferencia del mensaje. El servidor responde con el código 354 (start mail input). El cliente envía el contenido del mensaje, el cual se termina con una línea que contiene sólamente un punto. El servidor responde con el código 250.

    Una vez transferido el mensaje, el cliente termina la conexión mediante el envío del mensaje ```QUIT``` al cual el servidor responderá con el código 221 (service closed). Por último, se debe cerrar la conexión TCP.

2. Comente los problemas que plantea el uso de SMTP en cuanto a que el protocolo no requiere obligatoriamente la autenticación por parte del usuario que envía correo y el abuso que esto puede acarrear.

    Los problemas que pueden ocurrir por la ausencia de autenticación en SMTP pueden ser los siguientes:
    - Cualquier persona puede enviar un mensaje haciéndose pasar por otra persona, permitiendo ataques de phishing.
    - Mediante el uso de servidores SMTP abiertos se pueden enviar mensajes spam de manera masiva.

3. Instale e inicie en el entorno kathará el laboratorio de email provisto por los docentes, disponible en https://github.com/redesunlu/kathara-labs/blob/main/tarballs/kathara-lab_email.tar.gz y realice las siguientes actividades:

    1. En el dispositivo capturador inicie la captura utilizando el comando tcpdump o tshark sobre la interfaz eth0 y redirija la salida a un archivo en el directorio /shared para su posterior análisis. (Ej. “tshark -i eth0 -w - > /shared/captura_email.pcap”)

    2. Desde la pc1, utilizando nc , conéctese al servidor SMTP mail.lugroma3.org (TCP puerto 25) y envíe un mensaje cuyo remitente sea <su-nombre@lugroma3.org> destinado a la cuenta de correo <guest@nanoinside.net> .

            root@pc1:/# nc mail.lugroma3.org 25
            220 dnslug ESMTP Exim 4.96 Thu, 18 Sep 2025 15:06:49 +0000
            HELO pc1.lugroma3.org
            250 dnslug Hello pc1.lugroma3.org [192.168.0.111]
            MAIL FROM:<mateonomico@lugroma3.org>
            250 OK
            RCPT TO:<guest@nanoinside.net>
            250 Accepted
            DATA
            354 Enter message, ending with "." on a line by itself
            Subject: Resolucion del ejercicio 3

            Nombre: Mateo Nomico

            Legajo: 168102

            Este es un mensaje de prueba.

            .
            250 OK id=1uzGEK-00003j-1Y

        • Indique en el encabezado Subject: “Resolucion del ejercicio 3”. Escriba un cuerpo de mensaje de al menos 3 líneas, incluyendo su nombre y su legajo.

            DATA
            354 Enter message, ending with "." on a line by itself
            Subject: Resolucion del ejercicio 3

            Nombre: Mateo Nomico

            Legajo: 168102

            Este es un mensaje de prueba.

        • Finalice el mensaje escribiendo un punto en una línea en blanco. Deberá ver la respuesta 250 OK id=... indicando que el mensaje fue procesado correctamente.

            .
            250 OK id=1uzGEK-00003j-1Y

    3. Desde la pc2, utilizando nc , conéctese al servidor POP3 pop.nanoinside.net (TCP puerto 110). Acceda a la cuenta de usuario guest (contraseña guest ), recupere el mensaje almacenado en la casilla, bórrelo y finalice adecuadamente la sesión POP.

        ```
        root@pc2:/# nc pop.nanoinside.net 110
        +OK Dovecot (Debian) ready.
        USER guest
        +OK
        PASS guest
        +OK Logged in.
        LIST
        +OK 1 messages:
        1 800
        .
        RETR 1
        +OK 800 octets
        Return-path: <mateonomico@lugroma3.org>
        Envelope-to: guest@nanoinside.net
        Delivery-date: Thu, 18 Sep 2025 15:08:08 +0000
        Received: from [192.168.0.11] (port=52526 helo=dnslug)
                by dnsnano with esmtp (Exim 4.96)
                (envelope-from <mateonomico@lugroma3.org>)
                id 1uzGEy-000032-1y
                for guest@nanoinside.net;
                Thu, 18 Sep 2025 15:08:08 +0000
        Received: from [192.168.0.111] (port=39886 helo=pc1.lugroma3.org)
                by dnslug with smtp (Exim 4.96)
                (envelope-from <mateonomico@lugroma3.org>)
                id 1uzGEK-00003j-1Y
                for guest@nanoinside.net;
                Thu, 18 Sep 2025 15:08:08 +0000
        Subject: Resolucion del ejercicio 3
        Message-Id: <E1uzGEK-00003j-1Y@dnslug>
        From: mateonomico@lugroma3.org
        Date: Thu, 18 Sep 2025 15:07:45 +0000

        Nombre: Mateo Nomico

        Legajo: 168102

        Este es un mensaje de prueba.

        .
        DELE 1
        +OK Marked to be deleted.
        QUIT
        +OK Logging out, messages deleted.
        ```

    4. Detenga el proceso de captura en el dispositivo capturador.

    5. Analice la captura y discuta acerca de la confidencialidad de los datos transmitidos.

        Los mensajes SMTP no están cifrados, es decir que la información sobre direcciones de emisor y destinatario quedan expuestos, y el mensaje se puede ver en texto plano. Se intenta establecer una conexión segura con STARTTLS pero falla, ya que parece que el servidor no soporta TLS, y esto hace que la información se vea en texto plano, y por lo tanto, que los mensajes puedan ser interceptados por alguien y ser leídos o modificados.

    6. Identifique la conexión TCP que se establece entre los MTA’s. Utilice tshark para mostrar el contenido de dicho stream y adjúntelo.

    7. ¿Qué cosas adicionó al mensaje original el servidor mail.lugroma3.org ?

4. Seleccione un mensaje dentro de la carpeta SPAM de su casilla de correo y, utilizando el menú “. . .”, descargue el código RFC 822 del mismo (en Gmail corresponde a la opción Mostrar original, en Outlook a Ver origen del mensaje, en Yahoo a Ver mensaje original, etc). Analice
los encabezados del mensaje e indique:

    • La semántica y el valor de los campos de encabezado vistos en clase (From, To, CC, Date, Subject, Reply-To, MIME-Version, Content-Type),

    • El valor del campo Return-Path y si coincide con el valor del campo From,

    • La lista de servidores SMTP por los que fue pasando el mensaje (encabezados que comienzan con Received: from ), la hora en la que pasó por cada uno de ellos y qué protocolo se utilizó en la transferencia (indicado por with ... ),

    • Si es MIME de tipo _multipart/*_, determinar para qué se utiliza el valor del dato boundary , cuantos bloques componen el mensaje, qué tipo de contenido (Content-Type) y qué codificación se utiliza (Content-Transfer-Encoding) en cada bloque.

---

### Guia de Preguntas

1. Describa el objetivo y como opera la aplicación correo electrónico, indicando los elementos involucrados: que son y cuál es la función de los agentes de usuario (user agents - UAs) y agentes de transferencia de mensajes (mail transfer agent - MTAs).

2. ¿Cuáles son los comandos SMTP de una implementación mínima? Describa someramente cada uno.

3. Describa el formato de mensajes de Internet (Internet Message Format - IMF). Utilidad y alcance. ¿Qué resultado se obtendrá si se envía un correo electrónico que no respete el IMF?

4. ¿Cuál es el objetivo de las extensiones MIME? Describa cómo se implementa y brinde ejemplos de diferentes tipos de contenidos y codificación.

5. ¿Cuál es el propósito de los protocolos POP e IMAP? Describa brevemente los comandos disponibles para el protocolo POP3. ¿Qué ventajas ofrece el protocolo IMAP4 sobre POP3?

---

### Resumen

---

### Bibliografia

➤ [**FOR09**] - [TCP IP Protocol Suite](https://github.com/mnomico/tyr/raw/main/libros/FOR09.pdf)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ Capítulo 26: “Electronic Mail: SMTP, POP, IMAP and MIME”