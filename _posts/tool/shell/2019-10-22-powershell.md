---
layout: post
title: powershell
date: 2019-11-08 17:45:20
description: powershell
tag: windows

---

# powershell常用命令

## 问题集合

- 环境变量操作

$env：中的环境变量只是机器环境变量的一个副本，即使你更改了它，下一次重新打开时，又会恢复如初。

获取环境: $env:<变量名>
修改环境变量: $env:OS="Redhat Linux"    $env:OS=$env:OS";C:\work\go\bin"
删除换变量: del env:windir

获取所有环节变量值: Get-ChildItem env 或 dir env: 其中dir是Get-ChildItem的别名

- 运行 bat 脚本
  cmd /c test.bat

## 参考资料

- [PowerShell获取系统环境变量的方法](https://blog.csdn.net/WuLex/article/details/78193273)