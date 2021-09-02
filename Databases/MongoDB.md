# MongoDB
## Usage Cases

***
## Linux installation
from [docs](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-debian/):

    sudo apt-get install gnupg
    wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
    echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/4.4 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

    sudo systemctl start mongod
    sudo systemctl status mongod
    sudo systemctl stop mongod
    sudo systemctl restart mongod

    mongo

***

## Basic commands
iside mongoDB shell:

    mongo
    >show dbs

    > use NewDB
    switched to db NewDB

    > db
    NewDB

    > db.createCollection('mensajes')
    { "ok" : 1 }


insert a json object

    > db.mensajes.insert({"device":123, "timestamp": 23423423234234, "msg":"temperatura 11 °C"})
    WriteResult({ "nInserted" : 1 })


insertando un array con varios objetos json a la vez

    > db.mensajes.insert([{"device":123, "timestamp": 23423423234234, "msg":"temperatura 11 °C"},{"device":11, "timestamp": 23423423234234, "msg":"temperatura 14 °C"}])
    BulkWriteResult({
    	"writeErrors" : [ ],
    	"writeConcernErrors" : [ ],
    	"nInserted" : 2,
    	"nUpserted" : 0,
    	"nMatched" : 0,
    	"nModified" : 0,
    	"nRemoved" : 0,
    	"upserted" : [ ]
    })

muestro todo lo insertado hasta ahora:

    > db.mensajes.find()
    { "_id" : ObjectId("60da61c1a6ccfd9c95008447"), "device" : 123, "timestamp" : 123124, "msg" : "temperartura 10 °C" }


> db.mensajes.find().pretty()
{
	"_id" : ObjectId("60da61c1a6ccfd9c95008447"),
	"device" : 123,
	"timestamp" : 123124,
	"msg" : "temperartura 10 °C"
}
{
	"_id" : ObjectId("60da62680b28076094e56380"),
	"device" : 123,
	"timestamp" : 23423423234234,
	"msg" : "temperatura 11 °C"
}

busco una entrada con device ==11

    > db.mensajes.find({device:11})
    { "_id" : ObjectId("60da632f0b28076094e56384"), "device" : 11, "timestamp" : 23423423234234, "msg" : "temperatura 14 °C" }


cambiar valor de una entrada

    > db.mensajes.update({device:11},{$set:{device:12}})
    WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })


borrar el primero de la selección

    > db.mensajes.deleteOne({device:123})
    { "acknowledged" : true, "deletedCount" : 1 }

Salir

  > exit
  bye

***


## schema design

### normalization in classical SQL
* in a relational data base you try avoid data duplication and then join everything
* normalization allows simple updates without reduncancy
* cons: many joins in big tables can be slow
* sometimes you may end up making redundancy to gain speed


Good practice in MongoDB is to design the schema for your specific application usage. check [MongoDB forum](community.mongodb.com)


types of relationships:
* one to one
* one to many


hay un limite de tamaño para un documento en mongo de 16MB

    one to squillions:      _id: objectid("XXY")

                            logs:    _id: ...
                                     host:  Objectid("XXY")
                                     timestamp
                                     data

arrays can't grow with no limit

* many to many



***
### To Embed or Reference
Ejemplo producto + categoria:
* si lo guardo todo junto:
  * tengo una consulta rapida
  * pero si cambio el nombre de la categoria tengo q arreglarlo en cada producto
* si guardarlo aparte con una relación:
  * tengo q hacer dos consultas para llamar al producto con su categoría
  * si cambio el nombre de la categoría se arregla solo
Con esto se decide cuál escenario tiene más peso para nuestro diseño

***

### Anti-patterns
[from this video:](https://www.youtube.com/watch?v=8CZs-0it9r4&t=147s)
* masive arrays
* massive number of collections
* Unnecesary indexes
* bloated documents
* case-insensitive queries, without case-insensitive indexes
* separating data that is accessd together
