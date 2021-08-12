# SSH

***
## Server
you can connect to this machine from a remote connection

Installation

    ~$ sudo apt-get install openssh-server

Configuration:

    ~$ sudo nano -e /etc/ssh/sshd_config

start  / restart / stop   server:

    ~$ sudo /etc/init.d/ssh start


***
## Client
you can not connect to this machine, but you can connect to other one

    ~$ ssh <username>@ip

connect to remote machine with graphical interface:

    ~$ ssh -X <username>@ip

open file manager

    ~$ pcmanfm ~$ nautilus  ~$ thunar

***

# Create a pair of keys in the client

    ~$ ssh-keygen -o
        >>file to save:(valor por defecto)
        >> enter passphrase(blank para automatización)
    ~$ ssh-add

see your public key:

    ~$ cat ~/.ssh/id_rsa.pub

then pass your pub key to the server andd add it on:

    ~/.ssh/authorized_keys


***

## Connect to machineB behind other machineA

    ieferrari@localhost ~$ ssh -J ieferrari@machineA_globalip iferrari@machineB_localip

***
## Open file manager on remote machine

    >> open File manager
    >> otras ubicaciones
    >> conectar al servidor
    >> sftp://iferrari@remote_machine_global_ip/home/iferrari

***
## File manager on remote machine behind other machine

    #todo lo que entra en serv-middle:8822 sale en office_pc:22
    iferrari@srv-middle:~$ ssh -N -L localhost:8822:localhost:22 iferrari@office_pc_localIP

    #todo lo que entra en localhost:8822 sale en serv-middle:8822
    user@pc:~$ ssh -N -L localhost:8822:localhost:8822 iferrari@ser-middle_globalIP

    File manafer >> otras ubicaciones >> conectar al servidor >> sftp://iferrari@localhost:8822:/home/iferrari

***
##  Server on machine behind router

    #inicia el servicio en office_pc:8889
    iferrari@office_pc:~$ jupyter notebook --no-browser --port=8889

    # todo lo que entra en serv-middle:8888 sale en office_pc:8889
    iferrari@srv-middle:~$ ssh -N -L localhost:8888:localhost:8889 iferrari@192.168.200.246

    # todo lo que entra en localhost:8889 sale en serv-middle:8888
    user@pc:~$ ssh -N -L localhost:8889:localhost:8888 iferrari@ser-middle_globalIP
    user@pc:~$ firefox localhost:8889 # abro el servicio en localhost:8889<->srv-middle:8888<->office_pc:8889

***
## SSH_behind_firewall

Escenario
La computadora de trabajo se llama "A" y se encuentra detrás de un firewall o un router que no realiza el "port-foward", el usuario es "userA".

La computadora de tu casa, desde la que te querés conectar se llama "B" y es accesible via ssh detrás de un router configurable, el usuario es "userB"

Ambas computadoras corren openssh-server en el puerto 22 (puerto por defecto)

En el router de la computadora "B" se estableció una regla para que todo el tráfico que entre al puerto 12345 vaya al ip local de "B" al puerto 22

Para resolver el problema del ip dinámico la computadora "B" tiene una cuenta en no-ip con el nombre "pcB.zapto.org" que equivale a su dirección.

Como no podemos conectarnos desde B --> A, la solución es hacer que A abra un tunel B<===A   a travéz del cual podamos meter la conexión B--->A

Es decir "A" inica la conexión:

$ ssh -f -N -T -R22220:localhost:22  userB@pcB.zapto.org (-p 12345 )

Esto abre una entrada remota -R en el puerto 22220, todo lo que entre por ahí sale en localhost:22

-f manda el proceso a correr en el fondo. Durante las pruebas puede ser conveniente omitir este comando para cerrar más facil el programa
-N indica que abrimos la conexión, pero no para mandar comandos, sólo para hacer el tunel, es decir que no abre un shell
-T desabilita la formación de una tty (¿terminal virtual?) ya que no la vamos a usar


