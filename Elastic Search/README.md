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



Queries to try from kibana
- GET /_cluster/health
  - Get cluster health
- GET _cat/indices?expand_wildcards=all
  - Get indices  

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

