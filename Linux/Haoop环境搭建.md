1.JDK8配置

```
tar -zvxf jdk-8u131-linux-x64.tar.gz  -C /opt/server     -C后面跟的是指定目录
```

1.1配置JDK8环境变量   编辑/etc/profile文件

```
vi /etc/profile
#文件末尾增加
export JAVA_HOME=/opt/server/jdk1.8.0_131
export PATH=${JAVA_HOME}/bin:$PATH
```

执行source命令，是配置立即生效

```
source /etc/profile
```

检查是否安装成功

- [x] ```
  java --version
  ```


2.配置免密登录    Hadoop组件之间需要基于SSH进行通讯

配置映射  配置Ip地址和主机名映射

```
vim /etc/hosts
#文件末尾增加
192.168.52.110
```

生成公钥私钥

```
ssh-keygen -t rsa
```

授权  进入~/.ssh目录下，查看生成的公钥和私钥  并将公钥写入到授权文件

```
cd ~/.ssh
cat id_rsa.pub >>authorized_keys
chmod 600 authorized_keys
```

3.配置Haoop

```
tar -zvxf hadoop-3.1.0.tar.gz -C /opt/server
```

修改配置文件

进入/opt/server/hadoop-3.1.0/etc/hadoop 目录下

```
#修改hadoop-env.sh文件  设置JDK的安装路径
vim hadoop-env.sh
export JAVA_HOME=/opt/server/jdk1.8.0_131
```

修改core-site.xml文件   vim core-site.xml

```js
<configuration>
<property>
    指定namenode的  hdfs协议文件系统的通信地址
<name>fs.defaultFS</name>
<value>hdfs://server:8020</value>
</property>
<property>
    指定Hadoop  数据文件存储目录
<name>hadoop.tmp.dir</name>
<value>/home/hadoop/data</value>
</property>
</configuration>
```

修改hdfs-site.xml  vim hdfs-site.xml

```
<configuration>
<property>
这里搭建是单机版本   指定dfs的副本系统为1
<name>dfs.replication</name>
<value>1</value>
</property>
</configuration>
```

修改workers 文件  配置所有从属节点

```
vim workers 
#配置所有从属节点的主机名或IP地址，由于是单机版本，所以指定本机即可
server
```

3.初始化并启动HDFS

```
#查看防火墙状态
firewall-cmd --state
#关闭防火墙
systemctl stop firewalld
#禁止开机自启动
systemctl disable firewalld
```

第一次启动Hadoop时需要进行初始化  进入/opt/server/hadoop-3.1.0/bin目录下  执行以下命令

```
cd /opt/server/hadoop-3.1.0/bin
./hdfs namenode -format
```

Hadoop3中不允许使用root用户来一键启动集群  需要配置启动用户

```
cd /opt/server/hadoop-3.1.0/sbin
#编辑start-dfs.sh  stop-dfs.sh   在顶部加入以下内容
HDFS_DATANODE_USER=root
HDFS_DATANODE_SECURE_USER=hdfs
HDFS_NAMENODE_USER=root
HDFS_SECONDARYNAMENODE_USER=root

还是在该目录下  启动HDFS
./start-dfs.sh
```

4.配置Hadoop（YARN）环境变量

```
修改mapred-site.xml
<configuration>
<property>
   <name>mapreduce.framework.name</name>
   <value>yarn</value>
</property>
<property>
   <name>yarn.app.mapreduce.am.env</name>
   <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
</property>
<property>
   <name>mapreduce.map.env</name>
   <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
</property>
<property>
   <name>mapreduce.reduce.env</name>
   <value>HADOOP_MAPRED_HOME=${HADOOP_HOME}</value>
</property>
</configuration>
```

