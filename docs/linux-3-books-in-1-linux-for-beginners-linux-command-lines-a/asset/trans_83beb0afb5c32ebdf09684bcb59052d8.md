

这是 while 循环中的 18。

循环继续到最后一行：

这是 while 循环中的 1。

## 多个测试命令

你可以在 while 循环中打包多个测试命令。

```bash
$ cat test1133
#!/bin/bash
# Now I am testing a multicommand while loop in Linux shell
var15=20
while echo $var15
[ $var15 -ge 0 ]
do
  echo "This operation is being conducted inside the while loop."
  var15=$[ $var15 - 1 ]
done
```

```bash
$ bash -f main.sh
20
This operation is being conducted inside the while loop.
19
This operation is being conducted inside the while loop.
18
This operation is being conducted inside the while loop.
17
This will continue until it reaches the last number:
This operation is being conducted inside the while loop.
0
This operation is being conducted inside the while loop.
-1
```

第一个测试命令显示 var15 变量的当前值。第二个命令将使用测试命令来获知 var15 变量的值。echo 语句在循环内返回一条简单消息，表明循环已完成其执行过程。

### until 命令

until 命令的作用与 while 命令相反。它要求指定一个产生非零退出状态的简单测试命令，此时 bash shell 将执行 while 循环中的命令。

然而，与 while 命令类似，until 命令语句也可以包含多个测试命令，最终命令的退出状态是决定因素。

```bash
$ cat test1222
#!/bin/bash
# In this code block I will be using the until command
var15=100
until [ $var15 -eq 0 ]
do
    echo You are seeing the operations of the until command. The next digit in the loop is $var15
    var15=$[ $var15 - 5 ]
done
```

```bash
$ bash -f main.sh
You are seeing the operations of the until command. The next digit in the loop is 100

You are seeing the operations of the until command. The next digit in the loop is 95

You are seeing the operations of the until command. The next digit in the loop is 90

And continuing, until it reaches the final digit:

You are seeing the operations of the until command. The next digit in the loop is 5
```

该示例已成功测试 var15 变量，以确定循环何时停止——当变量值降至零时，until 命令立即停止。

```bash
$ cat test1222
#!/bin/bash
# In this code block, I will be using the until command
var15=100
until echo $var15
    [ $var15 -eq 0 ]
do
    echo You are seeing the operations of the until command. The next digit in the loop is $var15
    var15=$[ $var15 - 5 ]
done
```

```bash
$ bash -f main.sh
100
You are seeing the operations of the until command. The next digit in the loop is 100

95
You are seeing the operations of the until command. The next digit in the loop is 95

90
Again, this will continue to the last digit in the loop:

You are seeing the operations of the until command. The next digit in the loop is 5

0
```

## 嵌套循环

循环语句可以在循环内部使用其他命令，包括同一循环的其他命令。此过程称为嵌套循环。你将在另一个迭代内部拥有迭代，这将增加命令执行的次数。参见示例以了解如何嵌套循环。

```bash
$ cat test1444
#!/bin/bash
# The following code block shows nesting for loops
for (( x = 1; x <= 7; x++ ))
do
    echo "You are seeing the operations of the until command. The next digit in the loop is $x:"
    for (( y = 1; y <= 7; y++ ))
    do
        echo " Now you are seeing what is going on inside loop: $y"
    done
done
```

```bash
$ bash -f main.sh
You are seeing the operations of the until command. The next digit in the loop is 1:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

And so on, finishing with

Now you are seeing what is going on inside loop: 7

You are seeing the operations of the until command. The next digit in the loop is 2:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

Again, this will continue until it ends with

Now you are seeing what is going on inside loop: 7

You are seeing the operations of the until command. The next digit in the loop is 3:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

Ending with:

Now you are seeing what is going on inside loop: 7

You are seeing the operations of the until command. The next digit in the loop is 4:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

Ending with:

Now you are seeing what is going on inside loop: 7

The entire cycle continues through the loop, until it reaches:

Now you are seeing what is going on inside loop: 7
```

你可以尝试更改循环中的数字来收缩或扩展两个循环的大小。通过更改循环中的数字，你将能够改变循环的行为方式。

