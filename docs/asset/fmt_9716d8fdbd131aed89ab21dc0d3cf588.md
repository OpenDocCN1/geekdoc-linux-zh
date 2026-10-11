
进入`/path/to/xxx`目录，找到`xxx.json`。

如果你没有配置 `message command`，则消息将无法送达，Samba 会向发送者报告错误。遗憾的是，WWg 会完全忽略错误代码并继续运行，静静地删除它们，如下：

`"message command = rm %s"`

**默认值：**无 `message command`
示例：`message command = csh -c 'xedit;rm %s' &`

## min print space (S)
此选项设置了用户缓存打印作业之前必须可用的最小空磁盘空间。以千字节（KB）计算。默认值为 0，这意味着用户可以始终缓存打印作业。

另请参考 `printing` 参数。
**默认值：** `min print space = 0`
示例：`min print space = 2000`

## min wins ttl (G)
此选项告诉 `nmbd` 在作为 WINS 服务器运行（`wins support = true`）时，`nmbd` 处理的 NetBIOS 名称的“生存时间”是多少（秒）。你通常不需要更改此参数。默认值为 6 小时（21600 秒）。
**默认值：** `min wins ttl = 21600`

## name resolve (G)
此选项用于 Samba 套件中的程序来确定命名服务并将主机解析为 IP 地址。该选项接受一个由空格分隔的多个名称解析选项字符串。
选项有“lmhosts”、“host”、“wins”和“bcast”。它们导致按以下方式解析名称：

- `lmhosts：` 在 Samba hosts 文件中查找 IP 地址。
- `host：` 执行标准的主机到 IP 地址的解析，使用系统的 `/etc/hosts`、NIS 或 DNS 查找。这种名称解析方法依赖于操作系统，例如在 IRIX 或 Solaris 上，可能由 `/etc/nsswitch.conf` 文件控制。
- `wins：` 向 `wins server` 中列出的 IP 地址 处查询名称。如果未指定 WINS 服务器，将忽略此方法。
- `bcast：` 在 `interfaces` 参数中列出的每个已知本地接口上进行广播。这是名称解析方法中最不可靠的，因为它取决于目标主机是否在本地连接的子网上。
**默认值：** `name resolve = lmhosts wins bcast`

# 附录 C：Samba 手页

示例：`name resolve order = lmhosts bcast host`
这将导致检查本地 hosts 文件，然后尝试广播，最后进行正常的系统主机名查找。

## netbios aliases (G)
这是一组 `nmbd` 将作为 Samba 服务器已知标识的额外名称进行广播的 NetBIOS 名称列表。这允许一台机器在多个名称的列表中出现。如果一台机器正作为浏览服务器或登录服务器运行，则这些名称都不会被作为浏览服务器或登录服务器发布，只有机器的主机名称会带有这些功能发布。
另请参考 `netbios name`。
默认值：空字符串（无额外名称）
示例：`netbios aliases = TEST1 TEST2`

## netbios name (G)
此选项设置了用于标识 Samba 服务器的 NetBIOS 名称。默认情况下，它与主机 DNS 名称的第一个部分相同。如果机器作为浏览服务器或登录服务器，此名称（或主机 DNS 名称的第一个部分）将是这些服务发布时的名称。
另请参考 `netbios aliases`。
默认值：机器的 DNS 名称。
示例：`netbios name = MYNAME`

## nis homedir (G)
从 NIS 映射获取家目录服务器。对于使用自动挂载器的 UNIX 系统，用户的家目录通常会根据需要从远程服务器挂载到工作站上。
当 Samba 登录不是家目录服务器，而是通过 NFS 挂载家目录时，如果登录服务器告诉客户端使用自己作为家目录的 SMB 服务器（通过 SMB 和一个 NFS），则访问用户的家目录将需要两次网络跳转。这可能会非常慢。
此选项允许 Samba 返回家目录服务器为与登录服务器不同的服务器，只要家目录服务器上运行着 Samba 守护进程，它就会直接从目录服务器挂载到 Samba 客户端。当 Samba 向客户端返回家目录服务器时，它将咨询 `homedir map` 中指定的 NIS 映射并返回列出的服务器。
注意，要使此选项生效，必须有一个运行的 NIS 系统，并且带有此选项的 Samba 服务器也必须是一个登录服务器。
默认值：`nis homedir = false`
示例：`nis homedir = true`

# smb.conf (5)

