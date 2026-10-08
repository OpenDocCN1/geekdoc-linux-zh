

仅为记录中必要的字段分配所需空间，可使记录简洁明了。正如短句易于理解一样，短记录也更容易被理解。同样，应用程序设计得越简单，其性能就越好。不过，请确保包含一个字段来唯一标识文件中的每条记录。例如，程序员文件记录中包含一个程序员编号字段，以区分可能同名的程序员。

> **注意：** 程序员文件记录中的**程序员编号字段**应为数值型。**数值型字段**在唯一标识记录时优于非数值型字段，因为计算机处理数字的速度比处理非数值型字段更快。项目记录可以使用非数值型的项目代码来唯一标识每条项目记录，因为 Dominion 项目代码包含字母和数字（例如 EA-100）。

## 通过键链接文件

多个文件通过**键**进行连接——键是每个链接文件都共有的一个通用字段。在设计阶段，另一个重要任务是规划如何连接文件（如有必要）。例如，程序员-项目应用程序使用程序员的编号将程序员链接到项目文件。将程序员编号字段添加到项目记录中，以将程序员链接到项目。

> **注意：** 能够由简单、简短的记录组成并从多个文件中收集信息的灵活性，是关系型数据库系统的本质。UNIX 包含若干文件处理**命令**，提供了这种关系型数据库的部分灵活性。您将在本课时中实现其中的一些命令。

在开始为应用程序创建文件之前，请回顾图 5-1 中所示的程序员文件和项目文件的记录布局。

### 程序员文件 – 记录布局

| 字段名称 | 数据类型 | 示例 |
| :--- | :--- | :--- |
| programmer_number | 数值 | 101 |
| lname | 字母 | Johnson |
| fname | 字母 | John |
| midinit | 字母 | K |
| salary | 数值 | 39000 |

字段分隔符是冒号 :

示例记录：

101:Johnson:John:K:39000

### 项目文件 – 记录布局

| 字段名称 | 数据类型 | 示例 |
| :--- | :--- | :--- |
| project_code | 字母 | EA-100 |
| project_status | 数值 | 1 (*参见注释) |
| project_name | 字母 | Reservation Plus |
| programmer_number | 数值 | 110 |

字段分隔符是冒号 :

示例记录：

EA-100:1:Reservation Plus:110

*注释：项目状态代码 1=未安排 2=已开始 3=已完成 4=已取消

图 5-1：程序员和项目应用程序的记录布局

## 创建程序员文件和项目文件

既然您已回顾了设计和链接记录的基本要素，就可以开始实现应用程序设计了。正如第 2 章和第 3 章所述，UNIX 文件处理主要使用平面文件。处理这些文件很简单，因为您可以使用 vi 和 Emacs 等文本编辑器创建和操作它们。图 5-2 中的流程图概述并分析了从程序员文件和项目文件推导出的程序员项目分配情况。

![](img/6d8286a85e2d8ad63e16f1801102da59_176_0.png)

文件名: programmer
101:Johnson:John:K:39000
102:King:Mary:K:39800
103:Brown:Gretchen:C:35000
104:Adams:Betty:C:42000
105:Utley:Amos:V:36000
106:Wilson:Patricia:B:39000
107:Culligan:Thomas:F:39000
108:Mitchell:Hillary:N:32800
109:Arbuckle:Margaret:F:46700
110:Ford:Terrence:H:40200
111:Greene:Sarah:L:41700
112:Rose:Richard:P:40200
113:Daniels:Allan:S:30500
114:Edwards:George:J:38500

文件名: project
EA-103:3:Personnel Evaluations:106
WE-206:1:Reservations:102
WE-207:4:Accounting - Basic:101
WE-208:2:Executive-Decision-Maker:102
NE-300:1:Region P & L:103
NE-302:1:Housekeeping Logs:104
NE-304:4:Maintenance Logs:105

## 流程图逻辑

首先使用 vi 编辑器创建程序员文件。

**创建程序员文件的方法：**

1.  在 $ 命令提示符后，输入 **vi programmer** 并按 **Enter**。
2.  输入 **i** 切换到插入模式，然后输入以下文本，在每行末尾（最后一行除外）按 **Enter**：

    ```
    101:Johnson:John:K:39000
    102:King:Mary:K:39800
    103:Brown:Gretchen:K:35000
    104:Adams:Betty:C:42000
    105:Utley:Amos:V:36000
    106:Wilson:Patricia:B:39000
    107:Culligan:Thomas:F:39000
    108:Mitchell:Hillary:N:32800
    109:Arbuckle:Margaret:F:46700
    110:Ford:Terrence:H:44700
    111:Greene:Sarah:L:41700
    112:Rose:Richard:P:40200
    113:Daniels:Allan:S:30500
    114:Edwards:George:J:38500
    ```

3.  按 **Esc** 切换到命令模式。
4.  输入 **:wq** 保存文件并退出 vi。

