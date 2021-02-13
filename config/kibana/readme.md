- [ElasticSearch `http://localhost:9200`](http://localhost:9200)
  - [Indices](http://localhost:9200/_cat/indices)
- [Kibana `http://localhost:5601`](http://localhost:5601)
- [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html)
  - [Dev Tools](https://www.elastic.co/guide/en/kibana/current/devtools-kibana.html)
  - [Plugins](https://www.elastic.co/guide/en/kibana/current/kibana-plugins.html)

- Listing all installed plugins
```shell script
   $ bin/kibana-plugin list
```

- Install a plugin e.g. `kibana-swimlane-vis`
```shell script
   $ cd $KIBANA_HOME
   $ bin/kibana-plugin install kibana-swimlane-vis
```

- Start/Re-Start `elasticsearch, kibana, logstash` services 
```shell script
   $ elasticsearch-start
   $ kibana-start
   $ logstash-start
```

- [Install Plugins On Logstash And Kibana](https://docs.bitnami.com/bch/apps/elk/configuration/install-plugins-logstash-kibana/)