## nt pipe support (G)
此布尔参数控制 `smbd` 是否允许 Windows 客户端连接到 NT SMB 特有的 IPC$ 管道。这是一个开发者调试选项，可以保持不变。
默认值：`nt pipe support = yes`

## nt smb support (G)
此布尔参数控制 `smbd` 是否与 Windows 客户端协商 NT 特有的 SMB 支持。虽然这是一个开发者调试选项且应该保持不变，但基准测试发现，Windows 客户端在将此选项设置为“no”时获得更快的性能。这仍在调查中。如果此选项设置为“no”，则 Samba 提供的 SMB 调用与 Samba 2.0 之前的版本提供的完全一致。如果任何用户在 NT SMB 支持方面遇到问题，此信息可能派用用。
默认值：`nt support = yes`

## null passwords (G)
允许或不允许客户端访问具有空密码的账户。
另请参考 `smbpasswd(5)`。
默认值：`null passwords = no`
示例：`null passwords = yes`

## ole locking compatibility (G)
此参数允许管理员关闭 Samba 内部的字节范围锁定，以兼容 OLE 应用程序。Windows 应用程序使用字节锁定作为进程间通信的形式。将此参数设置为“no”会导致管理器崩溃或溢出问题。
默认值：`ole locking compatibility = yes`
示例：`ole locking compatibility = no`

## only guest (S)
`guest only` 的同义词。

## only user (S)
这是一个布尔选项，控制允许 `user` 列表中的用户名连接。默认情况下此选项是禁用的，以便提供一个供服务器使用的用户名。
注意，这意味着 Samba 不尝试从服务名推断用户名。
另请参考 `user` 参数。
默认值：`only user = False`
示例：`only user = False`

## oplocks (S)
此布尔选项告诉 `smbd` 是否对文件打开请求发布 oplocks（机会性锁）。oplock 可以极大地提高 Samba 上文件访问的速度（约 30% 或更多）。它允许客户端激进地缓存文件，你可以在不稳定的环境中禁用它（在 Windows 中默认开启）。更多信息请参见 Samba 目录下的 `Speed.txt`。可以根据共享选择性地关闭某些文件的 oplocks。在某些系统上，底层操作系统识别 oplocks。这允许通过 Samba 或 NFS 或本地 UNIX 进程访问已锁文件进行数据同步。详情请参见内核 oplocks 参数。
默认值：`opocks = True`
示例：`opocks = False`

## os level (G)
此值控制 Samba 在选举中的自我宣传程度。此参数的值决定了 `nmbd` 是否有机会成为本地广播区域 WORKGROUP 的主浏览器。将其设置为 0 将导致 `smbd` 总是输给 Windows 机器。详情请参见 Samba 目录下的 `BROWSING.txt`。
默认值：`os level = 32`
示例：`os level = 65` ; 这将赢得任何 NT 服务器

## packet size (G)
这是一个废弃的参数，对当前的 Samba 代码没有影响。它留在参数列表中是为了防止破坏旧的 `smb.conf` 文件。

## panic action (G)
这是一个 Samba ，允许在 `smbd` 或 `nmbd` 崩溃时调用系统命令。这通常用于引起对问题发生的注意。
默认值：`panic action = <empty string>`

## passwd chat (G)
此字符串控制 `smbd` 与本地密码更改程序之间更改用户密码时进行的“对话”过程。Samba 描述了一系列响应-接收对，`smbd` 使用这些对来确定向密码程序发送什么以及期望返回什么。如果没有收到预期的输出，则密码不会更改。

此对话序列通常是特定的，具体取决于使用了何种本地密码控制方法（如 NIS 等）。

字符串可以包含宏 `%o` 和 `%n`，分别替换为旧密码和新密码。它还可以包含标准宏 `\n`、`\r`、`\t` 和 `\s` 来提供换行、回车和制表符。

字符串还可以包含 `*`，它可以匹配任何字符序列。

双引号可用于对话序列的任何部分收集字符串，如果后面是句号 `.`，则不设置字符串。同样，如果预期的字符串是句号，则不期待字符串。

请注意，如果 `unix password sync` 参数设置为 `true`，当 `smbpasswd` 文件中的密码更改时，此序列会被调用为 `AS ROOT`，且无需访问旧密码明文。该旧密码明文被设置为 `""`（空字符串）。

另参见 `unix password sync` `passwd program` 和 `password debug`：示例：

```
# smb.conf (5) 285
```
