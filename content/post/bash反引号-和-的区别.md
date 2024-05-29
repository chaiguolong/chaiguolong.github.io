+++
title = "Bash反引号,$()和${} 的区别"
date = 2024-05-22T16:33:00+08:00
lastmod = 2024-05-22T16:33:48+08:00
draft = false
toc = true
+++

## 1.命令替换 {#1-dot-命令替换}


### 命令替换有两种方式: {#命令替换有两种方式}

-   反引号 <br/>
-   $() <br/>

反引号和$()的作用相同,用于命令替换,即完成引用命令的执行, <br/>
将其结果替换出来,与变量替换差不多.(简单说就是先运行里面的命令) <br/>

{{< highlight bash >}}
echo `date  +%Y-%m-%d-%H`
#或
echo $(date +%Y-%m-%d-%H)
{{< /highlight >}}

在shell脚本中建议使用$(),原因主要有两个: <br/>

-   (1) 反引号与单引号外形相似,容易混淆. <br/>
-   (2) 在多层次的符合替换中,内层反引号需要转义,而$()比较直观. <br/>


## 2.变量替换 {#2-dot-变量替换}


### 2.1直接变量替换 {#2-dot-1直接变量替换}

一般情况下,\\(var与\\){var}并没有区别,但用${}会比较精确的界定变量名的名称范围, <br/>
比方说: <br/>

{{< highlight bash >}}
AB="I am AB"
A="dablelv"
echo $AB
{{< /highlight >}}

原本是打算先将\\(A的结果替换出来,然后再补一个B字母于其后,但在命令行上,
真正的结果却是只会替换变量名称为AB的值.若使用\\){}就没有问题了. <br/>

{{< highlight bash >}}
AB="I am AB"
A="dablelv"
echo ${A}B
{{< /highlight >}}


### 2.2特殊变量替换 {#2-dot-2特殊变量替换}

${}除了直接替换变量内容,还有一些字符串变量的特殊功能. <br/>
假设我们定义了一个字符串变量为: <br/>

{{< highlight bash >}}
file='/dir1/dir2/dir3/my.file.txt'
{{< /highlight >}}

-   字符串提取 <br/>
    字符串提取可以使用\\({:}和\\){::}. <br/>
    1.  \\({var:n}
                  若n为正数,n从0开始,表示在变量var中提取第n个字符到末尾的所有
                  字符.若n为负数,提取字符串最后面n的绝对值个字符,使用时在冒号
                  后面加空格或一个算术表达式或整个num加上括号,如\\){var: -2}, <br/>
        \\({var:1-3}或\\){var:(-2)}均表示提取最后两个字符. <br/>
        {{< highlight bash >}}
        file='/dir1/dir2/dir3/my.file.txt'
        # 提取第一个字符及其后面的所有字符:
        # dir1/dir2/dir3/my.file.txt
        echo ${file:1}
        # 提取最后3个字符,注意冒号后面添加一个空格:txt
        echo ${file: -3}
        # 提取最后3个字符,冒号后米娜不需要添加空格:txt
        echo ${file:1-4}
        # 提取最后3个字符,冒号后面不需要添加空格:txt
        echo ${file:(-3)}
        {{< /highlight >}}
    
    2.  ${var:n1:n2} <br/>
        ${var:n1:n2}用于提取下标n1开始后面n2个字符,其中下标n1与n2 <br/>
        从0开始.如果长度n2为0,结果为空. <br/>
        {{< highlight bash >}}
        file='/dir1/dir2/dir3/my.file.txt'
        # 提取最左边的5个字符
        echo ${file:0:5}
        # 提取从第5个字符开始右边的连续5个字符:/dir2
        echo ${file:5:5}
        {{< /highlight >}}

-   字符串替换 <br/>
    ${var/pattern/pattern}表示将var字符串第一个匹配的pattern替换为 <br/>
    另一个pattern.不改变原有变量. <br/>
    {{< highlight bash >}}
    file='/dir1/dir2/dir3/my.file.txt'
    # 将第一个dir替换为path: /path1/dir2/dir3/my.file.txt
    echo ${file/dir/path}
    # 将全部dir替换为path:/path1/path2/path3/my.file.txt
    echo ${file//dir/path}
    {{< /highlight >}}

-   字符串截断 <br/>
    可以过滤掉符合指定规则的字符串,不改变源变量 <br/>
    {{< highlight bash >}}
    file='/dir1/dir2/dir3/my.file.txt'
    # 拿掉第一个/及其左边的字符串:dir1/dir2/dir3/my.file.txt
    echo ${file#*/}
    # 拿掉最后一个/及其左边字符串:my.file.txt
    echo ${file##*/}
    # 拿掉最后一个/及其右边的字符串:/dir1/dir2/dir3
    echo ${file%/*}
    # 拿掉第一个/及其右边的字符串:空串
    ${file%%/*}
    {{< /highlight >}}
    记忆方法为: <br/>
    
    1.  \#去掉左边,在键盘上#在%左边 <br/>
    
    2.  %去掉右边,在键盘上%在#右边 <br/>
    
    3.  一个符号是最小匹配,两个符号是最大匹配 <br/>

