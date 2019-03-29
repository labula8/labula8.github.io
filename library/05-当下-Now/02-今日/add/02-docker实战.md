docker实战

## 概念

1. Image 镜像
    Read
    Write
2. Container 容器
3. Respository 仓库
    Public
        Docker Hub
        Docker Pool
    Private

## 安装

### CentOs7.4

```
yum install -y docker

docker pull ubuntu

Using default tag: latest
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

//启动docker服务
service docker start &

//启动docker服务
[root@localhost]~# docker ps
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

service docker start

Redirecting to /bin/systemctl start docker.service

docker pull ubuntu

Using default tag: latest
Trying to pull repository docker.io/library/ubuntu ... 
latest: Pulling from docker.io/library/ubuntu

docker images

[root@localhost ~]# ls /var/lib/docker/ -alt
总用量 8
drwx------.  2 root root    6 1月  11 17:18 tmp
drwx------.  8 root root 4096 1月  11 17:18 overlay2
drwx--x--x. 11 root root  135 1月  11 17:15 .
drwx------.  2 root root    6 1月  11 17:15 swarm
drwxr-x---.  3 root root   19 1月  11 17:15 network
drwx------.  2 root root    6 1月  11 17:15 trust
drwx------.  2 root root   25 1月  11 17:15 volumes
drwx------.  3 root root   22 1月  11 17:15 image
drwx------.  4 root root   32 1月  11 17:15 plugins
drwx------.  2 root root    6 1月  11 17:15 containers
drwxr-xr-x. 29 root root 4096 1月  11 17:12 ..

du . --max-depth=2 -h

centos7

/var/lib/docker/overlay2/7f2fe07a52b6ac89b044cf368054e8e9ef6438882bde8be2d3fd04b373d78ebe

//运行一个centos docker
docker run -it centos

[root@a2d78a4b5f3b /]# df -h
Filesystem               Size  Used Avail Use% Mounted on
overlay                   37G   15G   23G  40% /
tmpfs                    920M     0  920M   0% /dev
tmpfs                    920M     0  920M   0% /sys/fs/cgroup
/dev/mapper/centos-root   37G   15G   23G  40% /etc/hosts
shm                       64M     0   64M   0% /dev/shm
tmpfs                    920M     0  920M   0% /proc/acpi
tmpfs                    920M     0  920M   0% /proc/scsi
tmpfs                    920M     0  920M   0% /sys/firmware


[root@localhost ~]# docker images

/来源              /标签                 /镜像ID             /创建时间         /镜像大小
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/ubuntu    latest              1d9c17228a9e        13 days ago         86.7 MB
docker.io/centos    latest              1e1148e4cc2c        5 weeks ago         202 MB

[root@localhost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker.io/ubuntu    latest              1d9c17228a9e        13 days ago         86.7 MB
docker.io/centos    latest              1e1148e4cc2c        5 weeks ago         202 MB
[root@localhost ~]# docker tag docker.io/centos  docker.io/centos-7.6.1810 
[root@localhost ~]# docker images
REPOSITORY                  TAG                 IMAGE ID            CREATED             SIZE
docker.io/ubuntu            latest              1d9c17228a9e        13 days ago         86.7 MB
docker.io/centos-7.6.1810   latest              1e1148e4cc2c        5 weeks ago         202 MB
docker.io/centos            latest              1e1148e4cc2c        5 weeks ago         202 MB

//src, 源镜像名, dest, 新镜像名
docker tag src dest

docker inspect 1e1148e4cc2c

docker inspect centos

docker inspect 1e1148e4cc2c -f {{".RepoTags"}}

[root@localhost ~]# docker search mysql
INDEX       NAME                                                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
docker.io   docker.io/mysql                                                  MySQL is a widely used, open-source relati...   7662      [OK]       
docker.io   docker.io/mariadb                                                MariaDB is a community-developed fork of M...   2505      [OK]       
docker.io   docker.io/mysql/mysql-server                                     Optimized MySQL Server Docker images. Crea...   580                  [OK]
docker.io   docker.io/zabbix/zabbix-server-mysql                             Zabbix Server with MySQL database support       159                  [OK]
docker.io   docker.io/hypriot/rpi-mysql                                      RPi-compatible Docker Image with Mysql          104                  
docker.io   docker.io/zabbix/zabbix-web-nginx-mysql                          Zabbix frontend based on Nginx web-server ...   84                   [OK]
docker.io   docker.io/centurylink/mysql                                      Image containing mysql. Optimized to be li...   60                   [OK]
docker.io   docker.io/1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5   ubuntu-16-nginx-php-phpmyadmin-mysql-5          48                   [OK]
docker.io   docker.io/centos/mysql-57-centos7                                MySQL 5.7 SQL database server                   45                   
docker.io   docker.io/mysql/mysql-cluster                                    Experimental MySQL Cluster Docker images. ...   39                   
docker.io   docker.io/tutum/mysql                                            Base docker image to run a MySQL database ...   31                   
docker.io   docker.io/bitnami/mysql                                          Bitnami MySQL Docker Image                      23                   [OK]
docker.io   docker.io/schickling/mysql-backup-s3                             Backup MySQL to S3 (supports periodic back...   23                   [OK]
docker.io   docker.io/zabbix/zabbix-proxy-mysql                              Zabbix proxy with MySQL database support        19                   [OK]
docker.io   docker.io/linuxserver/mysql                                      A Mysql container, brought to you by Linux...   18                   
docker.io   docker.io/centos/mysql-56-centos7                                MySQL 5.6 SQL database server                   12                   
docker.io   docker.io/circleci/mysql                                         MySQL is a widely used, open-source relati...   9                    
docker.io   docker.io/mysql/mysql-router                                     MySQL Router provides transparent routing ...   8                    
docker.io   docker.io/openshift/mysql-55-centos7                             DEPRECATED: A Centos7 based MySQL v5.5 ima...   6                    
docker.io   docker.io/dsteinkopf/backup-all-mysql                            backup all DBs in a mysql server                5                    [OK]
docker.io   docker.io/openzipkin/zipkin-mysql                                Mirror of https://quay.io/repository/openz...   2                    
docker.io   docker.io/jelastic/mysql                                         An image of the MySQL database server main...   1                    
docker.io   docker.io/ansibleplaybookbundle/mysql-apb                        An APB which deploys RHSCL MySQL                0                    [OK]
docker.io   docker.io/cloudfoundry/cf-mysql-ci                               Image used in CI of cf-mysql-release            0                    
docker.io   docker.io/cloudposse/mysql                                       Improved `mysql` service with support for ...   0                    [OK]

# docker pull : 从镜像仓库中拉取或者更新指定镜像

docker search mysql --filter=stars=100


[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
a2d78a4b5f3b        centos              "/bin/bash"         23 minutes ago      Up 23 minutes                           distracted_dijkstra

[root@localhost ~]# docker commit -m "add a new file" -a "Docker Newbee" a2d78a4b5f3b centos7-test
sha256:06fc3befc2f9c2155742facdea12ab8e488bf4f983dd21e2a4178cb3033dc11c

//启动变更后的测试镜像
 docker run -it centos7-test

//保存，导出，定制镜像
docker save -o centos7-test.tar centos7-test

[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
4828244c2c63        centos7-test        "/bin/bash"         7 minutes ago       Up 6 minutes                            condescending_wescoff
a2d78a4b5f3b        centos              "/bin/bash"         33 minutes ago      Up 33 minutes                           distracted_dijkstra
[root@localhost ~]# docker stop a2d78a4b5f3b
a2d78a4b5f3b
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
4828244c2c63        centos7-test        "/bin/bash"         7 minutes ago       Up 7 minutes                            condescending_wescoff

[root@localhost ~]# docker ps -a -q
4828244c2c63
a2d78a4b5f3b

//多终端会同步显示
[root@localhost ~]# docker attach 4828244c2c63
[root@4828244c2c63 home]# 

//进入某个已启动容器
[root@localhost]~# docker ps
CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS              PORTS                                                                                                                                NAMES
1c5825b51463        sequenceiq/hadoop-docker   "/etc/bootstrap.sh..."   22 minutes ago      Up 22 minutes       2122/tcp, 8030-8033/tcp, 8040/tcp, 8042/tcp, 8088/tcp, 19888/tcp, 49707/tcp, 50010/tcp, 50020/tcp, 50070/tcp, 50075/tcp, 50090/tcp   hadoop
[root@localhost]~# docker exec -it 1c5825b51463 /bin/bash 

[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
4828244c2c63        centos7-test        "/bin/bash"         12 minutes ago      Up 12 minutes                           condescending_wescoff
[root@localhost ~]# docker exec -it 4828244c2c63 /bin/bash
[root@4828244c2c63 /]# 

[root@localhost ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                       PORTS               NAMES
4828244c2c63        centos7-test        "/bin/bash"         15 minutes ago      Up 15 minutes                                    condescending_wescoff
a2d78a4b5f3b        centos              "/bin/bash"         41 minutes ago      Exited (137) 7 minutes ago                       distracted_dijkstra

yum list|grep gcc

yum install -y gcc-c++

yum -y install vim

//保存镜像
[root@localhost ~]# docker commit -m "update centos7-test" -a "docker update" 4828244c2c63 centos7-test
sha256:d09b60dada8bf04c42ccbc682cf9757a7c3b44c189d9056a5e7af31926a381dc

dockerfile 

docker search busybox

yum -y install openssh-server

mkdir /var/run/sshd

/usr/sbin/sshd -D &

[root@localhost]~# docker search mongodb
INDEX       NAME                                                   DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
docker.io   docker.io/mongo                                        MongoDB document databases provide high av...   5582      [OK]       
docker.io   docker.io/mongo-express                                Web-based MongoDB admin interface, written...   383       [OK]       
docker.io   docker.io/tutum/mongodb                                MongoDB Docker image – listens in port 270...   224                  [OK]
docker.io   docker.io/bitnami/mongodb                              Bitnami MongoDB Docker Image                    82                   [OK]
docker.io   docker.io/percona/percona-server-mongodb               Percona Server for MongoDB docker images        23                   
docker.io   docker.io/frodenas/mongodb                             A Docker Image for MongoDB                      17                   [OK]
docker.io   docker.io/centos/mongodb-26-centos7                    MongoDB NoSQL database server                   5                    
docker.io   docker.io/centos/mongodb-32-centos7                    MongoDB NoSQL database server                   5                    
docker.io   docker.io/centos/mongodb-36-centos7                    MongoDB NoSQL database server                   4                    
docker.io   docker.io/eses/mongodb_exporter                        mongodb exporter for prometheus                 4                    [OK]
docker.io   docker.io/quadstingray/mongodb                         MongoDB with Memory and User Settings           3                    [OK]
docker.io   docker.io/bigtruedata/php-mongodb                      PHP image with MongoDB support                  2                    [OK]
docker.io   docker.io/neowaylabs/mongodb-mms-agent                 This Docker image with MongoDB Monitoring ...   2                    [OK]
docker.io   docker.io/tozd/mongodb                                 Base image for MongoDB server.                  2                    [OK]
docker.io   docker.io/centos/mongodb-34-centos7                    MongoDB NoSQL database server                   1                    
docker.io   docker.io/nuxeoapbcatalog/nuxeo-mongodb-apb            MongoDB deployment for Nuxeo                    1                    [OK]
docker.io   docker.io/openshift/mongodb-24-centos7                 DEPRECATED: A Centos7 based MongoDB v2.4 i...   1                    
docker.io   docker.io/perconalab/percona-server-mongodb-operator   MOVED TO https://hub.docker.com/r/perconal...   1                    
docker.io   docker.io/webhippie/mongodb                            Docker images for mongodb                       1                    [OK]
docker.io   docker.io/ansibleplaybookbundle/mongodb-apb            An APB to deploy MongoDB.                       0                    [OK]
docker.io   docker.io/gebele/mongodb                               mongodb                                         0                    [OK]
docker.io   docker.io/mongodbsap/mongodbdocker                                                                     0                    
docker.io   docker.io/phenompeople/mongodb                          MongoDB is an open-source, document datab...   0                    [OK]
docker.io   docker.io/targetprocess/mongodb_exporter               MongoDB exporter for prometheus                 0                    [OK]
docker.io   docker.io/xogroup/mongodb_backup_gdrive                Docker image to create a MongoDB database ...   0                    [OK]

# 启动docker-mongo服务
docker run -it docker.io/mongo bash

cat /etc/issue

apt-get update
apt-get install net-tools

root@ccbb593cfa86:/data# mongo -version
MongoDB shell version v4.0.6
git version: caa42a1f75a56c7643d0b68d3880444375ec42e3
OpenSSL version: OpenSSL 1.0.2g  1 Mar 2016
allocator: tcmalloc
modules: none
build environment:
    distmod: ubuntu1604
    distarch: x86_64
    target_arch: x86_64

//保存镜像
[root@localhost ~]# docker commit -m "update ubuntu-mongo-test" -a "docker update" ccbb593cfa86 ubuntu-mongo-test

docker run -d -p 27017:27017 -v mongo_configdb:/data/configdb -v mongo_db:/data/db -it ubuntu-mongo-test bash



docker exec -it 246cf050d68b /bin/bash

cat /etc/issue
Ubuntu 16.04.5 LTS \n \l

# Codis

docker run -d --name="codis-master-yu1" -h "codis" -p 18087:18087 -p 11000:11000 -p 19000:19000 codis-master-yu


docker run -d --name="codis" -h "codis" -p 18087:18087 -p 11000:11000 -p 19000:19000 ruo91/codis
docker exec codis /bin/bash codis-start all start

docker exec -it fc89e2d984f5 /bin/bash


codis-start all start&

dashboard

http://192.168.39.63:18087/admin/

http://192.168.56.103:18087/admin/



whereis codis-server
codis-server: /opt/codis/bin/codis-server

#install redis-2.8.21

wget -c http://download.redis.io/releases/redis-2.8.21.tar.gz

tar xzf redis-2.8.21.tar.gz

make -j8

make install

whereis redis-server
redis-server: /usr/local/bin/redis-server

redis-cli -p 19000


[root@localhost]/usr/local/bin# redis-benchmark -n 10000 -q -p 19000
PING_INLINE: 14970.06 requests per second
PING_BULK: 18018.02 requests per second
SET: 15898.25 requests per second
GET: 16835.02 requests per second
INCR: 16666.67 requests per second
LPUSH: 17331.02 requests per second
LPOP: 17301.04 requests per second
SADD: 14124.29 requests per second
SPOP: 12468.83 requests per second
LPUSH (needed to benchmark LRANGE): 16611.29 requests per second
LRANGE_100 (first 100 elements): 10570.83 requests per second
LRANGE_300 (first 300 elements): 6309.15 requests per second
LRANGE_500 (first 450 elements): 4384.04 requests per second
LRANGE_600 (first 600 elements): 3541.08 requests per second
MSET (10 keys): 10548.52 requests per second


[root@localhost]/usr/local/bin# redis-benchmark -n 100000 -q -p 19000
PING_INLINE: 16173.38 requests per second
PING_BULK: 17301.04 requests per second
SET: 15124.02 requests per second
GET: 16669.45 requests per second
INCR: 16225.86 requests per second
LPUSH: 16761.65 requests per second
LPOP: 17256.26 requests per second
SADD: 16686.13 requests per second
SPOP: 17082.34 requests per second
LPUSH (needed to benchmark LRANGE): 16934.80 requests per second
LRANGE_100 (first 100 elements): 10458.06 requests per second
LRANGE_300 (first 300 elements): 6243.76 requests per second
LRANGE_500 (first 450 elements): 4463.69 requests per second
LRANGE_600 (first 600 elements): 3495.77 requests per second
MSET (10 keys): 10275.38 requests per second

docker run -d --name="codis-yu" -h "codis" -p 28087:28087 -p 21000:21000 -p 29000:29000 codis-yu

/usr/bin/docker-current: Error response from daemon: Conflict. The container name "/codis" is already in use by container 4b1409fb8ab6875786bad3f148b4aa017a3c6d8a8ea3fa19ddeb570488adfc40. You have to remove (or rename) that container to be able to reuse that name..
See '/usr/bin/docker-current run --help'.

docker commit -m "update codis-yu" -a "docker update" 4b1409fb8ab6 codis-yu

 apt-get update
 apt-get install vim

# Zookeepser 配置

echo ruok | nc localhost 2181

java -version
java version "1.7.0_79"
OpenJDK Runtime Environment (IcedTea 2.5.5) (7u79-2.5.5-0ubuntu0.14.04.2)
OpenJDK 64-Bit Server VM (build 24.79-b02, mixed mode)

egrep -v "^#|^$" zoo.cfg


```
java -Dzookeeper.log.dir=. -Dzookeeper.root.logger=INFO,CONSOLE -cp /opt/zookeeper/bin/../build/classes:/opt/zookeeper/bin/../build/lib/*.jar:/opt/zookeeper/bin/../lib/slf4j-log4j12-1.6.1.jar:/opt/zookeeper/bin/../lib/slf4j-api-1.6.1.jar:/opt/zookeeper/bin/../lib/netty-3.7.0.Final.jar:/opt/zookeeper/bin/../lib/log4j-1.2.16.jar:/opt/zookeeper/bin/../lib/jline-0.9.94.jar:/opt/zookeeper/bin/../zookeeper-3.4.6.jar:/opt/zookeeper/bin/../src/java/lib/*.jar:/opt/zookeeper/bin/../conf: -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.local.only=false org.apache.zookeeper.server.quorum.QuorumPeerMain /opt/zookeeper/bin/../conf/zoo.cfg
```


/opt/zookeeper/bin

./zkServer.sh status 

./zkServer.sh restart



root@codis:/opt/zookeeper/bin# netstat -anp | grep 172.17.0
tcp6       0      0 172.17.0.3:2888         :::*                    LISTEN      628/java        
tcp6       0      0 172.17.0.3:3888         :::*                    LISTEN      628/java        
tcp6       0      0 172.17.0.3:58654        172.17.0.2:3888         ESTABLISHED 628/java        
tcp6       0      0 172.17.0.3:2888         172.17.0.2:58394        ESTABLISHED 628/java       


./zkCli.sh -server 172.17.0.2:2181
Connecting to 172.17.0.2:2181
2019-03-26 08:25:59,396 [myid:] - INFO  [main:Environment@100] - Client environment:zookeeper.version=3.4.6-1569965, built on 02/20/2014 09:09 GMT
2019-03-26 08:25:59,401 [myid:] - INFO  [main:Environment@100] - Client environment:host.name=codis
2019-03-26 08:25:59,401 [myid:] - INFO  [main:Environment@100] - Client environment:java.version=1.7.0_79
2019-03-26 08:25:59,405 [myid:] - INFO  [main:Environment@100] - Client environment:java.vendor=Oracle Corporation
2019-03-26 08:25:59,405 [myid:] - INFO  [main:Environment@100] - Client environment:java.home=/usr/lib/jvm/java-7-openjdk-amd64/jre
2019-03-26 08:25:59,405 [myid:] - INFO  [main:Environment@100] - Client environment:java.class.path=/opt/zookeeper/bin/../build/classes:/opt/zookeeper/bin/../build/lib/*.jar:/opt/zookeeper/bin/../lib/slf4j-log4j12-1.6.1.jar:/opt/zookeeper/bin/../lib/slf4j-api-1.6.1.jar:/opt/zookeeper/bin/../lib/netty-3.7.0.Final.jar:/opt/zookeeper/bin/../lib/log4j-1.2.16.jar:/opt/zookeeper/bin/../lib/jline-0.9.94.jar:/opt/zookeeper/bin/../zookeeper-3.4.6.jar:/opt/zookeeper/bin/../src/java/lib/*.jar:/opt/zookeeper/bin/../conf:
2019-03-26 08:25:59,405 [myid:] - INFO  [main:Environment@100] - Client environment:java.library.path=/usr/java/packages/lib/amd64:/usr/lib/x86_64-linux-gnu/jni:/lib/x86_64-linux-gnu:/usr/lib/x86_64-linux-gnu:/usr/lib/jni:/lib:/usr/lib
2019-03-26 08:25:59,406 [myid:] - INFO  [main:Environment@100] - Client environment:java.io.tmpdir=/tmp
2019-03-26 08:25:59,406 [myid:] - INFO  [main:Environment@100] - Client environment:java.compiler=<NA>
2019-03-26 08:25:59,407 [myid:] - INFO  [main:Environment@100] - Client environment:os.name=Linux
2019-03-26 08:25:59,407 [myid:] - INFO  [main:Environment@100] - Client environment:os.arch=amd64
2019-03-26 08:25:59,407 [myid:] - INFO  [main:Environment@100] - Client environment:os.version=3.10.0-693.2.2.el7.x86_64
2019-03-26 08:25:59,407 [myid:] - INFO  [main:Environment@100] - Client environment:user.name=root
2019-03-26 08:25:59,407 [myid:] - INFO  [main:Environment@100] - Client environment:user.home=/root
2019-03-26 08:25:59,408 [myid:] - INFO  [main:Environment@100] - Client environment:user.dir=/opt/zookeeper/bin
2019-03-26 08:25:59,410 [myid:] - INFO  [main:ZooKeeper@438] - Initiating client connection, connectString=172.17.0.2:2181 sessionTimeout=30000 watcher=org.apache.zookeeper.ZooKeeperMain$MyWatcher@3e5a0cf
Welcome to ZooKeeper!
2019-03-26 08:25:59,481 [myid:] - INFO  [main-SendThread(172.17.0.2:2181):ClientCnxn$SendThread@975] - Opening socket connection to server 172.17.0.2/172.17.0.2:2181. Will not attempt to authenticate using SASL (unknown error)
JLine support is enabled
2019-03-26 08:25:59,499 [myid:] - INFO  [main-SendThread(172.17.0.2:2181):ClientCnxn$SendThread@852] - Socket connection established to 172.17.0.2/172.17.0.2:2181, initiating session
2019-03-26 08:25:59,528 [myid:] - INFO  [main-SendThread(172.17.0.2:2181):ClientCnxn$SendThread@1235] - Session establishment complete on server 172.17.0.2/172.17.0.2:2181, sessionid = 0x169b919fa760002, negotiated timeout = 30000

WATCHER::

WatchedEvent state:SyncConnected type:None path:null
[zk: 172.17.0.2:2181(CONNECTED) 0] ls /
[zk, zookeeper]
[zk: 172.17.0.2:2181(CONNECTED) 1] ls /
[zk, zookeeper]
[zk: 172.17.0.2:2181(CONNECTED) 2] ls /
[zk, zookeeper]
[zk: 172.17.0.2:2181(CONNECTED) 3] ls /
[zk, zookeeper]
[zk: 172.17.0.2:2181(CONNECTED) 4] ls /
[zk, zookeeper]
[zk: 172.17.0.2:2181(CONNECTED) 5] ls /
[zk, zookeeper]
[zk: 172.17.0.2:2181(CONNECTED) 6] quit
Quitting...
2019-03-26 08:27:05,480 [myid:] - INFO  [main:ZooKeeper@684] - Session: 0x169b919fa760002 closed
2019-03-26 08:27:05,481 [myid:] - INFO  [main-EventThread:ClientCnxn$EventThread@512] - EventThread shut down

docker commit -m "update codis-yu" -a "docker update" b09dc76a3f87 codis-yu

docker commit -m "update codis-master-yu" -a "docker update" 682a30a8af2c codis-master-yu

# 单独启动 codis-server


/opt/codis/conf

cat config.ini
zk=localhost:2181  //zookeeper的地址, 如果是zookeeper集群，可以这么写: zk=hostname1:2181,hostname2:2181,hostname3:2181,hostname4:2181,hostname5:2181,如果是etcd，则写成http://hostname1:port,http://hostname2:port,http://hostname3:port
product=test     //产品名称, 这个codis集群的名字, 可以认为是命名空间, 不同命名空间的codis没有交集
proxy_id=proxy_1  //proxy会读取, 用于标记proxy的名字, 针对多个proxy的情况, 可以使用不同的config.ini, 只需要更改 proxy_id 即可
net_timeout=5     //检测状态时间间隔
dashboard_addr=localhost:18087  //dashboard 服务的地址，CLI 的所有命令都依赖于 dashboard 的 RESTful API，所以必须启动
coordinator=zookeeper   //如果用etcd，则将zookeeper替换为etcd

cat usage.md 
0. start zookeeper       //启动zookeeper服务
1. change config items in config.ini  //修改codis配置文件
2. ./start_dashboard.sh  //启动 dashboard
3. ./start_redis.sh      //启动redis实例
4. ./add_group.sh        //添加redis组，一个redis组只能有一个master
5. ./initslot.sh         //初始化槽
6. ./start_proxy.sh      //启动proxy
7. ./set_proxy_online.sh  //上线proxy项目
8. open browser to http://localhost:18087/admin //访问web

#docker 重启

docker kill b09dc76a3f87


然后列出所有的容器 ID：

docker ps -a -q
删除前应该停止所有的容器：

docker stop $(docker ps -a -q)
批量删除tag为"<none>"镜像可以采用如下方法（下面两种方式均可以）：

docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
docker images | grep none | awk '{print $3}' | xargs docker rmi

# 删除 <none> 容器
docker images | grep none | awk '{print $3}' | xargs docker rmi

# 强制删除 <none> 容器
docker rmi -f fe93266bcf95 




```
/opt/codis/bin/codis-start all start &

root@codis:/opt/codis/bin# ./codis-start all start
Dashboard start...
done
Redis start...
done
Add group start...
add group 1 with a master (localhost:6380), Notice: do not use localhost when in produciton
{
  "msg": "OK",
  "ret": 0
}
add group 2 with a master (localhost:6381), Notice: do not use localhost when in produciton
{
  "msg": "OK",
  "ret": 0
}
add group 3 with a master (localhost:6382), Notice: do not use localhost when in produciton
{
  "msg": "OK",
  "ret": 0
}
add group 4 with a master (localhost:6383), Notice: do not use localhost when in produciton
{
  "msg": "OK",
  "ret": 0
}
done
slots initializing...
{
  "msg": "OK",
  "ret": 0
}
done

set slot ranges to server groups...
{
  "msg": "OK",
  "ret": 0
}
{
  "msg": "OK",
  "ret": 0
}
{
  "msg": "OK",
  "ret": 0
}
{
  "msg": "OK",
  "ret": 0
}
done
shut down proxy_1...
{
  "msg": "OK",
  "ret": 0
}
done

start new proxy...
done

sleep 3s..

  _____  ____    ____/ /  (_)  _____
 / ___/ / __ \  / __  /  / /  / ___/
/ /__  / /_/ / / /_/ /  / /  (__  )
\___/  \____/  \__,_/  /_/  /____/

set proxy_1 online
{
  "msg": "OK",
  "ret": 0
}
done

cat /tmp/zookeeper/myid 
2

./zkCli.sh -server 127.0.0.1:2181

rmr /zk/codis/db_test/dashboard
rmr /zk/codis/db_test/proxy

 cat zoo.cfg
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/tmp/zookeeper

clientPort=2181

server.1=172.17.0.2:2888:3888
server.2=172.17.0.3:2888:3888


./codis-start redis start

./codis-start proxy start


/usr/lib/zookeeper/bin/zkServer.sh start

nc -v -w 10 -z 127.0.0.1 2181


/usr/lib/zookeeper/bin/zkCli.sh -server 127.0.0.1:2181

/opt/codis/bin/codis-config -c /etc/codis/config.ini dashboard &

/opt/codis/bin/codis-config -c /etc/codis/config.ini slot init &


```











































############################################
[root@localhost]~# docker images
REPOSITORY                           TAG                 IMAGE ID            CREATED             SIZE
ubuntu-gitlab-yu                     latest              94b2bc062a30        3 weeks ago         1.62 GB
alpine-micro-yu                      latest              63e620ada1d9        3 weeks ago         705 MB
ubuntu-mongo-test                    latest              5014190b1f07        3 weeks ago         420 MB
docker.io/gitlab/gitlab-ce           latest              991cd608c116        4 weeks ago         1.59 GB
docker.io/mongo                      latest              0da05d84b1fe        5 weeks ago         394 MB
hadoop-docker-yu                     latest              a326d90ae97b        6 weeks ago         1.86 GB
ubuntu-test                          latest              a3aa3469f66c        2 months ago        87.1 MB
centos7-test                         latest              d09b60dada8b        2 months ago        399 MB
docker.io/ubuntu                     latest              1d9c17228a9e        2 months ago        86.7 MB
docker.io/centos-7.6.1810            latest              1e1148e4cc2c        3 months ago        202 MB
docker.io/centos                     latest              1e1148e4cc2c        3 months ago        202 MB
docker.io/beginor/gitlab-ce          11.3.0-ce.0         e25023de3746        5 months ago        1.62 GB
docker.io/whai/gomicrodevelop        latest              b70bbd3e32cf        8 months ago        700 MB
docker.io/google/golang              latest              09ec5b5ecced        3 years ago         665 MB
docker.io/sequenceiq/hadoop-docker   latest              5c3cc170c6bc        3 years ago         1.77 GB


docker run -it centos7-test


#多开终端
docker exec -it b4335d463a06 /bin/bash



#install go1.8.5

wget -c https://dl.google.com/go/go1.8.5.linux-amd64.tar.gz

参考      https://www.cnblogs.com/chy123/p/6750347.html

#install codis3.2.2-go1.8.5-linux.tar.gz

wget -c https://github.com/CodisLabs/codis/releases/download/3.2.2/codis3.2.2-go1.8.5-linux.tar.gz

参考      https://blog.csdn.net/lylclz/article/details/78570687

https://github.com/CodisLabs/codis/blob/release3.2/doc/tutorial_zh.md

#install redis

wget -c http://download.redis.io/releases/redis-3.2.8.tar.gz

```


## 应用

## 参考

https://www.cnblogs.com/renpingsheng/p/7845096.html

https://www.cnblogs.com/xhyan/p/6593075.html

https://www.cnblogs.com/jie-fang/p/7920863.html

gitlab

https://github.com/ruo91/docker-codis

http://blog.51cto.com/2179425/2082899

https://www.cnblogs.com/Finley/p/8595506.html

Zookeeper集群搭建

https://www.cnblogs.com/linuxprobe/p/5851699.html

https://www.cnblogs.com/xmzncc/p/6218694.html

https://blog.51cto.com/liweizhong/1639918

https://blog.csdn.net/zyx_ly/article/details/84726509 

https://www.cnblogs.com/liangsky/p/5458659.html

https://blog.51cto.com/navyaijm/1637688