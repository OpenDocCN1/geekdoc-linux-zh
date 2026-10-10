

vsftpd 服务器比 ProFTpd 更容易配置。要启用匿名访问，您只需确保 `/etc/vsftpd/vsftpd.conf` 文件中存在以下一行：`anonymous_enable=YES`

您还必须确保您的系统拥有 ftp 用户的账户。该用户的家目录将用于匿名 FTP 访问。

## 使用 FTP 客户端

FTP 客户端种类繁多。在 Linux 中最常见的之一是 `ftp` 程序，您可以通过输入程序名称，后接要访问的站点名称来使用它，例如 `ftp ftp.example.org`。然后，该程序会提示您输入用户名和密码。结果是一个 `ftp>` 提示符，您可以在这里输入各种命令，其中最常用的命令总结在表 11.3 中。

### 表 11.3 常见的 FTP 命令

| 命令名称 | 效果 |
| :--- | :--- |
| ascii | 设置 ASCII（纯文本）传输。 |
| binary | 设置二进制传输；与 image 同义。 |
| bye | 退出程序；与 exit 和 quit 同义。 |
| cd dir | 更改到服务器上的新目录。 |
| chmod mode file | 更改指定文件的模式（权限）。 |
| close | 终止 FTP 会话而不退出程序；与 disconnect 同义。 |
| delete file | 删除文件。 |
| dir | 获取目录列表；与 ls 同义。 |
| disconnect | 终止 FTP 会话而不退出程序；与 close 同义。 |
| exit | 退出程序；与 bye 和 quit 同义。 |
| get file | 获取文件；与 receive 同义。 |
| help command | 显示指定命令的帮助（或所有命令的列表）；与 ? 同义。 |
| image | 设置二进制传输类型；与 binary 同义。 |
| lcd dir | 更改客户端系统上的当前目录。 |
| ls | 获取目录列表；与 dir 同义。 |
| mdelete files | 删除多个文件。 |
| mget files | 获取多个文件。 |
| mkdir dir | 在远程系统上创建目录。 |
| mput files | 发送多个文件。 |
| open server | 打开与指定远程系统的连接。 |
| prompt | 切换多文件命令（mget、mput 等）中验证每个文件的提示。 |
| passive | 切换被动传输模式开/关。 |
| put file | 发送一个文件；与 send 同义。 |
| pwd | 显示服务器上的当前目录。 |
| quit | 退出程序；与 bye 和 exit 同义。 |
| recv file | 获取文件；与 get 同义。 |
| reget file | 从同名本地文件的末尾开始获取文件；适用于重启中断的传输。 |
| rstatus | 显示服务器状态。 |
| rename oldname newname | 重命名服务器上的文件。 |
| rmdir dir | 删除服务器上的目录。 |
| send file | 发送一个文件；与 put 同义。 |
| status | 显示当前状态。 |

![](img/9903a4d3f7abd8dcbef1035fa04a3406_527_0.png)

输入 **help** 或 ? 以获取 ftp 命令列表。输入 **help command** 或 ? **command** 以获取关于特定 *command* 功能的非常简明的描述。

还有许多其他 FTP 客户端可用，包括 gFTP（<http://gftp.seu1.org>）等 GUI 工具。Web 浏览器也可以作为 FTP 客户端使用；对于匿名访问，您输入 FTP 服务器的主机名，前面加上 `ftp://`，例如 `ftp://ftp.example.org`。对于非匿名访问，您在主机名前加上用户名和一个 at 符号（@），例如 `ftp://lucy@ftp.example.org`。然后，Web 浏览器会提示您输入密码。

一个不寻常但很有用的 FTP 客户端是 fuseftp（<http://freshmeat.net/projects/fuseftp>）。结合用户空间文件系统（FUSE；<http://fuse.sourceforge.net>）软件，fuseftp 允许您将 FTP 服务器的文件挂载，就像它们位于 SMB/CIFS 共享或 NFS 导出上一样。如果您想直接访问 FTP 服务器上的文件而无需将其存储在本地，这种类型的访问非常方便，例如查看图形文件或编辑文本文件。

FTP 是一种古老且行为怪异的协议，它有两个独特的陷阱。这些问题主要出现在客户端，因此用户应该意识到它们；然而，如果您配置防火墙，如第 9 章“配置高级网络”中所述，您可能需要考虑这些问题的第一个。

