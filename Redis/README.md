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
