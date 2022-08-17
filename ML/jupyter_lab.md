# Jupyter lab server

## First run setup
create a folder for the local volume with all the permissions

	mkdir jupyter_home
	chmod 777 jupyter_home

Bring up the service with
	
	docker-compose up

> copy the token from the terminal output

open the server in <server_ip>:<port>, and use the token to save a password

Stop the server with [ctrl]+[C] and restart it with
	
	docker-compose up -d

***


## install packages in local volume


	pip install -t packages my_lib



