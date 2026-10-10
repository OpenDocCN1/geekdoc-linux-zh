
## chroot 监狱
FTP 服务器通常运行在*chroot 监狱*中，这是一种运行程序的方式，使得程序只能看到计算机可用目录的有限子集。你应该查阅服务器文档，了解它是否支持此功能，如果支持，如何使用。通常，你会预留一个目录并复制一些文件到其中，包括 FTP 服务器应该提供的文件。

## 用户配置
FTP 服务器通常允许拥有常规账户的任何用户登录。一些服务器还支持 `/etc/ftpusers` 文件，该文件列出了*不得*使用 FTP 服务器的用户名。此文件通常包括系统账户，如 *root* 和 *daemon*，但你也可以将常规用户添加到此文件中。如果你的 FTP 服务器软件包未安装此文件，请查阅服务器文档以查看是否支持它。如果不支持，请检查服务器是否提供了限制谁能访问系统的其他手段。

## 匿名访问
大多数 FTP 服务器都提供了支持匿名访问的某种机制，但具体实现细节因 FTP 服务器而异。

匿名访问问题至关重要，因此我提供几个示例。首先，如前所述，**ftpd** 服务器被设计为仅提供*匿名*访问。因此，如果你希望只提供匿名访问而不提供常规用户访问，这是一个不错的选择。

如果你使用 **ProFTpd**，匿名配置需要在 `/etc/proftpd/proftpd.conf` 中设置许多选项：

```
<Anonymous  /home/ftp>
	User	anonymous
	Group	anonymous
	AnonRequirePassword off

	<Limit LOGIN>
	Allow	from all
	</Limit>

	<Limit LIST NLST RETR MDTM PWD XPWD	SIZE	STAT	CWD XCWD	CDUP XCUP >
	AllowAll
	</Limit>

	<Limit STOR STOU	APPE	RnFR RnTO	DELETE	MKD XMKD SITE_MKDIR	RMD XRMD>
	SITE_RMDIR	SITE	SITE_CHMOD	SITE_CHGRP >
	DenyAll
	</Limit>

</Anonymous>
```

你应该将第一行中的目录（在此示例中为 */home/ftp*）更改为指向保存你希望可用的文件的目录。其他一些选项比较直观，但有些选项比较晦涩。特别是第二个和第三个 `<Limit>` 块，指定了允许的操作类型，例如 **LIST** 和 **RETR**（分别用于列出和获取文件）。这些代码对于初学者来说可能令人困惑。因此，**GProFTpd** 配置工具的存在并不令人惊讶，因为它使用点选界面帮助你设置匿名（和非匿名）访问——但即使是 **GProFTpd** 也可能令人困惑。

*vsftpd* 服务器比 *ProFTpd* 更容易配置。要启用匿名访问，你只需确保 `/etc/vsftpd/vsftpd.conf` 文件中存在一行：`anonymous_enable=YES`

你还必须确保你的系统有一个 *ftp* 用户的账户。该用户的主目录将用作匿名 *FTP* 访问的目录。

## 使用 FTP 客户端

FTP 客户端种类繁多。在 Linux 中最常见的之一是 *ftp* 程序，你可以输入程序名称加上要访问的网站名称来使用它，例如 **ftp ftp.example.org**。然后程序会提示你输入用户名和密码。结果是一个 *ftp>* 提示符，在此处你可以输入各种命令，其中最常用的命令总结在表 11.3 中。

**表 11.3 常用 ftp 命令**

