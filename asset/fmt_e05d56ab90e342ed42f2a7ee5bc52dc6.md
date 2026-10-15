
| `syswrite(FILE_HANDLE, BUFFER, LENGTH, OFFSET)` | 从标量变量 `BUFFER` 的 `OFFSET` 位置开始向 `FILE_HANDLE` 写入 `LENGTH` 字节。它返回写入的字节数或未定义值。 |

| `tell(FILE_HANDLE)` | 返回 `FILE_HANDLE` 的当前文件位置。如果未指定 `FILE_HANDLE`，则返回上次读取的文件位置。 |

| `tell_telldir(DIR_HANDLE)` | 返回 `DIR_HANDLE` 的当前位置。返回值可以传递给 `seekdir()` 以访问目录中的特定位置。 |

| `truncate(FILE_HANDLE, LENGTH)` | 将在 `FILE_HANDLE` 上打开的文件截断为 `LENGTH` 长度。 |

| `unlink(FILE_LIST)` | 删除文件列表。如果没有指定 `LIST`，则 `$` 将是成功删除的文件数。否则，如果没有文件被删除，则返回 `false` 或 `0`。 |

## 第 9 章 -- 使用文件

| `utime(FILE_LIST)` | 此基于 UNIX 的函数更改 `FILE_LIST` 中每个文件的访问和修改时间。 |

| `write(FILE_HANDLE)` | 向 `FILE_HANDLE` 写入格式化后的记录。更多信息请参见第 11 章“创建报告”。 |

| Note | 基于 UNIX 的函数将在第 18 章“使用互联网协议”中进一步讨论。Perl 的 UNIX 实现有几个数据库函数可以使用，例如 `dbmopen()` 和 `dbmclose()`。这些函数超出了本书的范围。 |

## 示例：打开文件

`open()` 函数用于打开文件并创建一个名为文件句柄（file handle）的连接。基本的 `open()` 函数调用如下：

```
open(FILE_HANDLE);
```

此版本 `open()` 中的 `FILE_HANDLE` 参数是新文件句柄的名称。它也是存储你想要为输入打开的文件名的标量变量名。例如：

- 将文件名 `FIXED.DAT` 赋值给 `$INPUT_FILE` 变量。变量名使用全大写字母表示它也是文件句柄的名称。
- 以读取模式打开文件。
- 将整个文件读取到 `@array` 中。文件的每一行变成数组中的一个元素。
- 关闭文件。
- 使用 `foreach` 循环查看 `@array` 中的每个元素。
- 打印循环变量 `$`，它包含 `@array` 中的其中一个元素。

### 列表 9.7 09LST07.PL-如何为输入打开文件

```
$INPUT_FILE = "fixed.dat";

open(INPUT_FILE);
@array = <INPUT_FILE>;
close(INPUT_FILE);
```

```
foreach (@array) {
    print();
}
```

此程序显示：

| 1212Jan | Jasprite | Painter |

| 3453Kelly | Horton | Jockey |

尽快关闭通过 `open()` 函数建立的任何连接被认为是良好的编程习惯。虽然不是严格需要的，但它可以确保在发生断电或其他灾性故障时，所有临时缓冲区和缓存都会写入硬盘。

> Note: 对于 DOS 扩展，Windows 限制了你在任何时刻可以打开的文件数量。通常，你可以打开 20 到 50 个文件。通常情况下，这足够了。如果你需要打开更多文件，请查看你的 DOS 文档。

`open()` 函数有许多变体以不同的方式访问文件。表 9.4 显示了用于打开文件的所有不同方法。

### 表 9.4 打开文件的不同方法

