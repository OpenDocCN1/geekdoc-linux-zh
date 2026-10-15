
![](img/6e4cdc423ec40606ea72b32fdafff220_592_0.png)

## 命令控制的循环

在命令控制的循环中，命令的执行结果决定了循环是否执行。Korn shell 中有两种命令控制的循环：`while` 循环和 `until` 循环。

### `while` 循环

`while` 循环是一种基本的命令控制循环。它以 `while` 开始，后面包含循环命令，只要命令的退出状态为真（零），循环就会持续；否则循环终止。图 14.15 显示了 `while` 循环的格式。

![](img/6e4cdc423ec40606ea72b32fdafff220_593_0.png)

图 14.15 `while` 循环

任何语言中最常见的循环应用之一都是读取数据。脚本 14.13 是一个演示如何在循环中读取数据的简短示例。我们首先编写一个 `while` 循环，从键盘读取一行内容。只要 `read` 命令的退出状态为真，它就会累加数字并迭代。当输入文件结束符（UNIX 中的 `^d`）时，它会打印总和并停止。

### 脚本 14.13 简单的读取循环

```bash
#!/bin/ksh
# Script: loopAdd.scr
# Demo读取文件循环。累加并打印总和。
print "This utility adds numbers entered from the"
print "keyboard. When all numbers have been entered, \n"
print "key ^d (eof) to see the total.\n"
sum=0
print "Enter a number : \c"
while read data
do
  (( sum = sum + data ))
  print "Enter next number: \c"
done
print "\n"
Sum is: $sum
$loopAdd.scr
```

输出：

```
This utility adds numbers entered from the
keyboard. When all numbers have been entered,
key ^d (eof) to see the total.
```

### 脚本 14.13 简单的循环

```
Enter a number : 2
Enter next number: 4
Enter next number: 6
Enter next number: ^D
Sum is: 12
```

在脚本 14.13 中，我们一直读取到文件完全读完。另一种循环结构使用“哨兵”（sentinel）来终止循环。哨兵是一个停止循环的特殊值。常见的循环哨兵是 `-9999`。当然，哨兵值不能是一个有效的数据值。脚本 14.14 通过 `-9999` 来指示显示小计，演示了哨兵概念。

### 脚本 14.14 使用哨兵打印总和

```bash
#!/bin/ksh
# Script: loopSent.scr
# Demo读取文件循环。累加并打印总和。

print "This utility adds numbers entered from the"
print "keyboard. When all numbers have been entered,"
print "key -9999 to see the total."
print

sum=0
print "Enter a number : \c"
read data
while [[ $data != -9999 ]];
do
    (( sum = sum + data ))
    print "Enter next number: \c"
    read data
done

print "Sum is: $sum"
loopSent.scr
```

输出：

```
This utility adds numbers entered from the
keyboard. When all numbers have been entered,
-9999 to see the total.

Enter a number : 2
Enter next number: 4
Enter next number: 6
Enter next number: -9999
Sum is: 12
```

### `until` 循环

`until` 循环的工作原理与 `while` 循环相同，不同在于它在命令的退出状态为假时会持续循环。从这个意义上说，它是 `while` 循环的互补。`until` 循环的语法如图 14.16 所示。

![](img/6e4cdc423ec40606ea72b32fdafff220_595_0.png)

图 14.16 `until` 循环

你可能会奇怪为什么在 `while` 循环基本相同的情况下 UNIX 还要提供 `until` 循环——`until` 仅仅是 `while` 的互补。答案是，在某些情况下我们需要退出状态的互补值。这在脚本中很容易实现。例如，如果我们需要处理一个我们组内所有成员共享的文件，我们应该防止该文件在我们需要它时被他人使用。如果其他人正在写入该文件，我们就无法打开它。脚本 14.15 演示了一个简单的 `until` 循环，它可以防止这种情况，并一直循环直到文件可用。

### 脚本 14.15 演示 `until` 循环

| 行号 | 代码 |
| :--- | :--- |
| 1 | #!/bin/bash |
| 2 | if [[ -r $1 ]]; |
| 3 | then |
| 4 | # File is available. |
| 5 | ... |
| 6 | else |
| 7 | print "File $1 is not available." |
| 8 | until [[ -r $1 ]]; |
| 9 | do |
| 10 | sleep 5 |
| 11 | done |
| 12 | fi |

*(注：此处根据原文逻辑对表格内容进行了结构性对齐，保持对应关系)*

## 列表控制的循环

在列表控制的循环中，有一个控制列表。列表中的元素数量决定了迭代次数。如果列表包含五个元素，循环体就会执行五次；如果列表包含十个元素，循环体就会执行十次。

### `for-in` 循环

Korn 中第一个列表控制循环是 `for-in` 循环。列表可以是任何类型的字符串；例如单词、行或句子。图 14.17 显示了 `for-in` 循环的设计和代码。在每次迭代中，列表中的下一个元素会被移动到变量并进行处理。

![](img/6e4cdc423ec40606ea72b32fdafff220_596_0.png)

图 14.17 `for-in` 循环

让我们写一个简单的循环。在脚本 14.16 中，我们循环五次，每次循环控制字符串（一个数字）和单词“Hello”。

### 脚本 14.16 简单的 `for-in` 循环

| 行号 | 代码 |
| :--- | :--- |
| 1 | #!/bin/ksh |
| 2 | # Script: loopFor.scr |
| 3 | # Demo for-in循环 |
| 4 | for i in 1 2 3 4 5 |
| 5 | do |
| 6 | print $i Hello |
| 7 | done |

输出：

```
Hello
Hello
Hello
Hello
Hello
```

列表控制循环可以处理文件列表。在下一个示例中，我们处理文件列表，列表中的每个元素都是文件名。列表作为一个单独的文件创建，然后在脚本中使用该 `for` 循环。这种设计使得使用一个脚本处理不同的文件列表很容易。为了更加灵活，文件列表作为参数传递给脚本。在这个示例中，我们简单地 `cat` 文件。循环体首先打印文件名，然后打印文件内容。打印文件后，我们打印一个分隔符与下一个文件隔开。脚本及其输出见脚本 14.17。

### 脚本 14.17 文件处理循环

```bash
#!/bin/ksh
# Script: loopCatFiles.scr
# 此脚本合并控制列表中的文件
# 控制文件名是一个参数 ($1)
for filename in $(cat $1)
do
  print $filename
  cat $filename
  print "==================== End of $filename========\n"
done

***** End of File List ******
$ loopCatFiles.scr loopCatFiles.dat
$cat loopCatFiles.dat
```

输出：

```
file1
... (file1 和 file2 的内容) ...
```
