# 1. git补丁

- [1. git补丁](#1-git补丁)
  - [1.1. 简介](#11-简介)
  - [1.2. patch 和diff 的区别](#12-patch-和diff-的区别)
  - [1.3. 创建patch和diff](#13-创建patch和diff)
  - [1.4. 应用patch和diff](#14-应用patch和diff)
  - [1.5. 冲突解决](#15-冲突解决)
  - [1.6. 参考资料](#16-参考资料)

## 1.1. 简介

补丁是一个文本文件，其内容类似于git diff，但与代码一样，它也有关于提交的元数据; 例如提交ID，日期，提交消息等。我们可以从提交创建一个补丁，而其他人可以将它们应用到他们的存储库。

## 1.2. patch 和diff 的区别

Git 提供了两种补丁方案，一是用git diff生成的UNIX标准补丁`.diff`文件，二是`git format-patch`生成的Git专用`.patch` 文件。
`.diff`文件只是记录文件改变的内容，不带有commit记录信息,多个commit可以合并成一个diff文件。
`.patch`文件带有记录文件改变的内容，也带有commit记录信息,每个commit对应一个patch文件。

在Git下，我们可以使用.diff文件也可以使用`.patch` 文件来打补丁，主要应用场景有：CodeReview、代码迁移等。

## 1.3. 创建patch和diff

创建patch 文件的常用命令行

1. 某次提交（含）之前的几次提交
   `git format-patch 【commit sha1 id】-n`
2. 个提交的patch
   `git format-patch 【commit sha1 id】 -1`
3. 某两次提交之间的所有patch
   `git format-patch 【commit sha1 id】..【commit sha1 id】`

创建diff文件的常用方法
`git diff  【commit sha1 id】 【commit sha1 id】 >  【diff文件名】`

## 1.4. 应用patch和diff

应用patch和diff的相关命令行

1. 检查patch/diff是否能正常打入
    `git apply --check 【path/to/xxx.patch】`
    `git apply --check 【path/to/xxx.diff】`
2. 复制代码打入patch/diff
    `git apply 【path/to/xxx.patch】`
    `git apply 【path/to/xxx.diff】`
3. 复制代码或者
    `git  am 【path/to/xxx.patch】`

## 1.5. 冲突解决

1. 执行命令 `git  am xxxx.patch` 尝试直接打入补丁。因为我们使用的 patch 已经过时了，所以这一步肯定会报错并中断（注意，虽然命令停止执行了，但我们依然处于`git am`命令的运行环境中，可以通过`git status`命令查看到当前的状态）。
2. 执行命令 `git  apply --reject  xxxx.patch` 自动合入 patch 中不冲突的代码改动，同时保留冲突的部分。这些存在冲突的改动内容会被单独存储到目标源文件的相应目录下，以后缀为 .rej 的文件进行保存。比如对 `./test/someDeviceDriver.c` 文件中的某些行合入代码改动失败，则会将这些发生冲突的行数及内容都保存在 `./test/someDeviceDriver.c.rej` 文件中。我们可以在执行 `git am` 命令的目录下执行 `find  -name  *.rej` 命令以查看所有存在冲突的源文件位置。
3. 依据 步骤2 中生成的 `*.rej` 文件内容逐个手动解决冲突，然后删除这些 `*.rej` 文件。完成这一步骤的操作后，我们就可以继续执行 git am 的过程了。
4. 执行命令 `git  status` 查看当前改动过的以及新增的文件，确保没有多添加或少添加文件。
5. 执行命令 `git  add .` 将所有改动都添加到暂存区（注意，关键字add后有一个小数点 . 作为参数，表示当前路径）。
6. 执行命令 `git  am  --resolved` 继续 步骤1 中被中断的 patch 合入操作。合入完成后，会有提示信息输出。
7. 执行命令 `git  log` 确认合入状态。
至此，带有冲突代码的 patch 合入就操作完成了。如果要修改 commit 信息，执行 `git commit --amend` 命令即可。

说明：在打入patch冲突时，可以执行`git am --skip`跳过此次冲突，也可以执行`git am --abort`回退打入patch的动作，还原到操作前的状态。

## 1.6. 参考资料

1. [Git 打补丁-- patch 和 diff 的使用（详细）](https://juejin.im/post/5b5851976fb9a04f844ad0f4)