| Open 语句 | 描述 |
| :--- | :--- |
| `open(FILE_HANDLE);` | 打开 `$FILE_HANDLE` 中指定的文件，并使用 `FILE_HANDLE` 作为文件句柄连接到它。文件将仅以输入模式打开。 |
| `open(FILE_HANDLE, FILENAME.EXT);` | 使用 `FILE_HANDLE` 作为文件句柄以输入模式打开名为 `FILFILENAME.EXT` 的文件。 |
| `open(FILE_HANDLE, +FILENAME.EXT);` | 使用 `FILE_HANDLE` 作为文件句柄以输入模式打开名为 `FILFILENAME.EXT` 的文件。 |
| `open(FILE_HANDLE, <<FILENAME.EXT);` | 使用 `FILE_HANDLE` 作为文件句柄以输入模式打开名为 `FILFILENAME.EXT` 的文件。 |
| `open(FILE_HANDLE, >>FILENAME.EXT);` | 使用 `FILE_HANDLE` 作为文件句柄以输入模式打开名为 `FILFILENAME.EXT` 的文件。 |
| `open(FILE_HANDLE, >FILENAME.EXT);` | 使用 `FILE_HANDLE` 作为文件句柄以输入模式打开名为 `FILFILENAME.EXT` 的文件。 |
| `open(FILE_HANDLE, |FILENAME.EXT);` | 使用 `FILE_HANDLE` 作为文件句柄以输入模式打开名为 `FILFILENAME.EXT` 的文件。 |

## 第9章 -- 使用文件

我们将以默认文本模式读取文件。

- 初始化一个缓冲区变量。`read()` 和 `sysread()` 在执行函数前，需要初始化它们的缓冲区变量。
- 以只读模式打开 `BINARY.DAT` 文件。
- 使用 `read()` 函数读取文件的前 `20` 个字符。
- 关闭文件。
- 将 `$buffer` 变量中的字符创建一个数组，并使用 `foreach` 循环对其进行迭代。
- 以十六进制格式打印当前数组元素的值。
- 打印一个换行符。如果当前数组元素是换行符，则打印。

![](img/13bc4258f89bbca754b8ea331d6f5de2_369_0.png)

### 列表 9.8 09LST08.PL-读取文件以显示文本模式行结束符

```perl
$buffer = "";

open(FILE, ">binary.dat");
read(FILE, $buffer, 20, 0);

close(FILE);

foreach (split(//, $buffer)) {
    printf("%02x ", ord($$_));
    print "\n" if $_ eq "\n";
}
```

此程序显示：

```
30 31 0a
30 32 0a
30 33 0a
```

这个示例执行了本书书中尚未出现过的几项操作。`read()` 函数是使用菱形操作符（diamond operator）逐行输入的替代方案。它会从输入文件中读取指定数量的字节并将其赋值给缓冲区变量。第四个参数指定了开始读取的偏移量。在本示例中，我们从文件开头开始。

`foreach` 中的 `split()` 函数将字符串拆分为若干部分，并将这些部分放入数组中。双斜杠 `//` 表示字符串中的每个字符都是新数组的一个元素。

有关 `split()` 函数的更多信息，请参阅第5章“函数”和第10章“正则表达式”。

一旦创建了字符数组，`foreach` 循环就会对其迭代。`printf()` 语句在显示之前会将字符的序数值（ordinal value）转换为十六进制。字符的序数值是该字符的 ASCII 表示。例如，'0' 的序数值是 0x30 或 48。

下一行 `print` 语句会在当前字符是换行符时，强制将输出切换到新行。这样做仅仅是为了让输出显示看起来有点像输入文件。

有关 `printf()` 函数的更多信息，请参阅本章后半部分的“示例：重温打印”章节。

现在，让我们以二进制模式读取缓冲区变量，看看输出发生了变化。

- 初始化一个缓冲区。
- 以只读模式打开 `BINARY.DAT` 文件。
- 将模式改为二进制。
- 使用 `read()` 函数读取文件的前 `20` 个字符。
- 关闭文件。
- 将 `$buffer` 变量中的字符创建一个数组，并使用 `foreach` 循环对该数组进行迭代。
- 以十六进制格式打印当前数组元素的值。
- 打印换行符。如果当前数组元素是换行符，则打印。

### 列表 9.9 09LST09.PL-读取文件以显示二进制模式行结束符

```perl
$buffer = "";

open(FILE, "<binary.dat");

binmode(FILE);

read(FILE, $buffer, 20, 0);

close(FILE);

foreach (split(//, $buffer)) {
    printf("%02x ", ord($$_));

    print "\n" if $_ == "\n";
}
```

此程序显示：

```
30 31 0d 0a
30 32 0d 0a
30 33 0d 0a
```

当文件以二进制模式读取时，你可以看到每行末尾实际上有两个字符：换行符（linefeed）和换行符（newline）。
