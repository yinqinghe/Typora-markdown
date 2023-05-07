# Docker安装和使用

可选     卸载旧版本Docker

```
yum remove docker docker-client 
            docker-client-latest 
            docker-common
            docker-latest 
            docker-latest-logrotate
            docker-selinux
            docker-engine-selinux
            docker-engine
            docker-ce
```



1.安装yum工具

```
yum install -y yum-utils device-mapper-persistent-data lvm2 --skip-broken
```

2.更新yum本地软件源

```
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
已加载插件：fastestmirror, langpacks

sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo

yum makecache fast
元数据缓存已建立
```

3.安裝docker

```
yum install -y docker-ce

安装成功
已安装:
  docker-ce.x86_64 3:23.0.1-1.el7                                                                                                                                          
作为依赖被安装:
  audit-libs-python.x86_64 0:2.8.5-4.el7                    checkpolicy.x86_64 0:2.5-8.el7                        container-selinux.noarch 2:2.119.2-1.911c772.el7_8          
  containerd.io.x86_64 0:1.6.16-3.1.el7                     docker-buildx-plugin.x86_64 0:0.10.2-1.el7            docker-ce-cli.x86_64 1:23.0.1-1.el7                         
  docker-ce-rootless-extras.x86_64 0:23.0.1-1.el7           docker-compose-plugin.x86_64 0:2.16.0-1.el7           docker-scan-plugin.x86_64 0:0.23.0-3.el7                    
  fuse-overlayfs.x86_64 0:0.7.2-6.el7_8                     fuse3-libs.x86_64 0:3.6.1-4.el7                       libcgroup.x86_64 0:0.41-21.el7                              
  libsemanage-python.x86_64 0:2.5-14.el7                    policycoreutils-python.x86_64 0:2.5-34.el7            python-IPy.noarch 0:0.75-6.el7                              
  setools-libs.x86_64 0:3.3.8-4.el7                         slirp4netns.x86_64 0:0.4.3-4.el7_8               
```

4.Docker使用中会涉及到各种端口，为了方便使用最好关闭防火墙

```
#关闭防火墙
systemctl stop firewalld
#禁止开机启动防火墙
systemctl disable firewalld
```

5.查看安装的Docker的版本

```
docker -v
```

6.配置Docker国内镜像加速

```
https://cr.console.aliyun.com/    使用

sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://pha6w3rs.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

7.启动docker

```
systemctl start docker  #启动docker服务

systemctl stop docker   #停止docker服务

systemctl restart docker    #重启dockers服务
systemctl enable docker   设置docker开机自启
```

## Docker的使用

1.

```
docker run  新建并启动容器
docker start/stop/pause/unpause   启动、停止、暂停、恢复容器 
docker exec                   进入容器执行命令
docker logs                  查看容器运行命令
docker ps                     查看容器的状态
docker rm                        删除指定容器
docker ps -a                     查看已创建的
docker rmi                    删除指定镜像
```

2.Redis容器实例

```
拉取redis镜像    docker pull redis
创建并启动容器    docker run --name myredis -d -p 6379:6379 redis
进入容器         docker exec -it myredis bash
-it  给当前进入的容器创建一个标准输入、输出终端  允许我们与容器交互
bash  进入容器后执行的命令
进入容器后执行  ：redis-cli   使用


```

3.搭建sql-lib

```
1.docker search sqli-labs   搜索镜像
2.docker pull acgpiano/sqli-labs    下载镜像
3.docker images  查看镜像
4.docker run -dt  --name sqlib -p 88:80 -p 1026:3306 --rm acgpiano/sqli-labs   启动并创建sqlib容器 
映射了两个端口，一个是Apache(httpd)服务的  一个是mysql服务的   1026是宿主机端口
5.docker container ls  查看已经启动的容器列表

-dt  让其在后台运行
--rm  当其关闭后将删除开启的资源  就是关闭时删除创建的容器  yi'ci
docker ps -a      显示容器的id image命令  端口等信息
docker exec -it  容器名称/容器ID /bin/bash   

```

4.搭建MySQL8

```
docker run -p 3306:3306 --name mysql1 --privileged=true --restart unless-stopped -v /mnt/sda1/mysql8.0.21/mysql:/etc/mysql -v /mnt/sda1/mysql8.0.21/logs:/logs -v /mnt/sda1/mysql8.0.21/data:/var/lib/mysql -v /etc/localtime:/etc/localtime -e MYSQL_ROOT_PASSWORD=root123456 -d mysql:8.0.21
```





```
docker-compose  up -d   启动一个新的docker

docker-compose  down   删除所有docker-compose创建的容器
```

```
踩坑
docker-compose的安装   需要GitHub下载安装   国内的不行
```

