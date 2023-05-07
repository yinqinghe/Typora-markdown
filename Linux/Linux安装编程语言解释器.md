#### 1.go的安装

```
wget https://golang.google.cn/dl/go1.19.2.linux-amd64.tar.gz
 # 解压文件   解压到指定目录
 tar xfz go1.19.2.inux-amd64.tar.gz -C /usr/local
 根据自己使用的Shell是bash还是zsh
 判断自己使用的shell  用  echo $0
 
 #修改~/.zshrc
vim ~/.zshrc
#添加Gopath路径
export GOROOT=/usr/local/src/go     #GOROOT是系统上安装Go软件包的位置。
export GOPATH=/home/kali/interpreter/go_pkg/       #GOPATH是工作目录的位置。
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
# 激活配置
source ~/.zshrc
验证go安装是否成功
go version
```

1. 在GOPATH目录下创建hello目录，用于存放go的第一个程序。
2. 在hello目录下，创建hello.go文件，内容如下：

```go
package main
import "fmt"
func main() {
    fmt.Printf("Hello, World\n")
}
go run hello.go    运行hello.go文件

go build hello.go  使用go build 编译go文件  编译
./hello    执行名为hello的可执行文件
```

```
解决 go install 第三方包, 连接代理网址 proxy.golang.org 超时  ！！！！！！！！！！重要
go env -w GOPROXY=https://goproxy.cn     换一个国内能访问的代理地址
go env -w GOPROXY=https://goproxy.io.direct

go install  安装到GOPATHli
```

```

2.2.2 解压
执行tar解压到/usr/loacl目录下（官方推荐），得到go文件夹等

tar -C /usr/local -zxvf go1.16.6.linux-amd64.tar.gz
2.2.3 环境变量
添加/usr/loacl/go/bin目录到PATH变量中。添加到/etc/profile 或$HOME/.profile都可以

vi /etc/profile
# 在/etc/profile最后一行添加
export GOROOT=/usr/local/go
export PATH=$PATH:$GOROOT/bin
# 保存退出后source一下（vi 的使用方法可以自己搜索一下）
source /etc/profile
2.2.4 验证
执行go version，如果显示版本号，则Go环境安装成功。

```

### 2.JAVA的安装  卸载

```
卸载
Centos环境下yum安装更新jdk、删除自带的jdk
参考博客：https://blog.csdn.net/u013641234/article/details/76158026

查看CentOS自带JDK是否已安装:yum list installed | grep java
假使存在自带的jdk，删除centos自带的JDK
yum -y remove java-1.7.0-openjdk*
yum -y remove tzdata-java.noarch
结果显示为Complete!表示卸载完成!

```

```
1.进入 Oracle 官方网站 下载合适的 JDK 版本，准备安装。
注意：这里需要下载 Linux 版本。这里以jdk-8u151-linux-x64.tar.gz为例，你下载的文件可能不是这个版本，这没关系，只要后缀(.tar.gz)一致即可。
2.创建目录
在/usr/目录下创建java目录，
mkdir /usr/local/java
cd /usr/local/java
把下载的文件 jdk-8u151-linux-x64.tar.gz 放在/usr/local/java/目录下。
3.解压 JDK
tar -zxvf jdk-8u151-linux-x64.tar.gz
4.设置环境变量
修改 vi /etc/profile
在 profile 文件中添加如下内容并保存：
JAVA_HOME=/usr/local/java/jdk1.8.0_151        
JRE_HOME=/usr/local/java/jdk1.8.0_151/jre     
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH

注意：其中 JAVA_HOME， JRE_HOME 请根据自己的实际安装路径及 JDK 版本配置。
5. 让修改生效：
source /etc/profile
6. java -version
显示 java 版本信息，则说明 JDK 安装成功

```

