
Samba 将强制仅将日志条目发送到 syslog 进程。

### 国际化 (Internationalization)

Samba 对非英语的支持是另一个过时的领域。Samba 2.2.x 服务器应用程序在网络发送请求和响应时不支持 Unicode 字符串。这意味着 `smbd` 和 `nmbd` 依赖某些 `smb.conf` 参数来获取 CIFS 客户端正在使用的代码页信息。

所有 DOS 代码页都支持 ASCII（即英语）字符，因此支持英语客户端。这意味着支持使用英语代码页和另一种语言的 Windows 客户端。目前 Samba 服务器不支持支持两个非英语客户端（例如希腊语和中文）。

Unicode 支持计划在 Samba 3.0 版本中完成。一旦实现，这里描述的所有代码页和字符集参数将被废弃。

除了客户端使用的代码页外，某些 Unix 文件系统使用字符集在磁盘上存储文件名。图 5.3 阐了 Samba 如何弥补 DOS 代码页与 Unix 字符集之间的差距。

### 探索 Samba 的 smb.conf 文件

图 5.3
Samba 与 DOS 代码页和 Unix 字符集的交互。

![](img/e6dc042fe420c610acdd193e834a4772_92_0.png)

### client code page 参数

DOS 代码页用于使用两个字节来定义非 ASCII 字符，而不是表示 7 位 ASCII 字符所需的单个字节。该代码页允许使用扩展字符，如 á 或 ó。

在 CIFS 协议协商阶段，没有方法确定客户端所使用的代码页。因此，有必要手动配置 `client-code-page` 参数。如果需要支持使用简体中文代码页的 Windows 客户端，则需要在 `smb.conf` 的 `[global]` 部分中包含以下参数。

```
client code page = 936
```

936 是随 Samba 安装的预定义代码页。表 5.4 列出了当前支持的代码页。

> 可以使用 Samba 附带的 `make_smbcodepage` 工具创建新的代码页。更多细节请参阅 `make_smbcodepage` 的 man 页。

### 表 5.4 Samba 软件包代码页

| 代码页 | 描述 |
| :--- | :--- |
| 437 | MS-DOS Latin US |
| 737 | Windows 95 Greek |
| 850 | MS-DOS Latin 1 (默认) |
| 852 | MS-DOS Latin 2 |
| 861 | MS-DOS Icelandic |

### 表 5.4 续

| 代码页 | 描述 |
| :--- | :--- |
| 866 | MS-DOS Cyrillic |
| 932 | MS-DOS Japanese Shift-JIS |
| 936 | MS-DOS Simplified Chinese (简体中文) |
| 949 | MS-DOS Korean Hangul |
| 950 | MS-DOS Traditional Chinese (繁体中文) |

选择了 Shift-JIS (932) 代码页；可以定义一个编码系统参数，以确定传入的 Shift-JIS 日语字符如何从客户端使用的代码页映射到 Unix 文件系统的文件名。有关编码系统页的更多细节，请参考 `smb.conf` 页。

### code page directory 参数

这是一个方便参数，接受一个绝对目录路径，告知 `smbd` 去查找 DOS 代码页。厂商常用的一个位置是：

```
code page directory = /etc/samba/codepages
```

正常的默认配置会期望 DOS 代码页存在 `/usr/local/samba/lib/codepages` 中。

### character set 参数

如果 Unix 系统使用与 Microsoft 客户端相同的代码页，将会容易得多。当然，如果它们真的已经做到了，我不会这样心心愿地表达这种想法。如果需要将 DOS 代码页版本的文件名转换为服务器使用的 Unix 字符，则必须定义它并使其与 Samba 使用的静态映射之一匹配。表 5.5 给出了 Samba 2.2 支持的有效映射。

### 5.5 Samba 的 Unix 字符集与等效 DOS 代码页映射

