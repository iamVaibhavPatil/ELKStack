# ELK Stack
**- Elastic Search**  
1. Started off as scalable Lucene  
2. Horizontally scalable search engine  
3. Each "shard" is an inverted index of documents  
4. Can do full-text search, structured data and can aggregate data quickly  
5. Often fast solution than Hadoop/Spark/Flink etc.

**- LogStash**  
1. Ways to feed data into elastic search
2. FileBeat can monitor log files, parse them, and import them into Elastic search in near-real-time  
3. Logstash also pushesh data into ElasticSearch from many machines  
4. Not just logs. It is used for variety of other data

**- Kibana**  
1. Web UI for searching and visualizing  
2. Complex aggregations, graphs, charts  
3. Often used for log analysis

**- X-Pack**  
1. Security  
2. Alerting
3. Monitoring  
4. Reporting  
5. Machine Learning  
6. Graph Exploration

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

Use binary  data as input with shakespeare_7.0.json as binary data input for uploading data.

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

# Mapping and Indexing MovieLens Data

### Create mapping for movie document index

PUT - http://127.0.0.1:9200/movies

```json
{
	"mappings" : {
		"properties" : {
			"year" : {
				"type" : "date"
			}
		}
	}
}
```

GET - http://127.0.0.1:9200/movies/_mapping to check if the mapping is created.

