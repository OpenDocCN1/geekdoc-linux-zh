
# 处理文件

### 打开文件并分配句柄
**句柄**（handle）是你在 Perl 程序中用于引用已打开以读取和/或写入的文件或进程的名称。当你在 shell 中工作时，句柄被称为*文件描述符*（见第 921 页）。与在 shell 中工作时一样，内核在运行程序之前会自动打开标准输入（见第 230 页）、标准输出（见第 230 页）和标准错误（见第 284 页）的句柄。当程序运行结束后，内核会关闭这些描述符。这些句柄的名称分别为 **STDIN**、**STDOUT** 和 **STDERR**。你必须手动打开句柄，才能读取或写入其他文件或进程。**open** 语句的语法如下：

```perl
open (*file-handle*, [*mode*;] *"file-ref"*);
```

其中 *file-handle* 是句柄的名称，或者是你在程序中用于引用由 *file-ref* 命名的文件或进程的变量。如果省略 *mode* 或指定 *mode* 为 <，Perl 将打开文件用于输入（读取）。将 *mode* 指定为 > 可截断并写入文件，指定为 >> 可追加到文件。

关于读写进程的讨论，请参见第 1016 页。

### 写入文件
**print** 函数将输出写入文件或进程。**print** 语句的语法如下：

```perl
print [*file-handle*] *"text"*;
```

其中 *file-handle* 是你在 **open** 语句中指定的句柄名称，*text* 是你希望输出的信息。如前所述，*file-handle* 也可以是 **STDOUT** 或 **STDERR**。除了向标准输出发送信息外，你在 **print** 语句中必须指定一个句柄。不要在 *file-handle* 后添加逗号。另外，不要用括号包裹 **print** 的参数，因为这样做可能会导致问题。

### 从文件读取
以下表达式从与 *file-handle* 关联的文件或进程中读取一行（包括**换行符**（\n））：

```perl
<*file-handle*>
```

此表达式通常用于如下语句中：

```perl
$1line = <IN>;
```

该语句从由句柄 **IN** 标识的文件或进程中读取一行到变量 *$1line* 中。

### 魔法文件句柄（<>）
为了方便从命令行指定的文件或标准输入中读取，Perl 提供了*魔法文件句柄*。本书在大多数示例中使用此文件句柄。你可以用以下代码替代上面的一行：

```perl
$1line = <>;
```
这个文件句柄使得 Perl 程序表现得像许多 Linux 实用程序一样：除非程序调用时带有一个或多个参数，否则它从标准输入读取；如果有参数，则从参数指定的文件中读取。关于此功能如何与 cat 配合使用的解释，请参见第 234 页。

下一个示例第一行的 print 语句包含可选句柄 STDOUT；下一个 print 语句省略了此句柄；最后一个 print 语句使用 STDERR 文件句柄，这会导致 print 的输出发送到标准错误。第一个 print 语句提示用户输入一些内容。该语句输出的字符串以空格（SPACE）结尾，而不是换行符（NEWLINE），因此用户可以在与提示符相同的行上输入信息。第二行然后使用魔法文件句柄从标准输入读取一行，并将其赋值给 $userline。由于魔法文件句柄的原因，如果你调用 file1.pl 时带有一个作为文件名的参数，它将从该文件读取一行，而不是从标准输入读取。运行 file1.pl 的命令行使用 2>（见第 284 页的“文件描述符”）将标准错误（第三个 print 语句的输出）重定向到 file1.err 文件。

```bash
$ cat file1.pl
print STDOUT "Enter something: ";
$userline = <>;
print ">>".$userline."<<\n";
chomp ($userline);
print ">>".$userline."<<\n";
print STDERR "3. Error message.\n";

$ perl file1.pl 2> file1.err
Enter something: hi there
>>hi there
<<<
>>hi there<<<

$ cat file1.err
3. Error message.
```

file1.pl 中用户输入后的两个 print 语句显示 $userline 的值，前面紧跟着大于号（>），后面紧跟着小于号（<）。其中第一个语句表明 $userline 包含换行符（NEWLINE）；用户输入的字符串后面的小于号出现在该字符串所在行的下一行。chomp 函数如果存在，会从字符串末尾移除一个尾随的换行符（NEWLINE）。在 chomp 处理 $userline 后，print 语句显示该变量不再包含换行符。（chop 函数与 chomp 类似，除了它会移除字符串末尾的任何字符。）

