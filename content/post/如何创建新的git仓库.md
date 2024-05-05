+++
title = "如何创建新的git仓库"
date = 2024-05-05T01:50:00+08:00
lastmod = 2024-05-05T19:02:06+08:00
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

2.  生成SSH key:
    1.  进入.ssh文件夹
        {{< highlight nil >}}
        cd ~/.ssh/
        {{< /highlight >}}

    2.  生成秘钥
        {{< highlight nil >}}
        ssh-keygen -t rsa -C "example@qq.com"
        {{< /highlight >}}

    3.  获取SSH key: 根据命令行提示,获取以ssh-rsa的字符串(包括ssh-rsa),按回车键生成SSH Key(秘钥)

3.  SSH key生成的路径一般为~/.ssh下,打开id_rsa.pub,进行全选复制内容.

4.  登录github账号添加ssh key(将第四部的内容粘贴上去),SSH key的位置为(settings--&gt;SSH and GPG keys--&gt;new SSH key)

5.  检测是否添加成功(本地终端输入下列内容,然后输入yes就好了)
    {{< highlight nil >}}
    ssh -T git@github.com
    {{< /highlight >}}
