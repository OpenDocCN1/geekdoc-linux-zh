
### 解释

- 1. `symlink` 函数创建新文件名 `new`，链接到旧文件名 `/home/jody/test/old`。
- 2. `ls -ld` 命令列出符号链接文件。符号 `->` 指向新文件名。权限前的 `l` 也表示这是一个符号链接文件。

`readlink` 函数返回符号链接的值，如果文件不是符号链接，则返回 undefined（未定义）。

### 示例 16.19

```perl
$ perl -s 'print readlink("new");'

/home/jody/test/old
```

### 解释

- 1. 文件 `new` 是一个符号链接。它指向 `/home/jody/test/old`，这是 `readlink` 函数返回的值。

### 16.1.10 重命名文件

**`rename` 函数（UNIX 和 Windows）。** `rename` 函数更改文件名称，类似于 UNIX `mv` 命令。其效果是创建指向现有文件的新链接，然后删除现有文件。`rename` 函数成功时返回 `1`，失败时返回 `0`。此函数不能跨越文件系统边界。如果具有新名称的文件已经存在，其内容将被破坏。

### 格式

```perl
rename(OLDFILENAME, NEWFILENAME);
```

### 示例 16.20

```perl
1 rename("tmp", "datafile");
```

### 解释

- 1. 文件 `tmp` 被重命名为 `datafile`。如果 `datafile` 已经存在，其内容将被破坏。

### 16.1.11 更改访问和修改时间

**`*utime*` 函数。** `utime` 函数更改文件列表中每个文件的访问和修改时间，类似于 UNIX `touch` 命令。列表的前两个元素必须按顺序为数值访问时间和修改时间。`time` 函数将当前时间提供给 `utime` 函数。该函数返回成功更改的文件数量。列表中每个文件的 inode 修改时间被设置为当前时间。

### 格式

```perl
utime(LIST);
```

## 示例 16.21

```perl
(The Script---UNIX)

use warnings;

1 print "What file will you touch (create or change time stamp)? ",
  chomp(my $myFile=<>);

2 my $now=$time; # This example makes the file if it doesn't exist

3 utime($now, $now, $myFile) || open(my $tmp,">>","$myFile");
```

```text
(The Command Line)

$ is -l brandnewfile

brandnewfile: No such file or directory

$ perl update.pl

What file will you touch (create or update time stamp)? brandnewfile

$ is -l brandnewfile

-rw-r--r-x- 1 eillie 0 Mar 6 17:13 brandnewfile
```

## 解释

- 1. 用户将输入一个文件名，用于更新该文件的访问时间和修改时间；如果文件不存在，则创建该文件。
- 2. 变量 `$now` 被设置为 `time` 函数的返回值，即自 1970 年 1 月 1 日 UTC 以来的非闰秒数。
- 3. `$now` 的第一个参数是访问时间，第二个参数是修改时间，第三个参数是受影响的文件。如果 `utime` 函数因文件不存在而失败，则 `open` 函数将创建该文件，使用 TMP 作为文件名，模拟 UNIX 的 `touch` 命令。

## 16.1.12 文件统计

文件的信息存储在一个称为 inode 的数据结构中，由内核维护。对于 UNIX 用户来说，许多此类信息可通过 `ls` 命令获取。在 C 和 Perl 程序中，可以直接通过 `stat` 函数从 inode 中检索这些信息。请参阅 `File::Stat` 模块，它为 `stat` 函数创建了一个用户接口。尽管此处重点在于 UNIX，但 `stat` 函数也适用于 Win32 系统。

### stat 和 lstat 函数

`stat` 函数返回一个包含 13 个元素的数组，其中包含从文件的 inode 中检索到的统计数据。最后两个字段涉及块，仅在 BSD UNIX 系统上定义。¹⁰

`lstat` 函数与 `stat` 函数类似，但如果文件是一个符号链接，`lstat` 将返回关于链接本身的信息，而不是它引用的文件的信息。如果系统不支持符号链接，则执行常规的 `stat` 操作。

特殊的下划线文件句柄（`_`）用于提供最近一次执行 `stat` 操作的文件信息。返回的 13 元素数组包含存储在 stat 结构中的以下元素。（其顺序与 UNIX 系统调用 `stat` 略有不同。）

- 1. 设备号
- 2. inode 号
- 3. 模式
- 4. 链接计数
- 5. 用户 ID
- 6. 组 ID
- 7. 对于特殊文件，其引用设备的设备号
- 8. 常规文件的大小（以字节为单位）
- 9. 上次访问时间
- 10. 上次修改时间
- 11. 上次文件状态更改时间
- 12. 文件系统的首选 I/O 块大小
- 13. 实际分配的 512 字节块数

## 格式

```perl
stat FILEHANDLE;

stat EXPR;
```

## 示例 16.22

```perl
(UNIX)

use warnings;

open(my $myfile, "<", "perl1") || die "Can't open: $!\n";

@statistics=stat($myfile);

print "@statistics\n";

close $myfile;

my @stats=stat("perl*");

printf("The inode number is %d and the uid is %d.\n",
$stats[1], $stats[4]);

print "The file has read and write permissions.\n",
if -r _ && -w _;
(Output)

3 1819 142441 33261 1 9496 40 -21335 75 761965998 727296409 8192 2

The inode number is 142441 and the uid is 9496.

The file has read and write permissions.
```

## 解释

- 1. 文件 `perl1` 通过文件句柄表达式 `$myfile` 打开。
- 2. `stat` 函数从文件的 inode 中检索信息，并将该信息返回到一个 13 元素的数组 `@statistics` 中。
- 3. 打印该 13 元素数组。数组的最后两个元素分别是块大小和以 512 字节块为单位的块数。大小和块数可能不同，因为未分配的块不计入块数。负数表示 NIS 设备号。
- 4. 这次，`stat` 函数以文件名作为参数，而非文件句柄。
- 5. 打印数组的第二个和第五个元素。
- 6. 使用特殊的下划线文件句柄 `_` 从上一次 `stat` 调用中获取当前文件统计信息。最近执行 `stat` 的文件是 `perl`。文件测试运算符 `-r` 和 `-w` 使用 `perl` 的当前 stat 信息来检查该文件的读和写访问权限。

## 示例 16.23

```perl
(Windows)

# Since UNIX and Windows treat files differently,
# some of the fields here are
# blank or values returned are not meaningful

use warnings;

1 my @stats = stat('C:\\volume\\testing*');

2 print "Device: $stats[0]\n";

3 print "Inode #: $stats[1]\n";

4 print "File mode: $stats[2]\n";

5 print "Hard links: $stats[3]\n";

6 print "Owner ID: $stats[4]\n";

7 print "Group ID: $stats[5]\n";

8 print "Device ID: $stats[6]\n";

9 print "Total size: $stats[7]\n";

10 print "Last access time: $stats[8]\n";

11 print "Last modify time: $stats[9]\n";
```
