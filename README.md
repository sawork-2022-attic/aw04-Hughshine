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

```
wget https://repo1.maven.org/maven2/io/gatling/highcharts/gatling-charts-highcharts-bundle/3.7.6/gatling-charts-highcharts-bundle-3.7.6-bundle.zip
```

测试了1pos1redis/4pos1redis/4pos6redis, 分别在访问量50/500/1500的情况。运算量都在CPU可控范围内，

## 1pos1redis & 4pos1redis

发现忘记限制1pos的CPU使用了。明天早上补上。

## 4pos1redis & 4pos6redis

4pos1redis各组实验与4pos6redis区别较小（后者略微好一点，<800的比率差不多），认为可能是对单独的redis与6个redis没有做性能限制的缘故，而6redis能运用一定的多核性能，所以好一点。

![](images/4pos1redis-500.png)

![](images/4pos6redis-500.png)


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

> 不知道为什么，忽然不能wsl的localhost和win的不一致了... 再经过一个5000的访问之后

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

