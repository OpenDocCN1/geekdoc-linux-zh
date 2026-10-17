
`/usr/bin/test`: ELF 32-bit LSB executable, Intel 80386, version 1,

dynamically linked (used shared libs), stripped

对于脚本编程，`file` 的 `-b` (`brief`) 选项会忽略文件名，并仅返回文件的评估结果。

```
$ file -b orders.txt

ASCII text
```

其他有用的选项包括 `-f` (`file`)，用于从特定文件读取文件名。`-i` 选项返回适用于 Shell 编程的 MIME 类型描述。使用 `-z` (`compressed`) 选项，`file` 尝试确定存储在压缩文件中的文件类型。`-L` 选项跟踪符号链接。

```
$ file -b -i orders.txt

text/plain, ASCII
```

## 创建和删除文件

如第 3 章“文件、用户和 Shell 定制”所述，文件使用 `rm` (`remove`) 命令进行删除。`-f` (`force`) 命令即使在文件不存在时也能删除。粘性位（sticky bit）是一个例外，将在第 15 章“Shell 安全”中讨论。

当你处理文件时，在尝试删除它们之前总是检查文件是否存在。参见示例 11.2。

### 示例 11.2 `rm_demo.sh`

```
#!/bin/bash

# rm_demo.sh: 使用 rm 删除文件

shopt -s nounset
```

```
declare -rx SCRIPT=$0

declare -x FILE2REMOVE="orders.bak"

declare -x STATUS
```

```
if [ ! -f "$FILE2REMOVE" ]; then

  printf "%s\n" "$SCRIPT: \$FILE2REMOVE does not exist" >&2

  exit 1

else

  rm "$FILE2REMOVE"

  STATUS=$?
```
`if [ $STATUS -ne 0 ]; then
    printf "%s\n" "Error: unable to replace $FILE2REMOVE" >&2
    exit $STATUS
fi`
在删除多个文件时，避免使用 `-r` (`recursive`) 选项或文件名通配符。相反，使用文件列表（使用如 `find` 等命令），并在尝试删除任何文件之前对每个单独的文件进行测试。这比其他方法慢，但如果发生问题，没有任何文件会被删除，你可以安全地检查问题产生的原因。

新的空文件使用 `touch` 命令创建。该命令之所以被称为 touch，是因为当它用于现有文件时，会更改修改时间尽管对文件内容没有任何更改。

`touch` 经常与 `rm` 结合使用为脚本创建空文件。使用 `>>` 追加输出如果文件存在则不会报错，因此无需记住文件是否存在。

例如，如果有一个生成名为 `run_results.txt` 文件的脚本，可以通过示例 11.3 创建新文件。

### 示例 11.3 `touch_demo.sh`

```
#!/bin/bash
#
touch_demo.sh: 使用 touch 创建一个新的空文件

shopt -s -o nounset

declare -rx RUN_RESULTS="./run_results.txt"

if [ -f "$RUN_RESULTS" ]; then
    rm -f "$RUN_RESULTS"
    if [ $? -ne 0 ]; then
        printf "%s\n" "Error: unable to replace $RUN_RESULTS" >&2
    fi
    touch "$RUN_RESULTS"
fi
```

```
printf "Run stated %s\n" "$(date)" >> "$RUN_RESULTS"
```

`-f` 选项强制每次都创建新文件。

## 移动与复制文件

使用 `mv` (`移动`) 命令可以将文件重命名或移动到新目录。如果使用 `-f` (`强制`)，`move` 将覆盖现有文件而不是报告错误。仅在覆盖文件是安全的情况下才使用 `-f`。

你可以将 `touch` 与 `mv` 结合，以不同的名称备份旧文件。Linux 备份文件的习惯是在文件名末尾加上日期进行重命名。请参见列表 11.4。

### 列表 11.4 `backup_demo.sh`

