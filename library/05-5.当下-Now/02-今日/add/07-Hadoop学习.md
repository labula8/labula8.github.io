Hadoop

docker pull docker.io/sequenceiq/hadoop-docker

[root@localhost]~# docker run -it --name hadoop sequenceiq/hadoop-docker /etc/bootstrap.sh -bash
/
Starting sshd:                                             [  OK  ]
Starting namenodes on [1c5825b51463]
1c5825b51463: starting namenode, logging to /usr/local/hadoop/logs/hadoop-root-namenode-1c5825b51463.out
localhost: starting datanode, logging to /usr/local/hadoop/logs/hadoop-root-datanode-1c5825b51463.out
Starting secondary namenodes [0.0.0.0]
0.0.0.0: starting secondarynamenode, logging to /usr/local/hadoop/logs/hadoop-root-secondarynamenode-1c5825b51463.out
starting yarn daemons
starting resourcemanager, logging to /usr/local/hadoop/logs/yarn--resourcemanager-1c5825b51463.out
localhost: starting nodemanager, logging to /usr/local/hadoop/logs/yarn-root-nodemanager-1c5825b51463.out

bash-4.1# echo $HADOOP_PREFIX
/usr/local/hadoop

[root@1c5825b51463 hadoop]# bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.0.jar grep input output 'dfs[a-z.]+'
19/01/28 07:37:11 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/01/28 07:37:13 INFO input.FileInputFormat: Total input paths to process : 31
19/01/28 07:37:13 INFO mapreduce.JobSubmitter: number of splits:31
19/01/28 07:37:13 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1548678336305_0001
19/01/28 07:37:14 INFO impl.YarnClientImpl: Submitted application application_1548678336305_0001
19/01/28 07:37:14 INFO mapreduce.Job: The url to track the job: http://1c5825b51463:8088/proxy/application_1548678336305_0001/
19/01/28 07:37:14 INFO mapreduce.Job: Running job: job_1548678336305_0001
19/01/28 07:37:21 INFO mapreduce.Job: Job job_1548678336305_0001 running in uber mode : false
19/01/28 07:37:21 INFO mapreduce.Job:  map 0% reduce 0%
19/01/28 07:37:32 INFO mapreduce.Job:  map 3% reduce 0%
19/01/28 07:37:33 INFO mapreduce.Job:  map 19% reduce 0%
19/01/28 07:37:41 INFO mapreduce.Job:  map 23% reduce 0%
19/01/28 07:37:43 INFO mapreduce.Job:  map 29% reduce 0%
19/01/28 07:37:44 INFO mapreduce.Job:  map 32% reduce 0%
19/01/28 07:37:45 INFO mapreduce.Job:  map 39% reduce 0%
19/01/28 07:37:51 INFO mapreduce.Job:  map 42% reduce 0%
19/01/28 07:37:52 INFO mapreduce.Job:  map 45% reduce 0%
19/01/28 07:37:54 INFO mapreduce.Job:  map 55% reduce 15%
19/01/28 07:37:57 INFO mapreduce.Job:  map 55% reduce 18%
19/01/28 07:38:00 INFO mapreduce.Job:  map 58% reduce 18%
19/01/28 07:38:01 INFO mapreduce.Job:  map 65% reduce 18%
19/01/28 07:38:02 INFO mapreduce.Job:  map 71% reduce 18%
19/01/28 07:38:03 INFO mapreduce.Job:  map 71% reduce 24%
19/01/28 07:38:08 INFO mapreduce.Job:  map 74% reduce 24%
19/01/28 07:38:09 INFO mapreduce.Job:  map 84% reduce 25%
19/01/28 07:38:10 INFO mapreduce.Job:  map 87% reduce 25%
19/01/28 07:38:13 INFO mapreduce.Job:  map 87% reduce 29%
19/01/28 07:38:16 INFO mapreduce.Job:  map 90% reduce 29%
19/01/28 07:38:17 INFO mapreduce.Job:  map 100% reduce 29%
19/01/28 07:38:18 INFO mapreduce.Job:  map 100% reduce 100%
19/01/28 07:38:18 INFO mapreduce.Job: Job job_1548678336305_0001 completed successfully
19/01/28 07:38:18 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=345
		FILE: Number of bytes written=3697508
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=80529
		HDFS: Number of bytes written=437
		HDFS: Number of read operations=96
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=2
	Job Counters 
		Launched map tasks=31
		Launched reduce tasks=1
		Data-local map tasks=31
		Total time spent by all maps in occupied slots (ms)=242663
		Total time spent by all reduces in occupied slots (ms)=35242
		Total time spent by all map tasks (ms)=242663
		Total time spent by all reduce tasks (ms)=35242
		Total vcore-seconds taken by all map tasks=242663
		Total vcore-seconds taken by all reduce tasks=35242
		Total megabyte-seconds taken by all map tasks=248486912
		Total megabyte-seconds taken by all reduce tasks=36087808
	Map-Reduce Framework
		Map input records=2060
		Map output records=24
		Map output bytes=590
		Map output materialized bytes=525
		Input split bytes=3812
		Combine input records=24
		Combine output records=13
		Reduce input groups=11
		Reduce shuffle bytes=525
		Reduce input records=13
		Reduce output records=11
		Spilled Records=26
		Shuffled Maps =31
		Failed Shuffles=0
		Merged Map outputs=31
		GC time elapsed (ms)=2738
		CPU time spent (ms)=17450
		Physical memory (bytes) snapshot=8520540160
		Virtual memory (bytes) snapshot=23914962944
		Total committed heap usage (bytes)=6455558144
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=76717
	File Output Format Counters 
		Bytes Written=437
