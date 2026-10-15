
任何以`.tmp`结尾的文件，以及任何包含`root`单词的目录。

`veto files = /*Security*/.tmp/*root*/`

示例 2。

禁用 NetTalk 服务器创建的 Apple 特定文件。

`veto files = /.AppleDouble/.bin/.AppleDesktop/Network`

`Trash Folder/`

# 404 附录 E：Samba 手页

- 禁用 oplock 文件 (S)

此参数仅在共享上开启了`oplocks`参数时有效。它允许 Samba 管理员选择性地关闭对匹配通配符列表的选文件的 oplock 授予，类似于一个通配符列表，类似于`oplocks`参数在共享时已开启。

```
veto oplock files = /*Security*/
```

- 卷 (S)

此参数仅在共享上开启了`oplocks`参数时有效。它允许 Samba 管理员选择性地关闭对匹配通配符列表的选文件的 oplock 授予，类似于一个通配符列表，类似于`oplocks`参数在共享时已开启。它允许 Samba 管理员选择性地关闭对匹配通配符列表的选文件的 oplock 授予，类似于一个通配符列表，类似于`oplocks`参数在共享时已开启。它允许 Samba 管理员选择性地关闭对匹配通配符列表的选文件的 oplock 授予，类似于一个通配符列表，类似于`oplocks`参数在共享时已开启。

- 宽链接 (S)

此参数仅在共享上开启了`oplocks`参数时有效。它允许 Samba 管理员选择性地关闭对匹配通配符列表的选文件的 oplock 授予，类似于一个通配符列表，类似于`oplocks`参数在共享时已开启。

- wins 代理 (G)

此参数仅在共享上开启了`oplocks`参数时有效。它允许 Samba 管理员选择性地关闭对匹配通配符列表的选文件的 oplock 授予，类似于一个通配符列表，类似于`oplocks`参数在共享时已开启。

# 附录 E：Samba 手页 405

- wins 服务器 (G)

这指定 `nmbd` 应注册的 WINS 服务器的 IP 地址（或优选 DNS 名称）。如果你有多个子网并希望子网浏览正常工作。

注意：实际上，为特定系统正确生成`valid chars`行是非常困难的。`tino@ausburg.net` 编写了一个名为 "`validchars`" 的包，它可以为给定的客户端系统自动生成一个完整的`valid chars`行。在你的 Samba 源码发行版的 `examples/validchars/` 子目录下查找该包。

- wins 支持 (G)

此布尔值控制 `nmbd` 进程是否作为 WINS 服务器。你不应该在网络中的多一台机器上设置为 true。

- 工作组 (G)

这控制服务器在客户端查询时显示的工作组。注意，此参数还控制了与`security-domain`设置使用的域名。

- 可写 (S)

`writeable` 的同义词。

# 附录 E：Samba 手页 406

- 写入列表 (S)

这是一个被授予服务读写访问权限的用户列表。如果连接的用户在此列表中，他们将获得写入权限，无论`read only`（只读）选项如何设置。该列表可以使用 `@group` 语法包含组名。

- 写入允许 (S)

`writeable` 的同义词。

- 原始写入 (G)

此参数控制服务器在从客户端传输数据时是否支持原始写入 SMB's。你永远不需要更改此参数。

- writeable

一个反同义词是`只读`

# 附录 E：Samba 手页 407

### 示例：

- 只读 = 否
- 可写 = 是
- 写入正常 = 是

# 警告

尽管配置文件允许服务名称包含空格，但在比较时空格仍然会被忽略，但你的客户端可能不会。因此这不应该是一个问题——请注意这种可能性。

与类似，许多客户端（尤其是 DOS 客户端）将服务名称限制在八个字符。`Smbd` 没有这种限制，但如果这些客户端截断了服务名称，连接尝试将会失败。因此，你可能应该将你的服务名称保持在八个字符以内。

使用 `[homes]` 和 `[printers]` 特殊章节可以方便管理员的工作，但默认属性的各种组合可能会很棘手。在设计这些章节时要务必小心。特别要确保打印池目录的权限是正确的。

# 版本

此手页适用于 Samba 套件 2.0 版本。

# 另见

`smbd` (8), `smclient` (1), `nmbd` (8), `testparm` (1), `testprns` (1), `Samba`, `nmblookup` (1), `smbpasswd` (5), `smbpasswd` (8)。

# 作者

原始 Samba 软件和相关工具由 Andrew Tridgill 创建（`samba-bugs@samba.org`）。Samba 现在由 Samba 团队作为一个开源项目进行开发，类似于 Linux 内核的开发方式。

原始的 Samba 手页由 Karl Auer 编写。手页源码已转换为 YODL 格式（另一项优秀的开源软件，可在 `ftp://ftp.icce.rug/pub/unix/` 获取），并由 Jeremy Allison 为 Samba 2.0 发布更新了更新（`samba-bugs@amba.org`）。

# 408 附录 E：Samba 手页

请查看 `samba` (7) 以获取贡献者的完整列表以及如何提交错误报告、注释等详细信息。

# 附录 E.5 SMBCLIENT (1)

# SMBCLIENT (1)

SAMBA

1998年10月23日

# 名称

`SMBCLIENT`—访问服务器上 SMB/CIFS 资源的 FTP 类客户端

# 概要

`smbclient servicename [password] [-s smb.conf] [-B IP addr] [-O scope options][ -R name resolve order] [-M NetBIOS name] [-i scope] [-N -n NetBIOS name] [-d debuglevel] [-P] [-p port] [-l log basename] [-h] -i dest] [-E] [-U username] [-L NetBIOS name] [-t terminal code] [-m max protocol] [-W workgroup] [-T<c|x>IXFqbNan] [-D directory] [-c command string]`

# 描述

此程序是 Samba 套件的一部分。

`smbclient` 是一个可以与 SMB/CIFS 服务器“对话”的客户端。它提供了一个类似于 `ftp` 程序的接口（参见 `ftp` (1)）。操作内容包括从服务器获取文件到本地机器、将文件从本地机器放入服务器、从服务器检索目录信息等。

# 选项

- `servicename` `servicename` 是你想要在服务器上使用的服务名称。服务名称的格式为 `//server/service`，其中 `server` 是提供所需服务的 SMB/CIFS 服务器的 NetBIOS 名称，`service` 是所提供服务的名称。因此，要连接到名为 `smbserver` 的 SMB/CIFS 服务器上的服务，你应该使用 `servicename`

```
//smbserver/printer
```
