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
- 

