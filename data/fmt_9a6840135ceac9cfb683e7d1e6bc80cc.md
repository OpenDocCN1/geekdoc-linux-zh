
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

### 在管道序列中使用 `cat` 处理文件名中的 `?`

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

### 分配唯一文件名：追加信息

有时，应用程序——或用户或程序员——必须为文件分配一个唯一的名称。在本节中，我们讨论分配唯一名称的两种方法：

- 自动将进程编号作为后缀追加到文件名末尾
- 自动将日期作为后缀追加到文件名末尾

#### 向文件名追加进程编号

如所示和示例 9.20 中所示，通过在文件名末尾添加两个美元符号，shell 会自动将该文件名的末尾添加一个两到五位的进程编号。这种技术很可能每次都生成唯一的文件名。语法如下：

```bash
$ touch filename$$ <Enter>
```

##### 示例 9.20 向文件名追加进程编号

每天，RFI 柑橘部门的佩德罗·阿隆索都会订购新设备、肥料、种子、插条等。他需要一种方法来使每日订单文件具有唯一性。他这样做的方法是：

```bash
$ touch citdiv_order$$ <Enter>
$ ls citdiv_order* <Enter>
citdiv_order342 citdiv_order1105 citdiv_order12038
```

> **注意** 对于这两种技术，我们都使用 `touch` 命令来创建示例文件。当然，你可以用许多方式创建文件。

#### 向文件名追加日期

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
$ touch filename.`date +`[options]` <Enter>
```

无论你怎么决定，都要注意命令语法。注意，使用了两种类型的元字符：单引号（`'`）和反引号（`` ` ``）。

##### 示例 9.21 向文件名追加日期

仅仅几周后，`cividov_order$$` 文件开始让佩德罗和其他柑橘部门同事感到困惑。普雷斯顿建议他们使用

采用以下基于日期的方法，为订单文件分配唯一的文件名：

```
$ touch ctidiv_order.`date '+%m%d%R'`<Enter>
$ ls testfile.*<Enter>
ctidiv_order.072113  ctidiv_order.072215  ctidiv_order.072313
```

大家一致认为，现在只需查看文件名就能更容易地弄清楚订单是何时创建的。

## 练习

- 1. 登录系统并确保你位于主目录中。创建一个名为 *newdir* 的新子目录。切换到这个新的子目录，并在其中创建五个零长度文件。将这些文件命名为 1、2、3、4 和 5：

```
$ mkdir newdir<Enter>
$ cd newdir<Enter>
$ touch 1 2 3 4 5<Enter>
```

- 2. 列出 *newdir* 子目录的内容。然后，将输出传递给 `xargs` 以复制这些文件并使用 *file* 前缀重命名它们，使得复制后的文件名变为 *file1*、*file2* 等。最后，验证文件是否已复制且名称是否相应地分配：

```
$ ls<Enter>
$ ls | xargs -t -i cp {} file{}<Enter>
$ ls<Enter>
```

- 3. 将 `/etc/passwd` 文件复制到你的 *newdir* 子目录中，使该目录中包含一个含有文本的文件。子目录中的所有其他文件都将是零长度。使用 `find`、`xargs` 和 `grep`、`cat` 显示包含文本的文件的内容：

```
$ cp /etc/passwd .<Enter>
$ find . -type f | xargs -t grep '.*' | cat<Enter>
```

- 4. 识别 `find` 命令所在的目录：

```
$ whereis find<Enter>
```

或者

```
$ which find<Enter>
```

- 5. 确定 find 命令是什么类型的文件（例如可执行文件、ASCII 文件或目录）：

```
$ file /usr/bin/find<Enter>
```

- 6. 使用 find 命令，从你的主目录开始创建一个所有文件的递归列表，并将输出重定向到名为 myfiles 的文件。使用重定向后的 myfiles 文件，确定列表中文件的类型：

```
$ find /home/teammxx > myfiles ; file -f myfiles | less<Enter>
```

或者
