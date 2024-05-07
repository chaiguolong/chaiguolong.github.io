+++
title = "shell 脚本的疑难解惑"
date = 2024-05-07T17:51:00+08:00
lastmod = 2024-05-07T19:29:57+08:00
draft = false
toc = true
+++

## 1.shell -z和-n的使用区别 {#1-dot-shell-z和-n的使用区别}

-   -n: 字符串长度不等于0为真,助记符:no zero
-   -z: 字符串长度等于0为真,助记符:zero


## 2.git误上传了不需要上传的文件夹 {#2-dot-git误上传了不需要上传的文件夹}

一.当我们需要删除暂存区或分支上的文件,但本地又需要使用,只是不希望
这个文件被版本控制,可以使用:

{{< highlight nil >}}
git rm -r --cached 文件夹或文件名
git commit -m "delete remote somefile"
git push origin HEAD:当前分支(通常就是git push)
{{< /highlight >}}

二.当我们需要删除暂存区或分支上的文件,同时工作区也不需要这个文件了
可以使用:

{{< highlight nil >}}
git rm file_path
git commit -m "delete somefile"
git push
{{< /highlight >}}


## 3.bash内建命令和关键字的区别 {#3-dot-bash内建命令和关键字的区别}

-   1.内建命令值得就是包含在Bash工具包中的命令.
-   2.关键字的意思就是保留字.

对于shell来说关键字具有特殊的含义,
并且用来构建shell语法结构.比如:"for","while","do",和"!"都是关键字.
与内建命令相似的是:关键字也是Bash的骨干部分,但是与内建命令不同的是,
关键字本身并不是一个命令,而是一个比较大的命令结构的一部分.
