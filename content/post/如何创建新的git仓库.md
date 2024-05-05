+++
title = "如何创建新的git仓库"
date = 2024-05-05T01:50:00+08:00
lastmod = 2024-05-05T22:56:40+08:00
draft = false
toc = true
+++

## 一.设置用户信息 {#一-dot-设置用户信息}

1.  配置用户名和邮箱
    1.  安装完git之后,要做的第一件事就是设置你的用户名和邮件地址.
        {{< highlight nil >}}
        git config --global user.name "username"

        git config --global user.email "example@qq.com"

        git config --list #查看config配置
        {{< /highlight >}}

2.  配置SSH key:
    1.  进入.ssh文件夹
        {{< highlight nil >}}
        cd ~/.ssh/
        {{< /highlight >}}

    2.  生成秘钥
        {{< highlight nil >}}
        ssh-keygen -t rsa -C "example@qq.com"
        {{< /highlight >}}

    3.  获取SSH key:
        -   根据命令行提示,获取以ssh-rsa的字符串(包括ssh-rsa),按回车键生成SSH Key(秘钥)

    4.  复制SSH key秘钥:
        -   SSH key生成的路径一般为~/.ssh下,打开id_rsa.pub,进行全选复制内容.

3.  复制公钥至github:
    -   登录github账号添加ssh key(将步骤2.4的内容粘贴上去),SSH key的位置为(settings--&gt;SSH and GPG keys--&gt;new SSH key)

4.  检测是否添加成功(本地终端输入下列内容,然后输入yes就好了)
    {{< highlight nil >}}
    ssh -T git@github.com
    {{< /highlight >}}


## 二).初始化仓库 {#二-dot-初始化仓库}

1.初始化本地仓库：

{{< highlight nil >}}
git init
{{< /highlight >}}

2.添加文件到仓库中：

{{< highlight nil >}}
git add .
{{< /highlight >}}

3.提交你的更改到本地仓库：

{{< highlight nil >}}
git commit -m "first commit"
{{< /highlight >}}

4.如果你还没有远程仓库,需要在远程(例如GitHub)上创建一个仓库

-   4.1.在github上新建仓库:
    -   获取仓库地址:<https://github.com/chaiguolong/git_test.git>

<!--listend-->

-   4.2.本地仓库操作:
    -   将默认分支替换为main(因为在2020年将默认分支由master切换为main)
        {{< highlight nil >}}
        git branch -M main
        {{< /highlight >}}
    -   将本地仓库的更改推送到远程仓库:
        {{< highlight nil >}}
        git remote add origin https://github.com/chaiguolong/git_test.git
        {{< /highlight >}}
    -   将本地仓库推送至远程仓库
        {{< highlight nil >}}
        git push -u origin main
        {{< /highlight >}}