第一个 FTP 怪癖在于其管理端口的方式。FTP 注册了两个端口（TCP 端口 20 和 21）。端口 20 是数据端口，用于数据传输；端口 21 是命令端口，用于发出命令。此配置的大问题是，在正常的 FTP 主动模式下，客户端发起与命令端口的连接，然后服务器从服务器的命令端口向客户端发起反向连接。这种服务器到客户端的连接被某些防火墙阻止，因此 FTP 在未明确配置为允许此连接的防火墙上经常失败。解决此问题的客户端方法是使用 FTP 被动模式（通过在 ftp 程序中输入 passive 或在 GUI 或其他 FTP 客户端中选择等效选项）。在被动模式下，FTP 客户端发起两个连接，这克服了防火墙阻止所有传入连接的问题。然而，被动模式使用服务器上的非特权端口进行数据传输，这有时会违反防火墙规则。因此，您可能需要尝试主动和被动模式，以确定哪一个效果最好。

第二个 FTP 怪癖与传输模式有关。FTP 客户端通常默认使用 ASCII（纯文本）传输模式，在这种模式下，文件以动态更改字符编码的方式传输，以考虑不同操作系统存储纯文本文件的不同方式。（Linux/Unix、Windows 和原始 Mac OS 都使用不同的行结束符约定，甚至一些更奇特的系统使用非 ASCII 编码方法。）使用 ASCII 模式非常适合纯文本文件，但这种模式几乎总是会使二进制文件损坏，例如 tar 包、图形文件、字处理文档等。您可以使用 ftp 中的 `ascii` 和 `binary` 选项，或其他 FTP 客户端中的类似选项，来设置传输模式。如果不确定，请使用二进制模式；当今大多数文本编辑器都可以处理任何常见的行结束符类型，因此以错误格式获取文本文件造成的问题很小或没有。不过，某些 Linux 配置文件必须使用 Unix 风格的行结束符，因此如果您传输此类文件，可能需要关注这个细节。

## 配置 Web 服务器

Web 服务器是互联网的另一个重要组成部分。这些服务器处理超文本传输协议（HTTP），这就是为什么大多数 Web 页面地址以字符串 `http://` 开头的原因。（还存在一种安全的 HTTP 变体；此类页面以前导的 `https://` 表示。）Apache（http://httpd.apache.org）是 Linux 上最受欢迎的 Web 服务器。一些发行版默认安装 Apache，但许多并不安装，因此如果您想运行 Apache，可能需要安装它；它通常包含在一个名为 `apache` 或 `httpd` 的软件包中。

> **注意**
> 也存在其他 Web 服务器软件包，但没有一个像 Apache 那样流行。由于 Apache 通常随 Linux 一起分发并且有时默认安装，因此它通常是一个不错的选择，即使它提供的功能比许多站点所需的更多。

Apache 是一个极其复杂的服务器；本节仅介绍该服务器最基本的功能。要了解更多信息，请查阅其文档或相关书籍，例如 Charles Ald 的 *Linux Apache Server Administration, 2nd Edition*（Sybex, 2002）。

## 设置基本 Apache 选项

安装后，Apache 依赖于一个配置文件，该文件很可能名为 `httpd.conf` 或 `httpd2.conf`（后者的名称通常适用于 Apache 2.0 或更高版本的安装）。此文件通常出现在 `/etc/apache`、`/etc/httpd` 或 `/etc/apache2/conf` 中。无论如何，标准的 Apache 配置文件由以井号（#）开头的注释行和采用以下格式选项行组成：

```
Directive Value
```

Directive 是您想要设置的选项名称，Value 是您想要分配给 Directive 的值。此文件还包含选项块，由尖括号内的代码表示：

```
    <IfDefine APACHEPREFIX>
    Listen 8080
    </IfDefine>
```

默认的 Apache 配置通常从中心位置提供 Web 页面，该位置由 `DocumentRoot` 指令指定。您可能不想提供您的发行版的通用 Web 页面，因此您应该查找此指令，并将其更改为指向您自己的主页，或者用您创建的文件替换默认位置中的文件。除了主站点 Web 页面外，Apache 还可以提供用户 Web 页面，它从使用 `UserDir` 指令指定的目录读取。这些页面通常位于每个用户家目录的子目录中。例如，如果 `UserDir` 指向 `public_html`，则每个用户家目录中的 `public_html` 子目录持有该用户的 Web 页面，可以通过在 Web 地址末尾添加波浪号（~）和用户名来访问，例如 `http://www.asmallisp.net/~john/` 用于访问 john 的主页。

