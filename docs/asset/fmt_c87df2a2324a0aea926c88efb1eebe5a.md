
## Shell 编程简介

+   2. 保存文件并退出编辑器。
+   3. 给文件赋予执行权限并运行它。你的屏幕应该看起来像图 6-10。

![](img/6ed9bb33c68863516b7a954081187e3b_230_0.png)

图 6-10：`Phlist1` 脚本的输出

你意识到名称将添加到 `corp_phones` 文件中，因此你需要修改你的 Shell 脚本。

# 创建 `phoneadd` Shell 程序

`Phmenu` 程序提供了向 `corp_phones` 文件添加电话记录的选项；即用户与程序交互以输入新员工的电话记录。为了做到这一点，你可以使用与之前编写的类似的光标程序来设计你的数据输入界面，显示它，并将光标置于数据输入字段中。随后你可以为所有其他条目进行定位。

要创建一个允许添加的 `phoneadd` 程序：

+   * 使用你选择的编辑器创建脚本 `phoneadd`。在代码中输入以下：

``` 
# 脚本名称: phoneadd
# 作者: JQD
# 日期: 1999年3月
# 目的: 一个设置循环以向
# 员工添加到 Corp_phones 文件的脚本。
# 命令行语法: phoneadd
trap "rm -tmp/* 2>/dev/null; exit 0 1 2 3
# 写入磁盘
if "$fname" != "" ];
then
echo "$phonenum:$fname:$midname:$deptno:$jobtitle" >> phonefile
cursor 7 9; echo "A - Add Phone to List :"
cursor 8 9; echo "S - Search for Phone :"
cursor 9 9; echo "V - View Phone List : "
cursor 10 9; echo "Q - Quit"
cursor 11 32
read choice || continue
case choice in
[Aa]) phoneadd ;
[Pp]) phlist1 ;
[Ss]) phonefind ;
[Vv]) less $phonefile;
[Qq]) exit ;;
*) cursor 14 4; echo "Invalid Code";; read choice ;;
esac
```
done

+   2. 保存文件并退出编辑器。
+   3. 给文件赋予执行权限，并对其进行测试。

当你向 Dominion Consulting 的经理演示你的程序时，他们指出在输入额外信息时可能会发生某些错误。为了快速定位错误，你需要查看未格式化的记录。

# 查看未格式化的记录

拥有一个可以显示未格式化文件数据的程序通常是有用的，这意味着记录显示的内容与其在磁盘上存储的方式完全相同。在电话记录的情况下，显示将显示分隔变长度字段的冒号（`:`）字符。如果出现问题，查看原始数据将非常方便。为了做到这一点，你使用 `least` 命令在屏幕上显示记录。

使用 `least` 命令查看未格式化的记录：
1. 在你选择的编辑器中打开 `Phmenu`，并显示所示加粗行。

```
######################################################################
# 脚本名称: phmenu
# 作者: JQD
# 日期: 1999年3月
# 目的: 公司电话列表菜单
# 命令行: phmenu
######################################################################
```

```
phonefile=~/source/corp_phones
loop=y
while [ "$loop" = y ]
```

# 第6章，B 节

```
do
clear
cursor 3 12; echo "Corporate Phone Reporting Menu"
cursor 4 12; echo "========================"
cursor 6 9; echo "P - Print Phone List : "
cursor 7 9; echo "A - Add Phone to List : "
cursor 8 9; echo "S - Search for Phone : "
cursor 9 9; echo "V - View Phone List : "
cursor 10 9; echo "Q - Quit"
cursor 11 32;
read choice || continue
  case $choice in
    [Aa]) phoneadd ;;
    [Pp]) phlist1 ;;
    [Ss]) phonefind ;;
    [Qq]) exit ;;
    *) cursor 14 4; echo "Invalid Code"; ;
esac
done
```

+   2. 保存文件并退出编辑器。
3. 测试脚本。

你现在准备好运行你的程序原型了。为了实现这一点，你将使用 Awk 程序。

## 使用 Awk

`Awk` 程序提供了一个很好的示例，展示了 UNIX Shell 程序员如何快速创建应用程序模型。使用 `Awk` 可以加速开发，因为单条 `Awk` 命令就可以从许多记录中选择字段，并以指定的格式在屏幕上显示它们。要运行你的公司电话程序的原型，请将你之前编写的光标程序与一行 `Awk` 代码结合起来。

要使用 `Awk` 程序：
使用你选择的编辑器创建 `Phlist1` 程序。使用以下代码作为指南。

```
# ====================================
# 脚本名称: phlist1
# 作者: JQD
# 日期: 1999年3月
# 目的: 使用 awk 格式化冒号分隔的字段
```

```
# 在扁平文件中并显示到屏幕上
# 命令行: phlist
# ==================================================
clear
cursor 2 20; echo "Corporate Phone List"
cursor 3 20; echo "===================================="
cursor 5 0;
awk -F: ' { printf "%-12s %%-12s %%s\t%%s %%s %%10.10s %%s\n", \
$2, $3, $4, $1, $5, $6, $7 } corp_phones
```

+   2. 保存文件并退出编辑器。
+   3. 给文件赋予执行权限并运行它。你的屏幕应该看起来像图 6-10。

![](img/6ed9bb33c68863516b7a954081187e3b_230_0.png)

图 6-10：`Phlist1` 脚本的输出

你意识到名称将添加到 `corp_phones` 文件中，因此你需要修改你的 Shell 脚本。

# 创建 `phoneadd` Shell 程序

`Phmenu` 程序提供了向 `corp_phones` 文件添加电话记录的选项；即用户与程序交互以输入新员工的电话记录。为了做到这一点，你可以使用与之前编写的类似的光标程序来设计你的数据输入界面，显示它，并将光标置于数据输入字段中。随后你可以为所有其他条目进行定位。

要创建一个允许添加的 `phoneadd` 程序：

+   * 使用你选择的编辑器创建脚本 `phoneadd`。在代码中输入以下：

```
# 脚本名称: phoneadd
# 作者: JQD
# 日期: 1999年3月
# 目的: 一个设置循环以向
# 员工添加到 Corp_phones 文件的脚本。
# 命令行语法: phoneadd
trap "rm -tmp/* 2>/dev/null; exit 0 1 2 3
```
