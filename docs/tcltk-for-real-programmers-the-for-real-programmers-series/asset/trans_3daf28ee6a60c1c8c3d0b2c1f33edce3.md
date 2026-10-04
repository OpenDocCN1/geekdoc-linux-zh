

## 第 3 章 Tcl 语言简介

# 示例 3.3.3-1

一个简单的测试

```
set x 2
set y 3
if ($x < $y) {
    puts "x is less than y"
}
```

# 脚本输出

x is less than y

switch 命令允许 Tcl 脚本在多个模式中选择一种。switch 命令接收一个用于测试的变量和多个模式。第一个匹配测试短语的模式将被执行，而所有其他代码块将不会被执行。

语法：`switch ?opt? str pat1 bod1 ?pat2 bod2? ...?default?`

switch 根据字符串的值在 N 个可能的代码体中评估其中的 1 个。

?opt? 以下是这些可能的选项之一：

- -exact 将模式字符串与测试字符串精确匹配，包括可能出现的 "-" 字符。
- -glob 使用 glob 匹配规则将模式与测试字符串匹配。这是默认的匹配规则。
- -regexp 使用正则表达式字符串匹配规则将模式与测试字符串匹配。
- -- 绝对是最后一个选项。下一个字符串将作为字符串参数。这允许使用以破折号 (-) 开头的字符串作为参数，而不被解释为选项。

## 0.3 Tcl 命令

str 用于与模式匹配的字符串。
patN 与字符串比较的模式。
bdN 如果 patN 匹配字符串，则评估的代码体。
default 如果没有其他模式匹配，则将匹配的模式。

选项 -exact、-glob 和 -regex 控制字符串与 pat-term 之间的比较方式。

glob 匹配的规则如下：

- * 匹配 0 个或多个字符。
- ? 匹配单个字符。
- [] 匹配括号内定义的集合中的某个字符。
- [abc] 将 abc 定义为集合。
- [x-y] 将字母表中 x 和 y 之间（包含两者在内）的所有字符定义为集合。

- ? 匹配单个字符。

注意 glob 规则对 [] 的使用方式与 Tcl 评估-代码不同。你必须保护大括号使其免受 tcl 评估的影响，否则 tclsh 将尝试将大括号内的短语作为命令进行评估并可能会失败。将 glob 表达式封装在大括号中可以实现这一点。我将在下一章中解释。

正则表达式的规则与 glob 相似，允许你定义字符串中的字符模式，但它们更复杂、更强大。用于评估正则表达式的 regexp 命令将在下一章中讨论。

switch 命令也可以在模式和体周围使用大括号来编写。

```
Syntax: switch ?option? string {
  pattern1 body1
  ?pattern2 body2?
  ?default?
}
```

## 第 3 章 Tcl 语言简介

当使用大括号时，模式字符串必须是硬编码模式（hardcoded-patterns）。当不带括号使用 switch 命令时，模式字符串可以是变量，允许脚本在运行时修改 switch 命令的行为。

# 示例 3.3.3-2

```
set x 7
switch -glob $x {
  "1" puts "one"
  "2" puts "two"
  "3" puts "three"
  {[4-8]}puts "greater than 3"
  default{puts "Not 1, 2, or 3"}
}
```

脚本输出

greater than 3

## 3.3.4 循环

Tcl 提供了命令，允许脚本对计数器进行循环、对条件进行循环或对列表中的项进行循环。

这三个命令是：

- * for: 数字循环命令
- while: 条件循环命令
- foreach: 面向列表的循环命令

for 命令是数字循环命令。

语法：`for start test next body`

- * for: 循环直到某个条件变为为假。
- start: 定义循环开始条件的 Tcl 语句。
- test: 测试结束结束的语句。该语句必须是 expr 可接受的格式。

- next: 在每次通过循环后将进行评估的 Tcl 语句。通常这会递增计数器。

- body 在每次通过循环时要评估的代码体。

for 命令与 C、Fortran、Basic 等语言中的 for 循环类似。for 命令需要四个参数；第一个 (start) 设置初始条件，下一个 (test) 测试条件，第三个 (next) 修改测试状态。最后一个参数 (body) 是当测试返回真时评估的代码体。

# 示例 3.3.4-1

For 循环示例

```
for {set i 0} {$i < 2} {incr i} {
  puts "I is: $i"
}
```

脚本输出

- I is: 0
- I is: 1

while 命令用于循环直到测试条件变为为假。

语法：`while while test body`

- while 循环直到某个条件变为为假。
- test 测试结束结束的语句。该语句必须是 expr 可接受的格式。
- body 在每次通过循环时要评估的代码。

# 示例 3.3.4-2

While 循环示例

```
set x 0
while {$x < 5} {
  set x [expr $x+1]
  puts "X: $x"
}
```

脚本输出

X: 1

foreach 命令用于遍历列表项。

**语法：** `foreach listVar list body`

| foreach | 说明 |
| :--- | :--- |
| listVar | 用于存储当前处理项的变量。 |
| list | 要遍历的列表。 |
| body | 在每次循环时要评估的代码。 |

# 示例 3.3.5-3

Foreach 循环示例

```
foreach element one two {
    puts "this is $element"
}
```

脚本输出

this is one
this is two

## 3.3.5 字符串处理

string match 命令搜索目标字符串中的模式。它使用了与 switch 命令相同的 glob 技巧。

语法：`string match string`

- string 定义此为命令。
- match 如果模式匹配 string，则返回 1，否则返回 0。
- pattern 用于比较的模式。
- string 用于匹配的字符串。

string tolower 将字符串转换为小写。注意这不是原地操作。会返回一个新的小写字符串。

string toupper 使用相同的语法将字符串转换为大写。

语法：`string tolower string`

- string 定义此为命令。
- tolower 返回转换为小写的字符串。
- string 要转换的字符串。

string first 返回模式在测试字符串中首次出现的位置，如果模式不在测试字符串中则返回 -1。

语法：`string first substr string`

- string 定义此为操作字符串的命令。
- first 返回 substr 在 string 中第一次出现的位置。
- substr 要搜索的子字符串。
- string 要搜索的字符串。

string length 命令返回字符串中字符的数量。

语法：`string length string`

- string 定义此为字符串命令。
- length 返回 string 中字符的数量。
- string 字符串。

string range 命令返回字符串中两个点之间的字符。

语法：`string range string first last`

- string 定义此为字符串命令。
- range 返回 string 中 first 和 last 之间的字符。
- string 字符串。

