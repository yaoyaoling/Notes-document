# github

## 工作区、暂存区、版本库

* 工作区：就是你在电脑里能看到的目录。
* 暂存区：英文叫 stage 或 index。一般存放在 .git 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
* 版本库：工作区有一个隐藏目录 .git，这个不算工作区，而是 Git 的版本库。

Git将项目的存储分为4部分，每部分有自己的作用加下图：

<img src="Git.assets\image-20220507165252142.png" alt="image-20220507165252142" style="zoom:80%;" />

* Workspance：工作区（当前用户操作修改的区域）
* Index / Stage：暂存区（add后的区域）
* Repository：仓库区或本地仓库（commit后的区域）
* Remote：远程仓库（push后的区域）

整个过程简述：

- 工作区->add->暂存区->commit->本地仓库区->push->远程仓库区

- 远程仓库区->fetch->使用refs/remotes下对应的分支文件记录远程分支末端commit_id和本地仓库区->merge->工作区
- 远程仓库区->pull->使用refs/remotes下对应的分支文件记录远程分支末端commit_id本地仓库区and工作区



## 1. github base command

```perl
#1.把这个目录变成Git可以管理的仓库
git init 
#2.本地README.md文件添加到远程仓库
git add README.md 
#3.点就把当前目录下所有未追踪的文件全部add了，注意空格
git add . 
#4.把文件提交到仓库
git commit -m “注释” 
#5.本地关联远程仓库
git remote add origin https://github.com/yaoyaoling/Notes-document.git 
#6.把本地库的所有内容推送到远程库上（第一次需要加-u，后面就不用加了）
git push -u origin master  

#查看配置信息
git config -l
#查看状态
git status
#查案log
git log
```



## 2. 提交代码到github

```perl
#初始化
git init

#绑定账号
git config user.name "yaoyaoling"
git config user.email "826623996@qq.com"

#关联远程仓库
git remote add origin <httpAddress>

#将工作区的文件添加到暂存区(“.”是当前目录下的所有文件，也可只输入文件夹名称)
git add .

#提交到本地
git commit -m "commit message"

#推送到远程仓库
git push -u origin master
```



## 3. 提交代码到github

```perl
#初始化
git init
#绑定账号
git config user.name "yaoyaoling"
git config user.email "826623996@qq.com"
#关联远程仓库
git remote add origin <httpAddress>

#克隆
git clone <httpAddress>
git pull <httpAddress>

#添加到暂存
git add xxx

#描述信息
git commit -m "xxx"

#推送到远程
git push origin master
```



## 4. pull拉取最新代码

```perl
#本地仓库的代码还未被更新，此时：
#(1) 更新远程仓库的代码为最新的
git fetch --all

#(2) 让本地代码与origin / master完全相同
git reset --hard origin/master

#(3) git pull拉取远程代码
git pull origin master

#(4) git merge将暂存区代码更新到本地工作区
git merge master
```




## 5. git 关联仓库并上传代码

创建 git 仓库：

```perl
mkdir vuestart
cd vuestart
git init 
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin https://gitee.com/xxx/vuestart.git
git push -u origin "master"
```

已有仓库?

```perl
cd existing_git_repo
git remote add origin https://gitee.com/xdragon0/vuestart.git
git push -u origin "master"
```

查看关联的仓库

```perl
git remote -v
```



## 6. 关联已有仓库并提交代码

```perl
#第一步：找到适合位置，右键打开git工具
#第二步：克隆或拉取代码
git clone http://xxx.git
git pull http://xxx.git

#第三步：创建和切换分支
1.【git branch】查看一下本地分支，再【git branch -a】查看一下远程分支，对比下，远程存在哪些本地没有的新分支.
2.将某个远程主机的更新，全部取回本地：【git fetch】
3.再次查看远程分支：【git branch -a】 发现远程的分支已经可以看见了
4.拉取远程分支到本地：
创建远程分支并切换到该分支:【git checkout -b (远程分支名)】 
拉取远程分支代码到本地分支：【git pull origin (远程分支名称)]

#第四步：将要上传的代码拷贝到当前目录下
#第五步：上传并提交代码
git add xxx/
git commit -m "init-1.0"
git push origin feature

#其他命令：
git branch -r  //查看远程所有分支
git branch //查看本地所有分支
git branch -a //查看本地及远程的所有分支
git fetch  //将某个远程主机的更新，全部取回本地
git remote -v //查看仓库关联情况
git status //查看git状态
```

