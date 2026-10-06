
修改，否则你将陷入无限循环。在这个示例中，我们使用 shell 算术将变量值减  1：

```
var=$[$var - 1 ]
```

当测试条件不再为真时，`while` 循环停止。

## 使用多个测试命令

在一种比较奇异的情况下，`while` 命令允许你在 `while` 语句中定义多个测试命令。只有最后一个测试命令的退出状态被用于判断循环何时何时停止。如果你不小心，这可能会导致一些有趣的结果。这里有一个我意思的示例：

```
$ cat test11
!/bin/bash
# 测试多命令的 while 循环

var=10

while echo $var
  [$var -ge 0 ]
do
  echo "This is inside the loop"
  var=$[$var - 1 ]
done
./test11
10
This is inside the loop
9
This is inside the loop
8
This is inside the loop
7
This is inside the loop
6
This is inside the loop
5
This is inside the loop
4
This is inside the loop
3
This is inside the loop
2
This is inside the loop
1
This is inside the loop
0
```

This is inside the loop
1

请密切注意这个示例发生了什么。在 `while` 语句中定义了两个测试命令：

```
while echo $var
[ $var -ge 0 ]
```

第一个测试命令仅仅显示了 `var` 变量的当前值。第二个命令使用测试命令来确定 `var` 变量的值。在循环内部，`echo` 语句显示了一条简单的消息，表示循环已处理过。注意当你运行该示例时，输出是如何结束的：

This is inside the loop
-1

循环在 `var` 变量等于零时执行了 `echo` 语句，然后减少了 `var` 变量。接下来，执行了下次迭代的测试命令。`echo` 测试命令被执行，显示了 `var` 变量的值，此时它已经小于零了。直到 shell 执行了测试命令，`while` 循环才会终止。

这表明在多命令的 `while` 语句中，所有的测试命令在每次迭代中都会执行，包括最后一个测试命令失败的最后一次迭代。请注意这一点。

## until 命令

`until` 命令的工作方式与 `while` 命令完全相反。`until` 命令要求你指定一个通常产生非零退出状态的测试命令。只要测试命令的退出状态为非零，bash shell 就会执行循环中列出的命令。一旦测试命令返回零退出状态，循环就会停止。

正如你预期的那样，`until` 命令的格式如下：

```
until test commands
do
  other commands
done
```

与 `while` 命令类似，你可以在 `until` 命令语句中拥有多个测试命令。只有最后一个命令的退出状态决定了 bash shell 是否执行执行定义的其他命令。

这里有一个使用 `until` 命令的示例：

```
$ cat test12
!/bin/bash
# 使用 until 命令

var=100

until [ $var -eq 0 ]
do
    echo $var
    var=$[$var - 25 ]
done
$ ./test12
100
75
50
25
$
```

这个示例通过测试 `var` 变量来决定 `until` 循环何时应该停止。一旦变量的值等于零，`until` 命令就会停止循环。当你对 `until` 命令使用多个测试命令时，同样适用于 `while` 命令的注意事项：

```
$ cat test13
!/bin/bash
# 使用 until 命令

var=100

until echo $var
[ $var -eq 0 ]
do
    echo Inside the loop: $var
    var=$[$var - 25 ]
done
$ ./test13
100
Inside the loop: 100
75
Inside the loop: 75
50
Inside the loop: 50
25
Inside the loop: 25
0
$
```

shell 执行了指定的测试命令，并仅当最后一个命令为真时才停止。

## 嵌套循环

循环语句可以在循环内部使用任何其他类型的命令，包括其他循环命令。这被称为嵌套循环。使用嵌套循环时应小心，因为你正在迭代中执行迭代，这会导致命令运行的次数成倍增加。不注意这一点可能会导致你的脚本出现问题。这里有一个将 `for` 循环嵌套在另一个 `for` 循环中的简单示例：

