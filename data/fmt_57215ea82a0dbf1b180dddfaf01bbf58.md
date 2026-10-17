
在这个示例中，`diff` 发出指令 `2a3`，表示你必须在 `file m` 的第 2 行之后追加一行，使其与 `file p` 相同。`diff` 显示的第二行表示该行来自 `file p`（该行以 `>` 开头，表示 `file2`）。在这个示例中，你需要这一行的信息；追加的行必须包含文本 `rrrrr`。

下一个示例再次使用 `m`，这次使用文件 `r`，展示 `diff` 如何指示需要更改的行：

```
$ cat r

aaaaa

-q

ccccc

$ diff m r

2c2

---

< bbbbb

> -q
```

两个文件之间的差异在第 2 行：`File m` 包含 `bbbbb`，`file r` 包含 `-q`。`diff` 先显示 `2c2`，表示你需要更改第 2 行。在指示需要更改后，`diff` 显示你必须将 `file m` 中的第 2 行（`bbbb`）更改为 `file r` 中的第 2 行（`-q`），使文件相同。三个字符表示 `file1` 中文本的结束。

`--side-by-side` 选项和 `diff` 实用工具将输出宽度设置为 30 列（字符）时显示相同的输出。在输出中，小于符号指向 `m` 中多出的行，而 `diff/sdiff` 在 `n` 中留出一个空行，该额外行本所在的位置将使文件相同。

```
$ diff --side-by-side --width=30 m n

aaaaa aaaaa

bbbbb <

ccccc ccccc

$ diff -w 30 m n

aaaaa aaaaa

bbbbb <

ccccc ccccc
```

下一个示例再次使用 `m` 文件和新文件 `p`，展示 `diff` 发出一个追加（append）指令：

```
$ cat p

aaaaa

bbbbb

rrrrrrr

ccccc

$ diff m p

2a3

> rrrrr
```

在这个示例中，`diff` 发出指令 `2a3`，表示你必须在 `file m` 的第 2 行之后追加一行，使其与 `file p` 相同。`diff` 显示的第二行表示该行来自 `file p`（该行以 `>` 开头，表示 `file2`）。在这个示例中，你需要这一行的信息；追加的行必须包含文本 `rrrrr`。

下一个示例再次使用 `m`，这次使用文件 `r`，展示 `diff` 如何指示需要更改的行：

```
$ cat r

aaaaa

-q

ccccc

$ diff m r

2c2

---

< bbbbb

> -q
```

两个文件之间的差异在第 2 行：`File m` 包含 `bbbbb`，`file r` 包含 `-q`。`diff` 先显示 `2c2`，表示你需要更改第 2 行。在指示需要更改后，`diff` 显示你必须将 `file m` 中的第 2 行（`bbbb`）更改为 `file r` 中的第 2 行（`-q`），使文件相同。三个字符表示 `file1` 中文本的结束。

# du

显示磁盘使用信息

`du [options] | [path-list]`

`du`（磁盘使用）实用工具报告目录（及其所有子目录和文件）或文件占用的磁盘空间。默认情况下，`du` 显示占用的 1024 字节块数。

# 参数

如果不带参数，`du` 显示工作目录及其子目录和文件的信息。`path-list` 指定你想获取信息的目录和文件。

## 选项

- 不使用任何选项时，`du` 显示 `path-list` 中每个参数的总存储空间。对于目录，`du` 在递归列出每个子目录的总计后显示此。
- `--all` `-a` 与目录目录的同时显示所有普通文件的空间。
- `--total` `-c` 显示总计。
- `--human-readable` `-h` 以 K（千字节）、M（兆字节）和 G（吉字节）块显示大小。
- `--kilobytes` `-k` 以 1 千字节块显示大小。
- `--megabytes` `-m` 以 1 兆字节块显示大小。
- `--one-file-system` `-x` 仅报告与正在处理的参数相同文件系统的文件和目录。
- `--summarize` `-s` 仅显示命令行指定的每个目录或文件的总计；不显示总计。

# 示例

以下 `du` 显示关于工作目录子目录的大小信息。最后一行包含工作目录及其子目录的总计。

```
$ du

26 /Postscript

4 /RCS

47 /XIcon

4 /Printer/RCS

12 /Printer

105
```

总数（105）是工作目录下所有普通文件和目录占据的块数。尽管 `du` 仅显示目录的大小，但所有文件都会被计数。

接下来，使用 `--summarize` 选项，`du` 仅显示 `/home` 下每个目录的总计：

```
$ du --summarize /home/*

68 /home/Desktop

1188 /home/dou

100108 /home/dump

62160 /home/ftp

6540 /home/httpd

16 /home/lost+found

1862104 /home/alex

176 /home/max

88 /home/jenny

4 /home/tom
```

在之前的示例基础上添加 `--total` 选项，你可以得到相同的列表，并在最后获得总计：

```
$ du --summarize --total /home/*

68 /home/Desktop

...

4 /home/tom

2032456 total
```

如果 `du` 遇到一个你没有读取权限的文件或目录，它会向标准错误发送警告并跳过该文件。示例使用了 `s`（摘要）、`h`（人类可读）和 `c`（总计）选项：

```
$ du -shc /usr/*

112M /usr/x11R6

163M /usr/bin

4.0K /usr/dict

4.0K /usr/doc

4.0K /usr/etc

3.9M /usr/games
```

```
du: cannot change to directory '/usr/lost+found': Permission denied

30M /usr/sbin

du: cannot change to directory '/usr/share/shell/CA': Permission denied

797M /usr/share

188M /usr/src

2.2G total
```

最后一个示例以人类可读的格式显示了用户在 `/usr` 文件系统中可以读取的所有文件的总大小。通过将标准错误重定向到 `/dev/null` 可以丢弃所有关于不可读文件和目录的警告。

```
$ du --human-readable --summarize /usr 2>/dev/null

2.2G /usr
```
