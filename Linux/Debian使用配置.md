### Debian  使用配置

###### 1.解决media change:please insert the disc labeled

```
vi /etc/apt/sources.list
deb cdrom... bullseye contrib main    这行注释掉
apt update   更新仓库
```

###### Debian  ifconfig命令找不到解决办法

```
ifconfig、route、arp和netstat等命令行工具  统称为net-tools,管理和排查各种网络配置，这类工具原先起源于BSD TCP/IP工具箱，旨在配置老式Linux内核的网络功能。自2001年以后，它在Linux社区的发展就止步不前了。Debian ，Arch Linux ，CentOS/RHEL 7等一些Linux发行版已经弃用了net-tools，其他发行版计划弃用net-tools，改而使用iproute2。

iproute2：套件是网络和流量控制工具的一个软件集合，这些工具通过实时 netlink 界面与内核通讯，提供流传已久的 net-tools 命令 ifconfig 和 route 所不具备的高级特性。

ip addr show  查看ip地址
ip neigh   或  ip neigh show  查看arp 缓存表
apt install net-tools   想用ifconfig命令可以安装

```

###### 2.Debian  apt   下载慢的问题  换源

```
编辑/etc/apt/sources.list文件(需要使用sudo), 在文件最前面添加以下条目(操作前请做好相应备份)
去阿里源找到相应的源
deb https://mirrors.aliyun.com/debian/ buster main non-free contrib
deb-src https://mirrors.aliyun.com/debian/ buster main non-free contrib
```

3.允许root用户以ssh方式登录



