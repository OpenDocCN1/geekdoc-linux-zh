
## 第 7 章，单元 A

通过使用操作符，当输入来自另一个 UNIX 命令的输出时，该命令也可以作为过滤器工作。例如，以下命令将 `cat` 命令的输出发送给 `tr`：

此示例命令将 `names` 文件的内容发送给 `tr`。`tr` 实用程序将每个出现的 `:` 字符替换为空格。`tr` 实用程序的工作方式类似于 `sed` 命令，但 `sed` 是按行更改标准输入字符串，而不是逐字符。

你现在使用 `tr` 实用程序将小写字母转换为大写，并将冒号替换为空格。

### 使用 `grep` 和 `tr` 命令进行格式化：

1. 使用 `grep` 命令从 `corp_phones` 文件中检索匹配电话号码 `219-555-4501` 的记录，然后通过管道输出到 `tr`，以将记录中的冒号替换为空格。输入以下命令并按回车：

```
$ grep 219-555-4501 corp_phones | tr ':' ' '
```

你的屏幕看起来类似于图 7-18。

![](img/6ed9bb33c68863516b7a954081187e3b_259_0.png)

2. 通过输入以下命令并按回车，将 `corp_phones` 文件中的小写字母转换为大写：

```
$ cat corp_phones | tr '[a-z]' '[A-Z]'
```

你的屏幕看起来类似于图 7-19。

![](img/6ed9bb33c68863516b7a954081187e3b_260_0.png)

图 7-19：`cat` 和 `tr` 命令的输出

要在 `corp_phones` 文件中搜索电话号码，你的程序可以使用与你在上述步骤中执行的类似的技术。

为你的程序添加记录搜索功能：

1. `phmenu` 程序已经准备好，当用户从菜单中选择 S 时会调用 `phonefind` 脚本。此命令指示程序搜索电话号码。使用 `vi` 或 `Emacs` 编辑器创建 `phonefind` 程序。输入所示的代码：

## 第 7 章，单元 A

```
#!/bin/bash

###########################################=

# Script Name: phonefind

# By: TEG

# Date: November 2000

# Purpose: 在
corp_phones 文件中搜索指定的记录

###########################################=
phonefile=/source/corp_phones

clear

cursor 5 1

echo "Enter phone number to search for:"

cursor 5 35

read number

echo

grep $number phonefile | tr ':' ' '

echo

echo "Press ENTER to continue..."

read continue
```

2. 保存文件并退出编辑器。
3. 使用 `chmod` 命令使文件具有可执行权限，然后通过搜索号码 `219-555-7175` 测试脚本。你的屏幕应该类似于图 7-20。

![](img/6ed9bb33c68863516b7a954081187e3b_261_0.png)

图 7-20：`phonefind` 脚本的输出

你格式化了程序的记录输出；你的下一个任务是删除电话记录。

## 删除电话记录

在本节中，你回顾了 `sed` 命令。回想第 5 章，`sed` 获取输入文件的内容并将作为选项和参数提供的操作应用于文件内容。结果被发送到标准输出设备。使用 `sed` 删除电话记录的简单方法是使用 `d`（删除）选项。以下是必要步骤的伪代码表示：

- 输入电话号码
- 使用 `sed -d` 删除匹配的电话号码并输出到临时文件 `f`
- 确认接受
- 如果接受输出，将临时文件 `f` 复制回 `corp_phones`（覆盖它）

现在你修改 `phmenum` 脚本以包含删除操作。

- 通过编辑 `phmenum` 程序来删除电话记录：
1. 确保你在源目录中。使用 `vi` 或 `Emacs` 编辑器检索修改后的 `phmenum` 程序，并添加粗体显示的代码。

