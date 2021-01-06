---
layout: post
title:  Reto 2 Hacking CTF ... Seguimos buscando flags
---

Vamos a seguir con el siguiente de los puertos descubiertos por el escaneo nmap que ha conseguido extraer mucha información empleando el script ftp

```bash
<div style="border:1px solid black;height:100px;width:760px;overflow-y:hidden;overflow-x:scroll;">
<p style="width:250%;">
 
 9992/tcp  open  ftp   vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0        42 Jan 03 19:17 prueba2.txt
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 80.224.194.195
|      Logged in as ftp
|      TYPE: ASCII
|      Session bandwidth limit in byte/s is 6250000
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.2 - secure, fast, stable
|_End of status
</p>
</div>

```

Muestra cómo se ofrece un servicio ftp a la escucha, pero no sobre el puerto 21/tcp habitual sino sobre el  9992/tcp. Incluso describe nombre de la aplicación y versión de servidor vsFTPd 3.0.2 , con permiso de cliente anónimo, y hasta muestra un fichero *prueba2.txt* que posiblemente contenga nuestra segunda *bandera*...

No entraña ninguna dificultad ya que nmap ofrece toda la info, que replicaré en la conexión...Es decir emplearemos usuario: "anonymous" y aunque desconocemos la password, por la información sabemos que no debe existir ningún problema en conseguir el acceso... He aquí cómo:

<img src="{{ site.baseurl }}/public/Reto2_ftp.png">

Único detalle, activar el modo pasivo de la  conexión ftp para que nos permita ejecutar comandos de transferencia.  A modo de test, para emular el script ftp de nmap, ejecuto el mismo comando *rstatus* y  que nos muestre la misma información de conexión y versión del servidor FTP.  

> Y finalmente nos descargamos mediante un get el archivo *prueba2.txt* que contiene la bandera o  **Token 2: 0b12f707a8703238a11c78b607eaeae6**

<img src="{{ site.baseurl }}/public/Flag_reto2.png">


Este ha sido muy fácil. Vamos a por el tecer flag del reto.