| 命令名称 | 效果 |
| :--- | :--- |
| *ascii* | 设置 *ASCII*（纯文本）传输。 |
| *binary* | 设置*二进制*传输；与 *image* 同义。 |
| *bye* | 退出程序；与 *exit* 和 *quit* 同义。 |
| *cd dir* | 在服务器上切换到新目录。 |
| *chmod mode file* | 更改指定文件的模式（权限）。 |
| *close* | 终止*FTP* 会话而不退出程序；与 *disconnect* 同义。 |
| *delete file* | 删除文件。 |
| *dir* | 获取目录列表；与 *ls* 同义。 |
| *disconnect* | 终止*FTP* 会话而不退出程序；与 *close* 同义。 |
| *exit* | 退出程序；与 *bye* 和 *quit* 同义。 |
| *get file* | 获取文件；与 *receive* 同义。 |
| *help command* | 显示指定命令的帮助（或所有命令的列表）；与 *.?* 同义。 |
| *image* | 设置二进制传输类型；与 *binary* 同义。 |
| *lcd dir* | 更改客户端系统上的当前目录。 |
| *ls* | 获取目录列表；与 *dir* 同义。 |
| *mdelete files* | 删除多个文件。 |
| *mget files* | 获取多个文件。 |
| *mkdir dir* | 在远程系统上创建目录。 |
| *mput files* | 发送多个文件。 |
| *open server* | 打开到指定远程系统的连接。 |
| *prompt* | 切换在多文件命令（mget, mput 等）中验证每个文件的提示功能。 |
| *passive* | 切换被动传输模式的开和关。 |
| *put file* | 发送一个文件；与 *send* 同义。 |
| *pwd* | 显示服务器上的当前目录。 |
| *quit* | 退出程序；与 *bye* 和 *exit* 同义。 |
| *recv file* | 获取文件；与 *get* 同义。 |
| *reget file* | 从本地同名文件的末尾开始获取文件；适用于重启被中断的传输。 |
| *rstatus* | 显示服务器状态。 |
| *rename oldname newname* | 重命名服务器上的文件。 |
| *rmdir dir* | 删除服务器上的目录。 |
| *send file* | 发送一个文件；与 *put* 同义。 |
| *status* | 显示当前状态。 |

*输入 help 或 ? 以获取 ftp 命令列表。输入 help command 或 ? command 以获取特定命令功能的简要描述。*

还有许多其他 FTP 客户端可用，包括 GUI 工具，如 gFTP (http://gftp.seul.org)。Web 浏览器可以作为 FTP 客户端；对于匿名访问，你输入 FTP 服务器的主机名，前面加上 ftp://，例如 ftp://ftp.example.org。对于非匿名访问，你在主机名前面加上用户名和一个 at 符号（@），例如 ftp://lucy@ftp.example.org。然后 Web 浏览器会提示你输入密码。

一个不寻常但有用的 FTP 客户端是 fuseftp (http://freshmeat.net/projects/fuseftp/)。结合 Filesystem in User-space（FUSE；http://fuse.sourceforge.net）软件，fuseftp 允许你将 FTP 服务器上的文件挂载，就好像它们位于 SMB/CIFS 共享或 NFS 导出上一样。如果你想直接访问 FTP 服务器上的文件而不将其存储在本地（例如查看图形文件或编辑文本文件），这种访问方式非常方便。

FTP 是一个古老且怪癖的协议，它存在一些 FTP 特有的陷阱。这些问题主要是在客户端的，因此用户应该意识到它们；然而，如果你配置防火墙，如第 9 章“配置高级网络”中所述，你可能需要考虑这些问题中的第一个。

FTP 的第一个怪癖在于它管理端口的方式。两个端口（TCP 端口 20 和 21）注册给 FTP。端口 20 是数据端口，用于数据传输；端口 21 是命令端口，用于发出命令。这种配置的主要问题是，在正常的 FTP 主动模式下，客户端发起对命令端口的连接，然后服务器从服务器的命令端口发起对客户端的反向连接。这种服务器到客户端的连接被某些防火墙阻止，因此 FTP 常常在没有明确配置为允许此连接的防火墙上失败。解决此问题的客户端变通方法是使用 FTP 被动模式（在 *ftp* 程序中输入 *passive* 或在 GUI 或其他 FTP 客户端中选择等效选项）。在被动模式下，FTP 客户端发起两个连接，这克服了防火墙阻止所有传入连接的问题。然而，被动模式使用服务器上的非特权端口进行数据传输，这有时可能会遇到防火墙的问题。因此，你可能需要尝试主动和被动模式，以确定哪一个效果最好。

FTP 的第二个怪癖与传输模式有关。FTP 客户端通常默认使用 ASCII（纯文本）传输模式，在这种模式下，文件以动态改变字符编码的方式传输，以适应不同操作系统存储纯文本文件的不同方式。（Linux/Unix、Windows 和最初的 Mac OS 都使用了不同的行尾约定，还有一些更奇特的系统使用非 ASCII 编码方法。）使用 ASCII 模式对于纯文本文件效果很好，但这种模式几乎总是损坏二进制文件，例如 tar 包、图形文件、文字处理文档等。你可以在 *ftp* 中使用 *ascii* 和 *binary* 选项；其他 FTP 客户端有类似选项，以设置传输模式。如果不确定，请使用 *binary* 模式；如今大多数文本编辑器都可以处理任何常见的行尾类型，因此以错误格式获取文本文件会导致的问题很小或没有。不过，一些 Linux 配置文件必须使用 Unix 风格的行尾，因此如果你传输此类文件，可能需要注意这个细节。

