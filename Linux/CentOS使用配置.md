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

```

