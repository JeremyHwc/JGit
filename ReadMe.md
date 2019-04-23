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

### 09 填充.git目录
```text
1. cat命令主要用来查看文件内容，创建文件，文件合并，追加文件内容等功能。
cat HEAD 查看HEAD文件的内容 
git cat-file 命令 显示版本库对象的内容、类型及大小信息。
git cat-file -t b44dd71d62a5a8ed3 显示版本库对象的类型
git cat-file -s b44dd71d62a5a8ed3 显示版本库对象的大小
git cat-file -p b44dd71d62a5a8ed3 显示版本库对象的内容

HEAD：指向当前的工作路径
config：存放本地仓库（local）相关的配置信息。
refs/heads:存放分支
refs/tags:存放tag，又叫里程牌 （当这次commit是具有里程碑意义的 比如项目1.0的时候 就可以打tag）
objects：存放对象 .git/objects/ 文件夹中的子文件夹都是以哈希值的前两位字符命名 每个object由40位字符组成，前两位字符用来当文件夹，后38位做文件。
```

### 10 commit、tree和blob三个对象之间的关系
![](/images/commit_tree_blob_relation.jpg)
git cat-file -p "file名称或者blob、commit、tree的hash值"：查看内容

### 11 数一数tree的个数
> 新建的Git库，有且仅有1个commit，仅仅包含/doc/readme，请问内含多少个tree，多少个blob？
![](/images/count_tree.jpg)

### 12 分离头指针情况下的注意事项

### 13 进一步理解HEAD和Branch

HEAD其实最终的指向都是指向一个具体的commit;  
1 一个节点，可以包含多个子节点（checkout 出多个分支）  
2 一个节点可以有多个父节点（多个分支合并）    
3 ^是\~都是父节点，区别是跟随数字时候，^2 是第二个父节点，而\~2是父节点的父节点  
4 ^和\~可以组合使用,例如 HEAD\~2^2  


> git diff :比较分支的区别


## 第二章 独自使用Git时的常见场景


### 1. 怎么删除不需要的分支？
> git branch -d branch_name

### 2. 怎么修改最新commit的message？

> git commit --amend

```
1、git log --oneline -5

    查看最近5次commit的简要信息，输出信息为：简短commitID commit_message，可以根据需要查看最近n次的提交

    也可以git log -5，输出信息相对详细些，commitID为完整的，这里只需要加上参数--oneline查看简短commitID即可

2、git rebase -i <简短commitID>

    如果需要修改从上往下第2个commit_message，这里的简短commitID为上面输出信息的第3个，以此类推

    在弹出的窗口中，以VIM编辑方式显示了最近两次的提交信息

3、（按照VIM操作）按i键，进入编辑模式，将想要修改的提交前的pick改为reword，如果需要修改多个，也可以将对应的多个pick改为reword

4、（按照VIM操作）按ESC键        再按 shift + :        然后输入wq（w是保存，q是退出）        按回车键

5、在弹出的窗口中，按i进入编辑模式，就可以修改commit_message了

6、（按照VIM操作）按ESC键        再按 shift + :        然后输入wq（w是保存，q是退出）        按回车键（同第4步）

    如果第3步中修改了多个pick为reword，则会多次弹出修改界面，重复第5~6步即可

7、再使用第1步的命令查看一下修改结果，git log --oneline -5或者git log -5，查看修改是否已经完成

8、最后强制push上去git push --force
```

### 3. 怎么修改老舅commit的message？