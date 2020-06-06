# Redis in Docker
📅 [2020-05-01](https://arunsah.github.io/meta/changelog#2020-05-01) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Pune, India](https://en.wikipedia.org/wiki/Hinjawadi)

---

### Start a redis instance
```
$ docker run —-name redis-cache-container -d redis
// start with persistent storage
$ docker run —-name redis-cache-container -d redis redis-server —appendonly yes

// connecting via redis-cli
$ docker run -it —network some-network —rm redis redis-cli -h redis-cache-container

// Demo Command
$ docker run -p 7379:6379 --name redis-server -d redis:6.0-rc

$ docker exec -it 5e03d117ae3942146382d97a968d7ee63d4c92522d19b42054e271fb245b55e2 /bin/sh; exit
# redis-cli
127.0.0.1:6379> keys *
1) “users::1”
2) “users::2”
127.0.0.1:6379> get “users::1”
```

##### Interactive Docker Session
```
// Run the container in the following manner:
$ docker run -it -d ashok/pyashokproj bin/bash
// If you would like to attach to an already running container:
$ docker exec -it CONTAINER_ID /bin/bash
```


### References
- [Docker Hub](https://hub.docker.com/_/redis/)
- [Spring Boot Redis Cache - JournalDev](https://www.journaldev.com/18141/spring-boot-redis-cache)
- [Embedded Redis Server with Spring Boot Test - Baeldung](https://www.baeldung.com/spring-embedded-redis)
- https://hub.docker.com/_/redis/
- [Redis Cheat Sheet](https://lzone.de/cheat-sheet/Redis)
- [A Foundational Look At Cluster Architecture - Redis Labs](https://redislabs.com/redis-enterprise/technology/redis-enterprise-cluster-architecture/)
- [Scaling a High-traffic Rate Limiting Stack with Redis Cluster — Brandur Leach](https://brandur.org/redis-cluster)
