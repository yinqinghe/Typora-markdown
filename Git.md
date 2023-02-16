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
git status  查看
```

