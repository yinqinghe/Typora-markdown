1.vmware 网络连接模式net  配置静态IP

```
cd /etc/sysconfig/network-scripts/
vim ifcfg-en***   修改IP地址的文件
编辑文件内容
BOOTPROTO="static"
ONBOOT="yes"
IPADDR=192.168.52.110
GATEWAY=192.168.52.2
NETMASK=255.255.255.0
DNS1=192.168.52.2
保存文本后  执行命令  重启网络
systemctl restart network

手动修改  /etc/resolv.conf
nameserver 192.168.52.2
```

2.centos7  root远程连接

centos 允许 root远程登陆
操作过程请使用root用户，或者带有root用户权限的用户

```

安装 openssh-server
yum install -y openssl openssh-server
1
修改配置文件
vim /etc/ssh/sshd_config
修改内容为下面的：

#放开22端口
Port 22                                                                                               #AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::
//允许任意ip访问呢
ListenAddress :: 

#LoginGraceTime 2m
//允许root用户登陆
PermitRootLogin yes                                                                                   #StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no
# 允许使用密码认真
PasswordAuthentication yes



启动ssh服务
systemctl start sshd.service
重启网络
service network restart
设置开机启动ssh服务

systemctl enable sshd.service
```

3.centos7  ssh开启不了

```

在CentOS、RHEL或Fedora上，你所要做的是，删除现存（有问题的）密钥，然后重启sshd服务。

$ sudo rm -r /etc/ssh/ssh*key
$ sudo systemctl restart sshd
 
另外一个重新生成SSH主机密钥的方式是，使用ssh-keygen命令来手动生成。

$ sudo ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
$ sudo ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
$ sudo ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
```



```
ln -s /usr/local/python3/bin/python3 /usr/bin/python3

1、创建软链接

ln -s 【目标目录】 【软链接地址】
二、删除

rm -rf 【软链接地址】
三、修改

ln -snf 【新目标目录】 【软链接地址】
```

