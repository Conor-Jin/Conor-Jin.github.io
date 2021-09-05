---
title: git报错记录
tags: []
id: '154'
categories:
  - - 前端
date: 2018-10-12 00:31:10
---

Q：The file will have its original line endings in your working directory. S：

git rm -r --cached ./

git config core.autocrlf false

git add ./

  Q: You have not concluded your merge (MERGE\_HEAD exists). Please, commit your changes before you can merge. Analytical : 错误可能是因为以前pull下来的代码没有自动合并导致的 S: 1.**保留你本地的修改**

git merge --abort
git reset --merge

合并后记得一定要提交这个本地的合并，然后在获取线上仓库

git pull

2.**.down下线上代码版本,抛弃本地的修改**

git fetch --all

git reset --hard origin/master

git fetch

  Q: The file will have its original line endings in your working directory. Analytical : 原因是路径中存在 / 的符号转义问题，false就是不转换符号默认是true，相当于把路径的 / 符号进行转义，这样添加的时候就有问题 S:

git config --global core.autocrlf false

  Q: fatal: remote origin already exists. S: 先删除

git remote rm origin

再次执行上次操作即可