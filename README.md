# ELK Stack
**- Elastic Search**  
Started off as scalable Lucene  
Horizontally scalable search engine  
Each "shard" is an inverted index of documents  
Can do full-text search, structured data and can aggregate data quickly  
Often fast solution than Hadoop/Spark/Flink etc.



### Download and install the Elastic Search and start server
/bin/elasticsearch

this will start the server on http://127.0.0.1:9200/

```json
{
  "name" : "DESKTOP-OVU92S3",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "7utPwbM2QOm5zX8LgW0VFw",
  "version" : {
    "number" : "7.6.1",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "aa751e09be0a5072e8570670309b1f12348f023b",
    "build_date" : "2020-02-29T00:15:25.529771Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

### Create Schema document

PUT - http://127.0.0.1:9200/shakespeare

Use binary data as input with shakes-mapping.json as binary data.

OR
curl -H 'Content-Type: application/json' -XPUT '127.0.0.1:9200/shakespeare' --data-binary @shakes-mapping.json

### Upload data to Elastic search

POST - http://127.0.0.1:9200/shakespeare/_bulk?pretty

Use binary  data as input with shakespeare_6.0.json as binary data input for uploading data.

OR
curl -H 'Content-Type: application/json' -XPOST '127.0.0.1:9200/shakespeare/_bulk?pretty' --data-binary @shakespeare_7.0.json

### Search in document

GET - http://127.0.0.1:9200/shakespeare/_search?pretty

Search with below query -
```json
{
	"query" : {
		"match_phrase" : {
			"text_entry" : "to be or not to be"
		}
	}
}
```

curl -H 'Content-Type: application/json' -XGET '127.0.0.1:9200/shakespeare/_search?pretty' -d '{
	"query" : {
		"match_phrase" : {
			"text_entry" : "to be or not to be"
		}
	}
}'