
| 参数 | 功能 |
| --- | --- |
| source_dir | 要复制的文件目录。 |
| target_dir | 复制目标。如果 `target_dir` 不存在，`xcopy` 将创建它并将文件直接复制其中。 |

## 更多 Mtools 命令

以下命令也包含在 Mtools 工具包中。

| 命令 | 功能 |
| --- | --- |
| mattrib | 设置/清除属性位。 |
| mbad | 扫描坏块。 |
| mdeltree | 删除目录树。 |
| mformat | 格式化 MS-DOS 磁盘。 |
| mininfo | 显示 MS-DOS 文件系统引导扇区的字段内容。 |
| mkmanifest | 创建一个 LINUX shell 脚本，以消除 MS-DOS 转换为 8.3 文件名时的混乱问题。 |
| mlabel | 添加卷标签。 |

## 挂载 MS-DOS 媒体和分区

| 命令 | 功能 |
| --- | --- |
| mmount | 挂载 MS-DOS 文件系统。 |
| mmove | 重命名 MS-DOS 文件或目录。 |
| mpartition | 创建 MS-DOS 分区。 |
| mrd | 移除 MS-DOS 子目录。 |
| mren | 重命名 MS-DOS 文件或目录。 |
| mtoolest | 测试 Mtools 配置。 |

## 挂载 MS-DOS 媒体和分区

与其使用 Mtools，你也可以使用 LINUX 内置的对 MS-DOS 文件系统的支持。你可以像挂载任何其他文件系统一样挂载 MS-DOS 文件系统，然后将其视为 LINUX 文件层次结构的一部分。

## 挂载硬盘分区

如果你在 LINUX 计算机上有一个 MS-DOS 文件系统，你可以保留它。只需遵循以下步骤：

1. 以 root 身份登录。
2. 使用 `mkdir` 创建挂载点目录。
3. 编辑 `/etc/fstab` 并为相应的设备和挂载点添加挂载行。参见下表获取该行字段的示例。
4. 保存更新后的 `/etc/fstab`。
5. 输入 `mount -a` 强制重新读取 `/etc/fstab`。

| 字段 | 功能 |
| --- | --- |
| Device | 分区的设备名称。 |
| Mount point | 要挂载文件系统的目录名称。 |
| Filesystem type | 要使用的文件系统类型。MS-DOS 分区使用 `msdos`。 |
| Options | 挂载方式。使用默认值是安全的。 |
| Dump frequency | 如果不想让此分区包含在标准备份（dump）中，则使用 `0`。 |
| fsck order | 使用 `0`。 |

## 使用 Mac 媒体

例如，如果你的第一个硬盘上的第二个分区 (`/dev/hda2`) 是 MS-DOS 文件系统，你可以保留它。只需像挂载任何其他文件系统一样挂载 MS-DOS 文件系统，然后将其视为 LINUX 文件层次结构的一部分。

# 与 UNIX 文件和媒体交互

## 其他 hfsutils 命令

以下是可用的 HFS 工具程序：

| 命令 | 功能 |
| --- | --- |
| hattrib | 更改文件或目录属性。 |
| hformat | 创建新的 HFS 文件系统。 |
| hfs | 用于操作 HFS 卷的 Shell。 |
| hls | 列出 HFS 目录中的文件。 |
| hpwd | 打印当前 HFS 卷的工作目录名称。 |
| hrename | 重命名 HFS 文件或目录。 |
| hrmdir | 删除一个空 HFS 目录。 |
| hvol | 显示或更改当前 HFS 卷。 |
| xhfs | HFS 命令的图形化界面。 |

Mac 使用回车符（Return character）来分隔文本文件中的行。UNIX 和 LINUX 使用换行符（Newline character）。可以使用 `tr` 命令将回车符转换为换行符。例如，要将文件 `textfile.mac`（八进制 15）在拷贝过程中将其字符转换为换行符（八进制 12），请使用命令 `tr '\015' '\012' <textfile.mac> >textfile.linux`。

## 与 UNIX 文件和媒体交互

你在处理 UNIX 文件和媒体时应该不会遇到问题。LINUX 遵循的 POSIX 标准基于 UNIX。通过仔细地使用 `tar` 和 `cpio` 等工具的选项，你应该能够顺畅地在 UNIX 和 LINUX 系统之间传输文件。