```
$ cat test14
#!/bin/bash
# 嵌套循环

for (( a = 1; a <= 3; a++ ))
do
  echo "Starting loop $a:"
  for (( b = 1; b <= 3; b++ ))
  do
    echo " Inside loop: $b"
  done
done
./test14
Starting loop 1:
Inside loop: 1
Inside loop: 2
Inside loop: 3
Starting loop 2:
Inside loop: 1
Inside loop: 2
Inside loop: 3
Starting loop 3:
$
```

嵌套循环（也称为内层循环）在外层循环的每次迭代中遍历它的值。注意两个循环的 `do` 和 `done` 命令之间没有区别。bash shell 知道第一个 `done` 指的是内层循环而不是外部循环。当你混合命令时（例如将 `for` 循环放置在 `while` 循环内部），情况也是如此：

```
$ cat test15
#!/bin/bash
# 在 while 循环中放置 for 循环

var1=5

## 第二部分 Shell 脚本基础

```
while [ $var1 -ge 0 ]
do
    echo "Outer loop: $var1"
    for (( var2 = 1; var2 < 3; var2++ ));
do
        var3=$[$var1 * $var2]
        echo "Inner loop: $var1 * $var2 = $var3"
    done
    var1=$[$var1 - 1]
done
./test15
Outer loop: 5
Inner loop: 5 * 1 = 5
Inner loop: 5 * 2 = 10
Outer loop: 4
Inner loop: 4 * 1 = 4
Inner loop: 4 * 2 = 8
Outer loop: 3
Inner loop: 3 * 1 = 3
Inner loop: 3 * 2 = 6
Outer loop: 2
Inner loop: 2 * 1 = 2
Inner loop: 2 * 2 = 4
Outer loop: 1
Inner loop: 1 * 1 = 1
Inner loop: 1 * 2 = 2
Outer loop: 0
Inner loop: 0 * 1 = 0
Inner loop: 0 * 2 = 0
$
```

再次，shell 能够区分外层循环的 `do` 和 `done` 命令。如果你真的想测试大脑，甚至可以组合 `until` 和 `while` 循环：

```
$ cat test16
!/bin/bash
# 使用 until 和 while 循环

var1=3

until [ $var1 -eq 0 ]
do
    echo "Outer loop: $var1"
    var2=1
    while [ $var2 -lt 5 ]
do
        var3=`echo "scale=4; $var1 / $var2" | bc`
        echo "Inner loop: $var1 / $var2 = $var3"
        var2=$[$var2 + 1]
    done
    var1=$[$var1 - 1]
done
$ ./test16
Outer loop: 3
Inner loop: 3 / 1 = 3.0000
Inner loop: 3 / 2 = 1.5000
Inner loop: 3 / 3 = 1.0000
Inner loop: 3 / 4 = 0.7500
Outer loop: 2
Inner loop: 2 / 1 = 2.0000
Inner loop: 2 / 2 = 10000
Inner loop: 2 / 3 = .6666
Inner loop: 2 / 4 = .5000
Outer loop: 1
Inner loop: 1 / 1 = .10000
Inner loop: 1 / 2 = .5000
Inner loop: 1 / 3 = .3333
Inner loop: 1 / 4 = .2500
$
```

`until` 循环从值三开始，直到值等于零为止。内层循环从值一开始，只要只要值小于五就会继续。每个循环都必须更改测试条件中的值，否则循环将陷入无限循环。

## 遍历文件数据

通常，你必须遍历存储在文件中的项。这需要结合已涵盖的两种技术：

- 使用嵌套循环
- 更改 IFS 环境变量

通过更改 IFS 环境变量，你可以强制 `for` 命令将文件中的每行处理为单独的项目（如果数据包含空格的话）。一旦你提取了文件中的某行，你可能需要再次循环以提取其中包含的数据。

一个经典示例是处理 `/etc/passwd` 文件中的数据。这需要你按行遍历 `/etc/passwd` 文件，然后将 IFS 值更改为冒号，以便分离各个组件。

这里是执行该操作的示例：

```
#!/bin/bash
# 更改 IFS 值

IFS.OLD=$IFS
IFS='\n'
for entry in cat /etc/passwd
do
  echo "Values in $entry -"
  IFS=:
    for value in $entry
      echo " $value"
  done
done
```
