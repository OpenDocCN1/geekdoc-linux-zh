
```tcl
set x 1;

puts "X in stack1 starts as $x"

stack2

puts "X in stack1 ends as $x"

puts ""

}
```

# 第 6 章 过程技巧

# 创建带有局部变量 `x` 的过程 `stack2`。

# 显示 `x` 的值，调用 `stack3`，并再次显示 `x` 的值

`proc stack2 () {`

`set x 2;`

`puts "X in stack2 starts as $x"`

`stack3`

`puts "X in stack2 ends as $x"`

`}`

# 创建带有局部变量 `x` 的过程 `stack3`，

# 显示 `x` 的值，

# 使用相对调用栈层级显示调用 `stack3` 的过程作用域内 `x` 的值。

# 在调用 `stack3` 的过程（`stack2`）的 `x` 的值上加 10

# 在调用 `stack2` 的过程的 `x` 的值上加 100

# 在全局作用域的 `x` 的值上加 200

# 使用绝对调用栈层级显示 `x` 的值。

`proc stack3 () {`

`set x 3;`

`puts "X in stack3 starts as $x"`

`puts ""`

# 显示相对于当前层级的栈层级 `x` 值。

`for {set i 1} {$i <= 3} {incr i} {`

`upvar $i localX`

`puts "X at upvar $i is $localX"`

`}`

`puts "\n x is being modified from procedure stack3\n"`

# 在当前调用级以上过程的作用域中评估命令。

`uplevel 1 {incr x 10}`

`uplevel 2 {incr x 100}`

`uplevel #0 {incr x 200}`

`puts ""`

`}`

# 6.5 全局与局部作用域的操作

# 在绝对栈层级显示 `x` 的值

`for {set i 0} {$i < 3} {incr i} {`

`upvar #$i localX`

`puts "X at upvar #$i is $localX"`

`}`

`puts ""`

`proc b1 {} {`

# 声明 `X` 存在于全局作用域

# 不在局部作用域中创建 `x`。

`global x;`

`puts "X in global scope is: $x"`

`}`

# 示例脚本

```tcl
set x 0;
puts "X at global scope is $x"
stack1
b1
```

# 脚本输出

```
X at global scope is 0
x in stack1 starts as 1
x in stack2 starts as 2
x in stack3 starts as 3

X at upvar 1 is 2
x at upvar 2 is 1
x at upvar 3 is 0

x is being modified from procedure stack3
x at upvar #0 is 200
x at upvar #1 is 101
x at upvar #2 is 12

x in stack2 ends as 12
x in stack1 ends as 101

x in global scope is 200
```

# 第 6 章 过程技巧

在上述示例中，当过程 `stack3` 被评估时，作用域类似于下图的左侧所示。每个局部过程都嵌套在调用它的过程的作用域内。

当评估 `uplevel 1 (incr x 10)` 命令时，它会导致字符串 `incr x 10` 在当前 `stack3` 作用域的高一个作用域中评估，即 `stack2` 作用域。`uplevel #0 (incr x 200)` 命令在绝对作用域层级 0（即全局作用域）中评估。`uplevel #1` 命令的评估级是调用栈向下的第一层，在本例中为 `stack1`。

![](img/fdcc2919568b5b6c9f5301d50a10e8d7_183_0.png)

前面的示例演示了过程如何访问调用栈中其上方的所有层级，但不能访问下方。

从全局层调用的过程 `b1` 无法访问过程 `stack1` 局部作用域内的任何变量。过程 `stack1` 的局部变量作用域仅在 `stack1` 被评估期间存在。

162

## 6.6 创建一个 Tcl 对象

第 3 章提到 Tcl 为命令、关联数组索引和变量维护了独立的哈希表，并且 Tcl 命令的第一个单词必须是命令名。这些特性意味着任何名称都可以同时定义为变量名和过程名。解释器将根据该名称在命令行中的位置来确定它指的是哪一个。

本节将讨论使用相同标签同时作为变量名、数组索引和过程名的技巧。例如，`newTreeObject` 将定义一个数组索引并创建一个同名的过程。它将返回该过程的名字。

这使得我们能够实现将方法附加到数据对象的面向对象编程概念。Tcl 对象的实现与 C++ 或 Java 对象的实现大相同，但编程语义非常相似。

# 表 6.6-1

| C++ | Tcl |
|---|---|
| `object = new Object(arg1);` | `set myTree [newTreeObject arg1]` |
| `object->method(arg1, arg2);` | `$myTree method arg1 arg2` |

## 6.6 创建一个 Tcl 对象

这是一个简单的示例，这里有一些代码可以创建一个与水果名同名的过程，并测试其颜色是否有效。

# Example 6.6.1-1

An Object

6.6.1

Example Script

For a simple example, here's some code that creates

`set fruitList [list apples {red yellow} bananas {yellow} grapes {green purple}]`

```cl
# 1) Extract the info from the list
set fruitName [lindex $fruitList 0]
# 2) Create a variable with the name of the fruit.
# The contents will be possible colors.
set fruitColors [lindex $fruitList 1]

# 3) Create a body for
set body [format {if {[lsearch "%s" $clr] != -1} \
    return 1} else \
    return 0} $fruitColors]

# 4) Define the procedure.
proc fruitName {clr} $body

# Loop through the fruits, and ask the user for a color
# Read the input from the keyboard.
# Compare it to valid colors.
```cl

`foreach fruit $fruitList {`

`puts "What color are $fruit?"`

`gets stdin answer`

`if {[eval fruitName [list $answer]]]`

`puts "Correct, $fruit can be $answer"`

`} else {`

`puts "No, $fruit are $answer"`

`}`

`}`

# Script Output

```
What color are apples?           # User types red

Correct, apples can be red

What color are bananas?         # User types red

No, bananas are yellow

What color are grapes?           # User types red

No, grapes are green purple
```

# newTreeObject Example

```cl
# This function defines an array index and creates a procedure
# with the same name. It will return the name of the procedure.
proc newTreeObject {name} {
    eval "set $name(0) \"some data\""
    eval "proc $name {
```
