#  Redis
## Usage cases

***
## Launch a Redis instance with Docker-compose

using the docker-compose.yml file on this folder:

```sh
cd redis
docker-compose up -d
```

> now you have a Redis instance available on port 6379

## Connect to Redis

Using redis-cli

```sh
sudo apt-get install redis-tools
redis-cli -h localhost -p 6379 -a $MY_REDIS_PASSWORD

```

Using a GUI Redis explorer:

```sh
pip install qredis
qredis
``` 

Using a VScode extension:
https://marketplace.visualstudio.com/items?itemName=Dunn.redis


```
[ctrl] + [shift] + [p]
ext install Dunn.redis
```

with python

```
pip install redis 
```




## Work with Redis using Python

```py
import redis

redis_conn = redis.Redis(host=redis_host, port=6379, db=0, password=redis_password)
```


** 
check aditional configuration in [self documented redis.conf for Redis 7.0](https://raw.githubusercontent.com/redis/redis/7.0/redis.conf)


## Linux Installation
from [official docs](https://redis.io/topics/quickstart):


    wget http://download.redis.io/redis-stable.tar.gz
    tar xvzf redis-stable.tar.gz
    cd redis-stable
    make

    sudo make install

to start redis

    redis-server

in other terminal opend command-line for redis

    redis-cli

check redis performance

    redis-benchmark

***
# Commands

To install redis-cli on debian run:

    sudo apt-get install redit-tools

Connect to a redis server:

    redis-cli -h server_ip -p 6379 -a my_password



## Basic
inside redis-cli


    $ redis-cli
    > SET myKey  myValue
    OK

    > KEYS *
    "myKey"

    > GET myKey
    "myValue"

    > EXISTS myKey
    (integer) 1

    > DEL myKey
    (integer) 1

    > EXISTS myKey
    (integer) 0


    > quit


## Time to live
you can set the time for a key value to live

    > ttl myKey       # what is the time to live for myKey?
    (integer)  -1     # infinity

    > expire myKey 60 # will be drop in 60 seconds

    > setex temporaryKey  60 temporaryValue   #  will be drop in 60 seconds

## Arrays

    lpush myList newElement     # add newElement to myList on the left join
    rpush myList otherElement     # add otherElement to myList on the right join
    lrange myList 0 -1     # show every from element 0 to the last one of my list
    1)"newElement"
    2)"otherElement"

    LPOP myList      #deletes the first element form the left
    "otherElement"

## Sets
where every element is unique

    SADD mySet "setElement"
    SADD mySet "otherSetElement"
    SMEMBERS
    1)"setElement"
    2)"otherSetElement"
    SREM mySet "setElement"
    "otherSetElement"

## 


***

# Connections

## Python example

[check docs](https://github.com/redis/redis-py)
```python
import redis
import os

my_password = os.environ.get('REDIS_PASSWORD', 'my_password')
print(my_password)
r = redis.Redis(host='localhost', port=6379, db=0, password=my_password )
r.set('foo', 'bar')
r.get('foo')
```

### Queue example 

```python
import redis
import os
import time
import json

my_password = os.environ.get('REDIS_PASSWORD', '12345')
r = redis.Redis(host='localhost', port=6379, db=0, password=my_password )

# push some data to queue
for i in range(1001):
   data = {
         'seller_id': 'a',
         'item_id': i,
         'price': 2.3,
         'buyer_id': "aasdf",
         'time': time.time()
      }
   r.lpush('queue:email', json.dumps(data))
```


```python
# queue consumer to batch example
import redis
import os

BATCH_SIZE = 100
WAIT = 10 

my_password = os.environ.get('REDIS_PASSWORD', '12345')
r = redis.Redis(host='localhost', port=6379, db=0, password=my_password )

n= 0
while True:
    try:
        batch = r.rpop('queue:email',BATCH_SIZE)

        if batch:
            n+=1
            print(n, len(batch))
            # ml function to process batch here
        else:
            time.sleep(WAIT)
    except Exception as e:
        print(e)
```
## Go examples

[check docs](https://github.com/go-redis/redis)