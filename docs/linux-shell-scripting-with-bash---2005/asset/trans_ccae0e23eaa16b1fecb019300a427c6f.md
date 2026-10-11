

为了获得更高的校验和安全性，某些发行版包含了`md5sum`命令来计算 MD5 校验和。`–status` 开关会静默地测试文件。`–binary`（或 `-b`）开关将文件视为二进制数据，而不是文本。`–warn` 开关会打印关于错误 MD5 格式警告信息。`–check`（或 `-c`）检查文件的校验和。

```bash
$ md5sum orders.txt
945eeccl37074a43e232730a44774004  orders.txt
$ md5sum orders.txt > orderssum.txt
$ md5sum –check orderssum.txt
file1.txt: OK
```

两个文件之间的差异可以通过 Linux 的 `cmp` 命令来精确定位。

```bash
$ cmp orders.txt orders2.txt
orders.txt orders2.txt differ: char 179, line 6
```

如果两个文件没有差异，`cmp` 不会打印任何内容。

# 拆分大文件

使用 Linux 的 `split` 命令可以将极大的文件拆分为较小的文件。文件可以按字节或按行进行拆分。`–bytes=s`（或 `–b s`）开关创建的文件不超过 *s* 字节。`–lines=s`（或 `-l s`）开关创建的文件不超过 *s* 行。`–line-bytes=s`（或 `-c s`）开关限制每行不超过 *s* 字节。大小是一个数字，可选带有 b（512 字节块）、k（千字节）或 m（兆字节）后缀。最后一个参数是新文件名使用的文件前缀。

```bash
$ split –bytes=10k huge_file.txt small_file
$ ls -l small_file*
-rw-rw-r-- 1 kburtch kburtch 10240 Aug 28 16:19 small_fileaa
-rw-rw-r-- 1 kburtch kburtch 10240 Aug 28 16:19 small_fileab
-rw-rw-r-- 1 kburtch kburtch  1319 Aug 28 16:19 small_fileac
```

你可以使用 Linux 的 `cat` 命令重新组装拆分后的文件。该命令组合文件并将其写入标准输出。务必注意按正确顺序组合拆分后的文件。

```bash
$ cksum huge_file.txt
491404265 21799  huge_file.txt
$ cat small_fileaa small_fileab small_fileac > new_file
$ cksum new_file
491404265 21799 new_file
```

如果执行拆分的区域设置与重新组装文件时的区域设置相同，则可以使用通配符匹配（wildcard globbing）作为 `cat` 的文件名是安全的。

Linux 的 `csplit`（*上下文拆分*）命令在特定模式出现的位置拆分文件。

`csplit` 的基本模式是以斜杠包围的正则表达式，后跟可选的偏移量。该正则表达式表示将成为下一个新文件第一行的行。偏移量表示从匹配行向前或向后移动的行数，默认为零。模式 `*/\d\cg/\+\*` 将文件拆分为两个较小的文件，第一个文件以模式 `\d\cg` 的第一次出现结束。

对模式进行引用可以防止其被 Bash 解释，而不是由 `csplit` 命令解释。

`-prefix=R`（或 `-f P`）开关设置新文件名的前缀。`-suffix=S`（或 `-b S`）使用指定的 C printf 函数代码写入文件编号。`-digits=D`（或 `-n D`）开关指定文件编号的最大位数。默认值为两位数字。

```bash
$ csplit -prefix "chairs" orders.txt "/Chair/"   
107   
485   
$ ls -l chairs*
-rw-rw-r--   1 kburcht  kburcht   107 Oct  1 15:33 chairs00
-rw-rw-r--   1 kburcht  kburcht   485 Oct  1 15:33 chairs01
$ head -1 chairs01
Reclining Chair,1599.99,1,757  
```

模式 `Chair` 的第一次出现是在 `Reclining Chair` 行中。可以列出多个模式。用百分号（`%`）而不是斜杠分隔的模式表示应忽略文件的一部分，直到指示的模式为止。它也可以有偏移量。单独的数字表示该特定行开始下一个新文件。花括号内的数字重复最后一次模式特定次数，或者星号匹配模式的所有出现。

要将 `orders.txt` 文件拆分为独立的文件，每个文件都以单词 `Chair` 开头，请使用所有出现模式。

```bash
$ csplit -prefix "chairs" orders.txt "/Chair/*" "(* *)"
107   
222   
23    
179   
61    
$ ls -l chairs*
-rw-rw-r--   1 kburcht  kburcht   107 Oct  1 15:37 chairs00
-rw-rw-r--   1 kburcht  kburcht   222 Oct  1 15:37 chairs01
-rw-rw-r--   1 kburcht  kburcht   23  Oct  1 15:37 chairs02
-rw-rw-r--   1 kburcht  kburcht   179 Oct  1 15:37 chairs03
-rw-rw-r--   1 kburcht  kburcht   61  Oct  1 15:37 chairs04
```

