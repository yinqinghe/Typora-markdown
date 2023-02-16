#### 1.1.创建主redis

`docker run -itd --name redis-master -p 6379:6379 redis`

#### 1.2.创建从redis

`docker run -itd --name redis-slave1 -p 6380:6380 redis`

#### 1.3.查看主redis  IP地址

`docker inspect redis-master | grep IPAddress`

### 1.4.通过命令行配置主从复制

#### 1.4.1进入容器  命令

`docker exec -it redis-slave1 bash`

#### 1.4.2查看redis主从模式状态，  在redis命令行执行命令

`info replication`

#####   a.使redis成为从节点

`slaveof 172.17.0.2 6379` 

### 1.5.通过文件配置

#### 1.5.1  需要设置一个通用的配置文件 /opt/server/redisSlave1.conf并关联上容器的配置文件路径

`docker run -itd --name redis-slave1 -v /opt/server/redisSlave1.conf:/redisConfig/redisSlave1.conf -p 6380:6379 redis  redis-server /redisConfig/redisSlave1.conf`



## 2.哨兵模式集群

2.1   创建一个公用的哨兵配置文件

```
port 16379   哨兵监听端口
sentinel monitor master 172.17.0.2 6379 2    ip需是主redis地址
logfile "sentinel1.log"

```

授予相关目录权限    chmod -R 777 /opt/server   使程序运行时有写入权限，否则报错

2.2创建一个哨兵

```
docker run -itd --name redis-sentinel1 -v /opt/server:/redisConfig:z -p 16379:16379 redis redis-server /redisConfig/sentinel1.conf --sentinel
加:z  是突破seLinux的限制
```

2.3如果报错，运行不成功 ，查看日志文件

```
docker logs container-name
```

## 3.Cluster集群模式

3.1创建一个主节点配置文件cluster-m1.conf        配置三个

```
port 6379    依次6380
dir /redisConfig      
logfile cluster-m1.log     cluster-m2.log
cluster-enabled yes      开启cluster功能
cluster-config-file nodes-6379.conf    指定内部需要的配置文件   nodes-6380.conf
```

3.2创建一个从节点配置文件cluster-s1.conf   配置三个

```
port 16379
dir /redisConfig
logfile cluster-s1.log
cluster-enabled yes
cluster-config-file nodes-16379.conf
```

3.3创建主节点容器

```
docker run -itd --name redis-m1 -v /opt/server:/redisConfig:z -p 6379:6379 redis redis-server /redisConfig/cluster-m1.conf
```

3.4创建从节点容器

```
docker run -itd --name redis-s1 -v /opt/server:/redisConfig:z -p 16379:16379 redis redis-server /redisConfig/cluster-s1.conf
```

3.5节点之间相互连接

```
root@5eef754ed672:/data# redis-cli -p 6379 cluster meet 172.17.0.2 6380  后面的IP 端口 依次连接
```

3.6连接之后，查看连接状态

```
127.0.0.1:6379> cluster info
cluster_state:fail     cluster连接状态    如果没有分配过槽是fail的状态  分配后应是OK
cluster_slots_assigned:0
cluster_slots_ok:0
cluster_slots_pfail:0
cluster_slots_fail:0
cluster_known_nodes:6    cluster连接节点数
cluster_size:0
cluster_current_epoch:5
cluster_my_epoch:1
```

3.7使用脚本分配槽，创建脚本

```
[root@centos server]# vim setHashSlots.sh
脚本内容
1.
#!/bin/bash
for i in $(seq 0 5460)
do
/usr/local/bin/redis-cli -h 172.17.0.3 -p 6391 cluster addslots $i
done
~     
2.
#!/bin/bash
for i in $(seq 5461 10922)
do
/usr/local/bin/redis-cli -h 172.17.0.2 -p 6380 cluster addslots $i
done
~     
3.
#!/bin/bash
for i in $(seq 10923 16383)
do
/usr/local/bin/redis-cli -h 172.17.0.4 -p 6381 cluster addslots $i
done
~     
```

3.8获取cluster  node 信息

```
127.0.0.1:6379> cluster nodes
0deae282df63340130b4704cb7a406c0dbac9401 172.17.0.3:6379@16379 myself,master - 0 1674907647000 1 connected 0-5460
5a3d6668c336a42ad463133abf25b36c5849f646 172.17.0.4:6381@16381 master - 0 1674907651206 2 connected 10923-16383
e6060dec548932e74f810f1d12f1a766556cbca7 172.17.0.6:16380@26380 master - 0 1674907649000 0 connected
36742a23b86ae2ba4972257521dac64882f0744b 172.17.0.5:16379@26379 master - 0 1674907650183 3 connected
99a1a0c61f179e3ac38d97574df11c821bdfb42b 172.17.0.7:16381@26381 master - 0 1674907649000 5 connected
a10b5f2dc7d6a30ac2005ab4b45372527ac6b893 172.17.0.2:6380@16380 master - 0 1674907649161 4 connected 5461-10922
```

3.9设置三主三从

```
在主节点命令行设置从节点
127.0.0.1:16379> cluster replicate 36742a23b86ae2ba4972257521dac64882f0744b   后面的值是从节点ID
```

3.10设置完成后

```
127.0.0.1:6379> cluster nodes
0deae282df63340130b4704cb7a406c0dbac9401 172.17.0.3:6379@16379 myself,master - 0 1674908387000 1 connected 0-5460
5a3d6668c336a42ad463133abf25b36c5849f646 172.17.0.4:6381@16381 master - 0 1674908389179 2 connected 10923-16383
e6060dec548932e74f810f1d12f1a766556cbca7 172.17.0.6:16380@26380 slave a10b5f2dc7d6a30ac2005ab4b45372527ac6b893 0 1674908389000 4 connected
36742a23b86ae2ba4972257521dac64882f0744b 172.17.0.5:16379@26379 slave 0deae282df63340130b4704cb7a406c0dbac9401 0 1674908391345 1 connected
99a1a0c61f179e3ac38d97574df11c821bdfb42b 172.17.0.7:16381@26381 slave 5a3d6668c336a42ad463133abf25b36c5849f646 0 1674908390000 2 connected
a10b5f2dc7d6a30ac2005ab4b45372527ac6b893 172.17.0.2:6380@16380 master - 0 1674908390261 4 connected 5461-10922
```

3.11使用时命令行，要正确使用加上 -c

```
root@5eef754ed672:/redisConfig# redis-cli -c
127.0.0.1:6379> set name mike
-> Redirected to slot [5798] located at 172.17.0.2:6380
OK
172.17.0.2:6380> 
```



### 

