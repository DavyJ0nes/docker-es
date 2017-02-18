# Dockerised Elasticsearch

**To run v5.2 on Docker Machine on OSX you will need to update the max_map_count**
```
docker-machine ssh
sudo su
sysctl -w vm.max_map_count=262144
exit
exit
```
[reference](https://github.com/spujadas/elk-docker/issues/89)

## Description

This will load up a 3 node Elasticsearch cluster and Kibana. There are two versions for Elasticsearch v5.2 and v2.0

#### If you're running on OSX
- Remove .local Search Domain from Wi-Fi DNS settings. This causes delays when running docker-compose.

#### v2.0
- This version will work fine on both normal Docker and docker machine
- Haven't tested on Windows

#### v5.2
- v5.2 made some changes to how zen discovery works so need to load in custom config. Need to set network.host to specific interface and explicitly list the nodes in the cluster.
- This causes some issues in docker-machine because of file permissions when mounting local directories with docker-compose.
- There are also issues with DNS resolution in docker-compose.

## Usage Instructions

### Docker for Mac and Linux Docker
- Change to required version directory
- start cluster and Kibana with:
```
docker-compose up -d
```
- check cluster status with:
```
curl http://localhost:9200/_cat/health\?v\&h\=status,node.total,cluster
```
- Access Kibana at [http://localhost:5601](http://localhost:5601)

### Docker Machine on OSX (version 5.2)
- build docker image with name es52
```
docker build -t es52 .
```
- Run docker compose
```
docker-compose -f docker-compose.yml.dockermachine up -d
```
- check cluster status with:
```
curl http://<dockermachine_ip>:9200/_cat/health\?v\&h\=status,node.total,cluster
```
- Access Kibana at [http://dockermachine_ip:5601](http://dockermachine_ip:5601)

## License
MIT