`-elide-empty-files`（或 `-z`）开关不会保存空文件。`-keep-files`（或 `-k`）在发生错误时不会删除生成的文件。`-quiet`（或 `-silent` 或 `-q` 或 `-B`）开关隐藏进度信息。

`csplit` 在拆分包含重复信息的大文件时很有用，例如将客户发送的单个订单提取为单个文本文件。

# 制表符和空格

Linux expand 命令将制表符字符转换为空格。默认是八个空格，但你可以通过 -tabs=n（或 -t n）将其更改为 n 个空格。-tabs 开关也可以使用逗号分隔的制表位列表。

```bash
$ printf '\tA\tTEST\n' > test.txt
$ wc test.txt
        1       2       8 test.txt
$ expand test.txt | wc
        1       2      21
```

-initial（或 -i）开关仅转换一行之前的制表符。

```bash
$ expand -initial test.txt | wc
        1       2      15
```

对应的 unexpand 命令将多个空格转换回制表符。默认是八个空格对应一个制表符，但你可以使用 -tabs=n 开关更改此设置。默认情况下，仅转换初始制表符。使用 -all（或 -a）开关将考虑一行的所有空格。

在处理文件之前，使用 expand 移除文件中的制表符。

# 临时文件

临时文件，即仅在脚本执行期间存在的文件，传统上使用 $$ 函数命名。该函数返回当前脚本的进程 ID 号。通过在临时文件的名称中包含此数字，使每次运行脚本时文件名都是唯一的。

```bash
$ TMP="/tmp/reports.$$"
$ printf '%s\n' "$TMP"
/tmp/reports.20629
$ touch "$TMP"
```

这种传统方法的缺点在于临时文件的名称是可以预测的。恶意程序在你的脚本运行时可以看到其进程 ID，并利用这些信息识别你的脚本正在使用哪些临时文件。临时文件可能被删除或数据被替换，以改变你的脚本的行为。

为了获得更好的安全性，或创建多个具有唯一名称的文件，Linux 提供了 mktemp 命令。该命令创建一个临时文件，并将名称打印到标准输出，以便可以存储在变量中。每次 mktemp 创建新文件时，文件都会被赋予唯一的名称。名称由程序提供的文件名模板生成，该模板以字母 X 结尾，重复六次。mktemp 用唯一的随机代码替换这六个字母以创建新的文件名。

```bash
$ TMP=`mktemp /tmp/reports.XXXXXX`
$ printf "%s\n" "$TMP"
/tmp/reports.3LnWVw
$ ls -1 "$TMP"
-rw---- 1 kburcch kburcch    0 Aug  1 14:34 reports.3LnWVw
```

在这种情况下，字母 XXXXXX 被代码 3LnWVw 替换。

`mktemp` 使用 `-d (directories)` 开关创建临时目录。你可以使用 `-q (quiet)` 开关抑制错误消息。

# 锁定文件

当许多脚本共享相同的文件时，需要一种方法让一个脚本向另一个脚本表明它已完成其工作。这种情况通常发生在由两个不同开发团队监督的脚本需要共享文件时，或者共享文件在同一时间只能被一个脚本使用时。

同步脚本的一种简单方法是使用锁定文件。*锁定文件* 类似于标志变量：文件的存在表示某种条件，在这种情况下，表示该文件正被其他程序使用，不应被修改。

大多数 Linux 发行版包含一个名为 `/var/lock` 的目录，这是放置锁定文件的标准位置。

假设发票文件在同一时间只能被一个脚本访问。可以创建一个名为 `invoices_lock` 的锁定文件，以确保只有一个脚本具有访问权限。

```bash
declare -r INVOICES_LOCKFILE="/var/lock/invoices_lock"
while test ! -f "$INVOICES_LOCKFILE" ; do
   printf "Waiting for invoices to be printed...\n"
   sleep 10
done
touch "$INVOICES_LOCKFILE"
```

此脚本片段每 10 秒检查一次 `invoices_lock` 是否存在。当文件消失时，循环完成，脚本创建一个新的锁定文件并继续进行工作。当工作完成后，脚本应移除锁定文件，以允许其他脚本继续进行。

如果一个脚本完成时未移除锁定文件，会导致下一个脚本无限循环。可以修改 `while` 循环以使用超时，这样如果一段时间后发票文件无法访问，脚本将停止并报错。

```bash
declare -r INVOICES_LOCKFILE="/var/lock/invoices_lock"
declare -ir INVOICES_TIMEOUT=1800    # 30 minutes
TIME=$(date +%s)
TIME_STARTED=$TIME
time_out=0
while test ! -f "$INVOICES_LOCKFILE" ; do
   printf "Waiting for the invoices to be printed...\n"
```

