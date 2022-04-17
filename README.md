# Plain

basic functions with cache/session (redis)

```
// start your redis & config your application.properties 
mvn clean spring-boot:run
```

# with haproxy and redis cluster

```
# connect to host redis(not cluster): extra-hosts & change protected mode

https://stackoverflow.com/questions/19091087/open-redis-port-for-remote-connections
https://stackoverflow.com/questions/40678865/how-to-connect-to-remote-redis-server
https://stackoverflow.com/questions/48546124/what-is-linux-equivalent-of-host-docker-internal
```

redis cluster: at least 3 master. Don't know why it works :(, there was some issue between spring & redis cluster (MOVED error & CANNOT find partition). But it finally works with no reason.

```
mvn clean package
docker-compose build --no-cache
docker-compose up
```

# gatling

load testing

# dep

docker-compose:

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
docker-compose --version
```

pay attention to bridge network (related with `application.properties`)

use redis-cli:

```
redis-cli -c [-h redis1] [-p port]
> CLUSTER NODES
> keys *
> SET mykey "hello"
> get mykey
```

***


```
docker-compose up [-d] --force-recreate --renew-anon-volumes # not use old image

docker-compose pull
docker-compose up

docker-compose down -v
docker-compose build --no-cache
... should not build with cache
```

> Some network issues...

