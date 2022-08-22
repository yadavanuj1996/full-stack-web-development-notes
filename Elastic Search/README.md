# Elastic Search

## Basic of Elastic Search
### Why to use Elastic Search
Open source analytics and full text search engine generally used for search functionalities for application (including product in ecomm app) including:
- Auto completion 
- Typos
- Matching phrases
- Handling synonymns

Other Usages:
- Query & analyze structed data (and create charts)
- Application Performance Management (Analuze application logs and system metrics)
- Forecast future values with ML.
- Anamolity Detection
  - User drop from 50,000 to 5,000
  - Significant deviation reporting


### How does elastic search works
- Data is sotred as documents in Elastic Search (similar to rows in relational db - mysql)
- Documents are JSON data
- Document contains Fields (fields are similar to columne in relational db)

### Querying ElasticSearch
- Rest Based API 
- Build in Java, client available for python
- Able to handle big volume of data, search on  millions of document in still lightning fase




- Use client library for acessing elastic search from our web application backend
- Ingesting data
  - When new data needs to be added in web application, along with the db add the data in elasticsearch as well
  - Add existing data into elastic search using script.


### Basic Architecture of Elastic Search
#### Main Points:
- Elastic search cluster is a collection of nodes that are responsible for storing data
- Nodes referes to runnign instance of elastic search running on a virtual machine or docker
- Data is stored as documents, that are JSON objects.
- Documents are grouped together with indices.

#### Other Points:
- In prod env each node should run on different node/ virtual machine.
- A Elastic Search Deployment contains clusters (at least one) and each cluster can contain multiple nodes.
- Each unit of data stored in cluster is a document (json objects)
  - On indexing a document the original json object is stored with a metadata that is used internally.
- Every document in elastic search is stored within an index  
  - An index groups document and provides configuration option that are related to availability and scalability.
- **Index** is collection of documents with similar charactersticks and are logically related.
  - Ex:- People index (contains people details), Departments index (Contain departments - marketing)
  - Search runs on indexes




Curl Request to access elastic search cluster on elastic cloud
- curl -u user_name elastic_search_endpoint
  - curl -u elastic https://elastic-test-course-deployment.es.asia-south1.gcp.elastic-cloud.com 
  - Pass password for the user

Curl request to search terms in index **product**:
- curl -u elastic -X GET -H "Content-Type:application/json" https://elastic-test-course-deployment.es.asia-south1.gcp.elastic-cloud.com/products/_search -d '{"query": {"match_all": {}  }  }'
- Specify the Content-Type header when adding a request body


#### Sharding and scalability
- Sharding is a way to divide indices into smaller pieces
- Each piece is referred to as a shard
- Sharding is done at the index level
- The main purpose is to horizontally scale the data volume.
- One shard can be placed on one node

One index contains 600 Gb of data while the the cluster contains two nodes with 500 GB disk space, in such case the index size is greated than disk size
of a node thus the index is divided into shards and each shard is placed divided amongst the two nodes.

