# Redis

## Introduction
- Redis stands for REmote DIctionary Serve
- It is a **NoSQL** advanced **key-value data store**
- The read and write operations are very fast in Redis because it stores all data in memory
- Since Redis stores its data in memory, it is most commonly used as a cache


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