# 网络

互联网作为最大且最为人知的网络系统，实际上是 LINUX 诞生的关键。没有互联网，开发 LINUX 所投入的协作努力将是不可能的。因此，LINUX 为你提供与全球计算机用户交换数据的手段顺理成章。

在这一部分 ...

- 通过网络传输文件
- 在远程机器上进行交互式操作
- 检查网络连通性

# 解析网络地址

任何网络上的计算机（互联网是最大的例子）都使用各种网络地址方法。要更详细了解网络地址，请查阅《Linux SECRETS，第2版》（IDG Books Worldwide, Inc.）或 LINUX 文档页面上的《Linux 网络管理员手册》（点击 www.linuxresources.com 上的 LDP）。

# 域名地址

与其记住计算机系统的 IP 地址，我们人类更愿意记住一个名称。这时域名就派上用场了。域名是一个用于引用特定 IP 地址的符号名称。

多个域名可以指向同一个 IP 地址，多个域名也可以指向同一台机器上不同的 IP 地址。请查看 www.linuxjournal.com 和 www.linuxresources.com 示例。这两个 URL 将你带到同一台机器，但位于不同的主页。

要建立域名，你需要在 rs.internic.net 向 Internic 注册。

# IP 地址

互联网上的所有机器（极可能你的本地网络上也是如此）都有 IP（互联网协议）地址。IP 地址由四个数字组成，范围从 0 到 255，以点分四位数的格式（dotted quad quotation）写入。这意味着这四个数字是以点分隔的字符串形式书写的的。例如，`198.186.207.128` 是我其中一台计算机的 IP 地址。

为同一台机器分配多个 IP 地址是可能的，有时也是理想的。这种做法常见的用途是：当你希望你的 Web 服务器根据你访问它的地址执行不同的操作（例如，显示不同的主页）。

# DNS 服务器

当你注册域名时，你需要指定至少两个服务器的 IP 地址（这些机器拥有必要的信息，可以将你的域名映射到信息应该递送的计算机的 IP 地址）。服务器必须能够响应来自其他服务器的查询，以便在任何需要的地方提供名称到地址的转换。IP 地址与硬件地址之间的映射由地址解析协议（ARP）和反向 ARP（Reverse ARP）处理。

# ftp — 传输文件

FTP（文件传输协议）是通过互联网发送和接收文件最常用的方式。你也可以在本地网络上使用它。为了避免某些 ftp 与 FTP 之间的混淆，`ftp` 是 LINUX 中的程序名称，而 FTP 是泛指的过程。

要使用 FTP，你需要在远程机器上有一个账户。你可以用用户名 `anonymous` 登录许多公共服务器并接收文件。

```
ftp [-d] [-g] [-i] [-n] [-v] [host]
```

| 参数或参数 | 功能 |
| --- | --- |
| -d | 启用调试模式。 |
| -g | 禁用文件名通配符扩展（在 UNIX 中称为 globbing）。 |
| -i | 在多文件传输期间关闭交互式提示。 |
| -n | 指示程序不要尝试自动登录。`ftp` 通常会猜测你的登录名并提示，如果你满意，可以按回车键。在此模式下，不会进行任何登录尝试，你需要在 `ftp` 提示符处输入 `user`。 |
| -v | 显示来自远程服务器的所有响应和传输统计数据。 |
| host | 你想要连接的机器名称。如果省略 `host`，`ftp` 会询问机器名称。 |

# 连接到匿名 FTP 服务器

匿名 FTP 会话与普通 FTP 会话一样，不同之处在于你不需要自己的账户。许多服务器（如 `sunsite.unc.edu`）提供匿名 FTP，以便你可以访问公开文件。例如，所有的 LINIX 都可以通过匿名 FTP 获取。按照以下步骤连接到匿名 FTP：

1. 在 shell 提示符处输入 `ftp` 后跟服务器的名称。
2. 在提示登录名时，输入 `anonymous`。
3. 在提示密码时，输入你的邮箱地址。

