# Jupyter lab server
Install using docker-compose.yml


***
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

## Docker-compose overview


```yaml
version: "3.8"
services:
      jupyterlab:
        image: jupyter/tensorflow-notebook
        container_name: my_notebook
        restart: always
        ports:
          - 8888:8888
        environment:
           PYTHONPATH: "/home/jovyan/packages"
        volumes:
          - ./jupyter_home:/home/jovyan
        logging:
          driver: "json-file"
          options:
            max-size: "10m"  
```

jupyter_home/ is used a persistence volume, every notebook will be saved there there.

/home/jovyan/packages is included in PYTHONPATH, so any package installed there will be available to import

To install packages in local volume use:

	pip install -t packages my_lib
