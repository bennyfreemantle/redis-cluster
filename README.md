# Create a locally running redis cluster
A basic implmentation to spin up 6 redis nodes and connects them together as a cluster locally

## Run book

Spin up the docker container
```bash
docker-compose up -d
```

Create the redis cluster
```bash
docker exec -it redis-cluster-redis7000-1 redis-cli --cluster create redis7000:7000 redis7001:7001 redis7002:7002 redis7003:7003 redis7004:7004 redis7005:7005 --cluster-replicas 1
```

Validate its working
```bash
docker exec -it redis-cluster-redis7000-1 redis-cli -c -p 7000 cluster info
```

Test data replication
```bash
docker exec -it redis-cluster-redis7000-1 redis-cli -c -p 7000 set key value
docker exec -it redis-cluster-redis7001-1 redis-cli -c -p 7001 get key
```