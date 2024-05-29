+++
title = "shell 脚本的疑难解惑"
date = 2024-05-07T17:51:00+08:00
lastmod = 2024-05-24T14:57:09+08:00
draft = false
toc = true
+++

## 1.shell -z和-n的使用区别 {#1-dot-shell-z和-n的使用区别}

-   -n: 字符串长度不等于0为真,助记符:no zero <br/>
-   -z: 字符串长度等于0为真,助记符:zero <br/>


## 2.git误上传了不需要上传的文件夹 {#2-dot-git误上传了不需要上传的文件夹}


### 一.当我们需要删除暂存区或分支上的文件,但本地又需要使用,只是不希望这个文件被版本控制,可以使用: {#一-dot-当我们需要删除暂存区或分支上的文件-但本地又需要使用-只是不希望这个文件被版本控制-可以使用}

{{< highlight nil >}}
git rm -r --cached 文件夹或文件名
git commit -m "delete remote somefile"
git push origin HEAD:当前分支(通常就是git push)
{{< /highlight >}}


### 二.当我们需要删除暂存区或分支上的文件,同时工作区也不需要这个文件了,可以使用: {#二-dot-当我们需要删除暂存区或分支上的文件-同时工作区也不需要这个文件了-可以使用}

{{< highlight nil >}}
git rm file_path
git commit -m "delete somefile"
git push
{{< /highlight >}}


## 3.bash内建命令和关键字的区别 {#3-dot-bash内建命令和关键字的区别}

-   1.内建命令值得就是包含在Bash工具包中的命令. <br/>
-   2.关键字的意思就是保留字. <br/>

对于shell来说关键字具有特殊的含义, <br/>
并且用来构建shell语法结构.比如:"for","while","do",和"!"都是关键字. <br/>
与内建命令相似的是:关键字也是Bash的骨干部分,但是与内建命令不同的是, <br/>
关键字本身并不是一个命令,而是一个比较大的命令结构的一部分. <br/>


## 4.curl 一些选项的解释 {#4-dot-curl-一些选项的解释}

-   -s参数将不输出错误和进度信息 <br/>
-   -o参数将服务器的回应保存成文件 <br/>


## 5.Linux shell 中\\(() \` \`，\\){}，$[] $(())，[ ] (( )) [{{< relref "bash反引号-和-的区别" >}}]({{< relref "bash反引号-和-的区别" >}})作用与区别 {#5-dot-linux-shell-中----------post-bash反引号-和-的区别-dot-pre-processed-dot-md-作用与区别}


### 1.$( )与\` \`(反引号)都是用来做命令替换用(commandsubstitution)的. {#1-dot-----与--反引号--都是用来做命令替换用--commandsubstitution--的-dot}


### 2.${var}和$var是用来变量替换的 {#2-dot-var-和-var是用来变量替换的}


### 3.\\([]和\\)(())是用来数学运算的. {#3-dot-和----是用来数学运算的-dot}


## 6.update和upgrade的区别 {#6-dot-update和upgrade的区别}

-   update:命令只会获得系统上所有包的最新信息,并不会下载或者安装任何一个包. <br/>
-   upgrade:命令来把这些包下载和升级到最新版本.

