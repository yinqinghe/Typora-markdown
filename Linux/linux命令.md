```
sh example.sh one two three four 
#!/bin/bash
echo "当前脚本名称为$0"
echo "总共有$#参数  分别是$*"
echo "第一个参数$1  第五个参数$5"

linux查询磁盘使用情况
df           将系统内所有的文件系统列出来
df -h        将容量结果以易读的容量格式显示出来
df -aT       将系统内的所有特殊文件格式及名称列出来
df -h /etc   将/etc地下的可用的磁盘容量以易读的容量格式显示  
du       只列出当前目录下的所有文件夹容量  到文件系统内去搜索所有的文件数据
du -a        将文件的容量列出来
du -sm /*    检查根目录底下每个目录所占用的容量
```

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'IDENTIFIED BY '123456' WITH GRANT OPTION;    授权MySQL，mariDB  root 远程登录
flush privileges;

```

redhat7  

```
systemctl
```

