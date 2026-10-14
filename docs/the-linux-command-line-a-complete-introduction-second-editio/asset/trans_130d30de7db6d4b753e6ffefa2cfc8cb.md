

因为数值出现在每一行的开头。但是如果我们想根据行内找到的某个值对列表进行排序呢？例如，这里是 `ls -l` 的结果：

```bash
[me@linuxbox ~]$ ls -l /usr/bin | head
total 152948
-rwxr-xr-x 1 root root 34824 2016-04-04 02:42 [
-rwxr-xr-x 1 root root 101556 2007-11-27 06:08 a2p
-rwxr-xr-x 1 root root 13036 2016-02-27 08:22 aconnect
-rwxr-xr-x 1 root root 10552 2007-08-15 10:34 acpi
-rwxr-xr-x 1 root root 3800 2016-04-14 03:51 acpi_fakekey
-rwxr-xr-x 1 root root 7536 2016-04-19 00:19 acpi_listen
-rwxr-xr-x 1 root root 3576 2016-04-29 07:57 addpart
-rwxr-xr-x 1 root root 20808 2016-01-03 18:02 addr2line
-rwxr-xr-x 1 root root 489704 2016-10-09 17:02 adept_batch
```

暂时忽略 `ls` 本身可以按大小排序其结果这一事实，我们也可以使用 `sort` 按文件大小对这个列表进行排序。

```bash
[me@linuxbox ~]$ ls -l /usr/bin | sort -nrk 5 | head
-rwxr-xr-x 1 root root 8324216 2016-04-07 17:42 inkscape
-rwxr-xr-x 1 root root 8222692 2016-04-07 17:42 inkview
-rwxr-xr-x 1 root root 3746508 2016-03-07 23:45 gimp-2.4
-rwxr-xr-x 1 root root 3654020 2016-08-26 16:16 quanta
-rwxr-xr-x 1 root root 2928760 2016-09-10 14:31 gdbtui
-rwxr-xr-x 1 root root 2928756 2016-09-10 14:31 gdb
-rwxr-xr-x 1 root root 2602236 2016-10-10 12:56 net
-rwxr-xr-x 1 root root 2304684 2016-10-10 12:56 rpcclient
-rwxr-xr-x 1 root root 2241832 2016-04-04 05:56 aptitude
-rwxr-xr-x 1 root root 2202476 2016-10-10 12:56 smbcacls
```

`sort` 的许多用法都涉及 *表格数据* 的处理，例如前面 `ls` 命令的结果。如果我们将数据库术语应用于前面的表格，我们会说每一行是一个 *记录*，并且每个记录由多个 *字段* 组成，例如文件属性、链接计数、文件名、文件大小等等。`sort` 能够处理单个字段。用数据库术语来说，我们能够指定一个或多个 *键字段* 作为 *排序键*。在前面的例子中，我们指定 `n` 和 `r` 选项以执行反向数值排序，并指定 `-k 5` 使 sort 使用第五个字段作为排序键。

`k` 选项很有趣并且具有许多特性，但在首先我们需要讨论 `sort` 如何定义字段。让我们考虑以下简单文本文件，它包含一行作者姓名：

```
William Shotts
```

默认情况下，sort 将此行视为有两个字段。第一个字段包含这些字符："William"。第二个字段包含这些字符："Shotts"。

这意味着空白字符（空格和制表符）用作字段之间的分隔符，并且在排序时分隔符包含在字段中。

再次查看我们 ls 输出中的一行，如下所示，我们可以看到一行包含八个字段，并且第五个字段是文件大小：

```
-rwxr-xr-x 1 root root 8324216 2016-04-07 17:42 inkscape
```

对于我们接下来的系列实验，让我们考虑以下包含 2006 年至 2008 年发布的三个流行 Linux 发行版历史的文件。文件中的每一行有三个字段：发行版名称、版本号以及 MM/DD/YYYY 格式的发布日期。

| Distribution | Version | Date |
|---|---|---|
| SUSE | 10.2 | 12/07/2006 |
| Fedora | 10 | 11/25/2008 |
| SUSE | 11.0 | 06/19/2008 |
| Ubuntu | 8.04 | 04/24/2008 |
| Fedora | 8 | 11/08/2007 |
| SUSE | 10.3 | 10/04/2007 |
| Ubuntu | 6.10 | 10/26/2006 |
| Fedora | 7 | 05/31/2007 |
| Ubuntu | 7.10 | 10/18/2007 |
| Ubuntu | 7.04 | 04/19/2007 |
| SUSE | 10.1 | 05/11/2006 |
| Fedora | 6 | 10/24/2006 |
| Fedora | 9 | 05/13/2008 |
| Ubuntu | 6.06 | 06/01/2006 |
| Ubuntu | 8.10 | 10/30/2008 |
| Fedora | 5 | 03/20/2006 |

使用文本编辑器（也许是 vi），我们将输入这些数据并将 resulting 文件命名为 distros.txt。

接下来，我们将尝试对文件进行排序并观察这些结果：

```
[me@linuxbox ~]$ sort distros.txt
Fedora      10      11/25/2008
Fedora      5       03/20/2006
Fedora      6       10/24/2006
Fedora      7       05/31/2007
Fedora      8       11/08/2007
Fedora      9       05/13/2008
SUSE        10.1    05/11/2006
SUSE        10.2    12/07/2006
SUSE        10.3    10/04/2007
SUSE        11.0    06/19/2008
Ubuntu      6.06    06/01/2006
Ubuntu      6.10    10/26/2006
Ubuntu      7.04    04/19/2007
Ubuntu      7.10    10/18/2007
Ubuntu      8.04    04/24/2008
Ubuntu      8.10    10/30/2008
```

嗯，大部分工作正常。问题出现在 Fedora 版本号的排序上。因为在字符集中 1 在 5 之前，所以版本 10 排在顶部而版本 9 掉到底部。

为了解决这个问题，我们将不得不按多个键进行排序。我们希望对第一个字段进行字母排序，然后对第二个字段进行数值排序。sort 允许多次使用 -k 选项以便指定多个排序键。事实上，一个键可以包含一系列字段。如果没有指定范围（正如我们在之前的例子中所做的那样），sort 使用一个从指定字段开始并延伸到行尾的键。以下是我们多键排序的语法：

```
[me@linuxbox ~]$ sort --key=1,1 --key=2n distros.txt
Fedora      5       03/20/2006
Fedora      6       10/24/2006
Fedora      7       05/31/2007
Fedora      8       11/08/2007
Fedora      9       05/13/2008
Fedora      10      11/25/2008
SUSE        10.1    05/11/2006
SUSE        10.2    12/07/2006
SUSE        10.3    10/04/2007
SUSE        11.0    06/19/2008
Ubuntu      6.06    06/01/2006
Ubuntu      6.10    10/26/2006
Ubuntu      7.04    04/19/2007
```
