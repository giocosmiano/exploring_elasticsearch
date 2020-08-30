- [Elasticsearch](https://www.elastic.co/elasticsearch/)
  - [Elasticsearch Reference](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
  - [Logstash Reference](https://www.elastic.co/guide/en/logstash/current/index.html)
  - [Kibana Reference](https://www.elastic.co/guide/en/kibana/current/index.html)

- Add these settings to `.bashrc` for personal preference

```shell script
   export ELASTIC_SEARCH_HOME="${APPLICATIONS_HOME}/elasticsearch-6.4.3"
   export ELASTIC_SEARCH_BIN="${ELASTIC_SEARCH_HOME}/bin"

   alias elasticsearch-restart='sudo systemctl restart elasticsearch.service'
   alias elasticsearch-start='sudo systemctl start elasticsearch.service'
   alias elasticsearch-stop='sudo systemctl stop elasticsearch.service'
   alias elasticsearch-status='sudo systemctl status elasticsearch.service'
   alias elasticsearch-enable='sudo systemctl enable elasticsearch.service'
   alias elasticsearch-disable='sudo systemctl disable elasticsearch.service'
    
   export KIBANA_HOME="${APPLICATIONS_HOME}/kibana-6.4.3"
   export KIBANA_BIN="${KIBANA_HOME}/bin"

   alias kibana-restart='sudo systemctl restart kibana.service'
   alias kibana-start='sudo systemctl start kibana.service'
   alias kibana-stop='sudo systemctl stop kibana.service'
   alias kibana-status='sudo systemctl status kibana.service'
   alias kibana-enable='sudo systemctl enable kibana.service'
   alias kibana-disable='sudo systemctl disable kibana.service'
    
   export LOGSTASH_HOME="${APPLICATIONS_HOME}/logstash-6.4.3"
   export LOGSTASH_BIN="${LOGSTASH_HOME}/bin"

   alias logstash-restart='sudo systemctl restart logstash.service'
   alias logstash-start='sudo systemctl start logstash.service'
   alias logstash-stop='sudo systemctl stop logstash.service'
   alias logstash-status='sudo systemctl status logstash.service'
   alias logstash-enable='sudo systemctl enable logstash.service'
   alias logstash-disable='sudo systemctl disable logstash.service'
```

- Copy `elasticsearch, kibana, logstash` services and update the `systemd` service 
```shell script
   $ sudo cp elasticsearch.service /etc/systemd/system
   $ sudo cp kibana.service /etc/systemd/system
   $ sudo cp logstash.service /etc/systemd/system
   $ sudo systemctl daemon-reload
```
- Start/Re-Start `elasticsearch, kibana, logstash` services 
```shell script
   $ elasticsearch-start
   $ kibana-start
   $ logstash-start
```

## ELK
  - [ElasticSearch `http://localhost:9200`](http://localhost:9200)
  - [Kibana `http://localhost:5601`](http://localhost:5601)
    - [Unable to access Kibana on http://MYDOMAIN.com:5601](https://discuss.elastic.co/t/unable-to-access-kibana-on-http-mydomain-com-5601/107145/14)
    - [Cannot access Kibana on port 5601](https://discuss.elastic.co/t/cannot-access-kibana-on-port-5601/174121/2)
  - [Configuring Logstash](https://www.elastic.co/guide/en/logstash/current/configuration.html)
    - [Logstash Configuration Examples](https://www.elastic.co/guide/en/logstash/current/config-examples.html)
    - [Running Logstash from the Command Line](https://www.elastic.co/guide/en/logstash/current/running-logstash-command-line.html)
    - [Logstash is not listening on port 5044](https://discuss.elastic.co/t/logstash-is-not-listening-on-port-5044/84495)

- Installing `ELK`
  - [PhoenixNAP - Get Started With Elasticsearch, Logstash, Kibana, And Beats](https://phoenixnap.com/kb/elk-stack-tutorial)
  - [PhoenixNAP - How To Install ELK stack on Ubuntu 20.04](https://phoenixnap.com/kb/how-to-install-elk-stack-on-ubuntu)
  - [PhoenixNAP - How To Install Elasticsearch on Ubuntu 20.04](https://phoenixnap.com/kb/install-elasticsearch-ubuntu)
  - [DigitalOcean - How To Install ELK Stack on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elastic-stack-on-ubuntu-20-04)
  - [DigitalOcean - How To Install/Configure Elasticsearch on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-elasticsearch-on-ubuntu-20-04)

