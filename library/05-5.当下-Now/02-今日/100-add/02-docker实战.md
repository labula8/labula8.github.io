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

Codis

docker run -d --name="codis" -h "codis" -p 18087:18087 -p 11000:11000 -p 19000:19000 ruo91/codis
docker exec codis /bin/bash codis-start all start

docker exec -it fc89e2d984f5 /bin/bash

dashboard

http://192.168.39.63:18087/admin/



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

http://blog.51cto.com/2179425/2082899

https://www.cnblogs.com/Finley/p/8595506.html
