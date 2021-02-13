- [ElasticSearch `http://localhost:9200`](http://localhost:9200)
    - [Indices](http://localhost:9200/_cat/indices)
    - [`uszips_index - mapping`](http://localhost:9200/uszips_index)
    - [`uszips_index - data`](http://localhost:9200/uszips_index/_search)
- [Kibana `http://localhost:5601`](http://localhost:5601)
- [Logstash](https://www.elastic.co/guide/en/logstash/current/index.html)
  - [Input Plugins](https://www.elastic.co/guide/en/logstash/current/input-plugins.html)
    - [Elastic](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-elasticsearch.html)
    - [Jdbc](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-jdbc.html)
    - [File](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-file.html)  
    - [Kafka](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-kafka.html) 
  - [Output Plugins](https://www.elastic.co/guide/en/logstash/current/output-plugins.html)
    - [Elastic](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-elasticsearch.html)
    - [File](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-file.html)  
    - [Kafka](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-kafka.html)  
    - [Mongo](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-mongodb.html)  
  - [Filter Plugins](https://www.elastic.co/guide/en/logstash/current/filter-plugins.html)
    - [`elasticsearch`](https://www.elastic.co/guide/en/logstash/current/plugins-filters-elasticsearch.html)
    - [`mutate`](https://www.elastic.co/guide/en/logstash/current/plugins-filters-mutate.html)
    - [`csv`](https://www.elastic.co/guide/en/logstash/current/plugins-filters-csv.html)

- Listing all installed plugins
```shell script
   $ bin/logstash-plugin list
```

- Install a plugin e.g. `logstash-filter-uuid`
```shell script
   $ cd $LOGSTASH_HOME
   $ bin/logstash-plugin install logstash-filter-uuid
```

- Start/Re-Start `elasticsearch, kibana, logstash` services 
```shell script
   $ elasticsearch-start
   $ kibana-start
   $ logstash-start
```

- Some useful references
  - [Install Plugins On Logstash And Kibana](https://docs.bitnami.com/bch/apps/elk/configuration/install-plugins-logstash-kibana/)
  - [Using Logstash to help create an Elasticsearch mapping template](https://www.elastic.co/blog/logstash_lesson_elasticsearch_mapping)
  - [How to set an Elasticsearch output template in Logstash](https://stackoverflow.com/questions/49720821/how-to-set-an-elasticsearch-output-template-in-logstash)
  - [Monitoring Logstash Pipelines](https://logz.io/blog/logstash-pipelines/)  
  - [Common Logstash Use cases with GROK, JSON and Mutate filters](https://itnext.io/common-logstash-use-cases-with-grok-json-and-mutate-filters-elk-logstash-in-docker-filebeat-871ed58c7651)
  - [Using the Mutate Filter in Logstash](https://logz.io/blog/logstash-mutate-filter/)
  - [5 Logstash Filter Plugins You Need to Know About](https://logz.io/blog/5-logstash-filter-plugins/)  
  - [Logstash make a copy a nested field with mutate.add_field](https://stackoverflow.com/questions/39124087/logstash-make-a-copy-a-nested-field-with-mutate-add-field)

- Deleting an ES index via command line
```shell script
  $ curl -XDELETE http://localhost:9200/uszips_index?pretty
```

- Deleting an ES index via Kibana console
```shell
  DELETE /uszips_index
```

- How to load `uszips.csv` to `elastic`, as csv input, via `logstash`
```shell script
  $ cd ~/Documents/_projects/exploring_elasticsearch/config/logstash/resources
  $ cat uszips.csv | logstash -f uszips_csv.conf
```

- How to load `uszips_csv_index` to `elastic`, as elastic input, via `logstash`
```shell script
  $ cd ~/Documents/_projects/exploring_elasticsearch/config/logstash/resources
  $ logstash -f uszips_elastic.conf
```

- Kibana GEO location query with 5-mile radius distance from zip 14618
```json
GET /uszips_index/_search
{
  "query": {
    "bool": {
      "must": {
        "match_all" : {}
      },
      "filter": {
        "geo_distance": {
          "distance": "5mi",
          "geo_location": {
            "lat": 43.113,
            "lon": -77.55536
          }
        }
      }
    }
  }
}
```

- Kibana GEO location bounded box query with top_left=14622 and bottom_right=14618
```json
GET /uszips_index/_search
{
  "query": {
    "bool": {
      "must": {
        "match_all": {}
      },
      "filter": {
        "geo_bounding_box": {
          "geo_location": {
            "bottom_right": {
              "lat": 43.113,
              "lon": -77.55536
            },
            "top_left": {
              "lat": 43.21386,
              "lon": -77.55399
            }
          }
        }
      }
    }
  }
}
```

- Kibana GEO location polygon query with zip 14618, 14622, 14626
```json
GET /uszips_index/_search
{
  "query": {
    "bool": {
      "must": {
        "match_all" : {}
      },
      "filter": {
        "geo_polygon": {
          "geo_location": {
            "points": [
              { "lat": 43.113, "lon": -77.55536 },
              { "lat": 43.21386, "lon": 77.55399 },
              { "lat": 43.2143, "lon": -77.71383 }
            ]
          }
        }
      }
    }
  }
}
```














