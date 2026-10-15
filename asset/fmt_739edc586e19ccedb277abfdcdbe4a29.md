
### 说明

- 1 在这里声明哈希，`%course`。键和值将在稍后赋值。
- 2 将标量变量 `$course_number` 赋值为 `101`。
- 3 将字符串“What is the name of course 101?”打印到标准输出（`STDOUT`）。
- 4 哈希的名称是 `%course`。我们正为哈希元素之一赋值。
  键是 `$course_number`，需用花括号包裹。`chomp` 函数将移除用户赋值中的换行符。
- 5 打印新的哈希。它有一个键和一个值。

### 10.2.7 打开用于写入

打开文件进行写入时，如果文件不存在则会被创建；如果文件已存在，则必须具有写权限。如果文件已存在，其内容将被覆盖。文件句柄用于访问系统文件。

### 格式

```
open(my $filehandle, ">", "FILENAME"); # Three arguments, modern way

open(FILEHANDLE, ">FILENAME"); # Bareword, old way
```

### 示例 10.17

```
open($fh, ">", "temp");

open(PH, ">temp");
```

### 说明

- 1 用户定义的文件句柄 `$fh` 将用于向名为 `temp` 的文件发送输出。与 shell 一样，重定向符号将默认文件句柄 `STDOUT` 的输出重定向到 `temp` 文件。
- 2 这是创建用户定义句柄的较旧的双参数方式。

## 示例 10.18

**(脚本)**

```perl
use warnings;

# Write to a file with a filehandle. Scriptname: file.handle

my $file="/home/jody/ellie/perl/newfile";

open my $fh, ">", $file || die "Can't open newfile: $!\n";

print $fh "hello world.\n";

print $fh "Hello world again.\n";
```

**(在命令行中)**

```bash
$ perl file.handle

$ cat newfile
```

**(输出)**

```text
hello world.

hello world, again.
```

## 解释

- 标量变量 `$file` 被设置为名为 `newfile` 的 UNIX 文件的完整路径名。该标量将用于表示通过文件句柄输出定向的 UNIX 文件的名称。此示例在 Windows 上将以相同的方式工作，但如果你使用反斜杠作为目录分隔符，请用单引号包围路径，或者使用两个反斜杠；例如，`C:\home\ellie\testing`。
- 用户定义的文件句柄 `$fh` 会将默认的输出位置（通常是 `STDOUT`）更改为其代表的文件 `newfile`。符号 `>` 表示如果 `newfile` 不存在，则创建它并打开用于写入。如果它已存在，则会打开该文件并**覆盖**其中的任何文本，因此请小心！
- `print` 函数会将输出发送到文件，而不是屏幕。字符串 *hello world* 将通过 `$fh` 文件句柄写入 `newfile`。除非显式关闭文件或 Perl 脚本结束，否则文件 `newfile` 将保持打开状态（参见本章前面的“关闭文件句柄”）。
- `print` 函数会将输出发送到文件句柄 `$fh`，而不是屏幕。字符串 *hello world, again,* 将通过 `$fh` 文件句柄写入 `newfile`。操作系统会跟踪最后一次写入的位置，并将下一行输出发送到文件中最后一个字节之后的位置。
- 执行脚本。输出发送到 `newfile`。
- 打印文件 `newfile` 的内容。

## 10.2.8 Win32 二进制文件

Win32 区分文本文件和二进制文件。如果发现 **CR/LF**，程序可能会过早中止或在换行符转换方面出现问题。在读写 Win32 二进制文件时，使用 `binmode` 函数来防止这些问题。`binmode` 函数设置指定的文件句柄以二进制（原始）或文本模式进行读取或写入。如果未指定规则参数，模式将设置为 "raw"。规则是 `*raw`、` *crlf`、`*text`、`*utf8`、`*latin1` 之一，以此类推。

### 格式

```perl
binmode FILEHANDLE

binmode FILEHANDLE, DISCIPLINE
```

## 示例 10.19

```perl
# This script copies one binary file to another.
# Note its use of binmode to set the mode of the filehandle.
use warnings;

$infile="statebar.gif";

open( my $in, "<", $infile );

open( my $out, ">", "outfile.gif" );

binmode( $in ); # Crucial for binary files!
binmode( $out );

# binmode should be called after open() but before any I/O
# is done on the filehandle.
while ( read( $in, $buffer, 1024 ) ) {
    print $out $buffer;
}

close( $in );
close( $out );
```

## 解释

- 标量 `$infile` 被赋值为一个 `gif` 文件名。
- 文件 `statebar.gif` 以只读方式打开并连接到 `$in` 文件句柄。
- 文件 `outfile.gif` 以只写方式打开并分配给 `$out` 文件句柄。
- `binmode` 函数安排输入文件作为二进制文本读取。
- `binmode` 函数安排输出文件作为二进制文本写入。
- `read` 函数每次读取 1,024 个字节，并将读取的输入存储在标量 `$buffer` 中。
- 读取 1,024 个字节后，它们被发送到输出文件。
- 两个文件句柄均被关闭。结果是某个二进制文件被复制到了另一个二进制文件。

## 10.2.9 以追加方式打开

以追加方式打开文件时，如果文件不存在，将创建该文件；如果文件已存在，则必须具有写入权限。如果文件存在，其内容将保持不变，输出将追加到文件末尾。同样，使用文件句柄而不是访问其实际名称来访问文件。

### 格式

```perl
open(my $filehandle, ">>", FILENAME); # Three arguments, modern way

open(FILEHANDLE, ">>" FILENAME); # Bareword, alternate way
```

## 示例 10.20

```perl
open(my $fh, ">>", "temp");

open(APPEND, ">>" "temp");
```

## 解释

- 词法作用域标量 `$fh` 将用于向名为 *temp* 的文件追加输出。与 shell 一样，重定向符号将输出从默认的 `stdout` 文件句柄 `STDOUT` 重定向到 *temp* 文件。
- 文件句柄 `APPEND` 用于向名为 *temp* 的输出文件追加输出。

## 示例 10.21

**(文本文件)**

```bash
$ cat newfile

hello world.

hello world, again.
```

**(脚本)**

```perl
open(my $fh, ">>", "newfile") || die "Can't open newfile: $!\n";

print $fh qq{Just appended "hello world" to the end of newfile.\n};
```

**(输出)**

```bash
$ cat newfile

hello world.

hello world, again.

Just appended "hello world" to the end of newfile.
```
