# Redis

## Introduction
- Redis stands for REmote DIctionary Serve
- It is a **NoSQL** advanced **key-value data store**
- The read and write operations are very fast in Redis because it stores all data in memory
- Since Redis stores its data in memory, it is most commonly used as a cache
- Redis is also used as Message Queue


## Redis Commands

### Redis Data Types
```
As we have mentioned earlier that Redis is a key-value store, but that doesn’t mean that it stores only
string keys and string values.  Redis supports different types of data structures as values. 
The key in Redis is a binary-safe String, with a max size of 512 MB, but you should always consider
creating shorter keys. A binary-safe string is a string that can contain any kind of data, 
e.g., a JPEG image or a serialized Java object
```
- The list should be stored in those cases where the order of insertion matters and where the write speed matters as compared to the read speed. One such case is storing logs.

The data types that are supported in values:
- String
- List
  - If we use List in Redis, the elements are stored in a linked list
  - The list should be stored in those cases where the order of insertion matters and where the write speed matters as compared to the read speed. One such case is storing logs.
- Set
  - Set offers constant time performance for adding and removing operations. We can use set to store data where uniqueness matters, e.g., storing the number of unique visitors on our website.  
- Sorted set
- Hash
  - ![Screenshot 2022-05-11 at 5 38 07 PM](https://user-images.githubusercontent.com/22169012/167846147-e32fe92a-1f26-431e-8561-aba3b7fe6985.png)

## Redis Publisher/Subscriber Model
This section explains the concepts behind using Redis as a queue

### What is a message queue?
A message queue is a type of temporary storage for messages. The sender, also known as publisher, sends messages to the queue. The messages remain in the queue until a receiver also known as a subscriber, is ready to read the messages. The main use case for a message queue is when there are some larger jobs that need to be processed. The sender sends the jobs to a queue instead of directly sending it to the receiver. The receiver picks each job, one by one, and processes it.

Let’s say we are booking movie tickets on a website. There are a few things that should be done immediately, like selecting the seats, payment, etc. But a few things, like sending tickets via email, may take time and are not required to be done immediately. These tasks that time and are not required to be done immediately can be added to a queue and can be processed one by one.

### How Redis is used as a message queue?
As we discussed earlier, Redis can also be used as a message queue. The publisher can publish to only one channel, although a channel may have multiple subscribers. A subscriber can subscribe to one or more channels.

![Screenshot 2022-05-11 at 5 42 57 PM](https://user-images.githubusercontent.com/22169012/167846959-e3c21d4b-f607-4262-9141-73a6a8b41700.png)

- SUBSCRIBE channel_name
  - To Subscribe to a channel
- PUBLISH channel_name message
  - To Publish to a channel
- UNSUBSCRIBE channel
  - To Unsubscribe to a channel
- PSUBSCRIBE string*
  - Subscribing to a group of channels#
- PUNSUBSCRIBE string*
  - Unsubscribing from a group of channels 

```
It is possible for different clients to subscribe to the same channel. Whenever a publisher publishes 
this channel, all the receivers receive the message.
```

#### Commands
- redis-server
  - To start redis server
- redis-cli
  - To start redis cli  
- PSUBSCRIBE string*

### Redis: Persistence
- RDB persistence(snapshotting)
  - In RDB(Redis Database) persistence, snapshots of the data are stored in a disk in a dump.rdb file after a set interval of time.
- Append-only file (AOF) persistence
  - When AOF is enabled, every write operation received by the server is logged into a file. When the Redis is restarted, all the commands in the AOF file are run again, and the entire dataset is created. 

```
Redis uses snapshotting as the default strategy. If you are fine with losing a few seconds of data,
then this strategy should be used. If you need complete durability and can’t afford to lose any data,
then AOF should be used. You can also use both strategies but Redis will use AOF to populate data,
as it is the most accurate one.
```

### Redis: Replication

#### What is data replication?
- When data is stored on a server and there is a server crash, there is a chance that the data will be lost. To avoid this, the technique of data replication is used. The data is stored on two or more servers instead of a single server. That way, if a server goes down, data is not lost since it is available on the other server. Also, the application does not crash because the other server can cater to the user requests. Another benefit of data replication is that it can reduce the load on the servers because the user requests can be load balanced to the servers instead of sending it to a single server.

#### Replication in Redis

![Screenshot 2022-05-12 at 1 34 31 PM](https://user-images.githubusercontent.com/22169012/168022357-75cb2355-186d-4463-aff3-36a406628b2d.png)

Redis follows a master-slave approach for replication. One of the servers is a master, and the other servers are called slaves. The slaves are connected to the master. All the writes happen to the master and then the master, sends these changes to the slaves. The reads can then be handled by the slaves. Through this process, the load is distributed.

If a slave gets disconnected from the master, it automatically reconnects and tries to be the exact copy of the master. There are two approaches that a slave takes to get in sync with the master.


### Redis: Partitioning

#### What is partitioning?
In the previous lesson, we discussed replication. With replication, we make multiple copies of the data, and each server contains the complete data. But if the data is too large and can’t be saved on a single instance? In that case, we may need to split the data and store it in different instances. This is called partitioning the data.

Partitioning the data will not solve the problem of data safety. If a node goes down, the data stored in that node will be lost. So, replication is required in addition to partitioning. Although it will increase the amount of data that needs to be stored, the data will not be lost in the case of a failure.

#### Advantages of partitioning
- Partitioning helps in horizontal scaling of the data. If the data is spread across different servers, then the traffic can be routed to different servers, and and each server will have less load.
- Sometimes it may not be possible to store data on a single server because of its size. In this case, using partitioning is the only option left.


### Redis: Client side caching
#### What is client-side caching
- When the client requires data, they ask the Redis server to provide the data. Each back and forth from the server results in some bandwidth consumption, and it takes some time to get the result. It is possible to cache the result of the most frequently used keys on the client-side. This drastically improves the performance of the application, as it does not need to send requests to the database

#### Challenges in client-side caching
- The biggest challenge faced in caching the data on the client-side is how to invalidate the data. Suppose we have cached some data on the client-side, and it is changed on the server. The client will keep referring to the stale data present in its cache. There should be some mechanism to invalidate the data on the client’s cache if it is changed on the server. There are two mechanisms to deal for this situation:

- A TTL (time to live) can be set for each key that is cached on the client-side. After a certain time period has elapsed, the key will be automatically removed from the cache, and the client will need to refer to the database to get the value. Although this is a simple solution, it can only be used in those situations where the data is changed frequently. If the data is a few minutes old, then it does not matter. If the application is data sensitive and data is changing frequently, then this technique is not useful.
Another method is to use the PUB/SUB model of Redis to send invalidate messages to the client. Whenever a key is changed. the server will send invalidate messages to the clients. This will inform the clients that the key has been changed, and it should be deleted from the cache. The problem with this approach is that the server will need to send the message to all clients every time a key is changed, which can be very costly from the bandwidth point of view.


#### Client-Side caching in Redis
Redis provides support for client-side caching, called tracking. There are two different approaches that can be used:
- Default mode: In this approach, the server stores the information regarding which key is stored by which client. By doing this, if a key is changed, the server sends the message to only those clients who have cached that key. Although this saves a lot of bandwidth, it consumes some memory on the server side. The client needs to enable the tracking as it is not enabled by default.

- Broadcasting mode: In the second approach, the server does not need to keep track of the keys cached by the clients. The clients subscribe to key prefixes and will receive a notification message every time a key matching such prefix is touched. If the client does not specify any prefix, the invalidation message is received for each and every key. This approach saves a lot of memory on the server-side but can result in more bandwidth usage.

