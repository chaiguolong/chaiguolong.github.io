+++
title = "shell脚本中[]和[[]]的区别"
lastmod = 2024-05-07T18:39:39+08:00
draft = true
toc = true
+++

## 1.shell脚本中[]和[[]]的区别 {#1-dot-shell脚本中-和-的区别}


### 1.概述: {#1-dot-概述}

在Bash中比较变量时,我们通常交替使用单括号([])和双括号([[]]).
例如,我们可以在检查3是否等于3时使用表达式[3 -eq 3]或者[\\[3 -eq 3]\\]
两者都将成功比较,那么它们之间有什么区别呢?
在本教程中,我们将讨论Bash中单括号和双括号之间的区别.


### 2.主要区别 {#2-dot-主要区别}

在本节中,我们将简要讨论单括号和双括号之间的主要区别.

-   2.1单括号
    [是shell的内置命令,在Unix和Linux中始终可用于计算表达式.
    它仍然存在是为了向后兼容和POSIX合规性.
    让我们使用type命令验证[是shell的内置命令
    {{< highlight nil >}}
    $ type [
    [ is a shell builtin
    {{< /highlight >}}
    [是test内置命令的替代命令.我们可以互换使用它们:
    {{< highlight nil >}}
    $ [ 3 -eq 3 ] && echo "Numbers are eqal"
    Numbers are eqal
    $ test 3 -eq 3 && echo "Numbers are eqal"
    Numbers are eqal
    {{< /highlight >}}
    [和test之间的唯一区别是我们必须使用]来包围比较.
-   2.2双括号
    双括号[[]]是在Korn Shell中作为增强功能引入的,可以更轻松地在
    shell脚本的测试中使用.我们可以将其视为单括号的边界替代方案.
    它可以在Bash和zsh灯许多shell中使用.但是,双括号不符合POSIX标准.
    [[是关键字.我们使用type命令来检查它:
    {{< highlight nil >}}
    $ type [[
    [[ is a shell keyword
    {{< /highlight >}}


### 3.其它差异 {#3-dot-其它差异}


### 4.结论 {#4-dot-结论}
