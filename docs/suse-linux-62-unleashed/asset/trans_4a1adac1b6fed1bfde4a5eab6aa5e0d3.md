

第二行末尾的选项防止匿名客户端在 /incoming 下创建子目录。

> 提示
> 建议通过 ftp 将上传的文件设置为组所有，并赋予 775 文件权限。这允许只读访问，使得 /incoming 目录不会成为可疑材料（例如非法软件）的交易场所。

## 动态转换文件——ftpconversions 文件

ftpconversions 文件的格式如下：

<1>:<2>:<3>:<4>:<5>:<6>:<7>:<8>

<1> 是移除前缀（strip prefix）；<2> 是移除后缀（strip postfix）；<3> 是添加前缀（add-on prefix）；<4> 是添加后缀（add-postfix）；<5> 是调用的用于执行转换的外部命令；<6> 是文件类型；<7> 是用于日志的选项信息；<8> 是操作描述。

困惑吗？不用担心。每个选项实际上非常简单。接下来的章节将逐一描述。

## 移除前缀 (Strip Prefix)

移除前缀是文件名开头的字符串，在获取文件时应将其删除。例如，如果你想对以 discography. 开头的文件执行特殊操作，并在操作后删除该前缀，你可以指定 .discography。当客户端指定文件名时，不应包含该移除前缀。也就是说，如果文件名为 discography.orb 且客户端发出 get orb 命令，服务器将对文件执行可选命令并将结果传输给客户端。尽管文档中了他的相关说明，但目前不支持此功能。

## 移除后缀 (Strip Postfix)

移除后缀是文件名末尾的字符串，在获取文件时应将其删除。移除后缀通常用于在将 gzipped 文件传回客户端之前进行解压时，移除末尾的 .gz。

![](img/cbac72550c7126a22162e94d91a0c360_374_0.png)

## 添加前缀 (Add-On Prefix)

添加前缀是在文件从服务器传输到或传输时，插入文件名前的字符串。例如，你可能想在所有从服务器拉取并转换为大写的文件前插入字符串 uppercase.。尽管文档中了他的相关说明，但目前不支持此功能。

## 添加后缀 (Add-On Postfix)

添加后缀是在对文件执行操作完成后附加到文件名后的字符串。这种后缀通常用于客户端发出 largefile.gz 命令时，实际文件名仅为 largefile；在这种情况下，服务器使用 gzip 压缩文件并执行传输。

## 外部命令 (External Command)

每行的核心组件是外部命令。该条目指定了文件在与服务器之间传输时运行的程序。在文件传输过程中，它将通过程序进行过滤，其中下载（发送给客户端的文件）需要发送到标准输出，而上传（发送到服务器的文件）将来自标准输入。例如，如果你想为下载的文件提供 gzip 解压缩，条目将所示：

```
gzip -dc %s
```

行中的 %s 告诉服务器替换为用户请求的文件名。

## 文件类型字段 (Type of File Field)

ftpconversions 的 type 字段是可以处理的文件类型列表，类型名称之间用管道符号 (|) 分隔。识别的三种文件类型 T_REG、T_ASCII 和 T_DIR 分别代表普通文件、ASCII 文件和目录。该条目的示例为 T_REG|T_ASCII。

## 选项字段 (Options Field)

ftpconversions 的 options 字段与 type 字段类似，由一组用管道符号 (|) 分隔的名称组成。支持的三种选项类型 O_COMPRESS、O_UNCOMPRESS 和 O_TAR 分别指定命令是压缩文件、解压文件还是使用 tar 命令。示例条目为 O_COMPRESS|O_TAR，表示文件既经过压缩又进行了 tar 处理。

## ftpconversions 描述 (Description of ftpconversions)

ftpconversions 的最后一个参数是转换描述，这是一个自由格式条目，你可以在其中描述转换的类型。

## ftpconversions 条目示例 (Example of an ftpconversions Entry)

以下是一个按需使用 gzip 的示例条目。这允许想要获取 orb_discography.tar 的用户请求 orb_discography.tar.gz，让服务器在发送之前通过 gzip 压缩文件。实现此操作的配置行如下：

```
:..gz:/bin/gzip -9 -c s:$T_REG:O_COMPRESS:$GZIP
```

前两个参数不是必要的，因为你不想在向请求者发送文件名之前移除任何内容。第三个参数为空，因为你不想在发送之前在文件名开头添加任何字符串。第四个参数确实在发送之前为文件名添加了 .gz 后缀。第五个参数是用于压缩文件的实际命令。-9 选项告诉 gzip 尽可能压缩文件；-c 将压缩后的文件发送到标准输出；% 被服务器替换为用户请求的文件名（例如 orb_discography.tar）。第六个参数中的 T_REG 告诉服务器将该文件视为普通文件，而不是 ASCII 文件或目录。倒数第二个参数 O_COMPRESS 告诉服务器文件既经过压缩又进行了 tar 处理。

## 配置主机访问——ftosts (Configuring Host Access—The ftosts)

ftosts 文件基于用户建立规则。每行可以是以下两种之一：

```
allow <username> <addrglob>
```

```
deny <username> <addrglob>
```

allow 命令允许指定用户 <username> 从特定地址连接。你可以列出多个地址

![](img/cbac72550c7126a22162e94d91a0c360_376_0.png)

## FTP 日志文件—xferlog (The FTP Log File—xferlog)

虽然 xferlog 不是配置文件，但它起着重要作用，因为服务器生成的所有日志都存储在该文件中。日志的每行在表 10.1 中进行了描述。

表 10.1 xferlog 字段
| 日志字段 | 定义 |
|---|---|
| current-time | DDD MMM hh:mm:ss YYYY 格式的当前时间，其中 DDD 是星期，MMM 是日期，hh:mm:ss 是军用时间，YYYY 是年份。 |
| transfer-time | 传输文件花费的总秒数。 |
| remote-host | 发起传输的客户端主机名。 |
| file-size | 传输的文件大小。 |
| filename | 传输的文件名。 |
| transfer-type |传输类型，a 是 ASCII 文本，b 是二进制传输。 |
| special-action-flag | 操作列表，C 表示已压缩，U 表示已解压，T 表示已 tar 处理，- 表示未执行任何操作。 |
| direction | 表示文件是输出还是进入的标志，分别用 o 或 i 表示。 |
| completion-status | 文件传输完成或未完成的状态。 |

# ProFTPD

许多大型网站开始使用 Professional FTP 或 proftpd 用于重型 FTP 服务器应用程序。SuSE 6.2 发行版包含了 proftpd 二进制文件，可以通过 YaST 加载。ProFTPD 是 YaST 工具中“n”或网络服务的一部分。如果 both

