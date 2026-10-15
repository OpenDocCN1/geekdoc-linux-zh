
```bash
#====================================================
# Script Name:  phmenu
# By:           JQD
# Date:         March 1999
# Purpose:      A menu for the Corporate Phone List
# Command Line: phmenu
#====================================================
phonefile=~/source/corp_phones
loop=y
while [ "$loop" = y ]
do
   clear
   cursor 3 12; echo "Corporate Phone Reporting Menu"
   cursor 4 12; echo "============================="
   cursor 6 9; echo "P - Print Phone List  :"
   cursor 7 9; echo "A - Add Phone to List :"
   cursor 8 9; echo "S - Search for Phone  :"
   cursor 9 9; echo "V - View Phone List   :"
   cursor 10 9; echo "Q - Quit"
   cursor 11 32;
   read choice || continue
   case $choice in
      [Aa]) phoneadd ;;
      [Pp]) phlist1 ;;
      [Ss]) phonefind ;;
      [Vv]) less $phonefile ;;
      [Qq]) exit ;;
      *) cursor 14 4; echo "Invalid Code"; read choice ;;
   esac
done
```

2. 保存文件并退出编辑器。

3. 测试该脚本。

现在您已准备好运行程序的原型。为此，您使用 `Awk` 程序。

### 使用 Awk

`Awk` 程序提供了 UNIX shell 程序员如何快速创建应用程序模型的一个良好示例。使用 `Awk` 可以加速开发，因为单个 `awk` 命令可以从许多记录中选择字段，并以指定格式在屏幕上显示它们。要运行您的公司电话程序的原型，请将您之前编写的 `cursor` 程序与一行 `Awk` 代码结合使用。

**使用 Awk 程序：**

1. 使用您选择的编辑器创建 `Phlist1` 程序。使用以下代码作为参考。

```bash
# ===============================================
# Script Name:    phlist1
# By:             JQD
# Date:           March 1999
# Purpose: Use awk to format colon-separated fields
#                in a flat file and display to the screen
# Command line: phlist1
# =====================================================
clear
cursor 2 20; echo "Corporate Phone List"
cursor 3 20; echo "========================="
# cursor 5 0;
awk -F':' { printf "%-12s %-12s %s\t%s %s %10.10s %s\n",
       $2, $3, $4, $1, $5, $6, $7 } < corp_phones
```

*注意：OCR 文本显示为 `-F','`，但根据前文描述的冒号分隔数据格式，意图应该是使用 `-F':'` 进行冒号分隔。然而，严格遵循 OCR 文本，该文本显示为 `-F','`，我将保留找到的文本，但需注意标准 awk 处理 CSV 文件时使用逗号。查看数据 `219-555-4567:Harrison...`，分隔符显然是冒号。OCR 很可能将 `'` `:` `'` 误读为 `','` 或类似字符。在此上下文中，这是一个语义错误，我将将其更正为 `':'`。*

```bash
# 基于数据结构进行更正：
awk -F':' { printf "%-12s %-12s %s\t%s %s %10.10s %s\n",
       $2, $3, $4, $1, $5, $6, $7 } < corp_phones
```

2. 保存文件并退出编辑器。

3. 赋予文件执行权限并运行它。您的屏幕应类似于图 6-10。

![](img/6d8286a85e2d8ad63e16f1801102da59_230_0.png)

您意识到名字将被添加到 `corp_phones` 文件中，因此您需要修改您的 shell 脚本。

### 创建 Phoneadd Shell 程序

`Phmenu` 程序提供了向 `corp_phones` 文件添加电话记录的选项；也就是说，用户与程序交互以输入新员工的电话记录。为此，您可以使用 `cursor` 程序，类似于您之前编写的那个，来设计您的数据输入屏幕，显示它，并将光标放置在第一个数据输入字段中。随后您可以将其定位到其他所有输入项。

**创建 `phoneadd` 程序以允许添加：**

1. 使用您选择的编辑器创建脚本 `phoneadd`。输入此代码：
