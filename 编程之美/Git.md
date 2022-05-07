# github

## 1. github base command

```perl
#1.把这个目录变成Git可以管理的仓库
git init 
#2.本地README.md文件添加到远程仓库
git add README.md 
#3.不但可以跟单一文件，还可以跟通配符，更可以跟目录。一个点就把当前目录下所有未追踪的文件全部add了，注意空格
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



## 2. 上传文件到github

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

## 3. 拉去远程仓库

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
```



