---
title: git记录
tags: []
id: '152'
categories:
  - - 其他
date: 2018-10-12 00:28:28
---

上一篇文章已经写好了，如何配置。这篇文章主要记录日常使用的git 命令。

## **一、提交**

已有的一个项目，要把它托管到git（git也有）上去。 1.在工程的路径下 git init ： 建一个裸仓库 2.git remote add origin 远程仓库地址 ：将本地的仓库和远程仓库关联 3.git pull origin master :将远程仓库的东西拉下来，与本地仓库合并 注：因为两个仓库都有代码 可能冲突 比如 README.md 可自由选择保留那个 // 下面三步常规操作 4.git add  .    :将文件存进暂存区 5.git commit -am "提交的信息" 6.git push -u origin master    :提交到远程仓库

## 二、更新

把本地代码更新到 git 上面

1.  git status:  显示工作树的差异，即代码有无变更
2.  git add  .    :将文件存进暂存区
3.  git commit -m "提交的信息"
4.  git push

## 三、拉取

暴力的从git上面拉取，直接更新，不通过分支 1.git pull:  把远程代码拉到本地

## 四、git基础配置

1.git config --list：查看git配置信息 2.git config user.name :  查看当前用户名 3.git config user.email:   查看当前邮箱 4.git config --global user.name "name":  全局配置用户名 5.git config --global user.email "xx@xx.com":  全局配置邮箱  

## 五、从git/gitlab等上面拉取代码到本地

1.git clone http://\*\*\*\*\*\*\*.git 2.输入邮箱、密码即可    

## 六、git取消追踪已上传文件

1. （node\_modules文件夹示例）列出你需要取消跟踪的文件，查看列表

git rm -r -n --cached node\_modules

  2.  取消缓存不想要跟踪的文件

git rm -r --cached node\_modules

  3.根目录下新建.gitignore，添加忽略文件 4.提交  

## 七、放弃本地修改，直接覆盖

git reset --hard

 

## 八、新建远程分支

git checkout -b \[branch\_name\]  //新建本地为\[branch\_name\]的分支并切换至\[branch\_name\]分支

 

## 九、推送当前分支并建立与远程上游的跟踪

git push --set-upstream origin \[branch\_name\]

 

## 十、合并分支

1.切换分支

git checkout 1

2.合并分支

git merge 2

注： 1为主分支，2为要合并到1的分支 3. 同步  

## 十一、删除分支

1.删除远程分支

git push origin --delete \[branch\_name\]

2.删除本地分支

git branch -d \[branch\_name\]

3.查看本地分支验证

git branch -r

 

## 十二、查看远程分支

1.查看远程分支

 git branch -r

2.查看远程分支不全，更新

git fetch

 

## 十三、远程拉取指定分支\[branch\_name\]，并且创建指定分支\[branch\_name\]，并切换

git checkout -b \[branch\_name\] origin/\[branch\_name\]

 

## 十四、取消指定的提交内容

分两种情况，因为 commit 分为两种：一种是常规的 commit，也就是使用 git commit 提交的 commit；另一种是 merge commit，在使用 git merge 合并两个分支之后，你将会得到一个新的 merge commit 1.revert 常规 commit

git revert <commit id>

git 会生成一个新的 commit，将指定的 commit 内容从当前分支上撤除。   2.revert merge commit 但如果直接使用 git revert <commit id>，git 也不知道到底要撤除哪一条分支上的内容，这时需要指定一个 parent number 标识出"主线"，主线的内容将会保留，而另一条分支的内容将被 revert。需要注意的是 -m 选项接收的参数是一个数字，数字取值为 1 和 2，也就是 Merge 行里面列出来的第一个还是第二个。 我们要 revert will-be-revert 分支上的内容，即 保留主分支，应该设置主分支为主线，操作如下：

git revert -m 1 <commit id>

[参考](http://blog.psjay.com/posts/git-revert-merge-commit/)    

## 十五、从某次提交中创建分支

git checkout \[commit id\] -b \[branch\_name\]