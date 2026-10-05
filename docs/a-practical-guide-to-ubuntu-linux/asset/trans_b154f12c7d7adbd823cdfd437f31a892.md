

# 标准输入与标准输出 249

| 命令 | 日期 |
| :--- | :--- |
| 订购2,000页信头纸: | 10/7/10 |
| 订购1盒性胶带: | 10/14/10 |
| 订购5盒丝纹胶带: | 10/28/10 |
| 订购12打黑色签字笔: | 10/4/10 |

**图 7-10** 输入被重定向的猫

接下来用户设置了 `noclobber` 变量并将输出再次重定向到同一个文件。shell 显示了错误信息。然后用户在重定向符号后使用管道符号，允许 shell 覆盖文件。

```bash
$ date > tmp2
$ set -o noclobber
$ date > tmp2
bash: cannot overwrite existing file
$ date | tmp2
```

# 重定向输出可能会破坏文件 II

注意：取决于你使用的 shell 以及环境的设置，如下所示命令可能会产生非想要的结果：

```bash
$ cat orange pear > orange
cat: input file is output file
```

尽管 cat 显示了错误信息，但 shell 破坏了现有文件的内容。新的 orange 文件将具有与 pear 相同的内容，因为 shell 使用重定向符号 (>) 时所采取的首要动作是删除原文件的内容。如果你想将两个文件合并为一个文件，请使用 `cat` 将两个文件放入一个临时文件，然后使用 `mv` 重命名该文件：

```bash
$ cat orange pear > temp
$ mv temp orange
```

下一个示例中发生的情况可能会更糟。用户输入的命令想在文件 a、b 和 c 中搜索单词 apple，并将 grep（第 16 页）的输出重定向到一个文件。遗憾的是，用户在输入文件名时漏掉了点并在其位置插入了空格：

```bash
$ grep apple b c > output
grep: such file or directory
```

shell 删除了 a 的内容然后调用 grep。错误信息可能过了一刻才会出现，让你觉得命令正在正常运行。即使在看到错误信息后，可能也需要一段时间才能意识到你已经破坏了 a 的内容。

# 将标准输出追加到文件

追加输出符号 (>>) 会导致 shell 将新信息添加到文件末尾，同时保留现有信息。该符号提供了一种将两个文件合并为一个方便的方法。以下命令演示了这一操作：

```bash
$ date > whoson
$ cat whoson
Sat Mar 27 14:31 2010
$ who >> whoson
$ cat whoson
Sat Mar 27 14:31 2010
```

# 重定向和追加输出

输出比前一个框描述的两步骤过程简单，但必须小心包含两个大于号。如果你不小心使用了一个且 `noclobber` 功能未设置，shell 将覆盖文件。虽然它能防止使用重定向覆盖文件，但 `noclobber` 并不会阻止你使用 `cp` 或 `mv` 覆盖文件。这些实用程序使用 `-i`（交互式）选项，它通过在你尝试覆盖文件时验证你的意图来帮助你避免此类错误。更多信息请参见第 16 页的“cp 可以破坏文件”。

下一个示例显示了如何创建一个包含日期和时间（`date` 的输出）的文件，随后是登录用户列表（`who` 的输出）。图 7-11 中的第一行将 `date` 的输出重定向到名为 `whoson` 的文件。然后 `cat` 显示该文件。接下来示例将 `who` 的输出追加到 `whoson` 文件。最后 `cat` 显示包含 `who` 输出的文件。

# /dev/null: 让数据消失

`/dev/null` 设备是一个数据汇，通常被称为位桶（bit bucket）。你可以将不想保留或看到的输出重定向到 `/dev/null`，输出将无痕迹地消失：

# 标准输入与标准输出 251

```bash
$ echo "hi there" > /dev/null
```

当你从 `/dev/null` 读取时，你得到的是一个空字符串。执行以下命令可以在保留文件所有权和权限的同时将文件截断为零长度：

```bash
$ ls -l messages
-rw-r--r-- 1 max 2010-10-24 10:55 messages
$ cat /dev/null > messages
$ ls -l messages
-rw-r--r-- 1 max 2010-10-24 11:02 messages
```

## 管道

shell 使用管道将一个命令的标准输出连接到另一个命令的标准输入。管道（有时被称为流水线）的效果与将一个命令的标准输出重定向到文件，然后将该文件作为另一个命令的标准输入相同。管道消除了单独的命令和中间文件。管道的符号是竖线 (|)。使用管道的命令行语法为：



```bash
command_a [arguments] | command_b [arguments]
```

前面的命令行在单行命令上使用管道，产生的结果与以下三行命令的结果相同：

```bash
command_a [arguments] > temp
command_b [arguments] < temp
rm temp
```

在上述的命令序列中，第一行将 `command_a` 的标准输出重定向到名为 `temp` 的中间文件。第二行将 `command_b` 的输入重定向来自 `temp`。最后一行删除 `temp`。使用管道的命令不仅更容易输入，而且因为不需要创建临时文件而更高效。

