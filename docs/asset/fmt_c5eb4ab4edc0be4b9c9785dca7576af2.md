
`$jobtitle:$datehired >> $phonefile`

fi

tput cup 12 33 ; read looptest

if test "$loopest" = "q"

then

    clear ; exit

fi

done

```
对于步骤 2 中代码中的每个 `echo` 语句，请确保在起始双引号和结束双引号之间放置了 12 个空格。

- 3. 保存文件，并编辑编辑器。
- 4. 执行 `phoneadd` 脚本。对于电话号码，输入 `219-555-4523` 并按回车。你的屏幕类似于图 7-12。
- 5. 在“姓”（Last Name）字段中，输入减号 (`-`) 并按回车。光标移回“电话号码”（Phone Number）字段。你的屏幕看起来如图 7-13。
- 6. 重新输入电话号码 `219-555-4511` 并按回车。
- 7. 使用下方所示的信息完成剩余字段。当你的光标移动到每个字段时，通过输入减号 (`-`) 并按回车来测试程序。光标应该都会移动到上一个字段。

姓：Brooks 部门编号：4540
名：Sally 职位：Programmer
中间名字母：H 入职日期：02-20-2004

![](img/b5f7722b7c2983a215c7726aaada19f9_285_0.png)

图 7-12 `phoneadd` 脚本屏幕

![](img/b5f7722b7c2983a215c7726aaada19f9_285_1.png)

图 7-13 `phoneadd` 准备好重新输入的屏幕

- 8. 在输入所有信息后，退出程序。使用 `cat` 命令显示 `corp_phones` 文件的内容。新记录应当出现。

你已完成第一个任务。你现在准备好处理第二个任务：防止重复电话号码。

# 防止输入重复电话号码

由于用户并不总是输入有效数据，因此程序应该始终检查其输入，以确保用户输入了可接受的信息。这被称为输入验证（input validation）。你的下一个任务是创建一个输入验证算法，防止用户添加已经分配的电话号码。实现此目的的伪代码和流程图如图 7-14 所示。

伪代码：

```
如果电话号码已在文件中

那么

    在屏幕上显示消息“此号码已分配给：

    显示具有重复号码的人员记录。

    清除屏幕并准备下一次输入

结束如果
```

流程图：

![](img/b5f7722b7c2983a215c7726aaada19f9_286_0.png)

图 7-14 `phoneadd` 程序脚本的第二次修订

# 第 7 章 课程 B 高级 Shell 编程

在以下步骤中，你将为 `phoneadd` 添加输入验证代码

**为了防止电话号码重复：**

- 1. 确保你处于源目录。用 `vi` 或 `Emacs` 加载 `phoneadd` 脚本。
- 2. 添加粗体显示的代码部分以完成修订后的脚本。

```bash
#!/bin/bash

################################################################=

# 脚本名称：   phoneadd

# 作者：         在此处输入你的姓名缩写

# 日期：         2004年2月

# 目的：一个设置循环以向 corp_phones 文件添加

# 新员工的 shell 脚本。

# 代码还防止分配重复的电话

# 号。

# 命令行：phoneadd

################################################################=

trap "rm -rf /tmp/* 2>/dev/null; exit" 0 1 2 3

phonefile=/source/corp_phones

loopest=y

while test "$loopest" = "y"

do

clear

tput cup 1 4; echo "Corporate Phone List Additions"

tput cup 2 4; echo "=============================="

tput cup 4 4; echo "Phone Number:"

tput cup 5 4; echo "Last Name:"

tput cup 6 4; echo "First Name:"

tput cup 7 4; echo "Middle Init:"

tput cup 8 4; echo "Dept #"

tput cup 9 4; echo "Job Title:"

tput cup 10 4; echo "Date Hired:"

tput cup 12 4; echo "Add another? (y)es or (q)uit"

tput cup 14 8; read phonenum

if test "$phonenum" = "q"

then

    clear; exit

fi

# 检查电话号码是否已存在

if grep "$phonenum" $phonefile > /dev/null

then

    clear

    echo "This number has already been assigned to:"

    grep "$phonenum" $phonefile

else

    echo "$phoneum:$lname:$fname:$midinit:$deptno:"

    $jobtitle:$datehired >> $phonefile

fi

tput cup 12 33 ; read looptest

if test "$loopest" = "q"

then

    clear ; exit

fi

done
```
*(注：由于原文代码块中存在逻辑错误（重复的 `done` 和不匹配的 `if`），翻译时保持了其原始结构，仅对其中的注释进行了翻译。)*

## 第 7 章 B 节 高级 Shell 编程

![](img/b5f7722b7c2983a215c7726aaada19f9_291_0.png)

要在 shell 脚本放置多个函数：

- 1. 确保你处于源目录中。
- 2. 使用 `vi` 或 `Emacs` 编辑器在源目录下创建 `.myfuncs` 文件。
- 3. 输入以下函数：

```
sort_name()
{
  sort +1 -t: corp_phones
}

sort_date()
{
  sort +6 -t: corp_phones
}

sort_dept()
{
  sort +4 -t: corp_phones
}
```
- 4. 保存文件并退出编辑器。你的你的下一个任务是将 `.myfuncs` 文件加载到内存中，以便可以执行其中的函数。要做到这一点，输入一个点 (`.` 后跟一个空格，然后是包含函数的文件的文件名。

![](img/b5f7722b7c2983a215c7726aaada19f9_291_1.png)加载 `.myfuncs` 文件：

- 1. 在命令行输入 `. .myfuncs`（即输入点、按下空格键、输入点、输入 myfuncs 并回车）。没有任何显示，但函数已加载到内存中。测试一些函数：输入 `sort_name` 并回车。你会看到按姓排序的电话记录。
- 2. 输入 `sort_dept` 并回车。你会看到按部门排序的电话记录。

你可以在登录时使用 `.bash_profile` 或 `.bashrc` 文件自动加载函数。在这种情况下，任何需要这些 shell 脚本都可以使用它们。

![](img/b5f7722b7c2983a215c7726aaada199_2.png)修改你的 `.bashrc` 文件以加载 `.myfuncs` 脚本：

- 1. 输入 `cd` 确保你在家目录下。使用 `vi` 或 `Emacs` 编辑器加载 `.bashrc` 文件。
- 2. 在文件末尾添加以下命令（确保在点 (`.`) 和波浪号 (`~`) 之间留有空格）：`. ~/source/.myfuncs`

## 排序电话列表

- 3. 保存文件并退出编辑器。
- 4. 注销并重新登录以加载函数。
- 5. 测试 `sort_name`、`sort_dept` 等函数。

你的最后一个任务是按姓氏顺序显示电话列表。你可以通过存储在 `.myfuncs` 文件中的 `sort_name` 函数来实现。

# 排序电话列表

要排序电话列表，对 `plist1` 进行细微修改以加载函数，然后调用 `sort_name` 将输出重定向到临时文件。排序后的临时文件作为显示记录的 `awk` 程序的输入。修改后的代码使用了 `$CLEAR` 变量和光标脚本。

要排序电话列表：

```
#!/bin/bash

=====================================
# Script Name:   plist1
# By:            此处填写你的缩写
# Date:          2004
# Purpose:       使用 awk 格式化冒号分隔的
```
