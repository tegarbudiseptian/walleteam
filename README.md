###Steps:
* Install ElasticSearch and run: elasticsearch.bat
* Install Kibana and modify the kibana.yml to point the ElasticSearch:
  elasticsearch.url: "http://localhost:9200"
* Install Logstash and make a configuration file: logstash.conf
==================================
input {
  file {
    type => "java"
    path => "D:/life/antena/log/walleteam.log"
    codec => multiline {
      pattern => "^%{YEAR}-%{MONTHNUM}-%{MONTHDAY} %{TIME}.*"
      negate => "true"
      what => "previous"
    }
  }
}
 
filter {
  #If log line contains tab character followed by 'at' then we will tag that entry as stacktrace
  if [message] =~ "\tat" {
    grok {
      match => ["message", "^(\tat)"]
      add_tag => ["stacktrace"]
    }
  }
 
}
 
output {
   
  stdout {
    codec => rubydebug
  }
 
  # Sending properly parsed log events to elasticsearch
  elasticsearch {
    hosts => ["localhost:9200"]
  }
}
==================================
* Run the walleteam project to produce the log.
* Run Logstash with previous configuration: logstash -f logstash.conf
* The Logstash will retrieve the data from log file and and store it to ElasticSearch so we can visualize the log with Kibana.

###Material Source:
* [Javainuse](https://www.javainuse.com/spring/springboot-microservice-elk)
* [Youtube](https://www.youtube.com/watch?v=O5ou6lBwWYw0)

ElasticSearch: http://localhost:9200

Kibana: http://localhost:5601
