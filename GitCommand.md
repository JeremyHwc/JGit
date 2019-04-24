# Git命令


> git init：创建仓库  
> git status：查看仓库当前的状态  
> git diff:查看修改内容  
> git log:查看日志  
> git log --pretty=oneline：单行查看日志
> git log --oneline:单行查看日志

> git reset --hard HEAD^:当前版本回退到上一个版本
> git reset --hard HEAD`100:当前版本回退100个版本
> git reset --hard <798b61e85394bb489>：回退到具体版本

> git reflog:记录的每一次命令  
> git diff HEAD -- readme.txt：查看工作区和版本库里面最新版本的区别


> git checkout -- readme.txt：把readme.txt文件在工作区的修改全部撤销，命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令

> git rm <file>:git 删除一个文件

> git merge <branchname>:用于合并指定分支到当前分支
> git branch -d <branchname>：删除指定分支
> git branch ：查看分支
> git branch <name>：创建分支
> git checkout <name>：切换分支
> git checkout -b <name>：创建+切换分支
> git merge <name>：合并某分支到当前分支
> git branch -d <name>：删除分支

## 解决冲突
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。

## 分制管理策略
通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
> git merge --no-ff -m "merge with no-ff" dev
因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去

## Bug分支
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。

## Feature分支
添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

## 多人协作
多人协作的工作模式通常是这样：

1. 首先，可以试图用git push origin <branch-name>推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
4. 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

1. 查看远程库信息，使用git remote -v；
2. 本地新建的分支如果不推送到远程，对其他人就是不可见的；
3. 从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
4. 在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
5. 建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

6. 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

## Rebase
1. rebase操作可以把本地未push的分叉提交历史整理成直线；
2. rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

## 标签管理
### 创建标签
1. 命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；

2. 命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；

3. 命令git tag可以查看所有标签。
### 操作标签
1. 命令git push origin <tagname>可以推送一个本地标签；

2. 命令git push origin --tags可以推送全部未推送过的本地标签；

3. 命令git tag -d <tagname>可以删除一个本地标签；

4. 命令git push origin :refs/tags/<tagname>可以删除一个远程标签。
