
该命令使用的大部分选项与 `gzip` 相同（请参阅你的信息源）。例如，我们将在示例 9.18 中使用 `gunzip` 的 `-v` 选项。

## 示例 9.18 gunzip

当堂吉诃德的侄女收到来自 RFI 胡安娜的电话列表（文件名：`RFI_Phones`；参见示例 9.16）后，她对其进行解压，以便阅读和打印。以下是她如何使用 `gunzip` 进行此操作的说明：

```bash
$ gunzip -v RFI_Phones.gz <Enter>
RFI_Phones.gz : 50.0% - replaced with RFI_Phones
```

> **注意** 你的 Linux 发行版中可能还提供了 `zip` 和 `unzip` 命令。你或许更喜欢使用这些命令来压缩和解压文件。

## 显示不可打印字符：cat 命令选项

在这里，我们将讨论三个选项，这些选项可以与现在大家熟悉的 `cat` 命令结合使用（有关 `cat` 的原始讨论请参见第 5 章），以确定以下内容：

-   文本文件或文件名（即目录）中是否存在不可见或无法打印的字符
-   文本文件中空格的自然特性

第二次判定可能很重要，因为 `diff` 命令的输出可能出乎意料，或者 `sort` 命令的输出可能存在问题。当某人正在撰写文档或指定文件或目录名称时，可能会意外输入某些按键序列，从而导致文档或文件/目录名称出现意外结果。例如，请查看表 9.4，其中列出了在使用 `vi` 文本编辑器时有时会输入的一些奇怪的按键序列。该表还展示了在 `vi` 中创建文件期间、在命令行下使用 `cat` 命令时以及在使用 `cat` 的 `-etv` 选项时，这些按键序列的外观。

由于使用 `cat` 时不会显示任何字符，因此我们称这些字符为不可打印字符。因此，可能无法基于目录或文件内容的典型查看方式来解决这些问题。使用这里讨论的带有相应选项的 `cat` 可能有助于确定文件内容或名称是如何创建的，从而可能有助于你确定日后如何读取或操作它们。当然，其语法与其他情况下 `cat` 的语法相同：

```bash
$ cat [-options] [file(s)] <Enter>
```

示例 9.19 中使用的选项定义见表 9.5。

| 选项 | 描述 |
|---|---|
| -e | 显示 `$` 以指示行尾按键；即 Enter 或 Return。 |
| -t | 显示 `^I` 以指示用作空格的 Tab。 |
| -v | 显示 `^G` 以指示其他不可见的 Ctrl-G 按键序列。 |

## 示例 9.19 使用 cat 显示不可打印字符

胡安娜每天早上都会检查她的“请求”文件（`Req-K1`、`Req-K2` 和 `Req-K3`）。7 月下旬，她阅读了一条来自堂吉诃德的乱码信息：

```bash
$ cat Req-K1 <Enter>
Date: July @, 2001
   Subject: Request for Advance Funds for August Trip
Status: Urgent
Deadline: ASA
From: Quixote de

       a Mancha

need 100 Euros as an advance. For the August trip.
Sancho will requisition his own funds, etc.
zizante needs new equipment [shoes, blanket] and provisions.
Will likely leave  August     at }:3] HRS
lus, can someone make an appointment for me at Toledo spa?
now the manager?
hope this meets with your approval and
Very much appreciate your cooperation. t to . ady Dulcinea’s, too.
Signed, Q de
         a M
```

她打电话给堂先生讨论这一情况。一旦一切都满意了，她就打电话给弗雷斯顿，弗雷斯顿建议她对同一条信息执行以下操作：

```bash
$ cat -stv Req-K1 <Enter>
Date: July @\, 2001$
^\Subject: Request for Advance Funds for August Trip$
Status: Urgent$
Deadline: ASA^P$
From: Quixote de ^La Mancha$
$
^"I need i\"100 Euros as an advance. For the August trip.$
Sancho will requisition his own funds, etc.$
zizante needs new equipment [shoes, blanket] and provisions.$
Will likely leave ^"August     ^ _ at }:3] HRS$
^"Plus, can someone make an appointment for me at Toledo spa?
^Know the manager?
^"I hope this meets with your approval ^"I and ^lady DulM^-inea’s,
too.$
^{[Avery much appreM^-iate your M^-operation. t to .$
Signed, Q de ^La M$
```

这帮助胡安娜破译了*部分*按键序列，但并非全部。要确定所有按键序列，胡安娜必须查看堂吉诃陀文件中的原始文档。再次说明，示例 9.19 中使用的选项之前已在表 9.5 中定义。