这种会话就像普通的 FTP 会话，只是你不需要自己的账户。许多服务器提供匿名 FTP，以便你可以访问公开文件。例如，所有的 LINIX 都可以通过匿名 FTP 获取。按照以下步骤连接到匿名 FTP：

1. 在 shell 提示符处输入 `ftp` 后跟服务器的名称。
2. 在提示登录名时，输入 `anonymous`。
3. 在提示密码时，输入你的邮箱地址。

# 在 ftp 中执行本地命令

有时在处于 `ftp` 环境时，你可能需要检查本地机器上的某些内容（例如你当前处于哪个目录）。要实现这一点，只需输入 `!` 后紧跟你想要执行的 shell 命令即可。

你可能想用 `!` 命令来更改本地机器的目录。然而，你无法这样做！因为它会创建一个子壳（subshell）。命令执行后，子壳会终止，你将回到起点。请使用 `cd` 命令来更改本地目录。

# 退出 ftp

要断开与远程系统的连接并退出 `ftp` 程序，请输入 `quit`。

# ftp 命令摘要

`ftp` 提供了多种命令。以下是一些常用命令的摘要：

| 命令 | 含义 |
| --- | --- |
| asc | 设置 ASCII 传输模式。 |
| bin | 设置二进制传输模式。 |
| case | 将文件名的大小从大写转为小写，或从小写转为大写。 |
| cd dir | 更改远程机器目录。 |
| delete file | 删除远程系统上的文件。 |
| dir [files] [dest] | 列出远程系统中匹配模式 `files` 的文件名称（默认为所有文件）。如果指定了 `dest`，则输出将放在本地系统的该路径下，否则显示在屏幕上。 |
| get rfile [file] | 将远程系统的 `rfile` 传输到本地系统的 `file`。`file` 默认名称与 `rfile` 同名。 |
| hash | 开启/关闭每 1024 个字符在屏幕上打印一个井号 (`#`)。 |
| lcd dir | 更改本地系统的目录。 |
| mget files | 从远程系统获取指定的文件。 |
| mput files | 将指定的文件上传到远程系统。 |
| prompt | 切换 `mget` 和 `mput` 命令的提示模式。 |
| pwd | 显示远程系统当前目录的名称。 |

# ftp — 传输文件 149

| 命令 | 含义 |
| --- | --- |
| quit | 退出 `ftp`。 |
| verbose | 切换 `ftp` 的详细信息模式。 |
| ? | 打印帮助信息。后跟命令名称可获取特定命令的帮助信息。 |

# 使用 ftp 列出目录内容

通过 `ftp` 连接到远程系统后，你需要查找所需内容。输入 `dir`，`ftp` 将向你展示当前目录下的文件列表。

你可以使用两个可选参数使列表更具针对性：

| 参数 | 含义 |
| --- | --- |
| files | 文件选择模式。如果你想列出所有文件，请使用 `*`。例如，如果你想列出以某些字符开头的文件名，可以使用 `dir*`。这种模式匹配类似于通配符。（更多详细信息请参阅第二部分。） |
| destination | 你本地系统上的文件名。如果你使用此参数，`dir` 将输出发送到你的电脑而不是显示在屏幕上。如果目录包含的文件多于屏幕显示范围，你可以通过输入 `dir | more` 逐页查看列表。当需要看下一页时按空格键。 |

# 使用 ftp 导航远程主机

在了解主机上有什么内容后，你可能需要更改该机器的目录。该命令称为 `cd`，它的工作原理类似于 LINUX 中的 `cd` shell 命令。你可以使用相对路径或绝对路径来指定目标。例如，要移动到 `/pub/Linux/` 目录，输入 `cd /pub/Linux/`。在几乎所有的匿名 FTP 服务器上，所有内容都从 `/pub` 目录开始（那里几乎是公共访问文件的所在地）。

# 使用 ftp 传输多个文件

通常情况下，你想传输目录中的所有文件或匹配特定模式的所有文件：

- 要上传当前目录下的所有文件，输入 `mput`
- 要下载远程系统上的所有文件，输入 `mget`
- 如果你想有选择地操作，可以输入文件名列表而非仅仅 `*`。`mget` 和 `mput` 在传输每个文件之前都会询问你。按 `y` 传输文件或按 `n` 跳过。
- 如果你确定要传输所有内容，输入 `prompt` 关闭提示模式。

