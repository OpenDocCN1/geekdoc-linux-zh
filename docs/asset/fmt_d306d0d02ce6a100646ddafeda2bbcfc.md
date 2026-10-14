
`[me@linuxbox ~]$ cat -A distros.txt`

```
SUSE^I10.0^I12/07/2006$
Fedora^I10^I11/25/2008$
SUSE^I11.0^I06/19/2008$
Ubuntu^I8.04^I04/24/2008$
Fedora^I8^I11/08/2007$
SUSE^I10.0^I10/04/2007$
Ubuntu^I6.10^I10/26/2006$
Fedora^I7^I05/31/2007$
Ubuntu^I7.10^I10/18/2007$
Ubuntu^I7.04^I04/19/2007$
SUSE^I10.0^I05/11/2006$
Fedora^I6^I10/24/2006$
Fedora^I9^I05/13/2008$
Ubuntu^I6.06^I06/01/2006$
Ubuntu^I8.10^I10/30/2008$
Fedora^I5^I03/20/2006$
```

看起来不错——没有嵌入的空格，只有字段之间的单个制表符。由于文件使用制表符而不是空格，我们将使用 `-f` 选项来提取字段：

```
[me@linuxbox ~]$ cut -f 3 distros.txt
12/07/2006
11/25/2008
06/19/2008
04/24/2008
11/08/2007
10/04/2007
10/26/2006
05/31/2007
10/18/2007
04/19/2007
05/11/2006
10/24/2006
05/13/2008
06/01/2006
10/30/2008
03/20/2006
```

由于我们的 `distros` 文件是制表符分隔的，因此最好使用 `cut` 来提取字段而不是字符。这是因为当文件是制表符分隔时，很不可能每行包含相同数量的字符，这使得计算行内字符位置变得困难或不可能。在上面的示例中，我们现在已经提取了一个字段，该字段幸运地包含长度相同的数据，因此我们可以展示字符提取的工作原理，通过提取每行中的年份：

```
[me@linuxbox ~]$ cut -f 3 distros.txt | cut -c 7-10
2006
2008
2008
2008
2007
2007
2006
2007
2007
2007
2006
2006
2008
2006
2008
2006
```

通过在列表上再次运行 `cut`，我们能够提取字符位置 7 到 10，这对应于我们日期字段中的年份。`7-10` 记法是范围的一个示例。`cut` 手册页包含如何指定范围的完整描述。

在处理字段时，可以指定与制表符字符不同的字段分隔符。这里我们将从 `/etc/passwd` 文件中提取第一个字段：

```
[me@linuxbox ~]$ cut -d ':' -f 1 /etc/passwd | head
root
daemon
bin
sys
sync
games
man
```

```
lp
mail
news
```

使用 `-d` 选项，我们可以指定冒号字符作为字段分隔符。

## 展开制表符

我们的 `distros.txt` 文件非常适合使用 `cut` 提取字段。但如果我们想要一个可以用 `cut` 按字符（而非按字段）完全操作的文件，该怎么办呢？这就需要我们将文件中的制表符替换为相应数量的空格。幸运的是，GNU `coreutils` 软件包中包含了一个用于此目的的工具。这个名为 `expand` 的程序接受一个或多个文件参数或标准输入，并将修改后的文本输出到标准输出。

如果我们用 `expand` 处理 `distros.txt` 文件，就可以使用 `cut -c` 提取文件中任意范围的字符。例如，我们可以使用以下命令，通过展开文件并使用 `cut` 提取从第 23 个位置到行尾的每个字符，从而从列表中提取发行年份：

```
[me@linuxbox ~]$ expand distros.txt | cut -c 23-
```

`coreutils` 还提供了 `unexpand` 程序，用于将空格替换为制表符。

## `paste` — 合并文件行

`paste` 命令与 `cut` 相反。它不是从文件中提取文本列，而是向文件添加一列或多列文本。它通过读取多个文件，并将每个文件中的字段组合成单一的标准输出流来实现这一点。与 `cut` 一样，`paste` 接受多个文件参数和/或标准输入。为了演示 `paste` 的工作方式，我们将对 `distros.txt` 文件进行一些处理，以生成按时间顺序排列的发行版列表。

根据之前使用 `sort` 的工作，我们将首先生成一个按日期排序的发行版列表，并将结果存储在名为 `distros-by-date.txt` 的文件中：

```
[me@linuxbox ~]$ sort -k 3.7nbr -k 3.1nbr -k 3.4nbr distros.txt > distros-by-date.txt
```

接下来，我们将使用 `cut` 从文件中提取前两个字段（发行版名称和版本），并将结果存储在名为 `distros-versions.txt` 的文件中。

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

最后一项准备工作是提取发布日期，并将它们存储在名为 `distros-dates.txt` 的文件中。

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

现在我们已经有了所需的各个部分。要完成这个过程，请使用 `paste` 将日期列放在发行版名称和版本之前，从而创建一个按时间顺序排列的列表。只需使用 `paste` 并按需要的顺序排列其参数即可。

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
