

## 9.3.2 HP-UX

HP-UX 上 FTP 客户端的语法如下：

``````
ftp [-g] [-i] [-n] [-v] [-B size] [server-host]
```

-g、-i 和 -n 选项与 Windows 2000 版本 FTP 中的选项相同。B 选项将数据套接字的缓冲区大小设置为 1024 字节块的倍数。块范围为 1 到 64 之间，默认值为 56。默认连接类型为 ASCII，但如果你连接到另一个 HP-UX 系统，FTP 将切换到二进制连接。

## 9.3.3 FTP 子命令比较

每个平台上的 FTP 客户端支持的子命令各相同。表 9–1 比较了这些子命令。更多信息请参阅 HP-UX 上的 ftp 手页或 Windows 2000 上的帮助实用。

## 表 9–1 Windows 2000 和 HP-UX  FTP 子命令

| 命令 | Windows 2000 | HP-UX |
|---|---|---|
| ! | 是 | 是 |
| $ | 否 | 是 |
| ? | 是 | 是 |
| account | 否 | 是 |
| append | 是 | 是 |
| ascii | 是 | 是 |
| bell | 是 | 是 |
| binary | 是 | 是 |
| bye | 是 | 是 |
| case | 否 | 是 |
| cd | 是 | 是 |
| cdup | 否 | 是 |

## 表 9–1 Windows 2000 和 HP-UX FTP 子命令（续上）

| 命令 | Windows 2000 | HP-UX |
|---|---|---|
| chmod | 否 | 是 |
| close | 是 | 是 |
| cr | 否 | 是 |
| debug | 是 | 否 |
| delete | 是 | 是 |
| dir | 是 | 是 |
| disconnect | 是 | 是 |
| form | 否 | 是 |
| get | 是 | 是 |
| glob | 是 | 是 |
| hash | 是 | 是 |
| help | 否 | 是 |
| idle | 否 | 是 |
| lcd | 是 | 是 |
| literal | 是 | 否 |
| ls | 是 | 是 |
| macdef | 否 | 是 |
| mdelete | 是 | 是 |
| mdir | 是 | 是 |
| mget | 是 | 是 |

## 表 9–1 Windows 2000 和 HP-UX FTP 子命令（续上）

| 命令 | Windows 2000 | HP-UX |
|---|---|---|
| mkdir | 是 | 是 |
| mls | 是 | 是 |
| mode | 否 | 是 |
| modtime | 否 | 是 |
| mput | 是 | 是 |
| nlist | 否 | 是 |
| nmap | 否 | 是 |
| nrans | 否 | 是 |
| open | 是 | 是 |
| passive | 否 | 是 |
| prompt | 是 | 是 |
| proxy | 否 | 是 |
| put | 是 | 是 |
| pwd | 是 | 是 |
| quit | 是 | 是 |
| quote | 是 | 是 |
| recv | 是 | 是 |
| reget | 否 | 是 |
| rhelp | 否 | 是 |
| remotehelp | 是 | 否 |

## 表 9–1 Windows 2000 和 HP-UX FTP 子命令（续上）

| 命令 | Windows 2000 | HP-UX |
|---|---|---|
| rename | 是 | 是 |
| reset | 否 | 是 |
| restart | 否 | 是 |
| rmdir | 是 | 是 |
| rstatus | 否 | 是 |
| runique | 否 | 是 |
| send | 是 | 是 |
| sendport | 否 | 是 |
| site | 否 | 是 |
| size | 否 | 是 |
| status | 是 | 是 |
| sunique | 否 | 是 |
| system | 否 | 是 |
| tenex | 否 | 是 |
| trace | 是 | 否 |
| type | 是 | 是 |
| umask | 否 | 是 |
| user | 是 | 是 |
| verbose | 是 | 是 |

## 9.3.4 HP-UX ftpd

HP-UX 11 拥有一个与该操作系统之前的版本不同的 ftppd。新的 ftppd 支持传输日志、命令日志、即时压缩和归档、按类型和位置分类用户、按目录上传权限、受限访客账户、系统级按目录消息、目录别名、cpath、虚拟主机支持以及按类限制。正如我们将要看到的，最重大的变化之一是一个新选项：-K，它强制执行 Kerberos 认证。有关在 HP-UX 11 上配置 ftppd 的完整信息，请参阅 /usr/share/doc/RelNotes_newftp.txt 中的发布说明。

与 Windows 2000 FTP 服务器不同，HP-UX 默认不允许匿名登录。在 HP-UX 上设置匿名 FTP 的简单方法是使用 SAM。从 SAM 主界面，选择“Networking and Communications”（网络与通信）→“Network Services”（网络服务）。选择“Anonymous FTP”（匿名 FTP），然后从菜单栏选择“Actions”（操作）→“Enable”（启用），如图 9–1 所示。

![](img/1c1e7552b53cca888836b6c6895bdb48_144_0.png)

图 9–1 使用 SAM 在 HP-UX 上配置匿名 FTP。

此过程会将匿名 FTP 文件存放在 /home/ftp 目录下。如果你以匿名或 ftp 身份登录，你将进入此目录并看到以下子目录：dist、etc、pub 和 usr。

## 9.3.5 Windows 2000 FTP 服务器

尽管 Windows 2000 安装过程默认安装了 Internet 信息服务（IIS），但你仍必须确保也安装了 FTP 服务器。如果你运行“开始->设置->控制面板->添加/删除程序”，然后选择“添加/删除 Windows 组件->Internet 信息服务”，请确保你的窗口勾选了“文件传输协议 (FTP) 服务器”框框，如图 9–2 所示。

![](img/1c1e7552b53cca888836b6c6895bdb48_145_0.png)

图 9–2 在 Windows 2000 上配置匿名 FTP。

与 Windows 2000 FTP 服务器不同，HP-UX 默认不允许匿名登录。在 HP-UX 上设置匿名 FTP 的简单方法是使用 SAM。从 SAM 主界面，选择“Networking and Communications”（网络与通信）→“Network Services”（网络服务）。选择“Anonymous FTP”（匿名 FTP），然后从菜单栏选择“Actions”（操作）→“Enable”（启用），如图 9–1 所示。

此过程会将匿名 FTP 文件存放在 /home/ftp 目录下。如果你以匿名或 ftp 身份登录，你将进入此目录并看到以下子目录：dist、etc、pub 和 usr。

## 9.3.6 传输文件

传输文件的通用规则是：如果在相同系统之间传输，请使用 BINARY。如果你的系统不同，请使用 ASCII。

## 9.3.7 Windows 2000 FTP 客户端

如果你使用 Windows 2000 Internet Explorer 连接到 UNIX FTP 服务器，读取复制到系统中的文件将会遇到困难。例如，图 9–5 中有一个名为 *boot.txt* 的图标。该文件位于 *hpux1*（一个 UNIX 系统）上。你可以通过将图标拖到桌面将其复制到 Windows 2000 机器。然而，如果你用记事本打开该文件，将看到类似图 9–6 的内容。记事本不知道如何处理 UNIX 系统放在行尾的 NL（换行）字符。基于 Windows 的系统使用 CR-LF（回车-换行）字符来表示行结束。然而，如果你用 Wordpad 或 Word 打开该文件，这些程序可以很好地解释 UNIX 创建的文本文件。

