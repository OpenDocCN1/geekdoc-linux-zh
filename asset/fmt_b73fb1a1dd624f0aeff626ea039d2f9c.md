
# 解压

注意：大多数人使用 `"tar"` 和 `"untar"` 就像它们都是有效命令一样，但实际上 `"untar"` 只是使用了 `"x"`（提取）选项的 `tar`。这种困惑可能是因为 `compress` 和 `uncompress` 都是有效命令。

## 磁带

如果你需要在磁带上使用，`untar` 命令可能像这样：
```
tar -xvpf /dev/tape/home/larry_important_stuff.tar
```

## 错误消息

`“tar: blocksize error”` 意味着你的 `tar` 文件无效。如果你的 `tar` 文件包含字节很少（例如 2000 字节），那么你在 `ftp` 会话期间保存 `“tar 文件”` 时损坏了它（`ls` 问题在所有服务器上都不会发生）。

## 选项

某些系统提供以下选项：
- `-k` 保留现有文件；在解压时不覆盖它们
- `-X` 在创建 `tar` 时排除 `ABC`（换句话说，不要将目录 `ABC` 中的任何文件放入 `tar` 文件）
- `-z` 自动压缩或解压数据：
    - 创建 `tar` 文件时：`tar -cz myfile.tar`
    - 解压时：`tar -xz myfile.tar`
- `-z` 自动压缩（使用 `gzip`）或解压（`gunzip`）数据：
    - 创建 `tar` 文件时：`tar -czf myfile.tar.gz`
    - 解压时：`tar -xzf myfile.tar.gz`

## 关于 TAR 文件的一些话

注意：下面的方法是强烈建议的：如果你的 `UNIX Linux` 系统允许使用 `tar` 的 `-z` 选项，请使用它！
```
$ tar -czf myfile.tar.gz *.txt
```
此 `tar` 命令 `-c` 创建一个名为 `myfile.tar.gz` 的压缩 `tar` 文件，包含当前目录下所有以 `".txt"` 结尾的文件 `-p` 保留当前权限和日期。

```
$ tar -xzpf myfile.tar.gz
```
此 `tar` 命令 `-x` 提取名为 `myfile.tar.gz` 的 文件中的所有文件。`-z` 选项会自动解压/恢复文件到你的当前目录。`-p` 选项保留文件权限和日期。

```
# myfile.tar.gz
$ tar -tzf myfile.tar.gz
```
此命令 `-t` 列出名为 `myfile.tar.gz` 的 `tar` 文件中所有文件名。`-z` 选项会自动解压/恢复文件名，以便它们正确显示在你的屏幕上。如果你不确定 `tar` 文件是否经过压缩或如何压缩的，使用 `file` 命令获取更多信息。例如：`file myfile.tar.gz` `gzip` 压缩数据。`file` 命令的输出告诉该文件是一个 `tar` 文件，它是压缩过的（尽管没有 `.gz` 后缀），并且使用了 `gzip` 进行压缩。

## 更多备注

输出：`tar and untar.ksh`。
脚本执行方式：`./tar_and_untar.ksh`
目的：展示如何 `tar` 和 `untar`。

方法 A：完成创建放入 `tar` 文件的脚本列表：要 `tar` 的脚本总数为 9。`tar` 将在 3 秒后开始。现在压缩刚刚创建的 `tar` 文件：你的 `tar` 文件是 `/tmp/scripts.tar`。`tar` 完成。

现在让我们反转该过程（解压 `tar` 文件）：我们将从 `/home/larry/ROSETTA/` 拷贝的文件放置到 `/home/larryDir`。这是我们 `tar` 文件内部存储的文件：

