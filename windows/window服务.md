1.ssh的使用

```
ssh 用户名@0.0.0.0   连接上之后，输入密码

```



```
python -m pip install -U pip setuptools wheel -i https://mirrors.aliyun.com/pypi/simple/   gen'x
python -m venv test_env(虚拟环境名称)  创建python虚拟环境
cd  xxx/xxx/test_env/scripts    切换到虚拟环境目录下
.\activate    激活环境
deactivate    退出虚拟环境


python -m http:server 8000   python开启
```



```
shutdown /i，回车，就会弹出关机或者重启的窗口，在下拉框中，选择关机或重启后

shutdown /p 选择直接你使用命令进行关机，输入关机命令

重启命令则是：shutdown /r /t 0,使用/t参数，可以选择指定多长时间后进行重启。t为0则表示立即重启。


输入启用远程桌面连接的命令。

在命令提示符窗口中，输入以下命令来启用远程桌面连接功能：

reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
运行该命令后，将会关闭禁止远程桌面连接的设置，并且允许远程连接服务器。

如果需要使用 Windows 自带的防火墙，需要确保已经开启了远程桌面连接的端口。可以使用以下命令来添加防火墙规则：

netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```



```
NetSh Advfirewall set allprofiles state on //开启防火墙

NetSh Advfirewall set allprofiles state off //关闭防火墙
```

Windows修改用户密码

```
net user administrator 123456
```

