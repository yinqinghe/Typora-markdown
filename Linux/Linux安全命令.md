```
ps aux

查看当前登录用户
w
who
lslogins
getent passwd root  查看指定用户信息
getent hosts   获取所有主机信息
compgen -u     列出系统所有的用户
compgen -g     列出系统所有的组

uptime            查看系统的负载情况
watch -n 1 uptime  每秒刷新一次获得当前的系统负载情况

```

```
lastb    查看/var/log/lastlog 记录系统中所有用户最后一次登录时间的日志
lastlog    查看 /var/log/wtmp  记录所有用户的登录  注销信息
last    /var/log/utmp 记录当前已经登录的用户信息
echo> /var/log/lastlog   清除用户最后一次登录时间
echo> /var/log/utmp       清除当前登录用户的信息
cat/dev/null>  /var/log/secure    清除安全日志记录
cat/dev/null> /var/log/message    清除系统日志记录

find ./ -ctime 0 -name "*.php"   查找24小时内被创建的php文件


chattr +i shell.php  锁定文件
rm -rf shell.php     提示禁止删除 
lsattr shell.php     属性查看
chattr -i shell.php  解除锁定
rm -rf shell.php     删除文件
```

