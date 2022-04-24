## 基本配置

```bash
git init  # 初始化
git config --global user.name "xxx"   # 配置用户名
git config --global user.email "xxx"  # 配置邮箱
git config --global core.ignorecase false  # 配置大小写敏感
git config --list  # 查看配置信息

```

### 创建ssh

```bash
ssh-keygen -t rsa -C "youremail@exaple.com" 
```

ssh文件默认路径`C:\Users\<User Name>\.ssh`

创建本机ssh之后可以在GitHub的settings里面添加,然后就可以连接GitHub仓库了

```bash
git remote add origin git@github.com:Bad-Oranges/LearnGit.git  #添加远程仓库(SSH方式)
git branch -M main
git push -u origin main  # push到远程仓库
```



## 基本操作

```bash
ll -ah  # 查看文件列表，包括隐藏文件夹
git status  # 查看本地文件状态
git log  # 查看提交日志
git reflog  # 查看命令历史

git restore <file_name>  # 丢弃工作区的修改
git restore  # 丢弃工作区所有文件的修改
git restore --staged <file_name>  # 撤销暂存区的修改
git restore --source=HEAD~1  # 将工作区回滚至上n个版本
git restore --source=<commit> # 将工作区回滚至指定版本
```

## 文件状态

![image-20220130233742518](Basic.assets/image-20220130233742518.png)

### 文件提交 

```bash
# 一般提交流程
git rm <file-name>  # 删除文件
git add <file-name>  # 将文件放入暂存区(此时文件状态为staged）
git add .  # 将所有放入暂存区(此时文件状态为staged）
git commit <file-name> -m "some messages"  # 将文件提交至本地仓库并备注信息
git commit <file-name> -am "some messages"  # 等同于git add . && git commit -m
## git commit --amend  # 修改上次提交的备注信息
git push  # 将文件从本地仓库提交到远程仓库
```

### 修改已经commit的注释

```bash
git rebase -i HEAD~n  # 显示最近第N次的提交
# 将要修改的注释前的pick改为edit（如果修改多个注释，就多改几个）
git commit --amend
git rebase --continue
# 对于多次提交重复上面两个步骤
git push --force origin master  # 将代码push到远程仓库
```

```bash
# 从远程仓库获取文件
git fetch <远程主机名> <分支名>  # 获取远程仓库特定分支的更新
git fetch --all  # 获取远程仓库所有分支的更新
git pull <远程主机名> <远程分支名>:<本地分支名>  # 等同于 git fetch && git merge
git pull --rebase <远程主机名> <远程分支名>:<本地分支名>  # 使用rebase的模式进行合并

# 远程仓库
git remote -v  # 查看远程仓库
git remote add 仓库名 地址  # 添加远程仓库
```





## 分支与标签管理

```bash
git branch  # 查看本地分支
git branch -r  # 查看远程分支
git branch -a  # 查看本地和远程分支


git switch -c <branch-name>  # 创建分支
git switch <branch-name>  # 切换分支
git branch -d <branch-nane>  # 删除本地分支
git branch -m <old-branch-name> <new-branch-name>  # 重新命名分支

git commit -am "some message"  # 分支内容提交和正常没有区别
git push --set-upstream origin <branch-name>  # 第一次提交时需要设置远程分支

git merge <branch-name>  # 以当前分支为主分支合并目标分支
```

![image-20220130231917886](Basic.assets/image-20220130231917886.png)

### 分支策略

主分支仅用来发布新版本

dev分支负责开发工作

dev分支可以继续细分（按工作类型、人员）

### 标签管理

```bash
git tag  # 查看所有标签
git tag v1.0 (commmit ID)  # 创建标签(对指定Commit ID添加标签，SHA可以通过log查找)
git tag -a v0.1 -m (Commit ID)"version 0.1 released"   # 创建带有描述信息的标签
git show <tagname>  # 查看标签说明文字
git tag –d v0.1  # 删除指定标签

# 将本地标签发布到远程仓库
git push origin --tags  # 发送所有
git push origin 1.0.0  # 指定标签发送

# 删除远程仓库对应标签 （删除远程标签需要先删除本地标签！）
git tag -d v0.9
git push origin --delete v0.9  # Git版本 > V1.7.0
git push origin :refs/tags/v0.9  # 旧版本Git
```

## 其他

### commit message规范

[git commit 规范指南 - 简书](https://www.jianshu.com/p/201bd81e7dc9)

#### Breaking Change

以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。

```
BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

#### Closed Issue

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue

```
Closes #234
```

#### Revert

以revert:开头，后面跟着被撤销 Commit 的 Header

Body部分的格式是固定的，必须写成`This reverts commit <hash>`.，其中的hash是被撤销 commit 的 SHA 标识符。

```
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的Reverts小标题下面。