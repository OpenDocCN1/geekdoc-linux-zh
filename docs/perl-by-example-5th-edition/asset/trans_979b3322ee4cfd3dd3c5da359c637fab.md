
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
12 print "Last change inode time: $stats[10]\n";
13 print "Block size: $stats[11]\n";
14 print "Number of blocks: $stats[12]\n";
```

```text
(Output)
2 Device: 2
3 Inode #: 0
4 File mode: 16895
5 # Hard links: 1
6 Owner ID: 0
7 Group ID: 0
8 Device ID: 2
9 Total size: 0
10 Last access time: 981360000
11 Last modify time: 977267374
12 Last change inode time: 977267372
13 Block size:
14 Number of blocks:
```

## 16.1.13 数据打包和解包

还记得 `print` 和 `sprintf` 函数吗？它们用于将参数格式化为浮点数、十进制数、字符串等。`pack` 和 `unpack` 函数将这种格式化功能更进一步。这两个函数都作用于可以表示为位、字节、整数、长整数、浮点数等的字符串，但 `pack` 还可以作用于一般数据以及字符串。格式类型告诉 `pack` 和 `unpack` 如何处理这些字符串。

`pack` 和 `unpack` 函数有多种用途。这些函数用于将列表打包为二进制结构，然后将打包后的值重新展开为列表。在处理文件时，可以使用这些函数创建非 Unicode 文件、关系型数据库、Unicode 字符串和二进制文件。

在处理文件时，并非所有文件都是文本文件。例如，某些文件可能被打包为二进制格式以节省空间、存储图像等。这些文件无法像本页上的文本那样直接阅读。你可以使用 `pack` 和 `unpack` 函数将文件中的行从一种格式转换为另一种格式。`pack` 函数将列表转换为标量值，该值可以存储在机器内存中。表 16.8 中所示的模板用于指定字符类型以及要格式化的字符数量。例如，字符串 `c4` 或 `cccc` 将列表打包为 4 个无符号字符，而 `al4`（注：原文应为 A4 或类似，此处按原文直译）将列表打包为 14 字节的 ASCII 字符串，并用空字符填充。星号（如 `H*`）表示重复字符，代表直到字符串末尾的所有字符。`unpack` 函数将二进制格式化的字符串转换为列表。`pack` 的相反操作将字符串还原为 Perl 格式。

**表 16.8** pack 和 unpack 的模板——类型和值

| 模板 | 描述 |
| :--- | :--- |
| a | ASCII 字符串（空字符填充） |
| A | ASCII 字符串（空格填充） |
| b | 位字符串（从低到高顺序，类似 vec） |
| B | 位字符串（从高到低顺序） |
| c | 带符号字符值 |
| C | 无符号字符值 |
| d | 原生格式的双精度浮点数 |
| f | 原生格式的浮点数 |
| h | 十六进制字符串（低半字节在前，高半字节在后） |
| H | 十六进制字符串（高半字节在前） |
| i | 带符号整数 |
| I | 无符号整数 |
| l | 带符号长整型值 |
| L | 无符号长整型值 |
| n | “网络”（大端）顺序的短整型 |
| N | “网络”（大端）顺序的长整型 |
| p | 指向以空字符终止的字符串的指针 |
| P | 指向结构（定长字符串）的指针 |
| q | 带符号 64 位值 |
| Q | 无符号 64 位值 |
| s | 带符号短整型值（16 位） |
| S | 无符号短整型值（16 位） |
| u | uuencoded 字符串 |
| v | “VAX”（小端）顺序的短整型 |
| V | “VAX”（小端）顺序的长整型 |
| w | 基于 128 进制、高位在前的 BER 压缩无符号整数 |
| x | 空字节 |
| X | 回退一个字节 |
| @ | 填充至绝对位置的空字符 |

## 格式

```perl
$string=pack (Template, @list );
@list = unpack(Template, $string );
```

## 示例 16.24

```perl
(The Script)
1 $bytes=pack("C5", 80,101,114, 108, 012); # 5 ASCII characters
2 print "$bytes";
```

```text
(Output)
Perl
```

## 解释

- 1. 列表中的第一个元素，即模板（参见表 16.8），由类型和要打包的值数量组成；在本例中，是四个带符号字符。列表的其余部分由字符 *P*、*e*、*r* 和 *l* 的十进制值以及换行符的八进制值组成。该列表被打包为二进制结构。包含打包后结构的字符串被返回并存储在 *$bytes* 中。（请参见你的 ASCII 表。）
- 2. 打印这 5 个字节长的字符串。
