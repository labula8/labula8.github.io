# CacheCloud

## 安装

mysql

/opt/cachecloud-web

CREATE TABLE `machine_info` (
  `id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT '机器的id',
  `ssh_user` varchar(20) COLLATE utf8_bin NOT NULL DEFAULT 'cachecloud' COMMENT 'ssh用户',
  `ssh_passwd` varchar(20) COLLATE utf8_bin NOT NULL DEFAULT 'cachecloud' COMMENT 'ssh密码',
  `ip` varchar(16) COLLATE utf8_bin NOT NULL COMMENT 'ip',
  `room` varchar(20) COLLATE utf8_bin NOT NULL COMMENT '所属机房',
  `mem` int(11) unsigned NOT NULL COMMENT '内存大小，单位G',
  `cpu` mediumint(24) unsigned NOT NULL COMMENT 'cpu数量',
  `virtual` tinyint(8) unsigned NOT NULL DEFAULT '1' COMMENT '是否虚拟，0表示否，1表示是',
  `real_ip` varchar(16) COLLATE utf8_bin NOT NULL COMMENT '宿主机ip',
  `service_time` timestamp NOT NULL COMMENT '上线时间',
  `fault_count` int(11) unsigned NOT NULL DEFAULT '0' COMMENT '故障次数',
  `modify_time` timestamp NOT NULL COMMENT '修改时间',
  `warn` tinyint(255) unsigned NOT NULL DEFAULT '1' COMMENT '是否启用报警，0不启用，1启用',
  `available` tinyint(255) NOT NULL COMMENT '表示机器是否可用，1表示可用，0表示不可用；',
  `groupId` int(11) NOT NULL DEFAULT '0' COMMENT '机器分组，默认为0，表示原生资源，非0表示外部提供的资源(可扩展)',
  `type` int(11) NOT NULL DEFAULT '0' COMMENT '0原生 1 其他',
  `extra_desc` varchar(255) COLLATE utf8_bin DEFAULT NULL COMMENT '对于机器的额外说明(例如机器安装的其他服务(web,mysql,queue等等))',
  PRIMARY KEY (`id`),
  UNIQUE KEY `ip` (`ip`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='保存机器的静态信息';

ALTER TABLE `machine_info` ADD COLUMN `collect` int DEFAULT 1 COMMENT 'switch of collect server status, 1:open, 0:close';


insert into machine_info (ssh_user, ssh_passwd, ip, room, mem, cpu, real_ip) values('cachecloud', 'cachecloud', '127.0.0.1', 'songjiang-1', '1', '1', '127.0.0.1');

pwd
/usr/local/cachecloud

mvn clean compile install -Ponline

[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO] 
[INFO] cachecloud-open-parent 1.0-SNAPSHOT ................ SUCCESS [ 19.867 s]
[INFO] cachecloud-open-client ............................. SUCCESS [  0.008 s]
[INFO] cachecloud-open-client-basic ....................... SUCCESS [01:08 min]
[INFO] cachecloud-jedis ................................... SUCCESS [  9.425 s]
[INFO] cachecloud-open-common ............................. SUCCESS [  4.897 s]
[INFO] cachecloud-open-web ................................ SUCCESS [03:26 min]
[INFO] cachecloud-open-client-redis ....................... SUCCESS [  9.194 s]
[INFO] cachecloud-open-jedis-stat 1.0 ..................... SUCCESS [  0.316 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 05:18 min
[INFO] Finished at: 2019-05-18T12:04:24+08:00
[INFO] ------------------------------------------------------------------------

## 部署

/usr/local/cachecloud/cachecloud-open-web/src/main/swap/online.properties
/usr/local/cachecloud/cachecloud-open-web/src/main/swap/local.properties

cd /opt/cachecloud-web

./start.sh &

http://192.168.56.102:8585/

admin /admin


/opt/cachecloud/conf/redis-cluster-6393.conf

redis-server ./redis-cluster-6393.conf &

redis-server ./redis-cluster-6381.conf&
redis-server ./redis-cluster-6382.conf&
redis-server ./redis-cluster-6383.conf&
redis-server ./redis-cluster-6384.conf&
redis-server ./redis-cluster-6385.conf&
redis-server ./redis-cluster-6386.conf&
redis-server ./redis-cluster-6387.conf&
redis-server ./redis-cluster-6388.conf&
redis-server ./redis-cluster-6389.conf&
redis-server ./redis-cluster-6390.conf&
redis-server ./redis-cluster-6391.conf&
redis-server ./redis-cluster-6392.conf&
redis-server ./redis-cluster-6393.conf&
redis-server ./redis-cluster-6394.conf&
redis-server ./redis-cluster-6395.conf&
redis-server ./redis-cluster-6396.conf&
redis-server ./redis-cluster-6397.conf&
redis-server ./redis-cluster-6398.conf&
redis-server ./redis-cluster-6399.conf&

192.168.56.102:128:192.168.56.107
192.168.56.107:128:192.168.56.102
192.168.56.102:128:192.168.56.107
192.168.56.107:128:192.168.56.102

192.168.56.102:128:192.168.56.107
192.168.56.107:128:192.168.56.102


192.168.56.102:128:192.168.56.107
192.168.56.107:128:192.168.56.108
192.168.56.108:128:192.168.56.102

192.168.56.102:128:192.168.56.103
192.168.56.103:128:192.168.56.104
192.168.56.104:128:192.168.56.102


应用运维

http://192.168.56.103:8585/manage/app/index.do?appId=3


redis-cli -h 192.168.56.103 -p 6380 -c

## 启动

应用统计

http://192.168.56.103:8585/admin/app/index.do?appId=1

http://192.168.56.103:8585/manage/app/index.do?appId=2

## 参考

https://github.com/sohutv/cachecloud

https://blog.csdn.net/yujin2010good/article/details/71915255

https://cachecloud.github.io/2016/05/24/CacheCloud%E7%B3%BB%E7%BB%9F%E9%85%8D%E7%BD%AE%E8%AF%B4%E6%98%8E/

https://blog.51cto.com/chenwei/1958399

java

https://blog.csdn.net/zxb730916/article/details/80899429