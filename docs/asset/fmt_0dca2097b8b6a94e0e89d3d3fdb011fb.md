
## 二进制模式与 ASCII 传输模式

vsftpd FTP 服务器可以——但并不总是——提供两种模式来传输文件镜像。二进制模式传输文件的任何精确的、逐字节的镜像，且永远不会更改行符。使用二进制模式传输所有二进制文件。除非您需要转换行符，否则请使用二进制模式将 ASCII 文件作为文件传输。

ASCII 文件（如文本或源代码）在 Linux 下使用 `vi` 等文本编辑器创建时，使用单个 NEWLINE 字符（CONTROL-J，写为 `\n`）来标记每行的结束。其他操作系统则以不同的方式标记行结束。Windows 使用 RETURN（CONTROL-M，写为 `\r`）后跟一个 NEWLINE（两个字符）来标记每行的结束。Macintosh 使用单独的 RETURN。这些描述不适用于由 Word 或 OpenOffice 等字处理程序创建的文件，因为这些程序生成的是二进制文件。由于 `vsftpd` 服务器可以在您上传文件时将 Linux 行符映射到 Windows 行符，并在下载文件时将 Windows 行符映射到 Linux 行符。

若要在允许该操作的 FTP 服务器上使用 ASCII 模式，请在登录后输入 `ascii` 命令（第 738 页）并将 `cr` 设置为 ON（默认：第 738 页）。如果服务器不允许您在传输文件时更改行符，请在以二进制模式传输文件之前或使用 `unixdos`（第 159 页）或 `dosunix`（第 159 页）工具。

安全性：当针对非常大的文件运行时，显示文件大小的 `ftp size` 命令会消耗大量的服务器资源，并可能用于发起拒绝攻击（第 1034 页）。为了增强安全性，`vsftpd` 默认以二进制模式传输每个文件，即使它看起来是在使用 ASCII 模式。在服务器端，您可以通过设置 `ascii_upload_enable` 和 `ascii_download_enable` 参数（第 747 页）为 YES 来启用 ASCII 模式传输。如果服务器允许 ASCII 传输，客户端可以通过 `ascii`、`binary` 和 `cr` 命令（第 738 页）来控制是否进行行符映射。

## ftp 细节

本节介绍了使用 `ftp` 的细节。

## 格式

`ftp` 命令行具有以下格式：

```
ftp [options] [ftp-server]
```

其中 `options` 是下一节列表中出的一个或多个选项，`ftp-server` 是您想要交换文件的 FTP 服务器名称或网络地址。如果您没有指定 `ftp-server`，则需要在 `ftp` 运行后使用 `ftp open` 命令连接服务器。

## 命令行选项

- `-g` (globbing) 关闭通配符匹配。参见 `glob`（第 738 页）。
- `-i` (interactive) 在使用 `mget`（第 737 页）和 `mput`（第 738 页）传输文件期间关闭提示。另见 `prompt`（第 739 页）。
- `-n` (no automatic login) 禁用自动登录（第 735 页）。
- `-v` (verbose) 告诉您更多关于 `ftp` 如何工作的信息。显示来自远程计算机的响应，并且 `ftp` 会报告文件传输速度快的信息。另见（第 740 页）。

## ftp 命令

`ftp` 工具是交互式的：在启动 `ftp` 后，它会提示您输入命令来设置参数或传输文件。只要缩写是唯一的，您就可以缩写命令。在 `ftp` 提示符输入问号 (`?`) 可以显示命令列表。在问号后跟一个空格和一个命令，可以显示该命令功能的简要描述：

```
ftp > mget
get multiple files
```

## SHELL 命令

- `![command]` 如果不带命令，将转到（产生）本地系统上的 shell。在完成本地 shell 使用后，使用 Control-O 返回 `ftp`。在感叹号后跟命令，则仅在命令执行时执行；`ftp` 将显示一个 `ftp` 提示符，显示此命令是完成该命令的子命令。由于 `ftp` 产生的 shell 不会在返回 `ftp` 时保留您在该 shell 中所做的任何更改。具体来说，当您想将文件复制到启动 `ftp` 之外的其他本地目录时，需要使用 `ftp lcd` 命令更改本地工作目录：在派生的 shell 中执行命令不会产生您期望的更改。参见第 734 页的“Local cd (lcd)”示例。

## 传输文件

在以下描述中，`remote-file` 和 `local-file` 可以是路径。

- `append local-file [remote-file]`

将 `local-file` 追加到远程系统上的同名文件或指定的 `remote-file` 中。

- `get remote-file [local-file]`

将 `remote-file` 复制到本地系统并命名为 `local-file`。如果没有指定 `local-file`，`ftp` 将使用 `remote-file` 作为本地系统上的文件名。

- `mget remote-file-list`

（multiple get）将多个文件复制到本地系统，每个文件保持其原始文件名。您可以直接命名文件，或使用通配符（如 `glob`）。使用 `prompt`（第 739 页）在传输期间关闭提示。

- `mput local-file-list`

（multiple put）将多个文件复制到服务器，每个文件保持其原始文件名。您可以直接命名本地文件或使用通配符（参见 `glob`）。`prompt`（第 739 页）在传输期间关闭提示。

- `newer remote-file [local-file]`

如果 `remote-file` 的修改时间晚于 `local-file` 或 `local-file` 不存在，则复制 `remote-file`。

- `put local-file [remote-file]`

将 `local-file` 复制到服务器并命名为 `remote-file`。如果没有 `remote-file`，`ftp` 将使用 `local-file` 作为服务器上的文件名。

- `reget remote-file [local-file]`
