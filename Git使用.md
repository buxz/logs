---
title: Chrome搜索技巧
date: 2019-03-04 14:51:13
tags:
---
# 关联分支

>Idea 更新项目时，报错如下

```
    Can't Update
        No tracked branch configured for branch dev or the branch doesn't exist.
        To make your branch track a remote branch call, for example,
        git branch --set-upstream-to=origin/dev dev (show balloon)
```

- 使用Git 在本地新建一个分支后，需要做远程分支关联，如果没有关联会报错如上。
- 关联的目的是，在执行 git pull、 git push时，不需要指定对应的远程分支
> 解决方法如下：

```
git branch --set-upstream-to=origin/remote_branch  your_branch

其中，origin/remote_branch是你本地分支对应的远程分支；your_branch是你当前的本地分支。
```
