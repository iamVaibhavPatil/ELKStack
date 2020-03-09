# ELK Stack

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

### Upload data to Elastic search

POST - http://127.0.0.1:9200/shakespeare/_bulk?pretty

Use binary  data as input with shakespeare_6.0.json as binary data input for uploading data.

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