![IMG_9245](https://user-images.githubusercontent.com/22169012/185746391-30181f1f-aed7-4d62-b00f-4cacc607090e.jpg)


- A shard is an independent index
- Each shard is an Apache Lucene index
- A shard has no predefined size: it growsa as documents are added to it (2 billion documents can be stored in a shard)

##### Purpose of sharding
- Maintly to be able to store more documents 
- To easier fit large indices onto nodes
- Improved performance
  - Parllelization of queries increase the throughput of an index
  - Seach on multiple shards run simultaneously.
  - An index contains a single shard by default
  

#### Replication
- Replication is provided by elastic search, the replica is made at shard level & the replicated shard is stored on node (generally the one that doest not have primary shard)
- Snapshot feature provides a snapshot of elastic search data up till a certain point of time.

## Managing Documents

### Elastic Search Query

- Get cluster health 
```
GET /_cluster/health
```
  
- Get indices  
```
GET _cat/indices?expand_wildcards=all
```


- Create a index
```
PUT /products
{
  "settings":{
    "number_of_shards": 2,
    "number_of_replicas": 2
  }
}

```

- Delete a index
```
DELETE /pages 
```

- Add a document in a index
```
POST /products/_doc
{
  "name": "Coffee Maker",
  "price": 64,
  "in_stock": 10
}
```

- Add a document with explicitly providing id in a index (In dev mode the default settings creates a new index on PUT command if index is not present, should not be used in prod)
```
PUT /products/_doc/100
{
  "name": "Toaster",
  "price": 49,
  "in_stock": 4
  
}
```

- fetch a document using an id
```
GET /products/_doc/100
```

Reponse: 
```
{
  "_index": "products",
  "_id": "100",
  "_version": 1,
  "_seq_no": 0,
  "_primary_term": 1,
  "found": true,
  "_source": {
    "name": "Toaster",
    "price": 49,
    "in_stock": 4
  }
}
```
Note: If a id is not available found key will be false and _source key will not be returned.

- Update a doc
```
POST /products/_update/100
{
  "doc":{
    "in_stock": 3
  }
}
```

Response:
```
{
  "_index": "products",
  "_id": "100",
  "_version": 2,
  "result": "updated",
  "_shards": {
    "total": 3,
    "successful": 2,
    "failed": 0
  },
  "_seq_no": 1,
  "_primary_term": 1
}
```
result: "updated" states that the changes were made successfully

- Add a new key value pair in an existing document
```
POST /products/_update/100
{
  "doc":{
    "tags": ["electronics"]
  }
}
```

- Update value of one of the key of a document
```
POST /products/_update/100
{
  "script": {
    "source": "ctx._source.in_stock--"
  }
}
```

- Delete a document
```
DELETE /products/_doc/100
```

Reponse:
```
{
  "_index": "products",
  "_id": "100",
  "_version": 8,
  "result": "deleted",
  "_shards": {
    "total": 3,
    "successful": 2,
    "failed": 0
  },
  "_seq_no": 7,
  "_primary_term": 1
}
```
"result": "deleted" signifies that document is deleted.


- Indexing documents (Batch processing)

```
POST /_bulk
{ "index": { "_index": "products", "_id": 200 } }
{ "name": "Espresso Machine", "price": 199, "in_stock": 5 }
{ "create": { "_index": "products", "_id": 201 } }
{ "name": "Milk Frother", "price": 149, "in_stock": 14 }
```

- Updating and deleting documents

```
POST /_bulk
{ "update": { "_index": "products", "_id": 201 } }
{ "doc": { "price": 129 } }
{ "delete": { "_index": "products", "_id": 200 } }
```

- Specifying the index name in the request path

```
POST /products/_bulk
{ "update": { "_id": 201 } }
{ "doc": { "price": 129 } }
{ "delete": { "_id": 200 } }
```

- Retrieving all documents

```
GET /products/_search
{
  "query": {
    "match_all": {}
  }
}
```

- Replace the `match_all` query with any query that you would like. (Updating documents matching a query)

```
POST /products/_update_by_query
{
  "script": {
    "source": "ctx._source.in_stock--"
  },
  "query": {
    "match_all": {}
  }
}
```


- Deleting documents that match a given query (Delete by query)

```
POST /products/_delete_by_query
{
  "query": {
    "match_all": { }
  }
}
```

- Ignoring (counting) version conflicts

The `conflicts` key may be added as a query parameter instead, i.e. `?conflicts=proceed`.

```
POST /products/_delete_by_query
{
  "conflicts": "proceed",
  "query": {
    "match_all": { }
  }
}
```
##### When to use bulk API 
- When you need to perform lots of write operations at same time
  - ex: while importing data or modifying lots of data

### Routing
- Routing helps Elastic Search know where to store documents.
- Routing helps Elastic Search know where to find documents once they are stored.
- Routing is process of resolving a shard for a document
  - shrad_num =  hash(routing) % num_of_primary_shards
- No of shards cannot be changed after the index is created (although you can split a read only shard using Split API)

- Process of fetching a data from Elastic Search on Client (App with elastic search sdk, kibana console, dev machine etc) request.
![IMG_9257](https://user-images.githubusercontent.com/22169012/185916266-98ca26dd-fdf8-49d4-aba2-ffa18ae410e6.jpg)

Routing returns a replication group (Primary Shard+ all replicated shards) and the best shard from them from reading perspective is selected and the data is returned.

- Storing a document in elastic search
  - A request is made by client
  - A coordinator node find a primary Shard (Only primary shards can write the data in elastic search)
  - Primary Shards validates the data first
  - Once the data is validated the document is stored in the primary shard.
  - The document is replicated to other shards in the replication group i.e., other replicated shards of primary shards.


##### Optimistic Concurrency Control
- Issues that can come up
  - let's say during replication process the primary shard disk fails thus some shards in replication group will have a new document while the other won't to solve such problem there is a concept of _primary_term and _seq_no
    - _primary_term represents no of times primary shards are changed within a replication group
    - _seq_no represents the sequencing order in which the documents are updated.
  - Document is updated on old values, inventory data being updated by two different request that do not know about each other.


##### Importing data into local cluster using curl

```
curl -H "Content-Type:application/x-ndjson" -XPOST http://localhost:9200/products/_bulk --data-binary "@products-bulk.json"
```

 Importing data into Elastic Cloud 
```
curl -H "Content-Type:application/x-ndjson" -XPOST -u username:password https://elastic-cloud-endpoint.com:9243/products/_bulk --data-binary "@products-bulk.json"
```

## Analysis and mapping
- Text is anaylyzed and processed before getting stored in a searchable data structure inside elastic search
- A analyzer contains
  - Character filters
    - Add, removes or changes character. Removes html code to text 
    - Input: "I REALLY like beer!"
    - Output: "I REALLY like beer!"
  - Tokenizer
    - Tokenizes a string, i.e., splits it into tokens. 
    - Input: "I REALLY like beer!"
    - Output: ["I", "REALLY", "like", "beer"]
  - Token filters
    - Receives the output of tokenizer and add, remove or modify tokens, one examole is lowercase filter
    - Input: "I", "REALLY", "like", "beer"
    - Output: "i", "really", "like", "beer"

- API to see analyze result
```
POST /_analyze
{
  "text": "2 guys walk into   a bar, both the third... DUCKS! :-)",
  "analyzer": "standard"
}
```
Response
```
{
  "tokens": [
    {
      "token": "2",
      "start_offset": 0,
      "end_offset": 1,
      "type": "<NUM>",
      "position": 0
    },
    {
      "token": "guys",
      "start_offset": 2,
      "end_offset": 6,
      "type": "<ALPHANUM>",
      "position": 1
    },
    {
      "token": "walk",
      "start_offset": 7,
      "end_offset": 11,
      "type": "<ALPHANUM>",
      "position": 2
    },
    {
      "token": "into",
      "start_offset": 12,
      "end_offset": 16,
      "type": "<ALPHANUM>",
      "position": 3
    },
    {
      "token": "a",
      "start_offset": 19,
      "end_offset": 20,
      "type": "<ALPHANUM>",
      "position": 4
    },
    {
      "token": "bar",
      "start_offset": 21,
      "end_offset": 24,
      "type": "<ALPHANUM>",
      "position": 5
    },
    {
      "token": "both",
      "start_offset": 26,
      "end_offset": 30,
      "type": "<ALPHANUM>",
      "position": 6
    },
    {
      "token": "the",
      "start_offset": 31,
      "end_offset": 34,
      "type": "<ALPHANUM>",
      "position": 7
    },
    {
      "token": "third",
      "start_offset": 35,
      "end_offset": 40,
      "type": "<ALPHANUM>",
      "position": 8
    },
    {
      "token": "ducks",
      "start_offset": 44,
      "end_offset": 49,
      "type": "<ALPHANUM>",
      "position": 9
    }
  ]
}
```
