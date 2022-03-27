An ELK Implementation (ElasticSearch, Logstash, Kibana) to visualize logs (e.g error log, etc) for monitoring and tracing.

#Steps:
* Install ElasticSearch and run: elasticsearch.bat
* Install Kibana and modify the kibana.yml to point the ElasticSearch:
  elasticsearch.url: "http://localhost:9200", and run: kibana.bat
* Install Logstash and make a configuration file: logstash.conf
* Run the walleteam project to produce the log.
* Run Logstash with previous configuration: logstash -f logstash.conf
* The Logstash will retrieve the data from log file and and store it to ElasticSearch so we can visualize the log with Kibana.

#Material Source:
* [Javainuse](https://www.javainuse.com/spring/springboot-microservice-elk)
* [Youtube](https://www.youtube.com/watch?v=O5ou6lBwWYw0)

ElasticSearch: http://localhost:9200

Kibana: http://localhost:5601