```bash
#!/bin/bash
## backup_demo.sh
shopt -s
declare RUN_RESULTS="./results.txt"
if [ -f "$RUN_RESULTS" ]; then
  mv -f "$RUN_RESULTS"
  if [ $? -ne 0 ]; then
    printf "%s\n" "Error: unable to backup $RUN_RESULTS" >&2
  fi
  touch "$RUN_RESULTS"
fi
printf "Run %s\n" "$date"
```

因为在 Linux 中覆盖备份总是总是安全的，所以移动通常比删除文件更好。与 `mv` 类似的是 `cp` (`复制`)，`cp` 会创建文件的副本而不删除原始文件。`cp` 还可以使用链接开关创建链接而不是副本。

## 关于文件的更多信息

有两个命令可以显示关于文件的信息，这些信息无法通过 `test` 命令发现。`stat` 命令显示文件的通用信息，包括所有者、大小和最后访问时间。

```
$ stat ken.txt
File: 'ken.txt'
Size: 84      Blocks: 8      Regular File
Access: (064)-rw-r-- Uid: (100) Gid: (100)
Device: 0 Inode: 13 Links: 1
Access: Feb 20 16:34
Modify: Feb 20 16:34
Change: Feb 20 16:34
```

为了让脚本中的信息更具读性，使用 `-t` (`时间`) 开关。每个项目之间用空格分隔。

```
$ stat -t orders.txt
orders.txt 21704 48 503 114674 1 899439021490652
```

`stat` 命令具有与 `date` 类似的功能，但有更广泛的格式选项。`stat` 类似于 `date` 命令：它有一个字符串参数，用于描述状态信息的显示方式。该参数通过 `-f` (`格式`) 开关指定。最常用的 `stat` 代码如下：

- `%c`—标准格式
- `%d`—天（零补齐）
- `%D`—mm/dd/yy
- `%H`—小时（24小时制）
- `%I`—小时（12小时制）
- `%j`—天（1..366）
- `%m`—月份
- `%M`—分钟
- `%S`—秒
- `%U`—周数（星期日）
- `%w`—星期几（星期日）
- `%Y`—年份
- `%P`—百分比字符
- `%A`—使用文件的最后访问时间
- `%a`—文件名（无后缀）
- `%c`—使用文件的 inode 时间
- `%d`—设备 ID
- `%e`—自 epoch 以来的秒数
- `%f`—文件系统类型
- `%i`—inode 节点
- `%L`—使用当前（本地）时间
- `%n`—硬链接数
- `%M`—使用文件的最后修改时间
- `%m`—类型/属性/访问位
- `%n`—文件名
- `%r`—Rdev ID（字符/块设备）
- `%s`—文件大小（字节）
- `%U`—使用当前（UTC）时间
- `%u`—用户 ID (`uid`)
- `%z`—序列号 (1,2,...)

完整列表出现在本章末尾的参考部分。默认情况下，任何引用时间的格式代码将基于文件的修改时间。

```
$ stat -f "%c" orders.txt
Tue Feb 6 15:17:32 2001
```

可以通过时间代码选择其他类型的时间。格式参数从左到右读取，这意味着不同的时间代码可以组合在一个格式字符串中。例如，使用 `%c` 会将格式更改为 inode 时间（通常是文件创建的时间）。使用 `%L`（本地时间）或 `%U`（UTC）会让 `stat` 的行为变得像 `date` 命令。

```
$ stat -f "modified time = %c current time = %L%c" orders.txt
modified time = Tue Feb 6 15:17:32 2001 current time = Wed May 9 15:49:01 2001
```

```
$ date
Wed May 9 15:49:01 2001
```

`stat` 可以创建有意义的文件名。通常文件以 `orders.txt` 的名称发送，脚本会使用日期作为名称的一部分来对文件进行排序。

```bash
$ BYTES=$(stat -f "%Y%m%d" orders.txt)
mv orders.txt orders_$BYTES
```

## 验证文件

