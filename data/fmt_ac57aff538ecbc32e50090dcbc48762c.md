
## 传输文件

通常，除非指定了新文件名，否则文件名保持不变。要指定新文件名，我们使用图 7.13 所示的第二个命令参数。如果文件已存在，它将被覆盖。

有两个传输文件的命令：`get` 和 `put`。`get` 将文件从远程系统复制到本地系统，而 `put` 将文件写入远程系统。这些命令如图 7.13 所示。

![](img/6e4cdc423ec40606ea72b32fdafff220_302_0.png)

图 7.13 `get` 和 `put`

当我们 ftp 文件时，必须位于正确的目录（`cd`）。例如，我们可以更改目录、创建目录和删除目录。我们还可以列出远程目录。这些命令与 UNIX 中的对应命令相同。ftp 命令的完整列表见表 7.7。

表 7.7 ftp 命令完整列表

| | | | |
| :--- | :--- | :--- | :--- |
| `account` | `debug` | `pwd` | `size` |
| `$` | `dir` | `mget` | `quit` |
| `append` | `disconnect` | `mkdir` | `status` |
| `ascii` | `form` | `mode` | |
| `bell` | `get` | `newer` | `restart` | `system` |
| `binary` | `hash` | | |
| `bye` | | | |

表 7.7 ftp 命令完整列表（续）

| | | | | |
| :--- | :--- | :--- | :--- | :--- |
| `case` | `help` | `nlist` | `rhelp` | `umask` |
| `cd` | `idle` | `nmap` | `rmdir` | `user` |
| `cdup` | `image` | `nrans` | `status` | `verbose` |
| `chmod` | `lcd` | `open` | `runique` | `win` |
| `close` | `ls` | `prompt` | `send` | |

要显示 ftp 命令，使用 `help` (?)。要查看命令的简要解释，使用帮助命令加上命令名。ftp 帮助命令在会话 7.12 中演示。它显示命令的前两行以及显示的下一行。它还显示两个单独命令的结果。

会话 7.12 ftp 帮助系统

```
ftp ?

命令可以缩写。命令有：

  debug mdir put size

  $ dir mget pwd status

***

delete mdelete sendport site

ftp ? ls

ls list contents of remote directory

ftp ? rmdir

rmdir remove directory on the remote machine
```
