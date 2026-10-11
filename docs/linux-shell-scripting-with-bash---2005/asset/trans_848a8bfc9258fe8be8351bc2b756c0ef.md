
在本例中，文件描述符 3 指向 *orders*.txt。第二行不起作用，因为描述符 3 已经打开。如果使用 *exec*，第二行会将描述符 3 重新打开为 *orders2*.txt。

为了节省文件描述符，*exec* 可以将一个描述符复制到另一个描述符。若要使输入文件描述符 4 指向与文件描述符 3 相同的文件，请执行以下操作：

```
exec 4<&3
```

现在，描述符 3 和 4 指向同一文件，可以互换使用。描述符 3 可以用来打开另一个文件，并通过从描述符 4 复制回来将其恢复为原始值。如果省略描述符 4，Bash 假设你想更改标准输入（描述符 0）。

你可以通过在文件描述符后添加减号来移动它。这会在描述符被复制后关闭原始文件。

```
exec 4<&3-
```

类似地，你可以使用 *>&* 复制输出文件描述符，并通过添加减号来移动它们。默认输出是标准输出（描述符 1）。

要打开文件以进行写入，请使用输出重定向符号 *(&)*。

```
exec 3>orders.txt
exec 4>&3
while read LINE <&3 ; do
    printf "${A}n\" "$LINE" >&4
done
```

*<&* 符号用于以读写模式打开文件。

```
exec 3<>orders.txt
```

读取或写入将从文件开头顺序进行。向文件写入会覆盖其内容。只要被覆盖的字符长度与原始字符相同，新字符就会替换旧字符。例如，如果文件中的下一行是 *dog*，写入 *cat* 覆盖 *dog* 会替换单词 *dog*。然而，如果文件中的下一行是 *horse*，写入 *cat* 会产生两行——*cat* 行和 *se* 行。*cat* 后面的换行符会覆盖字母 *r*。脚本现在将读取 *se* 这一行。

*<&* 在常规文件中的实用性有限，因为没有办法“回退”并重写刚刚读取的内容。你只能覆盖即将读取的内容。

列表 11.7 中的脚本读取整个文件，并在文件末尾添加“*Processed* on”消息。

### 列表 11.7 open_files2.sh

```bash
#!/bin/bash
#
# open_files2.sh

shopt -o -S nounset

declare LINE

exec 3>orders.txt
while read LINE <&3 ; do
    printf "%s\n" "$LINE"
done
printf "\n" "Processed on "'date' >&3
exit 0
```

`<>` 对于套接字编程特别有用，这在第 16 章“网络编程”中有讨论。

文件可以被打开，也可以被关闭。输入文件描述符可以用 `<&-` 关闭。请务必包含一个文件描述符，否则这将关闭标准输入。输出文件描述符可以用 `>&-` 关闭。如果没有指定描述符，这将关闭标准输出。

作为一种特殊的 Bash 约定，文件描述符可以通过路径名引用。形式为 `/dev/fd/n` 的路径指的是文件描述符 `n`。例如，标准输出是 `/dev/fd/1`。使用此语法，可以在运行 Linux 命令时引用已打开的文件描述符。

```bash
$ exec 4>results.out
$ printf "\n" "Send to fd 4 and standard out" | tee /dev/fd/4
Send to fd 4 and standard out
$ exec 4>&-
$ cat results.out
Send to fd 4 and standard out
```

## 使用 head 和 tail

Linux `head` 命令返回文件中的前几行。默认情况下，`head` 打印前 10 行。你可以使用 `-lines=n`（或 `-n n`）开关指定行数。

```bash
$ head -lines=5 orders.txt
Birchwood China Hutch, 475, 99, 1, 756
Bookcase Oak Veneer, 205, 99, 1, 756
Small Bookcase Oak Veneer,205.99,1,756
Reclining Chair,1599.99,1,757
Bunk Bed,705.99,1,757
```

你可以将 `-lines` 开关缩写为一个减号和行数。

```bash
$ head -3 orders.txt
Birchwood China Hutch,475.99,1,756
Bookcase Oak Veneer,205.99,1,756
Small Bookcase Oak Veneer,205.99,1,756
```

行数后可以使用 c 表示字符，l 表示行数，k 表示千字节，或 m 表示兆字节。`-bytes`（或 `-c`）开关打印你指定的字节数。

```bash
$ head -9c orders.txt
Birchwood
$ head -bytes=9 orders.txt
Birchwood
```

Linux `tail` 命令显示文件中的最后几行。与 `head` 类似，行数或字节数后可以使用 c 表示字符，l 表示行数，k 表示千字节，或 m 表示兆字节。

