+++
title = "如何给普通用户添加sudo权限"
date = 2024-05-08T00:40:00+08:00
lastmod = 2024-05-08T00:40:22+08:00
draft = false
toc = true
+++

## linux用户添加sudo权限: {#linux用户添加sudo权限}

1.切换到root用户下,方法为直接在命令行输入:su,然后输入密码

{{< highlight nil >}}
$ su
passwd:
{{< /highlight >}}

2.添加sudoers文件的写权限
sudoers文件默认是只读的,对root来说也是,因此需先添加sudoer文件的写权限,执行下面的命令:

{{< highlight nil >}}
chmod u+w /etc/sudoers
{{< /highlight >}}

3.编辑sudoers文件,执行下面的命令

{{< highlight nil >}}
vi /etc/sudoers
{{< /highlight >}}

找到这行root  ALL=(ALL)  ALL,在他下面添加dream  ALL=(ALL)  ALL(这里dream是你的用户名)
根据需要可以选择下面四行中的一行:

{{< highlight nil >}}
youuser  ALL=(ALL)  ALL
%youuser  ALL=(ALL)  ALL
youuser  ALL=(ALL)  ALL  NOPASSWD:  ALL
%youuser  ALL=(ALL)  ALL  NOPASSWD:  ALL
{{< /highlight >}}

第一行:允许用户youuser执行sudo命令(需要输入密码).
第二行:允许用户组youuser里面的用户执行sudo命令(需要输入密码).
第三行:允许用户youuser执行sudo命令,并且在执行的时候不需要输入密码.
第四行:允许用户组youuser里面的用户执行sudo命令,并且在执行的时候不需要输入密码.
4.撤销sudoers文件的写权限

{{< highlight nil >}}
chmod u-w /etc/sudoers
{{< /highlight >}}