这意味着你不能在批文件中包含密码。解决此问题的办法是使用 `ssh-keygen` 命令使用 SSH 的公钥认证。如果你还没有这样做，请按照以下方式生成新密钥。

```bash
$ ssh-keygen -t rsa
```

一对认证密钥存储在主目录下的 `.ssh` 中。你必须将公钥（以 `.pub` 结尾的文件）复制到远程机器，并将其添加到名为 `/.ssh/authorized_keys` 的文本文件中。每个访问远程登录的本地登录都需要 `authorized_keys` 中的一个公钥。如果存在密钥对，SFTP 将自动使用密钥而不是登录密码。

与 FTP 一样，SFTP 需要一个命令列表来执行。SFTP 包含一个 `-b`（批）开关，用于指定包含要执行命令的批文件。为了在脚本中使用方便的文件，可以使用名为 `/dev/stdin` 的批文件。

SFTP 理解的命令与 FTP 类似。出于脚本编写的目的，基本的传输命令是相同的。传输始终是“二进制”的。有一个 `-v`（详细）开关，但它会产生大量信息。当使用 `-b` 开关时，SFTP 会显示执行的命令，因此不需要 `-v` 开关来记录传输过程中发生的情况。

```bash
sftp -b /dev/stdin root@our_web_site.com <<!
cd /httpd
get http.conf
!
STATUS=$?
if [ $STATUS -ne 0 ]; then
printf "%s\n" "Error: SFTP transfer failed" >&2
exit $STATUS
fi
```

> `-c`（压缩）选项尝试压缩数据以加快传输。

有关 ssh、sftp 及其相关程序的更多信息，请访问：

http://www.openssh.org/

## 验证文件

通过 FTP 或 wget 发送的文件可以通过计算校验和来进一步检查。Linux 的 `cksum` 命令计算文件的字节数并打印循环冗余检查（CRC）校验和，这可以用于验证文件是否完整且无损。该命令使用符合 POSIX 标准的算法。

```bash
$ cksum orders.txt
491404265 21799 orders.txt
```

Linux 的 `sum` 命令可以提供与旧 Unix 系统的兼容性，但请注意 `cksum` 与 `sum` 不兼容。

## 第 11 章文本文件基础

为了获得更高的校验和安全性，某些发行版包含 `md5sum` 命令来创建 MD5 校验和。`-status` 开关静默地测试文件。`-binary`（或 `-b`）开关将文件视为二进制数据而非文本。`-warn` 开关会打印关于 MD5 格式的警告。`-check`（或 `-c`）检查文件的校验和。

```bash
$ md5sum orders.txt
945ecc13070da243e22730a44740004 orders.txt
$ md5sum orders.txt > ordersum.txt
$ md5sum -check ordersum.txt
file1.txt: OK
```

Linux 的 `cmp` 命令可以确定两个文件之间的差异。

```bash
$ cmp orders.txt orders2.txt
orders.txt orders2.txt differ: char 179, line 6
```

如果两个文件不同，`diff` 什么都不输出。

## 分割大文件

可以使用 Linux 的 `split` 命令将极大的文件分割为较小文件。文件可以按字节按行分割。`-bytes=s`（或 `-b`）开关创建小于 `s` 字节的文件。`-lines=s`（或 `-l s`）开关创建小于 `s` 行的文件。`-line-bytes=s`（或 `-c`）开关将每行切割为小于 `s` 字节。大小是一个数字，可选 `b`（512 字节块）、`k`（千字节）或 `m`（兆字节）。最后一个参数是用于文件名的名前缀。

```bash
$ split -bytes=10k huge_file.txt small_file
$ ls -1 -small-file*
-rw-rw-r- 1 kburch kburtch 10240 Aug 28 16:19 small_filea
-rw-rw-r- 1 kburch kburtch 10240 Aug 28 16:19 small_fileab
-rw-rw-r- 1 kburch kburtch 1319 Aug 28 16:19 small_fileac
```

你使用 Linux 的 `cat` 命令重组文件。该命令合并文件并将其写入标准输出。请注意按正确的顺序合并分割的文件。

