git 配置 https和ssh 免密码登录

一. 区分https clone 和 ssh clone

不同的克隆方式导致校验方式不同，对应的免秘方式也不一样。
https通过记住账号密码免登，ssh通过校验生成的密钥免登。 通常都用ssh校验。

 

二.https免密配置方法

设置配置 .git/config

git config --global credential.helper store

[credential]  
    helper = store

输入一次账号密码后第二次就会记住账号密码。

 

三.ssh免密配置方法

配置信息

git init

git config --global user.name '用户名'

git config --global user.email '用户邮箱'

执行生成公钥和私钥的命令:

ssh-keygen -t rsa

按回车3下     一般都是直接不写为空   直接回车

执行查看公钥的命令:

cat ~/.ssh/id_rsa.pub

文件windows位置：

 

 

github添加 你的ssh操作步骤：

 

clone项目搞定：

git clone  git@github.com:'项目url'

 

 

git常用操作命令

提交步骤:

git status                查看状态
git add .                 添加所有的修改文件
git status                查看状态
git commit -m '备注信息'   添加备注
git push origin 分支名     提交到分支上

分支合并master:

git checkout master             切到master分支
git pull origin master          拉取master
git merge origin 需合并分支名     合并分支
git status                      查看状态
git push origin master          推送master

 

--git本地项目代码上传至远程仓库操作 :
复制代码

初始化:
git init

本地第一次安装git,先配置基本的信息：
git config--global user.name '用户名'
git config --global user.email '用户邮箱'

本地仓库与远程仓库关联: 
git remote add origin '项目url' 

更新项目,确保没有和远程仓库的代码有冲突: 
git pull --rebase origin master 

把项目复制到，本地git目录下准备上传。 

操作提交master步骤: 
git add . 
git status 
git commit -m '备注信息' 
git push origin master -f     第一次使用,强制提交master分支.（以后提交最好不要使用！）

复制代码

 

--文件目录操作命令

mkdir *   创建一个空目录 *指目录名
pwd       显示当前目录的路径。
cat *     查看*文件内容
git rm *  删除**文件

--git初始化操作

git init                   把当前的目录变成git仓库，生成隐藏.git文件。
git remote add origin url  把本地仓库的内容推送到GitHub仓库。
git clone git@url/test.git 从远程库克隆
git add *                  把x文件添加到暂存区去。
git commit –m "*"          提交文件 –m 后面的是注释。

 --git 克隆分支

git clone xxx.git                最简单直接的命令
git clone xxx.git "指定目录"      clone到指定目录
git clone -b branchname xxx.git  clone时创建新的分支替代默认Origin HEAD（master）

--查看命令

git status        查看仓库状态
git diff  *       查看X文件修改了那些内容   
git log           查看历史记录
git reflog        查看历史记录的版本号id（记录你的每一次命令,不论是否提交）
git log --pretty=oneline 如果信息量太多可以进行比较好的列表显示

--版本回退

git reset –hard HEAD^       回退到上一个版本
git reset --hard HEAD~第几个 如果想回退到第3个版本，使用git reset –hard HEAD~3
git reset --hard 057d       回退到某一个具体的版本号

 --撤销修改

git checkout file-name 恢复某个已修改的文件（撤销未提交的修改）：
git revert HEAD        还原最近一次提交的修改：
git revert commit-id   还原指定版本的修改

--分支管理
复制代码

git branch                   查看本地所有的分支
git branch -a                查看远程所有的分支
git branch name              创建分支
git branch –d dev            删除dev分支
git push origin --delete dev 删除远程的dev分支
git branch -m dev develop    重命名分支

git checkout –b dev          创建dev分支 并切换到dev分支上
git merge dev                在当前分支上合并dev分支代
git push origin zyf-dev      把当前新疆的zyf-dev分支推送到远程库(远程仓库没有给分支则会新建立该分支)
 
git checkout — *                     把XX文件在工作区的修改全部撤销。
git checkout master                  切换回master分支
git push --set-upstream origin dev   提交修改并创建远程分支dev

复制代码

--tag相关操作

git tag         列出所有的tag
git tag name    打轻量标签 name
git tag -d name 删除本地的tag
git push origin --delete tag name  删除远程的tag
git show name        查看tag信息
git push origin name 将tag提交到远程

--隐藏的文件

git stash       把当前的工作隐藏起来 等以后恢复现场后继续工作
git stash list  查看所有被隐藏的文件列表
git stash apply 恢复被隐藏的文件，但是内容不删除
git stash drop  删除文件
git stash pop   恢复文件的同时 也删除文件

--查看远程库信息(git  remote的用法)

git remote       查看远程库的信息
git remote –v    查看远程库的详细信息
git remote add  name url          添加远程仓库
git remote rename oldname newname 重命名仓库
git remote rm                     删除仓库

--将远程分支拉取到本地

方法一：git checkout -b 本地分支名x origin/远程分支名x
方式二：git fetch origin 远程分支名x:本地分支名x

--git pull操作
复制代码

git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并，基本的格式如下。
$ git pull <远程主机名> <远程分支名>:<本地分支名>
  
取回origin主机的next分支，与本地的master分支合并，需要写成下面这样
$ git pull origin next:master
  
如果远程分支是与当前分支合并，则冒号后面的部分可以省略。
$ git pull origin next
  
上面命令表示，取回origin/next分支，再与当前分支合并。实质上，这等同于先做git fetch，再做git merge。
$ git fetch origin
$ git merge origin/next
 
在某些场合，Git会自动在本地分支与远程分支之间，建立一种追踪关系(tracking)。比如，在git clone的时候，
所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动”追踪”origin/master分支。
Git也允许手动建立追踪关系。
git branch --set-upstream master origin/next

上面命令指定master分支追踪origin/next分支。如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名。
$ git pull origin




thanks: [echo 曦]https://www.cnblogs.com/cxx8181602/p/11125539.html