# 使用 ftp 上传文件

向远程计算机上传或发送文件与下载非常相似，只是方向相反。按照以下步骤上传文件：

1. 使用 `cd` 命令移动到你想上传文件的目录。
2. 如果你不在文件所在的本地机器目录中，输入 `cd` 后跟名称以更改目录。
3. 设置传输模式以匹配你打算获取的文件类型。要执行此操作，输入 `asc` 将模式设为 ASCII，或为非 ASCII 文件输入 `bin`。
4. 输入 `put`、你想上传的文件名，以及可选的远程系统上该文件的新名称。如果你省略了名称，该文件将与本地文件同名。

在 PPP 连接上，上传和下载可能花费很长时间。如果你想在进行时查看状态报告，请在 `ftp` 提示符处输入 `hash`。之后你会在每传输 1024 个字符后看到一个 `#`。再次输入 `hash` 即可关闭此命令。

# nslookup — 查询互联网服务器

`nslookup` 程序显示名称服务器上当前可用的信息。

```
nslookup [-option] [host]

nslookup [-option] host server

nslookup [option] server
```

# nslookup — 查询互联网服务器 151

| 选项或参数 | 功能 |
| --- | --- |
| -option | 任意选项之一（见下表）。你可以输入多个选项。必须在每个选项前放置前缀，并以 `keyword=value` 的格式输入每个项。 |
| host | 要查找的主机名。如果你未指定 `host`，`nslookup` 将进入交互模式。 |
| server | 用于查询的名称服务器。 |

如果你尝试使用 `nslookup host` 进行查询并得到 `>` 提示符，说明你的 `nslookup` 版本不支持此模式。中止 `nslookup`（使用你的终止字符或按 `Ctrl+D`）。然后，输入 `nslookup` 并按回车。

`nslookup` 支持以下选项。你可以在命令行中输入它们，也可以在交互模式下在关键字后输入。

| 选项 | 含义 |
| --- | --- |
| all | 显示常用设置选项的当前值。 |
| domain=name | 将默认域更改为 `name`。这是附加到未指定域的查询中的后缀名称。 |
| querytype=type | 更改搜索的记录类型。默认是 `A`（地址记录）。其他常用值是 `CNAME`（用于别名的标准名）、`MX`（邮件交换器）和 `ANY`（表示搜索所有记录类型）。 |

当你处于交互模式时，可以使用以下命令：

| 命令 | 功能 |
| --- | --- |
| exit | 返回 shell。 |
| finger | 连接到最近成功查询的主机。你可以使用标准 shell 重定向符重定向其输出。 |
| help | 显示命令摘要。 |
| ls domain | 列出域的信息。你可以使用标准 shell 重定向符重定向其输出。 |
| lserver | 将名称服务器改为域。该命令使用初始服务器进行查询。 |
| server domain | 将名称服务器改为域。该命令使用当前服务器进行查询。 |

# ping — 向网络主机发送测试包

在以下示例中，我首先输入带选项的 `nslookup`，然后按回车进入默认名称服务器的交互模式。然后我输入 `pacificbeachwa.com` 查询该名称服务器注册的该域的任何记录。我执行默认查询（地址记录），通过输入 `querytype=ANY` 设置查询类型，并重复查询。

```
Default Server: hendrix.aa.net

Address: 204.157.220.4

> pacificbeachwa.com

Server: hendrix.aa.net

Address: 204.157.220.4

Name: pacificbeachwa.com

Address: 199.184.169.73

> set querytype=ANY

> pacificbeachwa.com

Server: hendrix.aa.net

Address: 204.157.220.4

Non-authoritative answer:

pacificbeachwa.com nameserver = UNCLE.SSC.COM

pacificbeachwa.com nameserver = BROKENOWN.SSC.COM

pacificbeachwa.com internet address = 199.184.169.73

Authoritative answers can be found from:

pacificbeachwa.com nameserver = UNCLE.SSC.COM

pacificbeachwa.com nameserver = BROKENOWN.SSC.COM

UNCLE.SSC.COM internet address = 204.157.223.65

BROKENOWN.SSC.COM internet address = 204.157.223.78

>exit
```
