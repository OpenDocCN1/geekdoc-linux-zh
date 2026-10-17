
```
source-archive:
!:,"sources","*wanted",*\d\
:Tc,nn
/archive -f -i
usr/spool/news.archive/INDEX
```

文件通过创建链接来复制。如果失败，则创建一个新文件。如果使用了 `-n` 标志，文件将复制到目标位置，并且输入文件将被替换为指向新文件的符号链接。`-m` 标志会被忽略。

默认情况下，`archive` 将错误消息发送到 `/var/log/news/errlog`。使用 `-r` 标志可抑制此重定向。

如果输入耗尽，`archive` 以零状态退出。如果发生 I/O 错误，它会尝试将其输入缓冲，将其复制到文件中。如果没有输入文件名，则输入将被复制到 `/news/spool/news.archive`。如果没有输入文件名，则输入将被复制到 `/news/spool/news.archive`。如果没有输入文件名，则输入将被复制到 `/news/spool/news.archive`。如果没有输入文件名，则输入将被复制到 `/news/spool/news.archive`。如果没有输入文件名，则输入将被复制到 `/news/spool/news.archive`。如果没有输入文件名，则输入将被复制到 `/news/spool/news.archive`。如果没有输入文件名，则输入将被复制到 `/news/spool/news.archive`。如果没有输入文件名，则输入将被复制到 `/news/spool/news.archive`。

# 历史

由 John Doe (`john@example.com`) 编写。

# 另参

`newsfeeds(5)`

# archive

`archive`——the input is copied to `/news/spool/news.archive`. If there was no input filename, then the input is copied to `/news/spool/news.archive`. If there was no input filename, then the input is copied to `/news/spool/news.archive`.

# archive

`archive`——the input is copied to `/news/spool/news.archive`. If there was no input filename, then the input is copied to `/news/spool/news.archive`.

# archive

`archive`——the input is copied to `/news/spool/news.archive`. If there was no input filename, then the input is copied to `/news/spool/news.archive`.

`buffer` 输入被解释为一组行。每行包含数固定数量的初始字段，其后是若干数量不相同的文件名字段。每行中的所有字段都由空白符分隔。默认的初始字段数量为一；可以使用 `-f` 标记来指定不同的字段数量。示例请参见 `filechan(8)`。

在初始字段之后，每个剩余的字段都指定一个要写入的文件名。可以使用 `-s` 标记来指定一个格式字符串，将字段映射到文件名：这是一个 `sprintf(3)` 格式，应提供给一个 `-s` 参数。默认值为 `/tmp/output.going`；详情请参见 `filechan(8)` 中对该标记的描述。可以使用 `-d` 标记来指定程序在启动前切换的目录。如果使用了此标记，`-s` 标记的默认值可以改为简单的字符串。

一旦 `buffer` 打开了一个文件，它将一直保持打开状态。输入中指定的文件数绝不能超过描述符所能保持的数量。如果使用了 `-b` 标记，`buffer` 将分配一个缓冲区并使用 `setbuf(3)` 将其附加到文件。使用 `-u` 标记将返回无缓冲输出。

- 如果配合数字使用 `-n` 标记，则 `buffer` 在每写入 n 行到文件后将执行 `flush()`。如果配合数字 n 使用 `-c` 标记，则 `buffer` 在每写入 n 行到文件后将关闭并重新打开文件。
- 如果配合数字使用 `-l` 标记，则所有文件每 n 秒将刷新一次。同样地，可以使用 `-c` 标记指定所有文件每 n 秒关闭并重新打开一次。

默认情况下，程序将其标准错误设置为 `/var/log/news/error`。请使用 `-r` 标记。如果使用了 `-p` 标记，程序将把包含其进程 ID（in）的文本行写入指定的文件。

`buffer` 可以作为一个发送 `news(5)` 的解说器来被调用。因此，如果某行以感叹号开头，则它被视为注释。共有三条命令：

## flush

`flush` 命令关闭并重新打开打开的文件：`flush` 仅针对指定的站点（site）。这些类似于 `ctlnews(8)` 的 `flush` 命令，并且可以通过发送 `flush xxx` 命令来实现。应用程序可以在发布命令之前通过重命名文件来告知 `flush` 已完成；当原始文件名出现时，`buffer` 完成该命令。

`buffer` 在刷新或关闭每个输出文件时还会还会文件的访问权限从所有人的只读更改为所有者的读写。如果它重新打开同一个文件，它会将模式改回只读。

`drop` 命令与 `flush` 类似，区别在于不会重新打开任何文件。如果指定了参数，则指定的站点将被删除；否则，所有站点将被删除。（注意：输入流文件中的 site 指该站点。）当使用 `ctlnews "drop site"` 时，如果该站点是向此解说器提供数据的漏斗（funnel），它将自动执行 `buffer` 命令。要删除所有站点，请使用 `ctlnews send buffer-site drop` 命令。

使用 `-m` 标记指定的 map 文件将进行重新加载。

## drop

## readmap

# HISTORY

由 Rich Salz (`rsalz@uunet.net`) 为 InterNews 编写。

# SEE

`ctlnews(8)`, `filechan(8)`, `innd(8)`, `newsfeeds(5)`。

# cfdisk

`cfdisk`——基于 Curses 的 Linux 磁盘分区管理器。

## SYNOPSIS

```
cfdisk [ -av ] [ -c cylinders ] [-h heads ] [-s sectors-per-track ] [-P opt]
[ device ]
```

## DESCRIPTION

`/dev/hda` [default]

`/dev/hdb`

`/dev/sda`

`/dev/sdb`

`/dev/sdc`

`/dev/sdd`

`cfdisk` 首先尝试读取硬盘的几何结构。如果读取失败，将显示错误消息并退出。这只有在没有 BIOS 的适配器上对 SCSI 磁盘进行分区时才允许。为了解决这个问题，你可以在命令行上设置柱面（`cylinders`）、磁头（`heads`）和每磁道扇区数。`cfdisk` 然后尝试从硬盘读取分区表。如果它无法确定分区表，将显示错误并退出程序。这可能是由错误的几何信息引起的，并可以在命令行上覆盖。解决此问题的另一种方法是使用 `-x` 选项。使用此选项，你可以忽略磁盘上的分区表。

主界面由四个部分组成，从上到部分别是：头部、命令行和警告行。头部包含版本号，随后是驱动器名称及其几何结构。分区部分显示分区表。命令和文本已启用。可用命令通常分块显示。警告行通常为空，除非有重要的信息需要显示。当前分区用反色视频高亮（如果给了 `-a` 选项，则用箭头表示）。特定分区的命令适用于当前分区。
