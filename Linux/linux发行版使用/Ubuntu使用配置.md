1.vmware 网络连接模式net  配置静态IP

```
编辑  vim /etc/network/interfaces  修改文件
iface etho inet static
address 192.168.52.114
netmask 255.255.255.0
gateway 192.168.52.2

配置域名服务器
vim /etc/resolv.conf
nameserver 192.168.52.2  添加这行域名地址

修改这些文件，还需要root权限
sudo passwd root   修改root密码

su root
```

2.Ubuntu20.04  配置网络设置

```
ip addr
cd /et/netplan   路径下有一个yaml文件名   
cp xxx.yaml xxx.yaml.bak  先备份一下yaml
vim xxx.yaml
network:
      version: 2    必需元素
      renderer: networkd    
      ethernets:  
          eno33:   设备类型   可以指定一个或多个网络接口
                dhcp4: no
                addresses:
                       - 192.168.52.116/24
                gateway4: 192.168.52.2
                nameservers:
                        addresses:[192.168.52.2]
                        
 保存文件 执行命令   sudo netplan apply
 
```

Ubuntu安装docker

```
apt-get remove docker docker-engine docker.io contained runc 如果有旧版，先卸载旧版

apt-get install ca-certificates curl gnupg lsb-release

curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -   安装证书

sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"   写入软件源信息

sudo apt-get install docker-ce docker-ce-cli containerd.io

service start docker

```

解决wsl-ubuntu安装docker网络问题

```
sudo rm /etc/resolv.conf
sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
sudo bash -c 'echo "[network]" > /etc/wsl.conf'
sudo bash -c 'echo "generateResolvConf = false" >> /etc/wsl.conf'
sudo chattr +i /etc/resolv.conf
```