Desde "B" se usa ese tunel para conectarse:

$ ssh -p 2220 userA@localhost

Manda la conexión por el puerto 2220 del local host. recordemos que todo lo que entra por ahi sale en el puerto 22 de la otra máquina

#Para terminar los procesos ssh que fueron a background con -f, (junto con todos los procesos ssh):
pkill ssh


***

## para permitir el uso de web server:

#agregar la siguiente línea en  /etc/ssh/sshd_config
GatewayPorts yes

    iferrari@serv-middle ~$ sudo service sshd restart

    iferrari@office_pc ~$ ssh -N -T -R 8000:localhost:8000: iferrari@192.168.200.2




***
## ssh backdoor behind firewall


#office_pc is behind firewall

    iferrari@office_pc:~$ ssh  -N -T -R 12345:localhost:22 iferrari@192.168.200.2

#office_pc abre un tunel para que todo lo que entre en el puerto 12345 de srv entra en el 22 de localhost

***
## server is open to internet


random pc in internet

    user@localhost:~$ ssh -N -L localhost:8890:localhost:12345 iferrari@ser-middle_globalIP
#se conecta al server y conecta el su puerto 12345 con el puerto local 8890

    user@localhost:~$ ssh  -p 8890 iferrari@localhost
#entra en el 8890:localhost  >>sale en 12345:server >>sale en 22:office_pc>>entra en office_pc

***
## En la compu detrás del firewall

    $ ssh -f -N -T -R12345:localhost:22 urs@192.168.43.139

abre una entrada remota -R en el puerto 12345 lo que entre por ahí sale en el localhost:22

    -f manda el proceso a correr en el fondo
    -N indica que abrimos la conexión, pero no para mandar comandos, sólo para hacer el tunel, es decir que no abre un shell
    -T desabilita la formación de una tty (¿terminal virtual?) ya que no la vamos a usar

En la compu accesible desde internet

    $ ssh -p 12345 user@localhost
Manda la conexión por el puerto 12345 del local host. recordemos que todo lo que entra por ahi sale en el puerto 22 de la otra máquina

    -L	#local
    -R	#remote

***
## SSH tunell

* serv = server_behind_router
* house= machine_with_router_config_permission

ssh remote port forwarding

    user@srv$ -8022:localhost:22 house.com
//se conecta a house y abre el puerto 8022 y hace portfoward


***
## ssh_port_foward_dinamic_ip

ssh through android access point

In order to access a device behind a router within  a specific port, you need to first configure your router to forward specific port request.

Example of net Architecture:
The router has a public ip ex: 181.83.238.38
Every device connected to the router has a private ip:  192.168.X.X
*	router		local ip 192.168.0.1
*	computer A	local ip 192.168.0.2
*	computer B	local ip 192.168.x.43

You want to run:
*	ssh service computer A port 22
*	ssh service computer B port 22

In the router you have to configure
*	in port 2221 (example number) forward to 192.168.0.2	port 22
*	in port 2222			forward to 192.168.x.43	port 22

The example port number can be any unused port, so has to be different for every device we port foward
To configure thin in android you have to install Forward-app from play-store  (or fwd app?)


To connect from outside of the wlan or lan you will do:

    $ ssh user@181.83.238.38 -p 2221	//for computer A
    $ ssh user@181.83.238.38 -p 2222	//for computer B


The public ip is usually dynamic, this mean that it changes over the time and in every connection.
To allow automatic connection we have two options:
* Make an script
	*	Server: run script to get ip and post an encrypted message on web.
	*	Client: run script to download and decrypt updated ip
* Use Noip.org after create an account  with a web direction ej mycomputer.zapto.org
	*	Server: run noip2 to update your ip to the asociated web direction
	*	client: $ ssh user@mycomputer.zapto.org -p xxxx


***
# Aditonal security for ssh server
*		disable root login
*		set up private key
*		set up welcome/warning banner
*		set up tool for checking logs attempts
*		set up time delay between log attempts to avoid brute-force attack