| 权限 | 用户 | 组 | 大小 | 日期 |
| :--- | :--- | :--- | :--- | :--- |
| -rwxr-xr-x | 1 | larry | 80 | 2007-04-11 | tail.ksh |
| -rwxr-xr-x | 1 | larry | 23473 | 2007-04-11 | ROSETTA.ksh |
| -rwxr-xr-x | 1 | larry | 155 | 2007-04-11 | test_file.ksh |
| -rwxr-xr-x | 1 | larry | 1382 | 2007-04-11 | do_nothing.ksh |
| -rwxr-xr-x | 1 | larry | 1193 | 2007-04-11 | touch.ksh |
| -rwxr-xr-x | 1 | larry | 6038 | 2007-04-11 | tr.ksh |
| -rwxr-xr-x | 1 | larry | 1790 | 2007-04-11 | truncate.ksh |
| -rwxr-xr-x | 1 | larry | 2678 | 2007-04-11 | typeset.ksh |

我们现在正在从 `tar` 文件中提取（解压）文件：
tail.ksh
ROSETTA.untar.ksh
test_file.ksh
do_nothing.ksh
touch.ksh
tr.ksh
truncate.ksh
typeset.ksh

这是我们刚刚放入 `/tmp/LarryDir` 的文件列表：总共 6 个文件

| 权限 | 用户 | 组 | 大小 | 日期 |
| :--- | :--- | :--- | :--- | :--- |
| -rwxr-xr-x | 1 | larry | 80 | 2007-04-11 | tail.ksh |
| -rwxr-xr-x | 1 | larry | 23473 | 2007-04-11 | ROSETTA.ksh |
| -rwxr-xr-x | 1 | larry | 155 | 2007-04-11 | test_file.ksh |
| -rwxr-xr-x | 1 | larry | 1382 | 2007-04-11 | do_nothing.ksh |
| -rwxr-xr-x | 1 | larry | 1193 | 2007-04-11 | touch.ksh |
| -rwxr-xr-x | 1 | larry | 6038 | 2007-04-11 | tr.ksh |
| -rwxr-xr-x | 1 | larry | 1790 | 2007-04-11 | truncate.ksh |
| -rwxr-xr-x | 1 | larry | 2678 | 2007-04-11 | typeset.ksh |

当 `perl -c` 发现没有更多主要错误时，它会发出命令 `"syntax OK."`
（`"OK"` 并不意味着“完美”。）

```
perl -w ./myscript.pl
```
`-w` 输出关于只使用一次的标识符警告。
就个人而言，我总会在 Perl 脚本内部使用 `use warnings;` 和 `use strict;`，因此我从不在命令行上使用 `-w` 选项。

```
perl -d ./myscript.pl
```
`-d` 是调试选项。
你将收到提示 `"DBdb;"`；你可以回复
（任意 `RETURN`）来逐行执行脚本。
我建议你在考虑使用 `-d`/调试选项之前，先尝试此页面上列出的任何调试技巧。

- 1. `BASH`：在执行脚本之前使用 `"bash -n"` 检查语法：
```
bash -n ./myscript.bash
```
- `"n"` **不会**执行脚本；只检查语法错误。
所执行的错误检查是非常少少的！

- 3. 对于 `bash` 和 `ksh` 的调试，当你在执行脚本时，日志有时**非常有帮助**：
```
/bin/bash -x myscript.bash
```
或者
```
/bin/bash -x myscript.bash
```
使用 `-x`（在屏幕上）会按照你执行的方式精确显示每一行代码，以及所有变量展开后的行。
此外，`-x` 允许你看到 `if-then-else` 语句执行了哪部分。

从脚本中获得的输出可能让你有些无从措，但有一种简单的方法可以只关注几行代码。
当你怀疑问题所在的一行可以使用 `"set -x"`，然后在该点下方的一行使用 `"set +x"` 显示追踪；当你使用这种技术时，像往常一样提交你的作业。
例如：`./myscript.pl` 或 `myscript.bash`

## 3A. PERL

有时要弄清楚你在哪里漏掉了引号（`'` 或 `"`）或大括号（`{` 或 `}`）是一项挑战。在这种情况下，我会在脚本中选择大约位于程序 25% 位置的点，将其放在一个 `END` 语句中。它看起来如下：

```
END
```

两个下划线然后 `END` 又是两个下划线。
