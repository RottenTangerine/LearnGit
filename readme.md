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
git remote add origin git@github.com:Bad-Oranges/LearnGit.git
git branch -M main
git push -u origin main
```



## 基本操作

```bash
ll -ah  # 查看文件列表，包括隐藏文件夹
git status  # c
```



### 
