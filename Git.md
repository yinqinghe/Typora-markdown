## Git的使用

### …or create a new repository on the command line           

```
echo "# spring-boot-learn" >> README.md
git init
git add .  添加该目录的所有文件
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/yinqinghe/spring-boot-learn.git
git push -u origin main
```

### …or push an existing repository from the command line           

```
git remote add origin https://github.com/yinqinghe/spring-boot-learn.git
git branch -M main
git push -u origin main
```



```
1.git branch               查看分支列表
2.git branch 新分支的名字    创建新分支
3.git checkout             切换分支
4.git checkout -b 分支名字   分支的快速创建和切换
假如在C分支   先切换到A分支  此时在A分支，合并A,C分支
5.git checkout A   git merge C
6.git branch -d xxx   删除分支  不在在该分支上删除该分支
```

```
Git分支的基本使用
git checkout -b 新分支名称
git push -u origin  新分支名称
git checkout   分支名称
git branch

```

```
git status  查看状态
git diff  本地分支名  origin/远程分支名
关联远程分支与本地分支
git branch --set-upstream-to=origin/<远程分支名> <本地分支名>
// 例如： git branch --set-upstream-to=origin/fix_xiaoming fix_xiaoming
```

```
git log：查看所有提交过的版本信息。（按 q 或 ctrl + z 均可退出）
git log --pretty=oneline：查看 完整 hash 版本号 和 commit 信息。
git log --graph --pretty=oneline --abbrev-commit：查看 简短 hash 版本号 和 commit 信息。
git reflog：查看所有分支的所有操作记录（包括已经被删除的 commit 记录和 reset 的操作），内容由 hash 版本号、HEAD 记号 和 commit 信息 组成。（按 q 或 ctrl + z 均可退出）

GitHub  设置代理
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy https://127.0.0.1:7890

```



```

配置个人的用户名称和电子邮件地址：

$ git config --global user.name "runoob"
$ git config --global user.email test@runoob.com

如果用了 --global 选项，那么更改的配置文件就是位于你用户主目录下的那个，以后你所有的项目都会默认使用这里配置的用户信息。

如果要在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。
$ git config  user.name "mikejordan1984"
$ git config  user.email mikejordan1984@gmail.com
```

