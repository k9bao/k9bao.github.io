# 1. brew

- [1. brew](#1-brew)
  - [1.1. 简介](#11-简介)
  - [1.2. 安装brew](#12-安装brew)
  - [1.3. 常用方法](#13-常用方法)
  - [1.4. 修改默认源](#14-修改默认源)
  - [1.5. 参考资料](#15-参考资料)

## 1.1. 简介

## 1.2. 安装brew

在Mac中打开Termal:  输入命令

`ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"`

## 1.3. 常用方法

- `brew install git` 安装
- `brew uninstall wget` 卸载
- `brew search /wge*/` 查询 /wge*/是个正则表达式， 需要包含在/中
- `brew list` 列出已安装的软件
- `brew update` 更新brew
- `brew home` 用浏览器打开brew的官方网站
- `brew info` 显示软件信息

## 1.4. 修改默认源

```shell
cd "$(brew --repo)"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
brew update
```

## 1.5. 参考资料

1. [官方网站](http://brew.sh)
2. [Mac安装brew并更改源](https://www.jianshu.com/p/22820319f71b)
