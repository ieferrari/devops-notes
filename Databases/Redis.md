#  Redis
## Usage cases

***
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
## commands
### Basic
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


### Time to live
you can set the time for a key value to live

    > ttl myKey       # what is the time to live for myKey?
    (integer)  -1     # infinity

    > expire myKey 60 # will be drop in 60 seconds

    > setex temporaryKey  60 temporaryValue   #  will be drop in 60 seconds

### arrays

    lpush myList newElement     # add newElement to myList on the left join
    rpush myList otherElement     # add otherElement to myList on the right join
    lrange myList 0 -1     # show every from element 0 to the last one of my list
    1)"newElement"
    2)"otherElement"

    LPOP myList      #deletes the first element form the left
    "otherElement"

### Sets
where every element is unique

    SADD mySet "setElement"
    SADD mySet "otherSetElement"
    SMEMBERS
    1)"setElement"
    2)"otherSetElement"
    SREM mySet "setElement"
    "otherSetElement"