```bash
#!/bin/bash

################################################

# Script Name: phmenum

## By: JQD

## Date: November 1999

# Purpose: 一个菜单

################################################

phonefile~/source/corp_phones

loop="y"

while $loop = "y"

do

  clear

  echo "Phone Menu"

  echo "V - View List"

  echo "P - Print"

  echo "A - Add Phone"

  echo "S - Search"

  echo "D - Delete"

  echo "Q - Quit"

  read choice

  case $choice in

    Dd*) echo "Delete $number"; read Accept

      if $Accept = "y"

        then

        sed "/$number/d" $phonefile > f

        cp f $phonefile

        rm f

      fi

    Qq*) exit ;;

    *) echo "Invalid Code"; ;;

  esac

done
```

2. 保存文件并退出编辑器。
3. 使用 `more` 命令查看文件，测试删除选项。你的屏幕类似于图 7-21。

![](img/6ed9bb33c68863516b7a954081187e3b_221_0.png)

图 7-21：`corp_phones` 文件的内容

4. 运行 `phmenu` 程序并通过删除号码 `219-555-4567` 测试删除选项。你的屏幕类似于图 7-22。

![](img/6ed9bb33c68863516b7a954081187e3b_222_0.png)

图 7-22：删除屏幕

5. 输入 `y` 确认删除。
6. 在主菜单上选择 `V` 查看文件。你的屏幕类似于图 7-23。

![](img/6ed9bb33c68863516b7a954081187e3b_223_0.png)

图 7-23：查看列表选项

注意号码 `219-555-4567` 的记录不再于文件中。

在本节中，你开始修改 shell 程序以满足 Dominion Consulting 的需求。你在 `phmnu` 脚本中添加了删除操作。在下一节中，你将添加防止文件中输入重复电话号码的代码。

## 总结

- 最流行且有效的分析工具是程序流程图和伪代码。流程图是使用一组标准符号绘制的逻辑图，解释流程和要的操作。
- 伪代码是程序的模型。它使用类似于自然语言的句子编写。

- 你可以使用程序脚本文件的第一行来告诉操作系统在解释脚本时使用哪种 shell。
- 你可以使用 `test` 命令验证目录和文件是否存在并比较数值和字符串值。你可以将其放在 shell 脚本中或直接从命令行执行。
- `translate` 实用程序逐字符地更改键盘输入的字符，并且当输入来自另一个 UNIX 命令的输出时也可以作为过滤器。标准输入也可以从文件重定向而不是键盘。
- `sed` 命令读取文件作为输入并输出修改后的内容。你指定选项并传递参数给 `sed` 以控制文件内容的修改方式。

## 复习题

1. 伪代码是为了 __________。
a. 引导程序员编写程序
b. 帮助消除程序中遗漏必要指令的机会
c. 在口头上匹配流程图中的符号表示
d. 以上都是

2. 要告诉系统使用 Bash shell 来解释脚本，请在脚本的第一行使用此代码 __________
a. `#!/bin/bash`
b. `#/bin/bash`
c. `#!/bin/bash`
d. `#$/bin/bash`

## 第 7 章，节 A

- c. 测试隐藏文件
d. 逻辑非

- 6. `test` 命令的 `-o` 选项是操作符。
  a. 逻辑与
  b. 逻辑或
  c. 覆盖
  d. 逻辑非

- 7. `tr` 命令
  a. 仅翻译在键盘输入的内容
  b. 像 `sed` 一样按行翻译
  c. 逐字符翻译
  d. 仅翻译来自文件的字符

- 8. 使用 `tr` 命令将电话记录更改为包含所有小写字母
  a. `tr upper lower corp_phones`
  b. `tr [a-z] [A-Z] corp_phones`
  c. `cat corp_phones | tr [a-z] [A-Z]`
  d. `tr [A-Z] [a-z] < corp_phones`

- 9. `test` 命令返回一个值表示 TRUE 或返回一个值表示 FALSE。
  a. `0, 1`
  b. `1, 0`
  c. 空 err
  d. OK, !OK

