
mongoDB

docker 安装

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

service --status-all

systemctl list-unit-files
mongod.service                             disabled

systemctl enable mongod.service

## 参考

mongo docker 安装

https://www.jianshu.com/p/2181b2e27021

https://www.cnblogs.com/web424/p/6928992.html

mongoDB client

https://studio3t.com/download-thank-you/?OS=win64
https://www.cnblogs.com/charleswong/p/9545729.html

http://www.runoob.com/mongodb/mongodb-databases-documents-collections.html

https://wenku.baidu.com/view/89af7597ddccda38366baf81.html

https://www.cnblogs.com/xhyan/p/6593075.html

