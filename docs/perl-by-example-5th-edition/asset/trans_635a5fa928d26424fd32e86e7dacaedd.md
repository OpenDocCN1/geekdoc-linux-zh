
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

Win32 区分文本文件和二进制文件。如果发现 **CR/LF**，程序可能会过早中止或在换行符转换方面出现问题。在读写 Win32 二进制文件时，使用 `binmode` 函数来防止这些问题。`binmode` 函数设置指定的文件句柄以二进制（原始）或文本模式进行读取或写入。如果未指定规则参数，模式将设置为 "raw"。规则是 `*raw`、`*crlf`、`*text`、`*utf8`、`*latin1` 之一，以此类推。

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

- 词法作用域标量 `$fh` 将用于向名为 *temp* 的文件追加输出。与 shell 一样，重定向符号将输出从默认的 stdout 文件句柄 `STDOUT` 重定向到 *temp* 文件。
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

## 解释

- 用户定义的文件句柄 `$fh` 将用于发送并追加输出到名为 *newfile* 的文件。与 shell 一样，重定向符号将输出从默认文件句柄 `STDOUT` 重定向，并将输出追加到文件 *newfile*。如果无法打开文件，例如因为关闭了写入权限，`die` 运算符将打印错误消息 *Can't open newfile: Permission denied.*，并且脚本将退出。
- 字符串 `Just appended "hello world" to the end of newfile` 将通过 `$fh` 文件句柄写入 *newfile* 的末尾。

## 10.2.10 `select` 函数

`select` 函数将默认输出设置为指定的文件句柄，并返回先前选择的文件句柄。所有打印都将发送到所选句柄。一旦使用 `select`，请务必记住将默认输出重置为 `STDOUT`，否则脚本的所有输出将继续发送到“已选择”的文件句柄。

### 示例 10.22

**(脚本)**

```perl
use warnings;
open (my $fh, ">", "newfile") || die "Can't open newfile: $!\n";
select $fh;  # Select the new filehandle for output
open (my $db, "<", "datebook") || die "Can't open datebook: $!\n";

while(<$db>) {   # Output goes to $fh, i.e., newfile
    print;
}
select(STDOUT);   # Send output back to the screen
print "Good-bye.\n";   # Output goes to the screen
```

### 解释

- *newfile* 以只写方式打开并分配给文件句柄 `$fh`。
- `select` 函数将 `$fh` 指定为当前的默认输出文件句柄。`select` 函数的返回值是被关闭的文件句柄的名称（`STDOUT`），以便选择现在已打开用于写入的 `$fh`。
- `$db` 文件句柄以只读方式打开。
- 当从 `$db` 引用的文件中读取每一行到 `$_` 变量时，随后打印到当前选定的文件句柄 `$fh`。注意，你不需要指定文件句柄的名称。
- 通过选择 `STDOUT`，程序其余部分的输出将发送到屏幕。

## 10.2.11 使用 `flock` 进行文件锁定

为了防止两个程序同时写入文件，你可以锁定文件以获得独占访问权，然后在使用完毕后解锁。`flock` 函数接受两个参数：一个文件句柄和一个文件锁定操作。这些操作列在表 10.1 中。

### 表 10.1 文件锁定操作

| 名称 | 操作 | 作用 |
| :--- | :--- | :--- |
| *lock_sh* | 1 | 创建共享锁。 |
| *lock_ex* | 2 | 创建独占锁。 |
| *lock_nb* | 4 | 创建非阻塞锁。 |
| *lock_un* | 8 | 解锁现有锁。 |

获取共享锁需要对文件有读取权限，获取独占锁需要写入权限。对于操作 1 和 2，请求文件的调用者通常会被阻塞（等待），直到文件解锁。如果在文件句柄上使用非阻塞锁，当请求获取已锁定文件时，会立即产生错误。（有关锁的更好实现，请参见 *Fcntl.pm*。）

## 示例 10.23

```perl
use warnings;
# Program that uses file locking -- UNIX
$LOCK_EX = 2;
$LOCK_UN = 8;

print "Adding an entry to the datafile.\n";
print "Enter the name: ";
chomp($name=<STDIN>);
print "Enter the address: ";
chomp($address=<STDIN>);

open(my $fh, ">>", "datafile") || die "Can't open: $!\n";

flock($fh, $LOCK_EX) || die ; # Lock the file

print $fh "$name:$address\n";

flock($fh, $LOCK_UN) || die; # Unlock the file
close $fh;
```

## 解释

- 标量被赋值为 *flock* 函数用于锁定文件的操作值。此操作用于阻塞（等待），直到可以创建独占锁。可以通过从 *Fcntl.pm* 导入常量来定义，例如 `use Fcntl qw(:flock);`
- 此操作用于告知 *flock* 何时解锁文件，以便其他人可以写入。
- 向用户请求更新文件所需的信息。此信息将追加到文件中。

