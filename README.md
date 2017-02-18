# Dockerised Elasticsearch

**This will not run on boot2docker. This is because of file permissions on the config directory**

## Description

This will load up a 3 node elasticsearch cluster and kibana. There are two versions for elasticsearch v5.2 and v2.0

## Usage Instructions
- start cluster and kibana with:
```
docker-compose up -d
```
- check cluster status with:
```
curl http://localhost:9200/_cat/health\?v\&h\=status,node.total,cluster
```
- Access Kibana at [http://localhost:5601](http://localhost:5601)


## License
MIT
