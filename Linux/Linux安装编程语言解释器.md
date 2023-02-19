#### 1.go的安装

```
wget https://golang.google.cn/dl/go1.19.2.linux-amd64.tar.gz
 # 解压文件   解压到指定目录
 tar xfz go1.16.linux-amd64.tar.gz -C /usr/local
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
解决 go install 第三方包, 连接代理网址 proxy.golang.org 超时
go env -w GOPROXY=https://goproxy.cn     换一个国内能访问的代理地址
go install  安装到GOPATHli
```

