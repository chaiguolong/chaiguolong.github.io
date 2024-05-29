+++
title = "shell脚本中单中括号和双中括号的区别"
date = 2024-05-07T18:49:00+08:00
lastmod = 2024-05-09T12:03:50+08:00
draft = false
toc = true
+++

## 1.概述: {#1-dot-概述}

在Bash中比较变量时,我们通常交替使用单括号([])和双括号([[]]).例如,我们可以在检 <br/>
查3是否等于3时使用表达式[3 -eq 3]或者[\\[3 -eq 3]\\]两者都将成功比较,那么它们之 <br/>
间有什么区别呢?在本教程中,我们将讨论Bash中单括号和双括号之间的区别. <br/>


## 2.主要区别 {#2-dot-主要区别}

在本节中,我们将简要讨论单括号和双括号之间的主要区别. <br/>


### 2.1单括号 {#2-dot-1单括号}

[是shell的内置命令,在Unix和Linux中始终可用于计算表达式.它仍然存在是为了向后 <br/>
兼容和POSIX合规性. <br/>


#### [和test之间的唯一区别是我们必须使用]来包围比较. {#和test之间的唯一区别是我们必须使用-来包围比较-dot}


#### 让我们使用type命令验证[是shell的内置命令 {#让我们使用type命令验证-是shell的内置命令}

{{< highlight shell >}}
type [
[ is a shell builtin
{{< /highlight >}}

[是test内置命令的替代命令.我们可以互换使用它们: <br/>

{{< highlight shell >}}
[ 3 -eq 3 ] && echo "Numbers are eqal"
Numbers are eqal
{{< /highlight >}}

{{< highlight shell >}}
test 3 -eq 3 && echo "Numbers are eqal"
Numbers are eqal
{{< /highlight >}}


### 2.2双括号 {#2-dot-2双括号}

双括号[[]]是在Korn Shell中作为增强功能引入的,可以更轻松地在shell脚本的测试中 <br/>
使用.我们可以将其视为单括号的边界替代方案.它可以在Bash和zsh灯许多shell中使用. <br/>
但是,双括号不符合POSIX标准. <br/>


#### [[是关键字.我们使用type命令来检查它: {#是关键字-dot-我们使用type命令来检查它}

{{< highlight bash >}}
type [[
[[ is a shell keyword
{{< /highlight >}}


## 3.其它差异 {#3-dot-其它差异}

在本节中,我们将讨论单括号和双括号的其他区别. <br/>


### 3.1比较运算符 {#3-dot-1比较运算符}


#### 可以将比较运算符和双括号一起使用.让我们使用小于运算符(&lt;)进行字符串比较 {#可以将比较运算符和双括号一起使用-dot-让我们使用小于运算符-----进行字符串比较}

{{< highlight bash >}}
[[1 < 2]]&& echo "1 is less than 2"
is less than 2
{{< /highlight >}}


#### 在这里,我们使用小于运算符检查1是否小于2.比较成功.但是,使用单括号而不是使用双括号就会产生语法错误: {#在这里-我们使用小于运算符检查1是否小于2-dot-比较成功-dot-但是-使用单括号而不是使用双括号就会产生语法错误}

{{< highlight bash >}}
[1 < 2] && echo "1 is less than 2"
Bash: 2: No such file or directory
{{< /highlight >}}


#### 在这种情况下,Bash将&lt;运算符视为文件重定向运算符.因此,我们必须在&lt;运算符之前使用转义字符(\\),以便在单括号内成功进行比较: {#在这种情况下-bash将-运算符视为文件重定向运算符-dot-因此-我们必须在-运算符之前使用转义字符-----以便在单括号内成功进行比较}

{{< highlight bash >}}
$ [ 1 \< 2 ] && echo "1 is less than 2"
1 is less than 2
{{< /highlight >}}


#### 现在,使用单括号就比较成功了.同样,我们必须在大于运算符(&gt;)之前使用转义字符来进行单括号内的字符串比较.整数比较运算符(例如-eq,-ne,-gt,-lt,-ge和-le)的用法对于两者是是相同的. {#现在-使用单括号就比较成功了-dot-同样-我们必须在大于运算符-----之前使用转义字符来进行单括号内的字符串比较-dot-整数比较运算符--例如-eq-ne-gt-lt-ge和-le--的用法对于两者是是相同的-dot}


### 3.2布尔运算符 {#3-dot-2布尔运算符}


#### 使用双括号进行逻辑运算时,我们必须使用&amp;&amp;运算符进行逻辑与运算,并使用进行||运算符进行逻辑或运算. {#使用双括号进行逻辑运算时-我们必须使用-and-and-运算符进行逻辑与运算-并使用进行-运算符进行逻辑或运算-dot}

{{< highlight bash >}}
[[ 3 -eq 3 && 4 -eq 4 ]] && echo "Numbers are equal"
: Numbers are equal
{{< /highlight >}}


#### 但是,使用单括号时,我们必须分别使用-o和-a测试运算符逻辑或和逻辑与运算 {#但是-使用单括号时-我们必须分别使用-o和-a测试运算符逻辑或和逻辑与运算}


#### 让我们重复上次使用单括号进行的比较 {#让我们重复上次使用单括号进行的比较}

{{< highlight bash >}}
[ 3 -eq 3 -a 4 -eq 4 ] && echo "Numbers are eqal"
: Numbers are eqal
{{< /highlight >}}


#### 对比再次成功.但由于单括号,我们使用-a而不是&amp;&amp; {#对比再次成功-dot-但由于单括号-我们使用-a而不是-and-and}


### 3.3分组表达式 {#3-dot-3分组表达式}


#### **我们可以使用括号将表达式分组在双括号内**,分组的原因之一可能是更容易阅读表达式 {#我们可以使用括号将表达式分组在双括号内-分组的原因之一可能是更容易阅读表达式}

{{< highlight bash >}}
[[ 3 -eq 3 && (2 -eq 2 && 1 -eq 1) ]] && echo "Parentheses can be used"
{{< /highlight >}}


### 3.4模式匹配 {#3-dot-4模式匹配}


### 3.6分词 {#3-dot-6分词}


### 3.5常用表达 {#3-dot-5常用表达}


## 4.结论 {#4-dot-结论}

