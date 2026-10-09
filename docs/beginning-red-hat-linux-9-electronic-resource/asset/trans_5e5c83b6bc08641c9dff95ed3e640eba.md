

```perl
use strict;
open (MYPE, '/usr/bin/w |') || die "Cannot create pipe: $!\n";
while (<MYPE>) {
    # Read one line at a time into $_
    print; # Equivalent to: print $_;
}
close (MYPE);
exit (0);
```

如果你匆匆一瞥这个程序，可能会认为我们只是简单地遍历文件并显示每条记录。然而事实并非如此。实际上，我们是在向 `/usr/bin/w` 命令打开一个管道，读取并显示其输出：

```
5:12pm  up 15 days,  6:56,  3 users,  load average: 0.00, 0.00, 0.07
USER   TTY   FROM   LOGIN@   IDLE   JCPU   PCPU   WHAT
shishir   tty1   -   14Jan03  15days  2.27s  0.03s  startx
shishir   pts/0   :0   4:19pm   0.00s   0.37s   0.01s   perl
current_us
dzhiwei   pts/3   192.168.1.6   Fri  3pm  25:49m  17.31s  0.00s  script
```

你在这本书中可能已经见过管道的示例。这里有一个示例，用于查找位于 `/etc` 目录下的所有文件中单词 **perl** 出现的次数：

```
$ grep -d skip perl /etc/* | wc -l
30
```

当 Shell 看到这个命令时，它会执行 `grep` 命令，找出所有包含单词 **perl** 的行，然后将该输出作为输入传递给 `wc` 命令。换句话说，第一个命令的输出被作为第二个命令的输入传递。我们的程序也在做非常类似的事情。但是，如果你看看上面的 `open` 命令那一行，你会发现“管道”（竖线）字符后面没有指定任何内容。输出去哪里了？它去到了 `MYPIPE` 文件句柄，就像这样：

```
$ /usr/bin/w | MYPIPE
```

通过从 `MYPIPE` 文件句柄读取数据，我们实际上是在读取由 `/usr/bin/w` 程序产生的内容。这里的主要优点是我们可以一次读取一行内容，这不仅更高效，而且提供了更好的控制。类似地，我们也可以使用管道将数据发送给另一个应用程序作为输入：

```perl
#!/usr/bin/perl

# sort_numbers.pl: send list of numbers to /bin/sort to get sorted list

open (MYPIPE, '| /bin/sort -g') || die "Cannot create pipe: $!\n";
print MYPIPE "100\n50\n30\n70\n90\n60\n20\n80\n10\n40\n";
close (MYPIPE);

exit (0);
```

注意管道的位置；它在左侧而不是右侧。这意味着我们将通过 MYPIPE 文件句柄将输出发送给另一个应用程序作为输入。更具体地说，我们向 `sort` 命令传递一系列无序数字，该命令产生以下输出：

```
$ perl sort_numbers.pl
10
20
30
40
50
60
70
80
90
100
```

不幸的是，一旦我们将信息作为输入发送给外部应用程序，我们就无法控制它产生的输出；输出通常被发送到标准输出流。在我们继续查看主程序之前，我将向你展示另一种可用于与其他应用程序通信的技术。

## system 命令

如果我们想与一个不关心其输入或输出的程序交互怎么办？例如，一个启动某种服务器或编辑器的脚本，编辑器可能会打开一个空窗口。Perl 为我们提供了 `system` 命令，我们可以用它来调用应用程序。

让我们回顾一下上一节中的 `send_email.pl` 程序。想象一下，如果用户可以进入编辑器输入消息正文，那对用户来说会有多方便？我们可以使用 `system` 命令打开一个编辑器，将内容保存在临时文件中。然后，我们可以从文件中读取内容并将其传递给 Mail::Send 模块：

```perl
#!/usr/bin/perl

use Mail::Send;                  # Import/use Mail::Send
use POSIX;                       # Import/use POSIX
use strict;                      # Enable "strict" pragma

...

print 'Subject: ';
chomp ($subject = <STDIN>);

print "Enter the message in an editor, save and exit when you are done:";

# Call POSIX::tmpnam() to determine a name for a temporary file,
# which we'll use to store the content of the message.

my $file = POSIX::tmpnam();      # For example: /tmp/fileTwFpXe

system ("/usr/bin/gedit $file"); # Open the editor; Perl will wait until
                                  # user finishes, at which point a temp.
                                  # file is created by the editor.

{
    local $/ = undef;            # Undefine record separator

    if (open (FILE, $file)) {
        $message = <FILE>;       # Reads ENTIRE content from file, as
                                 # there is no record separator
        close (FILE);
    }
}

unlink $file;                   # Delete temp. file; ignore status

...

exit (0);
```

