
```
lp
mail
news
```

使用 -d 选项，我们可以指定冒号字符作为字段分隔符。

## 展开制表符

我们的 distros.txt 文件非常适合使用 cut 提取字段。但如果我们想要一个可以用 cut 按字符（而非按字段）完全操作的文件，该怎么办呢？这就需要我们将文件中的制表符替换为相应数量的空格。幸运的是，GNU coreutils 软件包中包含了一个用于此目的的工具。这个名为 expand 的程序接受一个或多个文件参数或标准输入，并将修改后的文本输出到标准输出。

如果我们用 expand 处理 distros.txt 文件，就可以使用 cut -c 提取文件中任意范围的字符。例如，我们可以使用以下命令，通过展开文件并使用 cut 提取从第 23 个位置到行尾的每个字符，从而从列表中提取发行年份：

```
[me@linuxbox ~]$ expand distros.txt | cut -c 23-
```

coreutils 还提供了 unexpand 程序，用于将空格替换为制表符。

## paste — 合并文件行

paste 命令与 cut 相反。它不是从文件中提取文本列，而是向文件添加一列或多列文本。它通过读取多个文件，并将每个文件中的字段组合成单一的标准输出流来实现这一点。与 cut 一样，paste 接受多个文件参数和/或标准输入。为了演示 paste 的工作方式，我们将对 distros.txt 文件进行一些处理，以生成按时间顺序排列的发行版列表。

根据之前使用 sort 的工作，我们将首先生成一个按日期排序的发行版列表，并将结果存储在名为 distros-by-date.txt 的文件中：

```
[me@linuxbox ~]$ sort -k 3.7nbr -k 3.1nbr -k 3.4nbr distros.txt > distros-by-date.txt
```

接下来，我们将使用 cut 从文件中提取前两个字段（发行版名称和版本），并将结果存储在名为 distros-versions.txt 的文件中。

```
[me@linuxbox ~]$ cut -f 1,2 distros-by-date.txt > distros-versions.txt
[me@linuxbox ~]$ head distros-versions.txt
Fedora 10
Ubuntu 8.10
SUSE 11.0
Fedora 9
Ubuntu 8.04
Fedora 8
Ubuntu 7.10
SUSE 10.3
Fedora 7
Ubuntu 7.04
```

最后一项准备工作是提取发布日期，并将它们存储在名为 distros-dates.txt 的文件中。

```
[me@linuxbox ~]$ cut -f 3 distros-by-date.txt > distros-dates.txt
[me@linuxbox ~]$ head distros-dates.txt
11/25/2008
10/30/2008
06/19/2008
05/13/2008
04/24/2008
11/08/2007
10/18/2007
10/04/2007
05/31/2007
04/19/2007
```

现在我们已经有了所需的各个部分。要完成这个过程，请使用 paste 将日期列放在发行版名称和版本之前，从而创建一个按时间顺序排列的列表。只需使用 paste 并按需要的顺序排列其参数即可。

```
[me@linuxbox ~]$ paste distros-dates.txt distros-versions.txt
11/25/2008 Fedora 10
10/30/2008 Ubuntu 8.10
06/19/2008 SUSE 11.0
05/13/2008 Fedora 9
04/24/2008 Ubuntu 8.04
11/08/2007 Fedora 8
10/18/2007 Ubuntu 7.10
10/04/2007 SUSE 10.3
05/31/2007 Fedora 7
04/19/2007 Ubuntu 7.04
12/07/2006 SUSE 10.2
10/26/2006 Ubuntu 6.10
10/24/2006 Fedora 6
06/01/2006 Ubuntu 6.06
05/11/2006 SUSE 10.1
03/20/2006 Fedora 5
```

## join — 基于共同字段连接两个文件的行

在某些方面，join 与 paste 类似，它向文件添加列，但方式独特。连接（join）是一种通常与关系数据库相关的操作，它将来自多个具有共享键字段的表的数据组合起来，以形成所需的结果。join 程序执行相同的操作。它基于共享键字段连接多个文件中的数据。

为了了解连接操作在关系数据库中的使用方式，让我们想象一个非常小的数据库，它由两个表组成，每个表包含一条记录。第一个表名为 CUSTOMERS，包含三个字段：客户编号（CUSTNUM）、客户的名（FNAME）和客户的姓（LNAME）：

| CUSTNUM | FNAME | LNAME |
| ------- | ----- | ----- |
| 4681934 | John | Smith |

第二个表名为 ORDERS，包含四个字段：订单号（ORDERNUM）、客户编号（CUSTNUM）、数量（QUAN）和订购项目（ITEM）：

| ORDERNUM | CUSTNUM | QUAN | ITEM |
| -------- | ------- | ---- | ---- |
| 3014953305 | 4681934 | 1 | Blue Widget |

请注意，两个表共享 CUSTNUM 字段。这一点很重要，因为它允许表之间建立关系。

执行连接操作可以让我们组合两个表中的字段，以实现有用的结果，例如准备发票。利用两个表中 CUSTNUM 字段的匹配值，连接操作可以生成以下结果：

| FNAME | LNAME | QUAN | ITEM |
| ----- | ----- | ---- | ---- |
| John | Smith | 1 | Blue Widget |

为了演示 join 程序，我们需要创建几个具有共享键的文件。为此，我们将使用 distros-by-date.txt 文件。从这个文件中，我们将构建两个额外的文件。一个包含发布日期（在本演示中作为共享键字段）和发行版名称：

```
[me@linuxbox ~]$ cut -f 1,1 distros-by-date.txt > distros-names.txt
[me@linuxbox ~]$ paste distros-dates.txt distros-names.txt > distros-key-names.txt
[me@linuxbox ~]$ head distros-key-names.txt
11/25/2008    Fedora
10/30/2008    Ubuntu
06/19/2008    SUSE
05/13/2008    Fedora
04/24/2008    Ubuntu
11/08/2007    Fedora
10/18/2007    Ubuntu
10/04/2007    SUSE
05/31/2007    Fedora
04/19/2007    Ubuntu
```
