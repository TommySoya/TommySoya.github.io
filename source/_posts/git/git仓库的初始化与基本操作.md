---
title: git仓库的初始化与基本操作
date: 2024-04-16 17:16:22
tags: 
    - 技术总结
    - 学习笔记
description: 
    - 记录git仓库初始化、上游仓库设置等基本设置
---

git是软件开发过程中管理代码版本最常用的工具之一。本文用于记录笔者在使用git过程中的一些常用情景的操作，以供参考。
**官方文档**: [开始使用 Git](https://docs.github.com/zh/get-started/getting-started-with-git)


# 如何使用git管理项目

使用git管理项目，需要先初始化一个git仓库，然后将项目文件添加到仓库中，最后提交文件到仓库中。

## 创建git仓库

```bash
    mkdir <project>
    cd <project>
    git init
```
`git init`会在本地新建一个.git目录，用于存放git仓库的相关信息，这个目录就是你的本地git仓库。
## 初始化README和.gitignore文件

git仓库初始化后，需要创建一个README.md文件，用于记录项目的基本信息。同时，还需要创建一个.gitignore文件，用于记录不需要被git管理的文件类型。

在编写完README.md和.gitignore文件后，需要将文件提交到仓库中。目前我们只有一个本地仓库，下面是将文件提交到本地仓库的过程：`git add  -->  git commit -m 'commit message'`
```bash
    git add README.md
    git commit -m "add README"
    git add .gitignore
    git commit -m "add .gitignore"
```

在git中，文件有3种状态：<strong><span style="color: red;">untracked</span></strong>、<strong><span style="color: green;">tracked</span></strong>、<strong><span style="color: gray;">ignored</span></strong>。默认情况下，一个新创建的文件均为`untracked`状态，若要将其添加到git的文件树，需要执行`git add`操作，此时文件才可以被`commit`、`push`。

现有的git管理工具均会对每个新建的文件进行状态提示。以IDEA为例，未被追踪的文件被标记为<strong><span style="color: red;">红色</span></strong>，这些文件无法进行添加、推送等操作，直到它们成为被追踪的文件。
git还会默认识别`.gitignore`文件，这些文件则被标记为<strong><span style="color: gray;">ignored</span></strong>，不被文件树追踪。

```bash
    git status
```
可以通过`git status`命令查看当前仓库的状态。
<!-- TODO: branch分支概念，stash和stash pop -->

至此，本地的git仓库的使用逻辑和常用命令就被我们基本上都掌握了。下面，是一些使用远程仓库进行代码托管时需要熟悉的内容。

## 添加远程仓库

在本地仓库中，可以通过`git remote add origin <url>`命令将本地仓库与远程仓库建立连接。

```bash
    git remote add origin <url>
```

origin是远程仓库的默认名称，可以修改为其他名称。

## 推送文件到远程仓库

```bash
    git push -u origin master
```
    
`

### ERROR：.gitignore不生效

在.gitignore文件中新增需要忽略的文件后，若发现新增的文件仍然被追踪，则需要重新执行`git add`操作。