下一个示例展示了如何从文件读取。它使用 open 语句将词法文件句柄 $infile 分配给文件 /usr/share/dict/words。while 结构的每次迭代都会评估一个表达式，该表达式从 $infile 表示的文件中读取一行并将该行赋值给 $line。当 while 到达文件末尾时，该表达式评估为 false；控制权随即跳出 while 结构。包含一条语句的块显示从文件中读取的行，包括换行符。

该程序将 /usr/share/dict/words 复制到标准输出。然后使用管道（|; 见第 158 页）将输出传递给 head（见第 154 页），head 显示文件的前四行（第一行是空行）。

```bash
$ cat file2.pl
open (my $infile, "/usr/share/dict/words") or die "Cannot open dictionary: $!\n";
while ($line = <$infile>) {
    print $line;
}

$ perl file2.pl | head -4
A
A's
AOL
```

### $!
$! 变量保存最后一个系统错误。在数值上下文中，它保存系统错误号；在字符串上下文中，它保存系统错误字符串。如果系统上没有 words 文件，file2.pl 将显示以下消息：

> 无法打开词典：没有那个文件或目录

如果你没有该文件的读取权限，程序将显示此消息：

> 无法打开词典：权限被拒绝

显示 $! 的值比仅说明程序无法打开文件能给用户提供更多关于出了什么问题的信息。

### 打开文件时始终检查错误
- **提示**：当 Perl 程序尝试打开文件并失败时，除非程序检查 open 是否返回了错误，否则程序不会显示错误消息。在 file2.pl 中，open 语句中的 or 运算符使 Perl 在 open 失败时执行 die（见第 993 页）。die 语句将“无法打开词典”消息后跟系统错误字符串发送到标准错误，并终止程序。

### @ARGV
@ARGV 数组保存调用 Perl 时从命令行传入的参数。当你用一组文件名调用以下程序时，它会显示每个文件的第一行。如果程序无法读取某个文件，die（见第 993 页）会将错误消息发送到标准错误并退出。foreach 结构循环遍历由 @ARGV 表示的命令行参数，依次将每个参数赋值给 $filename。foreach 块以 open 语句开始。Perl 执行 OR 布尔运算符（or）前面的 open 语句，或者如果该操作失败，Perl 执行 or 运算符后面的语句（die）。结果是 Perl 要么打开由 $filename 命名的文件并将 IN 分配为其句柄，要么如果无法打开该文件，则执行 die 语句并退出。print 语句显示文件名，后跟冒号和文件的第一行。当 Perl 接受 $line = <IN> 作为 print 的参数时，它会显示赋值后的 $line 值。从文件读取一行后，程序关闭该文件。

```perl
$ cat file3.pl
foreach $filename (@ARGV) {
    open (IN, $filename) or die "Cannot open file '$filename': $!\n";
    print "$filename: ", $line = <IN>;
    close (IN);
}

$ perl file3.pl f1 f2 f3 f4
f1: First line of file f1.
f2: First line of file f2.
Cannot open file 'f3': No such file or directory
```

下一个示例与前面的类似，除了它利用了几个使代码更简单的 Perl 特性。当无法读取文件时，它不会退出。相反，Perl 显示错误消息并继续执行。程序的第一行使用 *my* 声明 *$filename* 为词法变量。接下来，*while* 使用魔法文件句柄打开并读取由命令行参数命名的每个文件的每一行；*@ARGV* 保存文件名。当没有更多文件可读时，*while* 条件 [*<>*] 为 *false*，*while* 将控制权转移到 *while* 块外部，程序终止。Perl 负责所有文件打开和关闭操作；你不需要编写代码来处理这些任务。Perl 还执行错误检查。

该程序显示由命令行参数命名的每个文件的第一行。每次通过 *while* 块时，*while* 读取下一个文件。当一个文件读取完毕，它开始从下一个文件读取。在 *while* 块内，它测试是否正在处理一个新文件。如果是，*if* 块显示文件名和文件中的（第一）行，然后将新文件名（*$ARGV*）赋值给 *$filename*。

```perl
$ cat file3a.pl
my $filename;
while (<>) {
    if ($ARGV ne $filename) {
        print "$ARGV: $_";
        $filename = $ARGV;
    }
}

$ perl file3a.pl f1 f2 f3 f4
f1: First line of file f1.
f2: First line of file f2.
Can't open f3: No such file or directory at file3a.pl line 3. <> line 3.
f4: First line of file f4.
```

# 排序

- **reverse**：*sort* 函数根据 *locale*（见第 1091 页）环境返回按数字或字母顺序排列的数组元素。*reverse* 函数与 *sort* 无关；它只是按相反顺序返回数组的元素。

