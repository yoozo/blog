---
title: git如何管理文件
tags:
  - git
category:
  - git
date: 2019-05-20 00:22:42
---


> 你工作目录下的每一个文件都不外乎这两种状态：**已跟踪**或**未跟踪**。

| 树 | 用途 |
|----|----|
|HEAD | 上一次提交的快照，下一次提交的父结点 |
|Index | **暂存区**，预期的下一次提交的快照 |
|Working Directory | **工作区**，目录下用户看到的文件 |

<!-- more -->
下面是git常用的几个命令

## status
用于显示工作目录和暂存区的状态。
```bash
# 输出详细的文件状态
git status

# 输出简单的文件状态，状态意思看下表
git status -s
```
标识符是有两位的，第一位表示**暂存区**的文件状态，第二位表示是**工作区**的文件状态

| 标识 | 意思 |
|:--:|----|
| ?? | 未跟踪 |
| A  | 新添加 |
| M  | 被修改 |
| D  | 被删除 |


## diff
查看文件修改了那些内容
```bash
# 查看工作区修改的内容
git diff

# 查看暂存区stage中修改的内容
git diff --cached
git diff --staged
```



## add
使用命令 git add 开始跟踪一个文件，可以暂存**未跟踪文件**或者**已修改的跟踪文件**
```bash
# 把文件添加暂存区
git add <file>

# 跟踪所有未跟踪的文件
git add --all
```

## rm
删除暂存区以及目录的文件，并把这次修改记录到暂存区
```bash
# 删除文件，并删除暂存区文件
git rm <file>
# 其实就是执行了下面两个操作
rm <file>
git add <file>

# 删除目录
git rm -r <dir>
```

## commit

```bash
# 提交并且填写好备注信息
git commit -m '备注信息'

# 提交到上一次的提交的版本，即提交到HEAD
git commit --amend

# 撤回HEAD提交

```

## reset
移除已记录到暂存区中的文件修改
```bash
# 撤回文件修改
git reset HEAD <file>

# 查看其他撤回方法
git reset -h
```
