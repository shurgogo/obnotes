# elasticsearch
```bash
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.17.0
docker run --name es01-test --net elastic -p 127.0.0.1:9200:9200 -p 127.0.0.1:9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.17.0
```

# kibana
```bash
docker pull docker.elastic.co/kibana/kibana:7.17.0
docker run --name kib01-test --net elastic -p 127.0.0.1:5601:5601 -e "ELASTICSEARCH_HOSTS=http://es01-test:9200" docker.elastic.co/kibana/kibana:7.17.0
```

# filebeat
```bash
docker pull elastic/filebeat:7.5.1
docker run --name=fb01-test elastic/filebeat:7.5.1
```