我们不会详细讨论这段代码，但希望你能明白其大致思路。正如你从所有这些示例中看到的，通过反引号、管道和 system 命令与外部应用程序通信是相当直观的，但极其强大。我们可以与任何应用程序交互，无论是系统程序、某种脚本还是编译后的应用程序。

## 解析负载平均值

现在来到了应用程序中最困难的部分！我们在本章早些时候简要提到了正则表达式。然而，除了 `list_users.pl` 中的简单正则表达式外，我们还没有在程序中真正使用过它们。在这个应用程序中，我们需要从由 uptime 命令生成的输出中提取用户数量和负载平均值。虽然有很多技术可以完成这项任务，但正则表达式是目前处理这一问题最好且最简单的方式。

## 正则表达式

什么是正则表达式？简而言之，正则表达式是一组“普通”字符和特殊语法元素（元字符），用于在文本中匹配模式。你可以在所有类型的文本操作任务中使用正则表达式，范围从检查特定模式是否存在到查找特定字符串并替换它。

## 来自命令行的替换

例如，假设你有一组大型 HTML 文件，其中包含（除了其他信息外）你公司的物理地址。创建这些文件后不久，你搬到了新地点，现在必须更改所有文件中的地址。你会怎么做？一种繁琐的方法是每个文件手动查找并替换地址。但这显然不现实。然而，借助 Perl 及其正则表达式支持，我们可以毫不费力地在瞬间完成这项任务！

请看下面的 HTML 文件。我省略了除我们感兴趣修改的公司地址以外的所有内容：

```html
<HTML>
...
MechanicNet Group, Inc.<br>
43801 Mission Blvd., Suite 103<br>
Fremont, CA 94539
...
</HTML>
```

我们要将地址更改为显示为：

```html
<HTML>
...
MechanicNet Group, Inc.<br>
7150 Koll Center Parkway, Suite 200<br>
Pleasanton, CA 94566
...
</HTML>
```

有几种方法可以着手完成这项任务。讨论每种方法超出了本章的范围，因此我们将看一种紧凑、通用且非常容易使用的技术：

```bash
$ perl -0777 -p -i.bak -e \
'/s/43801 Mission Blvd., Suite 103<br>/s*Fremont, CA 94539/7150 Koll Center
Parkway, Suite 200<br>\nPleasanton, CA 94566/gsi' *.html
```

就这些，我们甚至不需要写一个完整的程序！我们从命令行运行 Perl 解释器，向其传递几个参数，包括一段执行实际替换的代码。我们先从 -0 开关开始，它将记录分隔符设置为八进制数 777。这与将未定义值作为分隔符的效果相同，因为八进制值 777 是不合法的。通过这样做，我们可以匹配跨越多行的字符串。你会问怎么做呢？通常，默认的记录分隔符是换行符；每次从文件句柄读取时，我们只得到恰好一行：

```perl
$record = <FILE>;    # One line
```

然而，如果记录分隔符未定义，一次读取会将整个文件吸入字符串中：

```perl
local $/ = undef;    # $/ = record separator; special Perl variable
$record = <FILE>;    # Entire file
```

这很方便，因为我们可以搜索字符串或模式而不用担心行边界。然而，你应该小心不要对非常大的文件使用此技术，因为这可能会耗尽系统内存。另一方面，如果你只需要匹配单个字符串或模式，可以安全地忽略此开关。

接下来，我们使用 -p 开关，它创建一个内部 while 循环，遍历指定文件中的每条记录，将内容存储在默认 Perl 变量 $_ 中。如果你看上一行单行语句的最右边，你会看到 Perl 将处理的文件列表。记住，由于记录分隔符未定义，$_ 将包含整个文件的内容，而不仅仅是一行。

-i 开关要求 Perl 就地修改这些文件，将原始文件移动到具有相同名称但带有 .bak 扩展名的另一个文件中。如果你不想为每个文件创建备份副本，只需在 -i 开关后移除 .bak。最后，我们使用 -e 开关来指定应从文件中读取的每条记录应执行的 Perl 代码。如果你想了解解释器接受的所有命令行开关的更多信息，应该查阅 perlrunc man 页面。

以下是执行替换的代码：

```perl
s/43801 Mission Blvd., Suite 103<br>\s*Fremont, CA 94539/7150 Koll Center Parkway, Suite 200<br>\nPLEASANTON, CA 94566/gsi;
```

这等价于：

```perl
$_ =~ s/43801 Mission Blvd., Suite 103<br>\s*Fremont, CA 94539/7150 Koll
Center Parkway, Suite 200<br>\nPLEASANTON, CA 94566/gsi;
```