**创建项目文件的方法：**

1.  在 $ 命令提示符后，输入 **vi project** 并按 **Enter**。
2.  输入 **i** 切换到插入模式，并输入以下文本，在每行末尾（最后一行除外）按 **Enter**：

    ```
    EA-100:1:Reservation Plus:110
    EA-100:1:Reservation Plus:103
    EA-100:1:Reservation Plus:107
    EA-100:1:Reservation Plus:109
    EA-101:2:Accounting-Revenues Version 4:105
    EA-101:2:Accounting-Revenues Version 4:112
    EA-102:4:Purchasing System:110
    EA-103:3:Personnel Evaluations:106
    WE-206:1:Reservations:102
    WE-207:4:Accounting - Basic:101
    WE-208:2:Executive-Decision-Maker:102
    NE-300:1:Region P & L:103
    NE-302:1:Housekeeping Logs:104
    NE-304:4:Maintenance Logs:105
    ```

3.  按 **Esc** 切换到命令模式。
4.  输入 **:wq** 保存文件并退出 vi。

## 格式化输出

第 4 章介绍了 awk 命令，它简化了格式化输出的准备。Awk 实际上是一种功能齐全的编程语言，需要单独一章来介绍。此处有限的介绍仅解释了 awk 命令中 printf 动作的使用，该动作用于格式化输出。printf 函数的语法如下：

| | |
| :--- | :--- |
| **语法** | `printf (format, expr1, expr2, expr3 ...)` |
| **解析** | - `format` 总是必需的。它是一个表达式，其字符串值包含字面文本以及如何格式化参数列表中表达式的规范。每个规范以百分比字符 (%) 开头，将其后的代码标识为修饰符（- 用于左对齐；width 用于设置大小；.prec 用于设置最大字符串宽度或小数点右侧的位数；s 表示字符数组（字符串）；d 表示十进制整数；f 表示浮点十进制数）。用双引号 (" ") 括起来，format 通常被称为覆盖在输入其中的数据字段（exprs）上的“掩码”。<br>- `$expr1, $expr2, $expr3` 是代表数据字段的 awk 表达式。这些表达式通常采用 $1, $2, $3 等形式。在程序员文件中，表达式 $1 表示程序员编号（第一个字段），$2 表示程序员的姓氏（第二个字段），$3 表示程序员的名字（第三个字段）。 |

您可以使用 awk 命令和 printf 函数打印 programmer_number、程序员姓氏和程序员名字，并且全部左对齐。

**打印三个字的方法：**

-   在 $ 命令提示符后，输入 `awk -F: '{printf "%d %-12.12s %-10.10s\n",$1,$2,$3 }' programmer` 并按 Enter。

格式字符串中的每个 % 符号对应一个 $ 字段：%d 指定如何显示 $1 字段，%-12.12s 指定如何显示 $2 字段，而 %-10.10s 指定如何显示 $3 字段。以下是每个说明符的分解：

-   %d 表示 $1 字段应以十进制数字显示。
-   %-12.12s 表示 $2 字段应以字符串显示。减号 (-) 指定字符串应左对齐。12.12 表示字符串应显示在填充至 12 个空格的字段中，最大大小为 12 个空格。
-   %-10.10s 表示 $3 字段应以字符串显示。减号 (-) 指定字符串应左对齐。10.10 表示字符串应显示在填充至 10 个空格的字段中，最大大小为 10 个空格。

格式字符串中出现的空格会精确地打印在相对于字段出现的位置（$1 之后打印一个，$2 之后打印另一个）。尾部的 \n 告诉 awk 在显示这三个字段后跳行。

当您需要提取和格式化数据字段用于输出时，Awk 提供了对其他 UNIX 文件处理命令的捷径。例如，虽然需要几行代码，但您可以使用 cut、paste 和 cat 命令从程序员文件中提取并显示程序员的姓氏和薪水。首先使用 cut 命令从程序员文件中提取姓氏（第 2 字段），并将输出存储到 temp1。接着使用 cut 命令从程序员文件中提取薪水（第 5 字段），并将输出存储到 temp2。然后使用 paste 命令组合 temp1 和 temp2，创建文件 progsal。最后使用 more 命令显示输出。您也可以用一条 awk 命令完成相同的任务。

**使用 cut、paste 和 more 提取并显示信息的方法：**

1.  在 $ 命令提示符后，输入 `cut -f2 -d: programmer > temp1` 并按 Enter。
2.  输入 `cut -f5 -d: programmer > temp2` 并按 Enter。
3.  输入 `paste temp1 temp2 > progsal` 并按 Enter。
4.  要使用 more 命令显示输出，输入 `more progsal` 并按 Enter。

您将看到与以下摘录类似的输出：

```
Johnson 39000
King 39800
Brown 35000
Adams 42000
Utley 36000
...
```