```bash
$ cksum huge_file.txt
491404265 21799 huge_file.txt
$ cat small_file small_fileab small_fileac > new_file
$ cksum new_file
491404265 21799 new_file
```

如果发生分割的区域（locale）与重组文件的区域相同，则使用通配符匹配（globbing）来处理 cat 文件名是安全的。

Linux 的 `csplit`（上下文分割）命令在特定模式出现的地方分割文件。

基本的 `csplit` 模式是斜杠中的正则表达式，后跟一个可选的偏移量。正则表达式表示将成为下一个文件第一行的。偏移量是从匹配行向前或向后移动的行数。

$ TMP='mktemp /tmp/reports.XXXXXX'

$ printf "%s\n" "$TMP"

/tmp/reports.3LnWvW

$ ls -l "$TMP"

-rw------- 1 kbturch kbturch 0 Aug 14:34 reports.3LnWvW

在这种情况下，字母 XXXXX 被代码 3LnWvW 替换。

`mktemp` 使用 `-d`（目录）切换开关创建临时目录。你可以使用 `-q`（静默）切换开关来抑制错误信息。

## 锁文件 (Lock Files)

当许多脚本共享同一个文件时，需要一种方法让一个脚本告知另一个脚本它已经完成了工作。这通常发生在由两个不同开发团队监督的脚本需要共享文件时，或者当一个文件一次只能由一个脚本使用时。同步脚本的一种简单方法是使用锁文件。锁文件就像一个标志变量：文件的存在表示某种情况，即文件正在被另一个程序使用，不应被修改。大多数 Linux 发行版包含一个名为 `/var/lock` 的目录，用于放置锁文件。假设一个文件一次只能由一个脚本访问，可以创建一个名为 `invoices_lock` 的锁文件来确保只有一个脚本有权限。

```bash
declare -r INVOICES_LOCKFILE=/var/lock/invoices_lock
while test ! -f "$INVOICES_LOCKFILE"; do
  printf "等待打印发票..."
  sleep 10
done
touch "$INICES_FILE"
```每 10 秒检查一次 `invoices_lock` 是否存在。当文件消失时，脚本创建一个新的锁文件并继续工作。当工作完成后，脚本应该删除锁文件以允许其他脚本继续。如果锁文件在结束时没有被删除，会导致下一个脚本无限循环。while 循环可以修改为使用超时，这样脚本在一段时间后如果无法访问文件将会停止。

```bash
declare -r INVOICES_LOCKFILE=/var/lock/invoices_1800
declare -i INVOICES_TIMEOUT=1800 # 30 分
declare -i TIME=0
TIME_STARTED=$(date +%s)
while test ! -f "$INVOICES_LOCKFILE"; do
  printf "等待打印发票..."
  sleep 10
  TIME=$(date +%s)
  TIME=$TIME-TIME_STARTED
  if [ $TIME -gt $INVOICES_TIMEOUT ]; then
    printf "等待打印发票超时"
    exit 1
  fi
done
```
``date` 命令的 `%s` 代码返回当前的秒数。将两个 `date` 执行的结果相减，结果是自执行第一个 `date` 命令以来的秒数。在这种情况下，超时时间为 1800 秒，或 30 分钟。

当少量脚本共享同一个文件时，锁是非常方便的。当有太多脚本在等待一个锁文件时，会发生竞态条件：计算机花费大量时间检查锁文件是否存在，而不是执行有用的工作。幸运的是，还有其他共享信息的方法。两个脚本使用一种名为命名管道的特殊文件。这些管道（称为 FIFO 或队列）是可以由一个脚本读取而另一个脚本写入的文件。其效果类似于管道符 (`|`)，它将一个命令的输出作为另一个命令的输入。与 shell 管道不同，使用命名管道的脚本独立运行，仅共享它们管道。不需要锁。`mkfifo` 命令创建一个新的命名管道。
