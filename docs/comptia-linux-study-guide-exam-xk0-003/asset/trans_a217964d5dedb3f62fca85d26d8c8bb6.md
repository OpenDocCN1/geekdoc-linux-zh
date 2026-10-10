
特别是当你自己编译 Samba 时。你还可以使用 `passdb` 后端选项来改变 Samba 存储加密密码的方式；有关详细信息，请查阅 `smb.conf` 手册页。）要向 Samba 密码数据库中添加用户，请向 `smbpasswd` 传递 `-a` 参数和用户名：

```
# smbpasswd -a john
```

如果本地 Linux 用户 **john** 已经存在，此命令将为 **john** 创建一个条目。（`smbpasswd` 程序只会为那些已经拥有标准 Linux 账户的用户创建条目。）当你输入此命令时，系统会提示你两次输入密码，正如使用 Linux `passwd` 命令更改密码时一样。实际上，之后你可以使用 `smbpasswd` 来更改现有用户的 Samba 密码。

![](img/9903a4d3f7abd8dcbef1035fa04a3406_515_0.png)

> 第一次使用 `smbpasswd` 命令时，它会抱怨缺少 `/etc/samba/smbpasswd` 文件。这种抱怨看起来像是一个**错误**信息，但该工具会创建此文件，因此没有异常，也不需要你特别关注。

### 在 Samba 中解析主机名

SMB/CIFS 最初是围绕非 TCP/IP 网络构建的，但如今的实现通常使用 TCP/IP。当涉及到名称解析时，这可能会造成一些混淆，因为不同实现解析名称的方式不同——一些使用 TCP/IP 主机名，但其他使用 NetBIOS 名称，即使它们是通过 TCP/IP 进行通信的。

为了最大限度地提高灵活性，Samba 支持一个名为 `lmhosts` 的文件，通常存储在 `/etc/samba` 中。该文件类似于 Unix `/etc/hosts` 文件，因为它提供主机名到 IP 地址的映射。它由每行一个主机组成，包含一个 IP 地址和一个主机名：

```
172.24.21.34 DANCE
```

这一行将 NetBIOS 名称 `DANCE` 映射到 `172.24.21.34`。如果你在使用 Samba 客户端定位 Windows 服务器时遇到问题，编辑 `lmhosts` 可能可以解决该问题。不过有时，此文件可能毫无用处。特别是，如果你的服务器 IP 地址经常更改（例如，因为你使用 DHCP 动态 IP 地址来配置它们），那么静态的 `lmhosts` 文件会很快过时。在这种情况下，应使用标准的 NetBIOS 名称解析。Samba 默认会尝试这样做，但为了确保万无一失，请检查你的 `smb.conf` 文件中的 `[global]` 部分中的 **name resolve order** 指令：

```
name resolve order = host lmhosts wins bcast
```

每个子系统按列出的顺序尝试。如果某个子系统未包含在列表中，则不会使用它。在此示例中，**host** 使用 Linux 的标准 DNS 查找，**lmhosts** 使用 `lmhosts` 文件，**wins** 使用 DNS 服务器的 NetBIOS 等效物，而 **bcast** 使用 SMB/CIFS 特有的低级广播查找。尝试这四种选项的不同顺序，直到找到一种有效的组合。

# 使用 Samba 共享文件

要通过 Samba 共享文件，你必须创建文件共享定义。这些定义可以非常简单，例如在 `smb.conf` 文件中放在方括号内的共享名称：

```
[sample]
```

这一行创建了一个名为 SAMPLE 的共享。如果直到文件末尾或下一个共享定义之前没有其他行，则该共享是只读的，并提供对 `/tmp` 目录的访问。要使共享有用，你很可能需要更改这些默认设置中的至少一些：

```
[sample]
     comment = Sample Samba Share
     path = /home/samba/sample
     read_only = No
```

