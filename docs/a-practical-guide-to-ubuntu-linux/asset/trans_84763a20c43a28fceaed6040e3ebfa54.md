

# 运行 ftp 和 sftp FTP 客户端 695

Windows 使用 RETURN（CONTROL-M，写为 \r）后跟一个 NEWLINE（两个字符）作为每行的结束标记。Macintosh 使用单独的 RETURN。这些描述不适用于由 Word 或 OpenOffice 等文字处理器创建的文件，因为这些程序生成的是二进制文件。vsftpd 服务器可以在你上传文件时将 Linux 行结束符映射到 Windows 行结束符，并在下载时将 Windows 行结束符映射到 Linux 行结束符。

要在允许 ASCII 模式的 FTP 服务器上使用该模式，请在登录后使用 ascii 命令（第 697 页）并将 cr 设置为 ON（默认值；第 697 页）。如果服务器不允许在传输文件时更改换行符，你可以在二进制模式传输文件之前或之后使用 todos（第 173 页）或 fromdos（第 173 页）工具。

在针对非常大文件运行时，用于显示文件大小的 `ftp size` 命令会消耗大量资源，并可被用于发起 DoS 攻击（第 1146 页）。为了增强安全性，vsftpd 默认以二进制模式传输每个文件，即使它似乎在使用 ASCII 模式。在服务器上，通过将 `ascii_upload_enable` 和 `ascii_download_enable` 参数（第 706 页）设置为 YES，你可以启用真实的 ASCII 模式传输。当服务器设置为 ASCII 传输时，客户端通过 `ascii`、`binary` 和 `cr` 命令（第 697 页）来控制是否映射行结束符。

## ftp 详细说明

本节介绍了使用 ftp 的细节。

## 格式

ftp 命令行的格式如下：

```
ftp [options] [ftp-server]
```

其中 `options` 是来自下一节列表中一个或多个选项，`ftp-server` 是你想要交换文件的 FTP 服务器的名称或网络地址。如果你没有指定 `ftp-server`，则在 `ftp` 运行后需要使用 `ftp open` 命令连接到服务器。

## 命令行选项

- -g (globbing) 关闭通配符匹配。见 glob（第 697 页）。
- -i (interactive) 选项在执行 `mget`（第 696 页）和 `mput`（第 696 页）文件传输期间会关闭提示。
- -n (no automatic login) 禁用自动登录（第 694 页）。
- -v (verbose) 告诉你更多关于 ftp 如何工作的信息。显示来自远程计算机的响应，并且 ftp 会报告文件传输速度的信息。另见 verbose（第 698 页）。

## ftp 命令

ftp 工具是交互式的：启动 ftp 后，它会提示你输入命令来设置参数或传输文件。只要缩写是唯一的，你就可以对命令进行缩写。在 ftp> 提示符处输入问号 (?) 可以显示命令列表。在问号后紧跟一个空格和一个命令可以显示该命令功能的简要描述：

```
ftp > mget
mget      multiple files
```

## SHELL 命令

如果不带命令，将在本地系统上转义（生成） shell。当你结束使用本地 shell 时，使用 CONTROL-D 或 exit 返回 ftp。在感叹号 (!) 后紧跟命令将仅执行该命令；当命令执行完成后，ftp 将显示一个 ftp 提示符。ftp 通过此命令生成的 shell 是运行 ftp 的 shell 的子进程，当你返回 ftp 时它会被保留。具体来说，当你想要将文件复制到启动 ftp 的目录以外的本地目录时，你需要使用 ftp 命令来更改本地工作目录：在生成的 shell 中执行 cd 命令不会产生你看到的更改。示例参见第 692 页上的“Local cd (cd)”。

## 传输文件

在以下描述中，remote-file 和 local-file 可以是路径名。

- - append local-file [remote-file]
- - 将 local-file 追加到远程系统中同名的文件中，或者如果指定了，则追加到 remote-file。
- - get remote-file [local-file]
- - 将 remote-file 复制到本地系统并命名为 local-file。如果不指定 local-file，ftp 将使用 remote-file 作为本地系统上的文件名。
- - get remote-file-list
- - （多个）将多个文件复制到本地系统，每个文件保持其原始文件名。你可以直接为远程文件命名，或使用通配符（见 glob）。使用 prompt（第 697 页）关闭传输期间的提示。
- - mput local-file-list
- - （多个 put）将多个文件复制到服务器，使用每个原始文件名。你可以直接为本地文件命名，或使用通配符（见 glob）。使用 prompt（第 697 页）关闭传输期间的提示。
- - newer remote-file [local-file]
- - 如果 remote-file 的修改时间于 local-file，或者 local-file 不存在，则将 remote-file 复制到本地系统并命名为 local-file。如果不指定 local-file，ftp 将使用 remote-file 作为本地系统上的文件名。此命令类似于 get，但不会用旧文件覆盖新文件。
- put local-file [remote-file]
将 local-file 复制到远程系统并命名为 remote-file。如果不指定 remote-file，ftp 将使用 local-file 作为远程系统上的文件名。
- regret remote-file [local-file]
如果 local-file 存在且比 remote-file 小，则将 remote-file 复制到本地系统并命名为 local-file。如果不指定 local-file，ftp 将使用 remote-file 作为本地系统上的文件名。

## 运行 ftp 和 sftp FTP 客户端 67

## 状态

- - ascii 将行类型设置为 ascii。
- - binary 将行类型设置为 binary。
- - cr 切换并显示 cr 模式，显示行结束符是否被转换为回车符。此命令的效果与在命令行上指定 -cr 选项相同。