开关与 `head` 命令类似。`-bytes=n`（或 `-c`）开关打印你指定的字节数。`-lines=n`（或 `-n`）开关打印你指定的行数。

```bash
$ tail -3 orders.txt
Walnut TV Stand,388.99,1,756
Victorian-style Sofa,1225.99,1,757
Grandfather Clock,2045.99,1,756
```

结合使用管道中的 `tail` 和 `head`，你可以显示任何一行或行范围。

```bash
$ head -5 orders.txt | tail -1
Bunk Bed,705.99,1,757
```

如果起始行使用的是加号而不是减号，`tail` 会从文件开头计数该数量的行并打印剩余部分。这是 `tail` 的一个特性，而不是 `head` 命令的特性。

```bash
$ tail +17 orders.txt
Walnut TV Stand,388.99,1,756
Victorian-style Sofa,1225.99,1,757
Grandfather Clock,2045.99,1,756
```

在脚本中对任意文件使用 `head` 或 `tail` 时，请务必检查文件是否为常规文件，以避免令人不快的意外情况。

## 文件统计信息

Linux `wc`（单词计数）命令提供关于文件的统计信息。默认情况下，`wc` 显示文件的行数、单词数和字符数。要使 `wc` 在脚本中有用，必须使用开关来返回单个统计值。

`-bytes`（或 `-c` 或 `-C`）开关返回文件大小，其值与 `stat -fsize` 返回的文件大小相同。

```bash
$ wc -bytes invoices.txt
20411 invoices.txt
```

要在脚本中使用 `wc`，请将文件通过标准输入传入，以抑制文件名的显示。

```bash
$ wc -bytes < status_log.txt
57496
```

`-lines`（或 `-l`）开关返回文件中的行数。也就是说，它统计换行符的数量。

```bash
$ wc -lines < status_log.txt
1569
```

`-max-line-length`（或 `-L`）开关返回最长行的长度。`-words`（或 `-w`）开关统计文件中的单词数。

当变量值被打印到管道中时，可以将 `wc` 与变量一起使用。

```bash
$ declare -r TITLE='Annual Grain Yield Report'
$ printf "%s\n" "$TITLE" | wc -words
4
```

## 截取

Linux `cut` 命令从文件中所有行中删除子字符串。

`-fields`（或 `-f`）开关打印由特定字符标记的行的一部分。`-delimiter`（或 `-d`）开关选择该字符。如果要使用空格作为分隔符，必须用反斜杠转义或将其括在引号中。

```bash
$ declare -r TITLE='Annual Grain Yield Report'
$ printf "%s\n" "$TITLE" | cut -d ' ' -f2
Grain
```

在本例中，分隔符是空格，由空格标记的第二个字段是 `Grain`。在使用 `printf` 进行截取时，请务必确保打印了换行符；否则，`cut` 将返回空字符串。

多个字段用逗号表示，范围表示为用减号 (-) 分隔的两个数字。

```bash
$ printf "%s\n" "$TITLE" | cut -d ' ' -f 2,4
Grain Report
```

使用分隔符字符分隔多个字段。要在显示结果时使用不同的分隔符字符，请使用 `-output-delimiter` 开关。

`-characters`（或 `-c`）开关打印指定字符的位置。这与美元符号表达式子字符串类似，但可以指定任何字符或字符范围。`-bytes`（或 `-b`）开关作用相同，但旨在为多字节国际字符提供未来的支持。

```bash
$ printf "%s\n" "$TITLE" | cut -characters 1,3,6-8
Anl G
```

`-only-delimited`（或 `-s`）开关忽略不包含分隔符字符的行。这是跳过数据文件开头的标题或其他注释的一种简单方法。

用于多行时，`cut` 会截取每一行。

```bash
$ cut -d, -f1 < orders.txt | head -3
Birchwood China Hutch
Bookcase Oak Veneer
Small Bookcase Oak Veneer
```

列表 11.8 中的脚本将 `orders.txt` 中的数量字段相加。

### 列表 11.8 cut_demo.sh

```bash
#!/bin/bash
#
# cut_demo.sh: compute the total quantity from orders.txt

shopt -o -s nounset

declare -i QTY
declare -ix TOTAL_QTY=0

cut -d, -f3 orders.txt | {
  while read QTY ; do
    TOTAL_QTY=TOTAL_QTY+QTY
  done

  printf "The total quantity is %d\n" "$TOTAL_QTY"
}
exit 0
```

## 粘贴

Linux `paste` 命令将两个或多个文件中的行合并为一行。对于两个文件，`paste` 将第一个文件的第一行、一个制表符字符以及第二个文件的第一行写入标准输出，然后继续处理第二行