此示例设置了三个参数。`comment` 行设置了一个与该共享相关联的注释字符串，它出现在许多客户端的网络浏览器中。它不直接影响共享的功能，但提供描述性注释可以帮助用户找到他们需要的共享。`path` 参数告诉 Samba 要共享哪个目录。默认值是 `/tmp`，但这通常没什么用。此参数的同义词是 `directory`。最后，设置 `read_only = No` 告诉 Samba 用户可以向共享写入。`writeable`、`writable` 和 `write_ok` 参数是 `read_only` 的反义词；也就是说，`writeable = Yes` 等同于 `read_only = No`。关于 Samba 写入权限的一个重要注意事项是，它们仍然在 Linux 文件权限的限制内工作，如第 2 章所述。访问 Samba 服务器的每个用户都是作为普通用户进行访问的。如果该用户无法写入某个目录或文件，Samba 将不允许用户这样做（至少，不使用更高级的参数就不行）。因此，如果你希望你的用户能够写入文件共享，必须确保权限在文件共享中设置得当。实际上，权限必须设置为用户能够读取他们有权读取的共享中的文件。在大多数情况下，0644 (r-w-r-r-r--) 权限对于只读共享中的文件就足够了，但管理读写共享中的权限可能会很复杂。

一个重要的特殊 Samba 共享是 `[homes]` 共享。与大多数共享不同，这个共享不指向单个目录；它指向用户的主目录，如在 `/etc/passwd` 中定义的。如果你希望用户能够在 Samba 服务器上存储他们的个人文件，`[homes]` 共享可能正是你需要的。大多数 `smb.conf` 示例文件都包含一个可工作的 `[homes]` 共享，所以你可能不需要做任何事情来添加它。在实际操作中，此共享显示为用户名——例如，用户 john 看到一个名为 john 的共享。

> Samba 是一个非常复杂且功能强大的服务器，此描述仅展示了最基本的 Samba 信息。如果你需要对 Samba 做更多操作，你应该查阅其详尽的文档或相关书籍，例如我的 Linux Samba Server Administration（Sybex，2001）。

# 使用 Samba 共享打印机

除了文件共享外，Samba 还支持打印机共享。共享打印机的最简单方式是使用 `[printers]` 共享，它类似于 `[homes]` 共享，两者都共享其类型的所有可用实例（分别是打印机或用户主目录）。典型的 `[printers]` 共享定义看起来像这样：

```
[printers]
    comment = 'All Printers'
    path = /var/spool/samba
    print ok = Yes
```

名为 `[printers]` 的共享会导致 Samba 服务器上定义的所有打印机与 SMB/CIFS 客户端共享。此定义依赖于 Samba 来识别打印机。在使用通用 Unix 打印系统（CUPS）进行打印的 Linux 系统上，通常应在 `[global]` 部分中包含一行 `printing = cups`，以告知 Samba 如何与打印系统接口。

除了 `[printers]` 定义之外，你还可以创建按打印机命名的定义。这些定义与 `[printers]` 共享一样，必须包含 `print ok = Yes` 参数或其同义词 `printable = Yes`。默认情况下，Samba 查找与打印机共享同名的本地打印机；然而，你可以使用 `printer name` 参数将 Samba 指向不同的共享，例如使用 `printer name = laser` 打印到名为 `laser` 的本地队列。

Samba 接受的打印作业会提交到 Linux 打印系统，仿佛它们是本地生成的一样。在大多数情况下，这意味着客户端应配置为像打印到 PostScript 打印机一样，即使打印机不是 PostScript 型号。通用的 PostScript 驱动程序通常工作良好，Apple LaserWriter 打印机的驱动程序也是如此。对于彩色打印机，可以尝试使用 QMS magicolor 打印机的驱动程序；这些驱动程序通常与 Samba 配合良好。某些打印机队列的智能过滤器识别本地打印机语言并原样传递此类文件。如果是这种情况，使用打印机制造商提供的驱动程序将起作用。最终，你可能需要进行实验，以确定在客户端端什么方法有效。

# 使用 Windows 域

严重依赖 SMB/CIFS 进行文件共享的大多数网络都部署了域配置，这与更简单的工作组配置在几个方面有所不同。其中最重要的是，域包括一个*域控制器*计算机，它管理域上所有计算机的账户。

如果你想让你的 Samba 服务器（或 Linux SMB/CIFS 客户端）使用 Windows 域，你必须设置几个 `smb.conf` 全局选项：

```
security = Domain
password server = 172.24.21.98
```

