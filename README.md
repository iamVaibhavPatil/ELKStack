
### Content
https://sundog-education.com/elasticsearch/

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