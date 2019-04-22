# JGit
Git学习库

## 第一章 Git基础

### 01 课程综述
1. 版本管理的演变 
     
(1)VCS出现前       
·用目录拷贝区别不同版本    
·公共文件容易被覆盖      
·成员沟通成本很高，代码集成效率低下      

(2)集中式VCS   
·有几种的版本管理服务器；   
·具备文件版本管理和分支管理能力；    
·集成效率有明显地提高；    
·客户端必须时刻和服务器相连；     

(3)分布式VCS   
·服务端和客户端都有完整的版本库；   
·脱离服务端，客户端照样可以管理版本；             
·查看历史和版本比较等多数操作，都不需要访问服务器，比集中式VCS更能提高版本管理效率。

2. Git的特点       
·最优的存储能力；       
·非凡的性能      
·开源的        
·很容易做备份     
·支持离线操作     
·很容易定制工作流程      

3. 内容顺序     
**[Git](https://git-scm.com/book/zh/v2)**  
·GitHub     
·GitLab     

### 03 使用Git之前需要做的最小配置
1. 配置User信息
$ git config --global user.name 'your_name'
$ git config --global user.email 'your_email@domain.com'

global的作用：每一次的变更，在哪个时间点是谁做出的变更，在做codeReview的时候，每一次的变更如果带上了
用户的email地址，那么评审的人员在平台上面指出哪里有问题以后，Git会自动把变更者的email取出来，并发送邮件。 

缺省等同于local
```text
$ git config --local  (注：local只对某个仓库有效,优先于global设置的)
$ git config --global （global对当前用户所有仓库有效）
$ git config --system （system对系统所有登录的用户有效,不常用）
```

显示config的配置，加--list
```text
$ git config --list --local
$ git config --list --global
$ git config --list --system
```

### 04 创建第一个仓库并配置local用户信息
1. 建Git仓库
两种场景
(1)把已有的项目代码纳入Git管理
```text
$ cd 项目代码所在的文件夹
$ git init 
```
(2)新建的项目直接用Git管理
```text
$ cd 某个文件夹
$ git init yout_project  #会在当前路径下创建和项目同名称同名的文件夹
$ cd your project
```

## 05 通过几次commit来认识工作区和暂存区
1. 4次提交，一个像模像样的静态页面生成了
(1)加入index.html 和 git-logo
(2)加入style.css
(3)加入script.js
(4)修改index.html和style.css

```text
git 相关命令：

xcopy:Dos命令行复制文件及文件夹
git add **:添加到暂存区
git commit -m'reason':
git status:
git log:

git add -u：将文件的修改、文件的删除，添加到暂存区。
git add .：将文件的修改，文件的新建，添加到暂存区。
git add -A：将文件的修改，文件的删除，文件的新建，添加到暂存区。
工作中一般是用到 git add . 或者 git add -A, 今天学习更进一步解了 git add -u 以及他们之间的区别

git add -A相对于git add -u命令的优点 ： 可以提交所有被删除、被替换、被修改和新增的文件到数据暂存区，而git add -u 只能操作跟踪过的文件
git add -A 等同于git add -all
```

工作目录 -- git add files --> 暂存区 -- git commit --> 版本历史

### 06 给文件重命名的简便方法
```text
git mv README.md readme.md
```

### 07 通过git log 查看版本演变历史
```text
git log --oneline：log
git log -n4 --oneline:最近4次log
git branch -v:本地有多少分支

git checkout -b temp  dd856d901d76308f5729d767179c8e03ae0c0f76//创建分支

git log --all --graph//图形化的分支代码演进关系

$ git log --oneline --all -n4 --graph
* 61c59b7 (HEAD -> temp) 创建分支
| * 917e16a (origin/master, origin/HEAD, master) 学习给文件重命名mv命令
|/
* dd856d9 学习给文件重命名mv命令
* 86becce 学习git add commit status log 等相关命令

笔记：

•    git log --all 查看所有分支的历史
•    git log --all --graph 查看图形化的 log 地址
•    git log --oneline 查看单行的简洁历史。
•    git log --oneline -n4 查看最近的四条简洁历史。
•    git log --oneline --all -n4 --graph 查看所有分支最近 4 条单行的图形化历史。
•    git help --web log 跳转到git log 的帮助文档网页
```

### 08通过图形界面工具来查看版本历史
```text
gitk:开启图形界面查看版本管理界面
gitk 后面可以跟上文件的路径， 这样能看单个文件的修改历史的具体内容。
```

### 10 commit、tree和blob三个对象之间的关系


## 独自使用Git时的常见场景

### 1. 怎么删除不需要的分支？