## 在管道序列中使用 cat 处理文件名中的 ?

在执行目录内容列表时，你有时可能会遇到包含问号（`?`）的文件名。创建此类文件名的人可能是故意插入问号的，但该符号也可以表示存在其他无法被 shell 直接解释的字符。在处理目录中这些奇怪的文件名时，你可以将 `cat` 用作管道命令集中的第二个过程。

例如，典型的 `ls` 命令可能会显示以下内容：

```bash
testfile1    te?stfile2
```

现在，我们尝试使用 `cat`：

```bash
$ ls | cat -vt
```

输出可能如下所示：

```text
testfile1
te^Gatfile2
```

此示例显示了一个 Ctrl-G（即 `^G`），它位于本应被称为 `testfile2` 的文件名中间。你如何更正文件名？你可以简单地按如下方式重命名文件：

```bash
$ mv te^Gatfile2 testfile2
```

> **注意** 你无法在命令行中输入 `te^Gatfile2`。如果你尝试这样做，你会听到 Linux 发出的错误“哔”声。

如果更正策略失败，你可以尝试另一种技术。首先，你需要使用 `ls -i` 获取该文件的 inode 编号。（请记住，显示的文件名可能是 `te?stfile2`，因为简单的 `ls -i` 不会显示隐藏的 Ctrl-G 字符。）

假设该文件的 inode 编号为 1311。现在，输入以下内容：

```bash
$ find . -inum 1311 -exec mv {} testfile2 <Enter>
```

> **注意** 人为制造这种情况有点困难。但这样的事情确实会发生。我们选择 Ctrl-G（或者 `^G`，如果你更喜欢这种表示法）作为我们的隐形字符，因为它 Linux 允许我们使用的唯一一个。

## 分配唯一文件名：追加信息

有时，应用程序——或用户或程序员——必须为文件分配一个唯一的名称。在本节中，我们讨论分配唯一名称的两种方法：

-   自动将进程编号作为后缀追加到文件名末尾
-   自动将日期作为后缀追加到文件名末尾

## 向文件名追加进程编号

如所示和示例 9.20 中所示，通过在文件名末尾添加两个美元符号，shell 会自动将该文件名的末尾添加一个两到五位的进程编号。这种技术很可能每次都生成唯一的文件名。语法如下：

```bash
$ touch filename$$ <Enter>
```

## 示例 9.20 向文件名追加进程编号

每天，RFI 柑橘部门的佩德罗·阿隆索都会订购新设备、肥料、种子、插条等。他需要一种方法来使每日订单文件具有唯一性。他这样做的方法是：

```bash
$ touch citdiv_order$$ <Enter>
$ ls citdiv_order* <Enter>
citdiv_order342 citdiv_order1105 citdiv_order12038
```

> **注意** 对于这两种技术，我们都使用 `touch` 命令来创建示例文件。当然，你可以用许多方式创建文件。

## 向文件名追加日期

虽然向文件名追加进程编号会生成唯一的文件名，但有些人更喜欢后缀能告诉他们更多关于文件的信息。这就是为什么另一种方法，即追加日期作为后缀，很受欢迎的原因。

但在讨论追加日期后缀方法之前，让我们仔细看看 `date` 命令的可能输出。以下是单独使用 `date` 命令时典型的 shell 响应：

```bash
$ date <Enter>
Wed Jul 14 12:48:32 CDT 2001
```

但在创建文件名时，你可能*不*希望包含星期或月份的文本名称（如 Wed 或 July）。相反，你希望使用它们的数字等价物（如 07 代表七月）。上述日期的数字等价物生成如下：

```bash
$ date +'%y%m%d%H%M%S' <Enter>
000714124832
```

在这里，我们要求 shell 以年（y）、月（m）、日（d）、时（H）、分（M）和秒（S）的格式输出日期。

如示例 9.21 所示，文件名格式为基本文件名，后跟一个点作为分隔符，然后是日期作为月-日-时格式的扩展名。不过，如果你每小时生成多个文件名，你应该在格式中添加更精确的日期字段（分钟甚至秒），以防止文件被覆盖（从而丢失有价值信息）。语法是：

```bash
$ touch filename.'date +'[options]' <Enter>
```

无论你怎么决定，都要注意命令语法。注意，使用了两种类型的元字符：单引号（`'`）和反引号（`` ` ``）。

## 示例 9.21 向文件名追加日期

仅仅几周后，`cividov_order$$` 文件开始让佩德罗和其他柑橘部门同事感到困惑。普雷斯顿建议他们使用