19/01/28 07:38:18 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/01/28 07:38:18 INFO input.FileInputFormat: Total input paths to process : 1
19/01/28 07:38:18 INFO mapreduce.JobSubmitter: number of splits:1
19/01/28 07:38:18 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1548678336305_0002
19/01/28 07:38:18 INFO impl.YarnClientImpl: Submitted application application_1548678336305_0002
19/01/28 07:38:18 INFO mapreduce.Job: The url to track the job: http://1c5825b51463:8088/proxy/application_1548678336305_0002/
19/01/28 07:38:18 INFO mapreduce.Job: Running job: job_1548678336305_0002
19/01/28 07:38:28 INFO mapreduce.Job: Job job_1548678336305_0002 running in uber mode : false
19/01/28 07:38:28 INFO mapreduce.Job:  map 0% reduce 0%
19/01/28 07:38:34 INFO mapreduce.Job:  map 100% reduce 0%
19/01/28 07:38:40 INFO mapreduce.Job:  map 100% reduce 100%
19/01/28 07:38:40 INFO mapreduce.Job: Job job_1548678336305_0002 completed successfully
19/01/28 07:38:40 INFO mapreduce.Job: Counters: 49
	File System Counters
		FILE: Number of bytes read=291
		FILE: Number of bytes written=230543
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=570
		HDFS: Number of bytes written=197
		HDFS: Number of read operations=7
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=2
	Job Counters 
		Launched map tasks=1
		Launched reduce tasks=1
		Data-local map tasks=1
		Total time spent by all maps in occupied slots (ms)=2942
		Total time spent by all reduces in occupied slots (ms)=3627
		Total time spent by all map tasks (ms)=2942
		Total time spent by all reduce tasks (ms)=3627
		Total vcore-seconds taken by all map tasks=2942
		Total vcore-seconds taken by all reduce tasks=3627
		Total megabyte-seconds taken by all map tasks=3012608
		Total megabyte-seconds taken by all reduce tasks=3714048
	Map-Reduce Framework
		Map input records=11
		Map output records=11
		Map output bytes=263
		Map output materialized bytes=291
		Input split bytes=133
		Combine input records=0
		Combine output records=0
		Reduce input groups=5
		Reduce shuffle bytes=291
		Reduce input records=11
		Reduce output records=11
		Spilled Records=22
		Shuffled Maps =1
		Failed Shuffles=0
		Merged Map outputs=1
		GC time elapsed (ms)=48
		CPU time spent (ms)=1420
		Physical memory (bytes) snapshot=440782848
		Virtual memory (bytes) snapshot=1512599552
		Total committed heap usage (bytes)=311951360
	Shuffle Errors
		BAD_ID=0
		CONNECTION=0
		IO_ERROR=0
		WRONG_LENGTH=0
		WRONG_MAP=0
		WRONG_REDUCE=0
	File Input Format Counters 
		Bytes Read=437
	File Output Format Counters 
		Bytes Written=197

