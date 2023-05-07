# anaconda  使用

```
1.conda info    查看当前环境的信息
2.conda info -e      查看已经创建的所有虚拟环境
3.conda activate xxx     切换到xx虚拟环境
一.  安装Tensorflow
a.python --version     查看Python  版本
b.conda create -n tensorflow python=3.7.6   创建python
c.conda info --envs     chrome /incognito  
d.activate tensorflow   激活Tensor Flow

```



```
1.conda env list       查看所有环境
2.conda create -n facemask python=3.7.4    创建新的虚拟环境指定名称和版本号
3.conda activate facemask       进入某个虚拟环境
4.conda list                 查看当前环境下安装了那些包
5.conda install -n tom redis    给指定的虚拟环境安装包
  python3.7 -m pip install redis  如果是bash环境的话，为了防止与系统自带的python2 python3不冲突，可以使用
  
6.conda remove -n facemask --all  删除某环境和该环境下所有的包
```



```
1.conda config --show-sources    查看当前使用的源
2.conda config --add channels          切换清华镜像源        https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/

conda config --set show_channel_urls yes 
3.conda config --remove-key channels  还原为默认镜像
4.pip install numpy -i https://pypi.tuna.tsinghua.edu.cn/simple   指定源使用
常用源
    -i  http://pypi.douban.com/simple 				# 豆瓣
	-i https://pypi.tuna.tsinghua.edu.cn/simple		# 清华
    -i  http://mirrors.aliyun.com/pypi/simple		# 阿里
    # 安装numpy使用豆瓣源加速
    pip install numpy -i  http://pypi.douban.com/simple
5.conda list numpy    查看指定包
6.pip install numpu==1.19.5   安装指定版本的包
7.pip uninstall numpy      卸载包
8.pip install --upgrade numpy    更新包
9.pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -r requirements.txt
一键安装环境配置reuirements.txt
10.jupter notebook  启动jupyter
```

```
windows/Linux下Anaconda更改默认python环境的方法
更改anaconda安装目录下\anaconda3\Scripts\activate.bat文件,将第24行

@CALL "%~dp0..\condabin\conda.bat" activate %*
1
更改为

@CALL "%~dp0..\condabin\conda.bat" activate 环境名

```

