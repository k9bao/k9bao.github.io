---
layout: post
title: git-push
date: 2019-11-20 14:18:38
description: git-push
tag: git

---

# 1. git add-commit-push

- [1. git add-commit-push](#1-git-add-commit-push)
  - [1.1. add/rm](#11-addrm)
    - [1.1.1. 相关概念](#111-相关概念)
    - [1.1.2. 常用命令](#112-常用命令)
  - [1.2. commit](#12-commit)
    - [1.2.1. 相关概念](#121-相关概念)
    - [1.2.2. 常用命令](#122-常用命令)
  - [1.3. push](#13-push)
    - [1.3.1. 相关概念](#131-相关概念)
    - [1.3.2. 常用命令](#132-常用命令)
  - [1.4. 参考资料](#14-参考资料)

## 1.1. add/rm

### 1.1.1. 相关概念

add 添加文件,此操作会添加到暂存区
rm 从缓存区移除文件

### 1.1.2. 常用命令

`git add <file>` 添加文件到Git暂存区注意，可反复多次使用
`git rm --cached/-r <file>` 从暂存区移除文件,和git add相对应,-f会同时删除本地文件，--cached会保留本地问题

可以使用通配符

## 1.2. commit

### 1.2.1. 相关概念

从暂存区提交数据到本地仓库，这里会产生唯一的commit_id

### 1.2.2. 常用命令

`git commit -m "message"` 提交某个分支到本地创库，这里会产生唯一 commit_id
`git commit --amend` 提交当前暂存区数据到上一次提交

## 1.3. push

### 1.3.1. 相关概念

说明: branch-name表示分支名称, origin表示远程主机名

- push分类，查看当前环境 push 模式 `git config --get push.default`
  - nothing - push操作无效，除非显式指定远程分支，例如git push origin develop（我觉得。。。可以给那些不愿学git的同事配上此项）。
  - current - push当前分支到远程同名分支，如果远程同名分支不存在则自动创建同名分支。
  - upstream - push当前分支到它的upstream分支上（这一项其实用于经常从本地分支push/pull到同一远程仓库的情景，这种模式叫做central workflow）。
  - simple - simple和upstream是相似的，只有一点不同，simple必须保证本地分支和它的远程upstream分支同名，否则会拒绝push操作。
  - matching - push所有本地和远程两端都存在的同名分支。

git2.0之前的版本，push.default = matching，git push后则会推送当前分支代码到远程分支
2.0之后，push.default = simple，如果没有指定当前分支的upstream分支，就会收到上文的fatal提示

### 1.3.2. 常用命令

`git push --set-upstream origin master` 或 `git push -u origin master`  
--set-upstream可缩写为-u
第一次推送分支到远端

`git push` 非第一次推送分支道远端

`git push -f` 强制推送，覆盖origin的内容，可以回退

## 1.4. 参考资料

1. [Git push与pull的默认行为](https://segmentfault.com/a/1190000002783245)