- 10. 当你在命令行输入内容时，`test` 命令的返回值会显示。
  a. `echo $$`
  b. `echo $?`
  c. `echo $-`
  d. `echo $$-`

## 练习

- 1. 使用 `tr` 命令翻译电话记录文件，用连字符（`-`）作为字段分隔符代替冒号（`:`）。（确保将翻译后的记录保存到不同的文件中。）

- 2. 设置环境变量 `RHL` 的值为“Red Hat Linux”，并使用 `test` 和 `echo $?` 命令来判断它是否匹配“Red Hat Linux”和“RED HAT LINUX”。你如何判断哪一个匹配？

- 3. 设置环境变量 `NUMVAL` 的值为 `2000`，并使用 `test` 和 `echo $?` 命令来判断它是否匹配值 `2000`。那么 `2020` 呢？你如何判断哪一个匹配？

- 4. 为一个程序编写流程图，该程序用于测试你执行简单算术的能力。程序应该显示两个要相加的数字，并要求用户输入和。如果提供的答案正确，程序应该向用户显示正确答案。

- 5. 为你在练习 4 中创建的流程图程序编写伪代码。

- 6. 为你在练习 4 中使用的数学测试程序编写实际代码，并为练习 5 开发伪代码。图 7-25 显示了程序屏幕输出的示例。

**图 7-25:** 数学测试程序

- 7. 使用 `vi` 或 `Emacs` 创建文件 `My_old_cars`。该文件应包含以下记录：
`1948:Ford:sedan`
`1952:Chevrolet:coupe`
`1960:Ford:Mustang`
`1972:Chevrolet:Corvette`
`1977:Plymouth:Roadrunner`

接下来，编写一个显示数据输入界面的 shell 脚本。脚本允许向文件中输入额外的记录。

- 8. 编写一个 shell 脚本显示 `My_old_cars` 中的所有记录。在输出之前，应将冒号转换为空格。

## 第 7 章，节 A

## 发现练习

- 1. 按姓氏对 `corp_phones` 文件排序，并将输出通过到 `tr` 命令，将所有字符转换为大写，并将输出存储在新文件 `Phoneupper` 中。

- 2. 在你的源目录下创建一个名为 `Scripts` 的目录，并使用 `test` 命令验证该目录是否存在。

- 3. 使用你选择的 `sed` 或 `tr` 命令，将 `corp_phones` 文件中所有出现的“Accountant”单词转换为“Bookkeeper”。

- 4. 用户身份验证程序：UNIX 使用存储在环境变量 `USER` 中的用户登录名。为一个程序设计流程图，询问用户他们是谁。他们的响应应该与 `USER` 变量的内容进行比较。如果两个字符串不匹配，应再次询问用户。此过程应一直重复，直到输入正确的用户名为止。

- 5. 用户身份验证程序：为你在发现练习 4 中设计的流程图编写伪代码。

- 6. 用户身份验证程序：为发现练习 4 中绘制流程图的程序编写实际代码，并为发现练习 5 编写伪代码。图 7-26 显示了程序的输出示例。

图 7-26: 用户身份验证程序的输出

## 节 B 目标

在本节中，你将：

- 创建一个解决问题的程序算法
- 学习创建一种快速清屏的技术
- 开发并测试一个在数据输入期间允许重新输入字段的程序
- 开发并测试一个消除重复记录的程序
- 开发并测试一个从文件中删除记录的程序
- 创建 shell 函数
- 登录时从命令行自动加载 shell 函数

## 完成案例项目

## 清屏

在开始完成编程任务之前，你决定更快速地清屏。`clear` 命令是一个实用的清理工具，用于在新屏幕出现之前清空屏幕（这在 shell 脚本中经常发生），你可以将 `clear` 命令的输出存储在 shell 变量中。回顾第 6 章，你可以通过用单引号括命令将命令输出存储在变量中。例如，此命令将日期的输出存储在变量 `TODAY` 中：

