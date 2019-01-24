---
title: GIT的使用
date: 2018-04-15 17:50:57
categories:
- GIT
tags:
- GIT
---

# 对Linux中GIT相关操作做个总结
<!--相关网站链接[linux_git][7]-->


---


## 创建仓库

分为三种方式:
- **创建工程目录后$git init**
- **$git init 工程名称**
- **$git clone [url]:例如:git clone git@github.com:huguanghui/linux.git**
- Linux上本地搭建Git服务器:
```shell
git daemon --reuseaddr --export-all --enable=receive-pack 
		--verbose --base-path=/root/GIT_local &
ufw allow 9418
```
注意当git push出现reject报错时, 仓库目录下执行chmod -R 777 *
---

<!--more-->

## 配置

- **显示当前配置:$git config - -list**
- **编辑Git配置文件:$git config -e [- -global]**
- **设置提交代码时的用户信息:**
```shell
git config [- -global] user.name "[name]" 
git config [- -global] user.email "[email address]"
```
## Github的认证

 - $ssh-keygen -t rsa -C "522146829@qq.com"           ##默认路径为~/.ssh/id_rsa
 - 将生成的~/.ssh/id_rsa.pub加入github的ssh列表中
 - 测试 ssh git@github.com
 

---


##  文件相关操作

- **添加指定文件到暂存区**
```shell
git add [file]
```
- **添加指定目录到暂存区**
```shell
git add [dir]
```
- **添加当前目录的所有文件到暂存区**
```shell
git add *
```
- **删除工作区文件,并将删除放入暂存区**
```shell
git rm [file] [file]
```
- **停止追踪指定文件,但该文件保留在工作区**
```shell
git rm --cached [file]
```
- **改名文件,并将这个改名文件放入暂存区**
```shell
git mv [file-original] [file-renamed]
```
----------


## 代码提交 ##

- **提交暂存区到仓库**
```shell
git commit -m [message]
```
- **提交指定文件到仓库**
```shell
git commit [file] .. -m [message]
```
- **提交工作区自上次commit之后的变化直接到仓库**
```shell
git commit -a
```
- **提交时显示所有diff信息**
```shell
git commit -v
```
- **如果代码没有任何变化,则用来改写上一次commit的提交信息**
```shell
git commit --amend -m [message]
```
- **重做上一次commit,并包括指定文件的新变化**
```shell
git commit --amend
```

## 分支 ##

- **列出所有本地分支**
```shell
git branch
```
- **列出所有远程分支**
```shell
git branch -r
```
- **列出所有本地分支和远程分支**
```shell
git branch -a
```
- **新建一个分支依然停留在当前分支**
```shell
git branch [new branch name]
```
- **新建分支切换分支**
```shell
git checkout -b [new branch name]
```
- **新建分支指向指定commit**
```shell
git branch [branch] [commit]
```
- **新建一个分支与指定远程连接建立追踪关系**
```shell
git branch --track [branch] [remote-branch]
```
- **切换到指定分区,并更新工作区**
```shell
git checkout [branch]
```
- **现有分支和远程分支建立追踪关系**
```shell
git branch --set-upstream [branch] [remote-branch]
```
- **合并指定分支到当前分支**
```shell
git merge [branch]
```
- **选择一个commit合并到当前分支**
```shell
git cherry-pick [commit]
```
- **删除分支**
```shell
git branch -d [branch]
```
- **删除远程分支**
```shell
git push origin --delete
git branch -dr
```
- **创建远程分支**
```shell
git push origin 本地分支名:远程分支名
```
- **查看分支的追踪关系**
```shell
git branch --v
```


---
## 标签 ##

- **列出所有tag**
```shell
git tag
```
- **新建一个tag在当前commit中**
```shell
git tag [tag]
```
- **新建一个tag在指定commit中**
```shell
git tag [tag] [commit]
```
- **查看tag信息**
```shell
git show [tag]
```
- **提交指定tag**
```shell
git push [remote] [tag]
```
- **提交所有tag**
```shell
git push [remote] --tags
```
- **新建一个分支,指向某个tag**
```shell
git checkout -b [branch] [tag]
```

---
## 查看信息 ##

- **显示有变更的文件**
```shell
git status
```
- **显示当前分支的历史版本**
```
git log
```
- **显示commit历史,以及每次commit发生变化的文件**
```shell
git log --stat
```
- **显示某个文件的版本历史,包括文件改名**
```shell
git log --follow [file]
git whatchanged [file]
```
- **显示指定文件相关的每一次diff**
```shell
git log -p  [file]
```

##仓库拉取
```shell
git pull <远程主机名>  <远程分支名>:<本地分支名>
```

---
##仓库同步##
```shell
git push -u <远程主机名>  <本地分支名>:<远程分支名>
git push origin 本地:master
```

---
## 远程同步 ##
- **将本地仓库与远程仓库关联**
```shell
git remote add origin git@github.com:huguanghui/hexo_blog.git
git push -u origin master
```
- **下载远程仓库的所有变动**
```shell
git fetch [remote]
```
- **显示所有远程仓库**
```shell
git remote -v
```
- **显示某个远程仓库的信息**
```shell
git remote show [remote]
```

---
## 撤销 ##

- **恢复暂存区的指定文件到工作区**
```shell
git checkout [file]
```
- **恢复某个commit指定文件到工作区**
```shell
git checkout [commit] [file]
```
- **恢复上一次commit的文件到工作区**
```shell
git checkout .
```
- **重置暂存区的指定文件,与上一次的commit保持一致,工作区不变**
```shell
git reset [file]
```
- **重置暂存区和工作区和上一次commit保持一致**
```shell
git reset --hard
```
- **重置当前分支的指针为commit,同时重置暂存区,工作区不变**
```shell
git reset [commit]
```
- **重置所有**
```shell
git reset  --hard [commit]
```
- **只重置Header,暂存区和工作区不变**
```shell
git reset --keep [commit]
```

---
## 过滤 ##

- **.gitignore的使用**

---
## 版本回退 ##

### 未使用git add ###
```shell
git checkout -- filepathname 放弃单个文件修改
git checkout . 放弃所有文件修改
```
### 使用了git add ###
```shell
git reset HEAD filepathname
git reset HEAD .
```
### 使用了git commit  ###
```shell
git reset --hard HEAD^ 退回上一次Commit的状态
git reset --hard commitid 退回对应id的的位置
```

## 账号和密码自动保存配置 ##

- 在你的用户目录下新建一个文本文件.git-credentials
 .git-credentials在文件中输入以下内容：https:{username}:{password}@github.com

- git config --global credential.helper store

---
<p style="color: red">
	注意事项:<源地址>：<目标地址>
</p>

---

[1]: http://math.stackexchange.com/
[2]: https://github.com/jmcmanus/pagedown-extra "Pagedown Extra"
[3]: http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
[4]: http://bramp.github.io/js-sequence-diagrams/
[5]: http://adrai.github.io/flowchart.js/
[6]: https://github.com/benweet/stackedit
[7]: http://www.cnblogs.com/probemark/p/5876821.html
