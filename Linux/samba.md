# Samba file server

# start stop restart server

		~$ sudo service smbd <start/stop/restart>

#Compartir carpeta con un servidor de archivos Samba


## EN EL SERVIDOR

	~$sudo apt-get install samba
	~$sudo smbpasswd -a <user>
		passwd:
		repeat passswd:

	~$ mkdir <shared_folder>
	~$ sudo nano -e /etc/samba/smb.conf

	##agregar al final del archivo
		[<shared_folder_name>]
		path= </home/user/shared_folder>
		aviable = yes
		valid users = <user>
		read only = no
		browsable = yes
		pulic = yes
		writable = yes
	##save changes and exit nano

	~$ sudo service smbd restart

	##get ip
	~$sudo ifcongig
		...
		ip:192.168.0.xxx
		...
	##

***

## EN EL CLIENTE WINDOWS
	crear acceso directo a:

		\\192.168.0.xxx\shared_folder
	pide
		usuario:
		password:

***

## EN EL CLIENTE LINUX

		~$ sudo apte-get install smbclient
		~$ smbclient --user=<usuario del servidor> -L //<ip del servidor>
			enter <usuario del servidor>'s password:
		~$ mkdir /<local folder dir>

		~$ nano -e /etc/fstab
		#agrego

		//<server ip>/<shared folder>   /<local folder dir>  username=<server user>, password=<server pass>,x-systemd.automount 0 0

		#verifico que el montado funcione correctamente  montando "all"
		~$ sudo mount -a
