---
layout: post
title:  Retos Hacking CTF del Centro de formación ciberseguridad Nallam
---

Como ejercicio  final incluido dentro del curso de Hacking ético se me planteó la consecución de 10  retos en los que se deberían conseguir sus correspondientes 10 *flags* o secuencias de 32 caracteres reconocibles.

El reto CTFs contaba con un final donde se necesitaba escalar privilegios hasta convertirse en administrador o root del equipo a vulnerar. En el reto 10.

La máquina presenta accesible y publicada en internet con la dirección 82.165.37.232 y la única pista de que los servicios vulnerables se encontraban por encima de los puertos 9000/tcp.

Como en todo proceso de pentesting, se seguirán las fases habituales de enumeración, explotación y  elevación de privilegios... en algún caso no será preciso ya que las *banderas* al menos la primera se mostrarán sin mayor secreto ni complicación.

Sin más, al lío .... empezamos por la fase imprescindible.

## Enumeración

Previamente  y como habitualmente, iniciamos  la primera fase habitual de Enumeración de servicios accesibles en la máquina remota a través un escaneo de puertos abiertos y estudio de servicios ofrecidos para identificar lo que nos ofrece la máquina. 

Continuaremos, de ser necesario y hasta localizar los flags con las fases de explotación y escalada de privilegios, llegado el caso, ... aunque el objetivo de los 10 retos CFT no lo expliciten.  


{% highlight bash %}
 #nmap -p- --open -v -Pn 82.165.37.232 -oG initScan
{% endhighlight %}


En resumen un nmap con los parámetros siguientes : 

Parámetro | Descripción 
--- | --- 
-p- |  inspecciona los 65535 puertos
- - open | sólo aquellos puertos que se encuentren abiertos
-v | verbose, o sea muestra todo por pantalla 
-Pn | no realiza comprobaciones de ping ni resolución DNS
-oG | se copia el resultado a archivo *initScan* que permita filtrar por grep y copiar al clipboard empleando una función de S4vitar


Con este resultado :


``` bash 
#nmap -p- --open -v -Pn 82.165.37.232 -oG initScan
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-01-03 19:21 CET
Initiating Parallel DNS resolution of 1 host. at 19:21
Completed Parallel DNS resolution of 1 host. at 19:21, 0.03s elapsed
Initiating SYN Stealth Scan at 19:21
Scanning s21356626.onlinehome-server.info (82.165.37.232) [65535 ports]
Discovered open port 9999/tcp on 82.165.37.232
Discovered open port 9994/tcp on 82.165.37.232
Discovered open port 9991/tcp on 82.165.37.232
Discovered open port 9997/tcp on 82.165.37.232
SYN Stealth Scan Timing: About 39.50% done; ETC: 19:22 (0:00:47 remaining)
Discovered open port 9992/tcp on 82.165.37.232
Discovered open port 9998/tcp on 82.165.37.232
Discovered open port 10010/tcp on 82.165.37.232
Discovered open port 10000/tcp on 82.165.37.232
Discovered open port 9995/tcp on 82.165.37.232
Discovered open port 9993/tcp on 82.165.37.232
Discovered open port 9996/tcp on 82.165.37.232
Discovered open port 2222/tcp on 82.165.37.232
Completed SYN Stealth Scan at 9:22, 98.31s elapsed (65535 total ports)
Nmap scan report for s21356626.onlinehome-server.info (82.165.37.232)
Host is up (0.22s latency).
Not shown: 65523 closed ports
PORT      STATE SERVICE
2222/tcp  open  EtherNetIP-1
9991/tcp  open  issa
9992/tcp  open  issc
9993/tcp  open  palace-2
9994/tcp  open  palace-3
9995/tcp  open  palace-4
9996/tcp  open  palace-5
9997/tcp  open  palace-6
9998/tcp  open  distinct32
9999/tcp  open  abyss
10000/tcp open  snet-sensor-mgmt
10010/tcp open  rxapi

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 98.56 seconds
           Raw packets sent: 111338 (4.899MB) | Rcvd: 109815 (4.393MB)

```

Vale, pues tras el escaneo obtenemos estos 12 puertos /tcp abiertos en la máquina con servcios a la escucha : 2222,9991,9992,9993,9994,9995,9996,9997,9998,9999,10000,10010


Para a intentar descubrir qué servicios corren sobre cada uno de ellos realizo un escaneo donde verificar las versiones y scripts relacionados con cada uno. Empleo para de nuevo nmap con alcance más limitado y guardo el resultado en un fichero de texto *portScan* :
 
```
nmap -p2222,9991,9992,9993,9994,9995,9996,9997,9998,9999,10000,10010 -sC -sV 82.165.37.232 -oN portScan

```
Con este resultado que muestro en dos capturas por ser demasiado extenso, curiosamente se observan 11 puertos abiertos (por encima del 9000/tcp) y debo buscar 10 *flags* o Tokens:

<img src="{{ site.baseurl }}/public/portScan1.png">
<img src="{{ site.baseurl }}/public/portScan2.png">


Bueno, pues empezaremos por el primer reto y encontrar el primer Token que es evidente ..... pues se muestra en el propio escaneo :-)

## **RETO 1**

Solo hay que fijarse, porque el Token1 aparece bajo el nombre de *Token Prueba1* y sobre el propio resultado del script ejecutado por nmap :

``` markdown 

9991/tcp  open  issa?
| fingerprint-strings: 
|   Kerberos, NULL, NotesRPC, SMBProgNeg, WMSRequest: 
|_     `Token Prueba 1: 601c12869ef93360c734bb95d9151276`


```

Y también se muestra el *Token Prueba 1* atacando directamente por http:// IP:puerto.


<img src="{{ site.baseurl }}/public/Token1.png">

Así pues,  Token Prueba 1: **601c12869ef93360c734bb95d9151276**

Encontrar este primer flag ha sido muy simple . La  siguiente entrada del blog mostraré cómo buscar la siguiente bandera.