```bash
$ cat test1444
#!/bin/bash
# The following code block shows nesting for loops
for (( x = 1; x <= 3; x++ ))
do
    echo "You are seeing the operations of the until command. The next digit in the loop is $x:"
    for (( y = 1; y <= 5; y++ ))
    do
        echo " Now you are seeing what is going on inside loop: $y"
    done
done
```

```bash
$ bash -f main.sh
You are seeing the operations of the until command. The next digit in the loop is 1:

Now you are seeing what is going on inside loop: 1

Repeated to:

Now you are seeing what is going on inside loop: 5

You are seeing the operations of the until command. The next digit in the loop is 2:

Now you are seeing what is going on inside loop: 1

Repeated to:

Now you are seeing what is going on inside loop: 5

You are seeing the operations of the until command. The next digit in the loop is 3:

Now you are seeing what is going on inside loop: 1

And finishing on:

Now you are seeing what is going on inside loop: 5
```

嵌套循环遍历外层循环迭代的值。对于两个循环，do 和 done 命令之间没有区别。你可以通过配对 for 循环和 while 循环来创建嵌套循环。

```bash
$ cat test15
#!/bin/bash
# This is how we can place a for loop in a while loop
var15=15
while [ $var15 -ge 0 ]
do
    echo "You are seeing the operations of nesting loops. The next digit in the loop is $var15:"
    for (( var12 = 1; var12 < 3; var12++ ))
    do
        var13=$[ $var15 * $var12 ]
        echo " Now you are seeing what is going on inside loop: $var15 * $var12 = $var13"
    done
    var15=$[ $var15 - 1 ]
done
```

```bash
$ bash -f main.sh
You are seeing the operations of nesting loops. The next digit in the loop is 15:

Now you are seeing what is going on inside loop: 15 * 1 = 15

Now you are seeing what is going on inside loop: 15 * 2 = 30

This will continue down to the final line:

You are seeing the operations of nesting loops. The next digit in the loop is 0:

Now you are seeing what is going on inside loop: 0 * 1 = 0

Now you are seeing what is going on inside loop: 0 * 2 = 0
```

在下一个示例中，我将配对 until 和 while 循环来测试嵌套循环的限制。参见以下示例。

```bash
$ cat test16
#!/bin/bash
var15=10
until [ $var15 -eq 0 ]
do
    echo "You are seeing the operations of the nested until and while loops: $var15"
    var12=1
    while [ $var12 -lt 5 ]
    do
        var13=$(echo "scale=4; $var15 / $var12" | bc)
        echo " This is how the inner section of the nested loop functions: $var15 / $var12 = $var13"
        var12=$[ $var12 + 1 ]
    done
    var15=$[ $var15 - 1 ]
done
```

```bash
$ bash -f main.sh
You are seeing the operations of the nested until and while loops: 10

This is how the inner section of the nested loop functions: 10 / 1 = 10.0000

This is how the inner section of the nested loop functions: 10 / 2 = 5.0000

This is how the inner section of the nested loop functions: 10 / 3 = 3.3333

This is how the inner section of the nested loop functions: 10 / 4 = 2.5000

This cycle is repeated, until it reaches the final one of:

You are seeing the operations of the nested until and while loops: 1

This is how the inner section of the nested loop functions: 1 / 1 = 1.0000

This is how the inner section of the nested loop functions: 1 / 2 = .5000

This is how the inner section of the nested loop functions: 1 / 3 = .3333

This is how the inner section of the nested loop functions: 1 / 4 = .2500
```

## 循环控制

你可能认为一旦循环开始，你就会被困在里面，直到循环完成其执行过程。然而，有出路。你可以向代码中添加几个命令，帮助你控制循环内部的操作。

break 命令是退出正在进行的循环的最简单方式。你可以使用 break 命令退出 while 和 until 循环。

```bash
$ cat test17
#!/bin/bash
for countries in 2 3 4 5 6 7 8 9 10 11 12 13 14
do
    if [ $countries -eq 12 ]
    then
        break
    fi
    echo "I am going to visit $countries after Covid-19 is over."
done
echo "I have visited all the countries."
```

```bash
$ bash -f main.sh
I am going to visit 2 countries after Covid-19 is over.

I am going to visit 3 countries after Covid-19 is over.

I am going to visit 4 countries after Covid-19 is over.
```

