# Cassandra in Docker
📅 [2020-05-01](https://arunsah.github.io/meta/changelog#2020-05-01) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Pune, India](https://en.wikipedia.org/wiki/Hinjawadi)

---
### Creating Network

```
// create network
docker network create cassandra-net
docker network rm cassandra-net
docker network ls
```

### Cassandra Nodes
```
// first node
docker run -p 9042:9042 --name cassandra-container1 --network cassandra-net -d cassandra:3

// follow up node
docker run -p 9042:9042 --name cassandra-container2 -d --network cassandra-net -e CASSANDRA_SEEDS=cassandra-container1 cassandra:3

docker run -p 9042:9042 --name cassandra-container3 -d --network cassandra-net -e CASSANDRA_SEEDS=cassandra-container1 cassandra:3

docker run -p 9042:9042 --name cassandra-container4 -d --network cassandra-net -e CASSANDRA_SEEDS=cassandra-container1 cassandra:3

// start another container for running clash
docker run -it --network cassandra-net --rm Cassandra-cli cqlsh cassandra-container
```


### Nodes List

```
# nodetool status
Datacenter: datacenter1
=======================
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address     Load       Tokens       Owns (effective)  Host ID                               Rack
UN  172.18.0.2  126.95 KiB  256          63.1%             d32f69f6-8277-45a8-9d63-32b0ed7246cf  rack1
UN  172.18.0.3  143.2 KiB  256          67.2%             649c9c40-f239-4b05-ac68-cbda22dfb6d4  rack1
UN  172.18.0.5  156.64 KiB  256          69.7%             1a59c286-ad02-4afc-baac-aee8187f7414  rack1

// [scripting - What is the best way to get a list of nodes that belong to a Cassandra cluster? - Server Fault](https://serverfault.com/a/718475)

# nodetool status | awk '/^(U|D)(N|L|J|M)/{print $2}'
172.18.0.2
172.18.0.3
172.18.0.5
# 
```


## Resources
- [Cassandra Frequently Asked Questions](https://cassandra.apache.org/doc/latest/faq/index.html)
- https://hub.docker.com/_/cassandra
