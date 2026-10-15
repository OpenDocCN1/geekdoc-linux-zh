
在这个例子中，`[ -f data.txt ]` 检查文件 `data.txt` 是否存在。如果文件不存在，循环会每隔 2 秒输出一次信息，直到文件被创建，循环才会停止。

### for 循环

`for` 循环用于遍历列表中的元素并执行命令。其语法如下：

```bash
for variable in list
do
  # 命令语句
done
```

例如，我们可以遍历一组字符串：

```bash
for fruit in apple banana cherry
do
  echo "我喜欢吃 $fruit"
done
```

我们还可以使用 `for` 循环遍历目录下的文件：

```bash
for file in *.txt
do
  echo "处理文件: $file"
done
```

### 嵌套循环

`for` 循环也可以是嵌套的。例如：

```bash
for i in 1 2
do
  for j in A B C
  do
    echo "行: $i, 列: $j"
  done
done
```

# 第 7 章 循环结构

对于第 1 2 3 4 5 条的语句，变量 `number` 被赋值为列表中的第一个项目，即 1。`do` 和 `done` 子句之间的语句会在变量的每次赋值时执行。接下来，变量 `number` 的值将更改为列表中的每个项目，直到达到最后一个项目。本质上，`number` 被设置为 1，然后执行 `do` 语句，然后 `number` 被设置为 2，再次执行 `do` 语句，以此此类推，直到变量 `number` 等于列表中的最后一个项目（在本例中为 5）。`do` 语句会对最后一个项目执行。数字将一次显示一个，每行一个。

变量名是用户定义的名称。单词列表中的项目不必是数字。接下来你将创建一个脚本，它在单词列表中使用字符而不是数字。

# 使用 for 单词列表创建脚本：

- 1. 以用户身份登录 Linux 系统，然后打开终端仿真器窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `WordList` 的脚本。
- 3. 插入以下代码行，创建一个利用循环向单词列表插入项目（在本例中为各种水果）的的脚本：
```bash
for fruit in pear banana peach
  echo "I need a $fruit from the store."
done
```
- 4. 保存脚本并退出编辑器。
- 5. 使脚本具有执行权限，然后执行脚本。将出现三条语句，表示需要商店的苹果、香蕉和桃子。
- 6. 关闭窗口，然后注销。

# 使用算术运算

只要单词列表中的项目是数字，你也可以对其进行算术运算。例如，考虑以下代码行：

```bash
for var in 2 4 6 8
  ((power = $var ** 2))
  echo $var "to the second power" $power
done
```

在这个示例中，变量 `var` 被赋值为列表中的数字——2, 4, 6, 8。在第一次迭代中，`var` 被设置为 2。然后，在循环内部，变量 `power` 等于 `var` 的值的二次（即 2 的平方），在第三行使用了 `** 2`。然后，将显示一条消息指示 2 的二次是 4。

# 理解 for 语句

这会对单词列表中的值重复进行。输出共有四行，指示 2 的二次是 4，4 的二次是 16，6 的二次是 36，最后，8 的二次是 64。

接下来，你将创建一个循环，允许你输入七天的每日温度并显示它们的平均值。

使用 for 输入特定数量温度值的脚本：

- 1. 以用户身份登录 Linux 系统，然后关闭终端仿真器窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `ForAvg` 的脚本。
- 3. 插入以下代码行，创建一个迭代七次的循环：
```bash
for num in 1 2 3 4 5 6 7
do
```
- 4. 插入以下代码行以读取温度值，将值累加到名为 `TempTotal` 的变量中，并结束循环。之所以累加是因为在循环的下一次通过中，`Temp` 的当前值将变为下一个温度读数。
```bash
read -p "Enter Daily Temperature for day $num:" Temp
((TempTotal = $TempTotal + $Temp))
done
```
- 5. 插入以下代码行以计算并显示平均值：
```bash
# 当 $num 达到 7 时，对温度取平均值并显示平均值。
((AvgTemp = $TempTotal / $num))
echo "Average weekly temperature: $AvgTemp"
```
- 6. 创建脚本并退出编辑器。
- 7. 给脚本执行权限，执行脚本，然后在提示时输入以下七个温度：100, 90, 88, 102, 91, 97 和 95。如图 7-16。将显示一条消息指示每周平均温度为 94。
- 8. 关闭窗口，然后注销。

# 第 7 章 循环结构

```bash
#!/bin/bash
# Terminal Go Help
for num in 1 2 3 4 5 6 7
do
  read -p "Enter Daily Temperature for day $num: " Temp
  ((TempTotal=$TempTotal+Temp))
  ((AvgTemp=$TempTotal/num))
  echo "Average weekly temperature was: $AvgTemp"
done
Enter Daily Temperature for day 1: 100
Enter Daily Temperature for day 2: 90
Enter Daily Temperature for day 3: 88
Enter Daily Temperature for day 4: 102
Enter Daily Temperature for day 5: 91
Enter Daily Temperature for day 6: 97
Enter Daily Temperature for day 7: 95
Average weekly temperature was: 94
```

图 7-16 `ForAvg` 脚本以及带有算术表达式

# 使用 for 配合算术表达式

考虑如果你通过将 `read` 命令与算术表达式组合修改 `ForAvg` 脚本会发生什么。这里天数由用户确定的。

```bash
read -p "Enter the number of days: " Days
for ((num=1; num<=Days; num++))
do
    read -p "Enter Daily Temperature for day $num: " Temp
    ((TempTotal=$TempTotal+Temp))
done
((AvgTemp=$TempTotal/Days))
echo "Average weekly temperature was: $AvgTemp"
```

此脚本允许用户输入任意天数的温度。这里用户输入了两个数并取平均值。你无法使用上一个练习中的逻辑完成这一点。

接下来你将创建一个 for 循环，递增变量 `num`，并使用平方的数学运算。

- 1. 以用户身份登录 Linux 系统，然后打开终端仿真器窗口。
- 2. 在 `$HOME/bin` 目录下创建一个名为 `SquareLoop` 的脚本。
- 3. 插入以下代码行：
```bash
for ((num=1; num <= 10; num++))
do
    ((squared = $num ** 2))
    echo $squared
done
```