[root@1c5825b51463 hadoop]# bin/hdfs dfs -cat output/*
6	dfs.audit.logger
4	dfs.class
3	dfs.server.namenode.
2	dfs.period
2	dfs.audit.log.maxfilesize
2	dfs.audit.log.maxbackupindex
1	dfsmetrics.log
1	dfsadmin
1	dfs.servers
1	dfs.replication
1	dfs.file

vi /etc/bashrc
# alias ll='ls -alt'
# source /etc/bashrc

[root@1c5825b51463 hadoop]# echo $JAVA_HOME
/usr/java/default

/usr/local/hadoop/etc/hadoop

[root@1c5825b51463 hadoop]# cat yarn-site.xml 
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>

    <property>
      <name>yarn.application.classpath</name>
      <value>/usr/local/hadoop/etc/hadoop, /usr/local/hadoop/share/hadoop/common/*, /usr/local/hadoop/share/hadoop/common/lib/*, /usr/local/hadoop/share/hadoop/hdfs/*, /usr/local/hadoop/share/hadoop/hdfs/lib/*, /usr/local/hadoop/share/hadoop/mapreduce/*, /usr/local/hadoop/share/hadoop/mapreduce/lib/*, /usr/local/hadoop/share/hadoop/yarn/*, /usr/local/hadoop/share/hadoop/yarn/lib/*</value>
    </property>

    <property>
    <description>
      Number of seconds after an application finishes before the nodemanager's
      DeletionService will delete the application's localized file directory
      and log directory.

      To diagnose Yarn application problems, set this property's value large
      enough (for example, to 600 = 10 minutes) to permit examination of these
      directories. After changing the property's value, you must restart the
      nodemanager in order for it to have an effect.

      The roots of Yarn applications' work directories is configurable with
      the yarn.nodemanager.local-dirs property (see below), and the roots
      of the Yarn applications' log directories is configurable with the
      yarn.nodemanager.log-dirs property (see also below).
    </description>
    <name>yarn.nodemanager.delete.debug-delay-sec</name>
    <value>600</value>
  </property>

</configuration>


## kiwenlau/hadoop

[root@localhost]~# docker pull docker.io/kiwenlau/hadoop
Using default tag: latest
Trying to pull repository docker.io/kiwenlau/hadoop ... 
manifest for docker.io/kiwenlau/hadoop:latest not found
[root@localhost]~# docker pull docker.io/kiwenlau/hadoop:1.0
Trying to pull repository docker.io/kiwenlau/hadoop ... 
1.0: Pulling from docker.io/kiwenlau/hadoop
6c953ac5d795: Pulling fs layer 
3eed5ff20a90: Pulling fs layer 
f8419ea7c1b5: Pulling fs layer 
51900bc9e720: Waiting 
a3ed95caeb02: Waiting 
bd8785af34f8: Waiting 
bbc3db9806c0: Waiting 
10b317fed6db: Waiting 
ff167c65c3cc: Waiting 
b6f1a5a93aa5: Waiting 
21f0d52e6cae: Waiting 
35ebd7467cfb: Waiting 
error pulling image configuration: Get https://production.cloudflare.docker.com/registry-v2/docker/registry/v2/blobs/sha256/a5/a59a341252723091fe4f13d7f3ba517b96ed02dc5da3c1aa6ef09af0350da8d8/data?verify=1548734735-f09FR2YXKABC%2B2qWuIVQaL1Utqw%3D: dial tcp 104.18.121.25:443: i/o timeout

http://192.168.56.103:8088/cluster

  PID TTY      STAT   TIME COMMAND
    1 ?        Ss     0:00 /bin/bash /etc/bootstrap.sh -bash
   27 ?        Ss     0:00 /usr/sbin/sshd
  135 ?        Sl     1:28 /usr/java/default/bin/java -Dproc_namenode -Xmx1000m -Djava.net.preferIPv4Stack=true -Dhadoop.log.dir=/usr/local/hadoop/logs -Dhadoop.log.file=hadoop.log -Dhadoop.home.dir= -Dhadoop.id.str=root -Dhadoop.root.logger=INFO,console -Djava.library.
  259 ?        Sl     1:25 /usr/java/default/bin/java -Dproc_datanode -Xmx1000m -Djava.net.preferIPv4Stack=true -Dhadoop.log.dir=/usr/local/hadoop/logs -Dhadoop.log.file=hadoop.log -Dhadoop.home.dir= -Dhadoop.id.str=root -Dhadoop.root.logger=INFO,console -Djava.library.
  427 ?        Sl     0:50 /usr/java/default/bin/java -Dproc_secondarynamenode -Xmx1000m -Djava.net.preferIPv4Stack=true -Dhadoop.log.dir=/usr/local/hadoop/logs -Dhadoop.log.file=hadoop.log -Dhadoop.home.dir= -Dhadoop.id.str=root -Dhadoop.root.logger=INFO,console -Djava
  591 ?        Sl     5:35 /usr/java/default/bin/java -Dproc_resourcemanager -Xmx1000m -Dhadoop.log.dir=/usr/local/hadoop/logs -Dyarn.log.dir=/usr/local/hadoop/logs -Dhadoop.log.file=yarn--resourcemanager-1c5825b51463.log -Dyarn.log.file=yarn--resourcemanager-1c5825b514
  690 ?        Sl     2:54 /usr/java/default/bin/java -Dproc_nodemanager -Xmx1000m -Dhadoop.log.dir=/usr/local/hadoop/logs -Dyarn.log.dir=/usr/local/hadoop/logs -Dhadoop.log.file=yarn-root-nodemanager-1c5825b51463.log -Dyarn.log.file=yarn-root-nodemanager-1c5825b51463.l
  906 ?        S      0:00 /bin/bash
 3484 ?        Ss+    0:00 /bin/bash

docker commit -m "update hadoop-docker" -a "Docker Newbee" 1c5825b51463 hadoop-docker-yu

[root@1c5825b51463 hadoop]# ./bin/hadoop fs -ls
Found 2 items
drwxr-xr-x   - root supergroup          0 2015-07-22 11:17 input
drwxr-xr-x   - root supergroup          0 2019-01-28 07:38 output
[root@1c5825b51463 hadoop]# 
[root@1c5825b51463 hadoop]# 
[root@1c5825b51463 hadoop]# 
[root@1c5825b51463 hadoop]# ./bin/hadoop fs -help ls
-ls [-d] [-h] [-R] [<path> ...] :
  List the contents that match the specified file pattern. If path is not
  specified, the contents of /user/<currentUser> will be listed. Directory entries
  are of the form:
  	permissions - userId groupId sizeOfDirectory(in bytes)
  modificationDate(yyyy-MM-dd HH:mm) directoryName
  
  and file entries are of the form:
  	permissions numberOfReplicas userId groupId sizeOfFile(in bytes)
  modificationDate(yyyy-MM-dd HH:mm) fileName
                                                                                 
  -d  Directories are listed as plain files.                                     
  -h  Formats the sizes of files in a human-readable fashion rather than a number
      of bytes.                                                                  
  -R  Recursively list the contents of directories.  

## 参考

hadoop+docker

https://github.com/kiwenlau/hadoop-cluster-docker

https://kiwenlau.com/2016/06/12/160612-hadoop-cluster-docker-update/


https://www.cnblogs.com/garfieldcgf/p/5462038.html

https://www.ibm.com/developerworks/cn/linux/l-hadoop-1/index.html


