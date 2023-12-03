Advanced search in Elasticsearch often involves using the Query DSL (Domain Specific Language) to construct more complex queries. Here are some advanced search examples using various query types in Elasticsearch:

### Match Query:
```bash
curl -X GET "localhost:9200/my_index/_search" -H 'Content-Type: application/json' -d '{
  "query": {
    "match": {
      "content": "Elasticsearch"
    }
  }
}'
```
This searches for documents in the "my_index" index where the "content" field contains the term "Elasticsearch."

### Multi-Match Query:
```bash
curl -X GET "localhost:9200/my_index/_search" -H 'Content-Type: application/json' -d '{
  "query": {
    "multi_match": {
      "query": "search engine",
      "fields": ["title", "content"]
    }
  }
}'
```
This searches for documents where either the "title" or "content" fields contain the terms "search" or "engine."

### Bool Query (Combining Conditions):
```bash
curl -X GET "localhost:9200/my_index/_search" -H 'Content-Type: application/json' -d '{
  "query": {
    "bool": {
      "must": [
        { "match": { "content": "Elasticsearch" }},
        { "range": { "publish_date": { "gte": "2022-01-01" }}}
      ],
      "must_not": [
        { "term": { "status": "archived" }}
      ],
      "should": [
        { "term": { "author": "John" }},
        { "term": { "author": "Jane" }}
      ]
    }
  }
}'
```
This is a boolean query combining multiple conditions. It must match documents containing "Elasticsearch" and published after a certain date, should match documents with authors "John" or "Jane," and must not match documents with a "status" of "archived."

### Range Query:
```bash
curl -X GET "localhost:9200/my_index/_search" -H 'Content-Type: application/json' -d '{
  "query": {
    "range": {
      "price": {
        "gte": 20,
        "lte": 50
      }
    }
  }
}'
```
This searches for documents where the "price" field is between 20 and 50.

### Wildcard Query:
```bash
curl -X GET "localhost:9200/my_index/_search" -H 'Content-Type: application/json' -d '{
  "query": {
    "wildcard": {
      "title.keyword": "el*"
    }
  }
}'
```
This searches for documents where the "title.keyword" field matches the wildcard pattern "el*."

### Fuzzy Query:
```bash
curl -X GET "localhost:9200/my_index/_search" -H 'Content-Type: application/json' -d '{
  "query": {
    "fuzzy": {
      "title": {
        "value": "quick",
        "fuzziness": "AUTO"
      }
    }
  }
}'
```
This performs a fuzzy search for documents where the "title" field is similar to "quick" with automatic fuzziness.

As you explore, refer to the [official Elasticsearch Query DSL documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html) for in-depth information on constructing complex queries.
