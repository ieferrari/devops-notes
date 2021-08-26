# AWS DynamoDB
* Fast ~1ms read time
* access controls
* flexible, scale to any workload
* stored on ssd, replicates and writes everything on three db servers
* event driven programming

***
## Read consistency
* eventually consistent reads[default]:
  * if you read inmediatly after a write it may not be replicated in all three servers already, so for a second you may read an old value, but really fast
* Strongly consistent reads[optional]:
  * can't read until every one of the three server are syncronized,

##  Provisioned Throughput Capacity
Reading is 10x cheaper than writing
* write: charge per hour, every 10 units -> 36.000 writes/ hour
* read: charge per hour, every 50 units -> 180.000 strongly consistent or 360.000 eventually consistent reads

## Setup
* AWS >> DynamoDB >> create >> table-name, primary-key
* read Capacity units, write Capacity units







***
## Steps for data modeling
[check this presentation](https://www.youtube.com/watch?v=6yqfmXiZTlM)

1. Understand your use cases. ¿is good for NoSQL, and or DynamoDB?
2. Understands your access patterns:
  * when are we going to write? data sources?
  * what are we going to query?
3. Data modeling
4. review 1,2,3,4 and repeat


### Data modeling
Each Table has many items, which **don't need to have the same attributes**. So you can mix different things like users posts, comments, etc in the same table.

**The primary key** is made by combining:
* partition key: access patter, determines data distribution
* sort key  [optional]: relationships that enables many kind of queries

the sum of partition key + sort key must be unique to work as primary key

* secondary index: lets you query data using an alternate key.
  * local secondary index, same partition key as the table but a different sort key. Max 5 by table.
  * global secondary index: primary key + sort key, different from the original partition key in the table. Max 20 by table.

It is fast and simple to find an object if you know the key, but it is slow and expensive to find without a key, because you must iterate aver many elements to find the target.
