---
layout: post
title: "函数（Function）"
categories: PowerShell
date: 2018-02-11 14:00:00 +0800
---

### 笔记
* 函数是最轻量级的PS命令。其只存在于内存中并服务于当前会话。会话退出后，函数消失。
* 脚本块（`scriptblock`）的定义`{<statement list>}`
* 函数的定义： `function <name> {<statement list>}`
* 函数和函数块都包含一组PS的语句。函数是一个命名的函数块，而函数块是一个匿名的函数
* 函数可携带参数。对于简单的函数，参数列表可由变量`$args`来获取。
    *  在调用时，PS会将函数名后面以空格分隔的所有字符作为参数封装进`$args`变量中
    *  在输出时，每个参数之间的分隔符由变量`$OFS`定义，默认为空格
    * `$args`和`$OFS`变量存储在帮助文件`about_Automatic_Variables`中
* 参数的显示定义：
    * `function <name> (<parameter list>) {<statement list>}`
    * `function <name> {param(<parameter list>) <statement list>}`
* 

### 例子
```powershell
function hello { 'Hello World' } 
function say-hello { "Hello $args" }
function say-hi { $OFS = ','; "Hi, $args" }
function count-args { 
    "`$args.count = " + $args.count
    "`$args[0].count = " + $args[0].count
}
```
### 调用

| 调用 | 结果 |
| ------ | ------- |
| PS> hello | Hello World |
| PS> say-hello Alice Bob | Hello Alice Bob |
| PS> say-hi Alice Bob | Hi, Alice,Bob |
| PS> count-args 1 2 3 | $args.count = 3 \n $args[0].count = 1 |
| PS> count-args 1,2,3  | $args.count = 1 \n $args[0].count = 3 |