| 字符集 | 支持的 DOS 代码页 |
| :--- | :--- |
| 西欧 (ISO8859-1) | 850 |
| 东欧 (ISO8859-2) | 852 |
| 俄语西里 (ISO8859-5) | 866 |
| 希腊 (ISO8859-7) | 737 |
| 俄语西里的备映射 (KOI8-R) | 866 |

通常情况下，`character set` 参数可以保持默认设置（即没有从 DOS 代码页的字符映射）。

## 探索 Samba 的 smb.conf

### 状态信息

除了 Samba 的静态配置文件，还维护了某些运行时信息以帮助配置服务器状态。

### lock directory 参数

`lock directory` 接受一个目录路径，决定 Samba 写入数据库文件、浏览列表和 WINS 数据库（如果启用了 WINS 支持）。默认锁目录在编译时确定，取决于所启用的配置选项。在完全默认的配置下，这是正常的 `/usr/local/samba/var/locks`。

有必要手动指定锁目录的一个实际示例是：默认锁目录位于 NFS 挂载的文件系统上的情况。许多站点使用 `/usr/local/` 下的文件系统来共享其网络特有的工具和实用程序。你可以在 Samba 服务器之间共享二进制文件，但无法共享锁目录。锁目录必须位于本地磁盘上，且对每个服务器是唯一的。

在 Samba 2.2.x 下，锁目录的内容在系统重启后持久存在也是一个要求。存储在锁目录中的某些文件包含服务器状态的信息。`/var/cache` 目录为此提供了一个合理的位置，也是许多 Samba 预编译包使用的位置。

```
lock directory = /var/cache/samba
```

### 总结

虽然 `smb.conf` 参数很少，但只需要设置你想要使用的，或者如果你像我一样过度谨慎。例如，这可能是我能想象到的最简单的可用 `smb.conf` 文件。这是一个不提供文件或打印共享的简单服务器。

```
[global]

    workgroup = STY-SAMBA
```

在本节中，我们涵盖了 `smb.conf` 的：

- 运行时变量
- 其他 NetBIOS 参数
- 连接日志
- 状态信息

### 问答

-问：修改 `smb.conf` 后需要重启 Samba 吗？
答：对于大多数更改，你不需要。Samba 会定期检查配置是否变化。如果有，向进程发送一个 HUP 信号。
-问：Samba 可以同时属于多个工作组吗？
答：不，Samba 只能属于一个。

![](img/e6dc042fe420c610acdd193e834a4772_96_0.png)

## 第6 章

### SWAT 和其他 GUI 工具

上一节中，我们开始探索许多 `smb.conf`。虽然剩余章节将继续呈现文本形式，但我们将转向基于 Web 的工具。

### SWAT

SWAT 是一个用于 Samba 的微型 Web 服务器和 CGI。SWAT 在每个页面都会放置所有配置选项的链接，让管理员轻松理解更改的影响。SWAT 作为大多数预编译包的一部分安装。如果你是从源码编译的，Samba 配置脚本支持一个选项来告诉 Samba 放置 HTML 文件：

```
configure --with-swatdir=/usr/share/swat
```

如果不指定 `--with-swatdir`（最常见的情况），SWAT HTML 文件安装在 `$(prefix)/swat`（即 `/usr/local/samba/swat`）。

### inetd 服务器

`inetd` 服务器由 `/etc/inetd.conf` 配置文件控制。该文件的实际格式在不同 Unix 之间、不同发行版之间可能不同，因此关于如何添加新条目的权威答案是咨询 `inetd.conf(8)` man 页。在配置 `inetd.conf` 之前，`etc/services` 文件中必须存在以下：

```
### 将 swat 分配到端口 901
swat 901/tcp
```

使用端口 901/tcp 更多是因为是因为技术原因。可以通过修改 `/etc/services` 中的项来配置 SWAT 使用替代端口。接下来，需要在 `/etc/inetd.conf` 添加如下行：

```
swat stream tcp nowait.400 root /usr/local/samba/bin/swat swat
```
