+++
title = "shell脚本中关于运算符是否加空格的语法整理"
date = 2024-05-29T14:30:00+08:00
lastmod = 2024-05-29T14:30:44+08:00
draft = false
toc = true
+++

## 目的 {#目的}

在编写shell脚本时经常遇到有时候运算符两边要加空格,有时候两边不能加空格, <br/>
当弄混时经常出现语法错误的问题,因此将遇到的问题梳理归纳起来. <br/>


## 两边不能加空格: {#两边不能加空格}

1 赋值时=两边不可加空格:如val = 1,val= 1都是非法的" <br/>


## 两边要加空格: {#两边要加空格}

1 表达式和运算符号之间要加空格: 如val = expr 1 + 1, <br/>
必须保证+号两边有空格. <br/>
2 条件表达式在方括号之间要加空格: 如[$a `= $b],必须
    保证==两边要有空格
    3 if语句,此情况虽然不是两边要加空格,但是if右边需要加
    空格,如if [a =` b] <br/>

