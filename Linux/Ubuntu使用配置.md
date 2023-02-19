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

