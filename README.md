# Plain

basic functions with cache/session (redis)

```
// start your redis & config your application.properties 
mvn clean spring-boot:run
```

# with haproxy and redis cluster

```
docker-compose up
```

> Some network issues...

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

You should first build your project to generate `.jar` (with correct properties), haven't tackle with this.

```
mvn clean package
```

***

# WebPOS

The demo shows a web POS system , which replaces the in-memory product db in aw03 with a one backed by 京东.


![](jdpos.png)

To run

```shell
mvn clean spring-boot:run
```

Currently, it creates a new session for each user and the session data is stored in an in-memory h2 db. 
And it also fetches a product list from jd.com every time a session begins.

1. Build a docker image for this application and perform a load testing against it.
2. Make this system horizontally scalable by using haproxy and perform a load testing against it.
3. Take care of the **cache missing** problem (you may cache the products from jd.com) and **session sharing** problem (you may use a standalone mysql db or a redis cluster). Perform load testings.

Please **write a report** on the performance differences you notices among the above tasks.

