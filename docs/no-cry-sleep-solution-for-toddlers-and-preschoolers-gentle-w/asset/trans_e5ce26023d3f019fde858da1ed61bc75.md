

| 命令 | 效果 |
|---|---|
| mput 正则表达式 | 使您能够一次向远程系统发送多个文件。您可以使用特殊字符指定文件；每个要传输的文件都会提示您 |
| runique | 切换使用唯一文件名存储文件。如果本地系统上已存在具有相同文件名的文件，则会生成新的文件名 |
| reget filename | 从中断处恢复传输文件 |
| binary | 以二进制模式传输文件 |
| ascii | 以 ASCII 模式传输文件 |
| cd directory | 在远程系统上更改目录 |
| lcd directory | 在本地系统上更改目录 |
| help or ? | 列出 ftp 命令 |
| mkdir directory | 在远程系统上创建目录 |
| rmdir | 删除远程目录 |
| delete filename | 删除远程系统上的文件 |
| mdelete file-list | 一次删除多个远程文件 |
| rename | 重命名远程系统上的文件 |
| hash | 在下载过程中显示进度哈希符号 |
| status | 显示 ftp 当前状态 |

**表 14-8 ftp 客户端命令（续）**

使用 mkdir 创建远程目录，并使用 rmdir 删除目录。使用 delete 命令擦除远程文件。使用 rename 命令可以更改文件名称。使用 close 命令关闭与系统的连接。然后如果需要可以打开另一个连接。要结束 ftp 会话，请使用 quit 或 bye 命令。

```
ftp> close
ftp> bye
Good-bye
$
```

要向远程系统传输文件并从远程系统传输文件，请使用 get 和 put 命令。get 命令从远程系统接收文件到本地系统，put 命令将文件从本地系统发送到远程系统。从某种意义上说，您的本地系统从远程获取文件并向远程放置文件。在下一个示例中，文件 weather 使用 put 命令从本地系统发送到远程系统：

```
ftp> put weather
PORT command successful.
ASCII data connection
ASCII Transfer complete.
ftp>
```

如果下载中断，您可以使用 reget 恢复下载。这对于极大的文件很有帮助。下载将从中断处恢复，因此无需再次下载整个文件。此外，请确保以二进制模式下载二进制文件。对于大多数 FTP 站点，二进制模式是默认模式，但某些站点可能将 ASCII（文本）作为默认模式。命令 ascii 设置字符模式，命令 binary 设置二进制模式。大多数在 Internet 站点上提供的软件包都是归档和压缩文件，即二进制文件。在下一个示例中，传输模式设置为二进制，并使用 get 命令将归档软件包 mydata.tar.gz 从远程系统发送到本地系统：

```
ftp> binary
ftp> get mydata.tar.gz
PORT command successful.
Binary data connection
Binary Transfer complete.
ftp>
```

您可能经常想要发送多个文件，并使用通配符指定其名称。但是 put 和 get 命令仅对单个文件操作，不适用于特殊字符。要一次传输多个文件，您必须使用另外两个命令 mput 和 mget。使用 mput 或 mget 时，会提示您输入文件列表。然后您可以输入文件列表或使用特殊字符的文件列表规范。例如，*.c 指定所有具有 .c 扩展名的文件，* 指定当前目录中的所有文件。在 mget 的情况下，文件一次一个地从远程系统发送到本地系统。每次都会提示您正在发送的文件名。您可以输入 y 发送文件或输入 n 取消传输。然后会提示您下一个文件。mput 命令以相同的方式工作，但它将文件从本地系统发送到远程系统。在下一个示例中，所有具有 .c 扩展名的文件都使用 mget 发送到本地系统：

```
ftp> mget
(remote-files) *.c
mget calc.c? y
PORT command successful
ASCII data connection
ASCII transfer complete
mget main.c? y
PORT command successful
ASCII data connection
ASCII transfer complete
ftp>
```