`TODAY = 'date'`

`clear` 命令的输出是一系列擦除屏幕内容的值。将这些值存储在变量并在屏幕上显示该变量的内容可以实现相同的效果，但速度快约十倍。这是因为系统不需要像执行 `clear` 命令时那样去查找并执行 `clear` 命令。

通过设置 shell 变量来清屏：

- 1. 通过输入以下内容将 shell 变量 `CLEAR` 设置为 `clear` 命令的输出：

`CLEAR='clear'`
`export CLEAR`

- 2. 在你的 shell 程序中使用新变量进行快速清屏操作：

`echo "$CLEAR"`

## 第 7 章，节 B

在继续之前进行这种快速清屏，请放置这两行代码：

```bash
CLEAR='clear'
export CLEAR
```

`clear` 命令的输出是一系列擦除屏幕内容的值。将这些值存储在变量并在屏幕上显示该变量的内容可以实现相同的效果，但速度快约十倍。这是因为系统不需要像执行 `clear` 命令时那样去查找并执行 `clear` 命令。

通过设置 shell 变量来清屏：

- 1. 通过输入以下内容将 shell 变量 `CLEAR` 设置为 `clear` 命令的输出：

`CLEAR='clear'`
`export CLEAR`

- 2. 在你的 shell 程序中使用新变量进行快速清屏操作：

`echo "$CLEAR"`

## 移动光标

在继续之前进行这种快速清屏，请放置这两行代码：

```bash
CLEAR='clear'
export CLEAR
```

`clear` 命令的输出是一系列擦除屏幕内容的

## 创建程序算法

算法是产生结果的一系列命令或指令。以下是重新定位光标的伪代码：

```
读取信息到 field2。
当 field2 等于 "-"
移动光标到 field1 的位置。
清除 field1 中显示的信息。
读取新信息到 field1。
如果 field1 = "q"
则
退出程序。
```

## 高级 shell 编程

`phoneadd` 程序中的一个代码添加使用了重新输入的算法：

```bash
cursor 5 18; read lname
while test "$lname" = "-"
do
    cursor 4 18; echo ""
    cursor 4 18; read phonenum
    cursor 5 18; read lname
done
```

将下方所示的**粗代码**添加到程序中。注意，修改后的代码还包含了你新的、更快的清屏功能。它还更改了现有的 `if` 语句，使其使用 `test` 命令。

```bash
#!/bin/bash

# Script Name: phoneadd

## By: JQD

# Date: March 1999

# Purpose: 一个 shell 脚本，设置循环以向 phonelist 文件
# 添加新员工。
# 代码还防止分配重复的电话# 号。
# Command Line: phoneadd

trap "rm ~/tmp/* 2>/dev/null; exit" 0 1 2 3

phonefile=~/source/corp_phones

loopest="y"

while test "$loopest" = "y";
  clear
  cursor 1 4; echo "Corporate Phone List Additions"
  cursor 2 4; echo "Phone Number:"
  cursor 4 4; echo "Middle Init:"
  cursor 5 4; echo "Last Name:"
  cursor 6 4; echo "First Name:"
  cursor 7 4; echo "Middle Init #"
  cursor 8 4; echo "Dept #"
  cursor 9 4; echo "Job Title"
  cursor 10 4; echo "Date Hired:"
  cursor 12 4; echo "Add another? (y)es or (q)uit"
  cursor 4 18; read phonenum
  if test $phonenum = "q";
  then
    clear; exit
    cursor 5 18; read lname
    while test "$lname" = "-";
      cursor 4 18; echo ""
      cursor 4 18; read phonenum
      if test $phonenum = "q";
      then
        clear; exit
      fi
    fi
    cursor 5 18; read lname
done
```

# 高级 Shell 编程

```bash
cursor 6 18 ; read fname
while test "$fname" = "-"
do
    cursor 5 18 ; echo ""
```
