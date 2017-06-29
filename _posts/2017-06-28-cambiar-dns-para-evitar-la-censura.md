---
layout: post
title: "Como cambiar tus DNS para evitar la censura"
description: Salta la censura cambiando tus DNS
headline: Tutorial para cambiar tus DNS y saltar la censura
modified: 2017-06-28
category: censorship
tags: [privacy, mozilla, censorship, venezuela, dns, tutorial]
imagefeature: 
comments: true
featured: false
published: true
---

Como una iniciativa para **Mozilla Venezuela**, en su lucha contra la **censura del internet**, buscando que sea **libre y privada** para todos los usuarios, una web **neutral** donde todas las opiniones sean escuchadas, presentamos una forma de evadir bloqueos cambiando la configuracion de resolucion de dominio.


# ¿Que es un DNS?

> El sistema de nombres de dominio (DNS, por sus siglas en inglés, Domain Name System) es un sistema de nomenclatura jerárquico descentralizado para dispositivos conectados a redes IP como Internet o una red privada. Este sistema asocia información variada con nombre de dominio asignado a cada uno de los participantes. Su función más importante es "traducir" nombres inteligibles para las personas en identificadores binarios asociados con los equipos conectados a la red, esto con el propósito de poder localizar y direccionar estos equipos mundialmente.

[DNS en Wikipedia](https://es.wikipedia.org/wiki/Sistema_de_nombres_de_dominio)

Basicamente resuelve el nombre de dominio de un formato de computadora, a uno que el humano pueda entender.

# ¿Como funciona el bloqueo?

En los nodos principales colocan en una lista negra los nombres y direcciones de los sitios web que desean bloquear, de esta forma el nodo no resolvera esos nombres, haciendo imposible para nosotros poder acceder al sitio web.

# Como cambiarlos en Windows

En la barra de tareas, hacer click derecho en el icono de WIFI o de Ethernet, y luego acceder a **Abrir centro de redes y recursos compartidos**  
![redes](https://i.imgur.com/8QWH9iT.png "Redes")  

En el centro de redes, hacer click izquierdo en el nombre de tu red, normalmente Red Local, o el nombre de tu WIFI.  
![redes](https://i.imgur.com/DhYurTR.png "Redes")

Al abrirse una ventana pequena donde se mostrara varia informacion sobre tu conexion, hacer click izquierdo en la parte inferior donde dice **Propiedades**.
![redes](https://i.imgur.com/WzTthmu.png "Redes")  
Luego hacer click en **Protocolo de Internet version 4 (TCP/IPv4)** y posteriormente hacer click en **Propiedades**  

![redes](https://i.imgur.com/BR5yLIM.png "Redes")  
Se abrira una ventana donde nos dejara elegir nuestro IP y nuestro DNS  
![redes](https://i.imgur.com/fFZcFqj.png "Redes")  

Ahora simplemente seleccionamos un DNS de nuestra lista y verificamos que tengamos todo en orden.


# Cambiando DNS en Linux

_Al usar Linux asumo que tienes conocimientos de la linea de comandos (CLI), ya que por medio de ella vamos a realizar los cambios._

Primero vamos a instalar el programa `nano` si tu sistema no lo tiene instalado.

Usamos el comando `sudo apt-get install nano -y` en debian/ubuntu/derivados `sudo yum install nano -y` en RHEL/CentOS

Luego, simplemente colocamos `nano /etc/resolv.conf` mostrando algo como esto

```
nameserver xxxxx
nameserver xxxxx
```

Donde xxxx, puede variar de equipo en equipo, ahora simplemte sustituimos donde muestran las **xxxxx** por nuestras direcciones DNS y guardamos con **CTRL+O** y presionamos **ENTER** despues salimos con **CTRL+X**


# Eligiendo un servidor DNS

Puedes elegir el que mas te guste, para este tutorial usaremos los DNS de Google, pero puedes elegir el que mas te guste.

### DNS de OpenDNS
[Web principal](https://www.opendns.com/)

Direcciones
```
DNS preferido: 208.67.222.222
DNS alternativo: 208.67.220.220
```

### DNS de DNS.Watch
[Web principal](https://dns.watch/index)

Direcciones:
```
DNS preferido: 84.200.69.80
DNS alternativo: 84.200.70.40
```

### DNS de Norton
[Web principal](https://dns.norton.com/)

Direcciones:
```
DNS preferido: 199.85.126.10
DNS alternativo: 199.85.127.10.
```

### DNS de Google
[Web principal](https://code.google.com/speed/public-dns/docs/using.html)

Direcciones:
```
DNS preferido: 8.8.8.8
DNS alternativo: 8.8.4.4
```

Existen otros servidores de DNS que puedes elegir buscando un poco, cabe destacar que algunos de ellos bloquean algunos sitios peligrosos, algunos tienen proteccion infantil y demas, _Recuerda siempre buscar informacion sobre los DNS que vas a colocar en tu PC_

# Verificando nuestros DNS

En algunos sistemas se debe reiniciar el driver de red para que la nueva configuracion sea cargada, si no sabes como hacerlo, puedes reiniciar la computadora.

Visita este [link](https://ipleak.net/ "Verificar mis DNS") para verificar que tus DNS funcionen correctamente

![redes](https://i.imgur.com/iv3JS51.png "DNS")  


Con estas configuraciones podras entrar a las paginas web bloquedas no solo en Venezuela, y disfrutar de una web mas abierta y sin censura.