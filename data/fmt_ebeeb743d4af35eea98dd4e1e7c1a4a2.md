
`[global]` 部分中的两个参数特别重要：`workgroup` 和 `encrypt passwords`。`workgroup` 参数设置 NetBIOS 工作组或域的名称。默认值通常是 `WORKGROUP`，但大多数网络有自己的工作组名称，因此你应该适当调整此参数。如果你不这样做，客户端使用其网络浏览器时可能会难以找到 Samba 服务器。`encrypt passwords` 参数是一个布尔值，它确定 Samba 是使用其自己的加密密码数据库，还是要求未加密的密码并使用标准 Linux 密码数据库进行身份验证。Samba 2.x 的默认值为 `No`，但 Samba 3.0 及更高版本的默认值为 `Yes`。在大多数情况下，`encrypt passwords = Yes` 是最合适的选择，因为自 1990 年代中期以来所有版本的 Windows 默认都要求使用加密密码。

不幸的是，使用加密密码意味着你必须维护一个 Samba 专用的密码数据库。原因是 SMB/CIFS 的加密密码交换工具与 Linux 用于在 `/etc/shadow` 中存储密码的方法不兼容。要创建和维护加密密码数据库，你可以使用 `smbpasswd` 实用程序，它默认将数据存储在 `/etc/samba/smbpasswd` 文件中。（此文件有时位于其他位置，特别是当你自己编译 Samba 时。你还可以使用 `passdb` 后端选项来改变 Samba 存储加密密码的方式；有关详细信息，请查阅 `smb.conf` 手册页。）要向 Samba 密码数据库中添加用户，请向 `smbpasswd` 传递 `-a` 参数和用户名：

```
# smbpasswd -a john
```

如果本地 Linux 用户 `john` 已经存在，此命令将为 `john` 创建一个条目。（`smbpasswd` 程序只会为那些已经拥有标准 Linux 账户的用户创建条目。）当你输入此命令时，系统会提示你两次输入密码，正如使用 Linux `passwd` 命令更改密码时一样。实际上，之后你可以使用 `smbpasswd` 来更改现有用户的 Samba 密码。

![](img/9903a4d3f7abd8dcbef1035fa04a3406_515_0.png)

> 第一次使用 `smbpasswd` 命令时，它会抱怨缺少 `/etc/samba/smbpasswd` 文件。这种抱怨看起来像是一个错误信息，但该工具会创建此文件，因此没有异常，也不需要你特别关注。

### 在 Samba 中解析主机名

SMB/CIFS 最初是围绕非 TCP/IP 网络构建的，但如今的实现通常使用 TCP/IP。当涉及到名称解析时，这可能会造成一些混淆，因为不同实现解析名称的方式不同——一些使用 TCP/IP 主机名，但其他使用 NetBIOS 名称，即使它们是通过 TCP/IP 进行通信的。

为了最大限度地提高灵活性，Samba 支持一个名为 `lmhosts` 的文件，通常存储在 `/etc/samba` 中。该文件类似于 Unix `/etc/hosts` 文件，因为它提供主机名到 IP 地址的映射。它由每行一个主机组成，包含一个 IP 地址和一个主机名：

```
172.24.21.34 DANCE
```

这一行将 NetBIOS 名称 `DANCE` 映射到 `172.24.21.34`。如果你在使用 Samba 客户端定位 Windows 服务器时遇到问题，编辑 `lmhosts` 可能可以解决该问题。不过有时，此文件可能毫无用处。特别是，如果你的服务器 IP 地址经常更改（例如，因为你使用 DHCP 动态 IP 地址来配置它们），那么静态的 `lmhosts` 文件会很快过时。在这种情况下，应使用标准的 NetBIOS 名称解析。Samba 默认会尝试这样做，但为了确保万无一失，请检查你的 `smb.conf` 文件中的 `[global]` 部分中的 `name resolve order` 指令：

```
name resolve order = host lmhosts wins bcast
```

每个子系统按列出的顺序尝试。如果某个子系统未包含在列表中，则不会使用它。在此示例中，`host` 使用 Linux 的标准 DNS 查找，`lmhosts` 使用 `lmhosts` 文件，`wins` 使用 DNS 服务器的 NetBIOS 等效物，而 `bcast` 使用 SMB/CIFS 特有的低级广播查找。尝试这四种选项的不同顺序，直到找到一种有效的组合。

### 使用 Samba 共享文件

要通过 Samba 共享文件，你必须创建文件共享定义。这些定义可以非常简单，例如在 `smb.conf` 文件中放在方括号内的共享名称：

```
[sample]
```

这一行创建了一个名为 `SAMPLE` 的共享。如果直到文件末尾或下一个共享定义之前没有其他行，则该共享是只读的，并提供对 `/tmp` 目录的访问。要使共享有用，你很可能需要更改这些默认设置中的至少一些：

```
[sample]
     comment = Sample Samba Share
     path = /home/samba/sample
     read_only = No
```

此示例设置了三个参数。`comment` 行设置了一个与该共享相关联的注释字符串，它出现在许多客户端的网络浏览器中。它不直接影响共享的功能，但提供描述性注释可以帮助用户找到他们需要的共享。`path` 参数告诉 Samba 要共享哪个目录。默认值是 `/tmp`，但这通常没什么用。此参数的同义词是 `directory`。最后，设置 `read_only = No` 告诉 Samba 用户可以向共享写入。`writeable`、`writable` 和 `write_ok` 参数是 `read_only` 的反义词；也就是说，`writeable = Yes` 等同于 `read_only = No`。关于 Samba 写入权限的一个重要注意事项是，它们仍然在 Linux 文件权限的限制内工作，如第 2 章所述。访问 Samba 服务器的每个用户都是作为普通用户进行访问的。如果该用户无法写入某个目录或文件，Samba 将不允许用户这样做（至少，不使用更高级的参数就不行）。因此，如果你希望你的用户能够写入文件共享，必须确保权限在文件共享中设置得当。实际上，权限必须设置为用户能够读取他们有权读取的共享中的文件。在大多数情况下，`0644` (`r-w-r-r-r--`) 权限对于只读共享中的文件就足够了，但管理读写共享中的权限可能会很复杂。

一个重要的特殊 Samba 共享是 `[homes]` 共享。与大多数共享不同，这个共享不指向单个目录；它指向用户的主目录，如在 `/etc/passwd` 中定义的。如果你希望用户能够在 Samba 服务器上存储他们的个人文件，`[homes]` 共享可能正是你需要的。大多数 `smb.conf` 示例文件都包含一个可工作的 `[homes]` 共享，所以你可能不需要做任何事情来添加它。在实际操作中，此共享显示为用户名——例如，用户 `john` 看到一个名为 `john` 的共享。

> Samba 是一个非常复杂且功能强大的服务器，此描述仅展示了最基本的 Samba 信息。如果你需要对 Samba 做更多操作，你应该查阅其详尽的文档或相关书籍，例如我的 *Linux Samba Server Administration*（Sybex，2001）。

### 使用 Samba 共享打印机

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

### 使用 Windows 域

严重依赖 SMB/CIFS 进行文件共享的大多数网络都部署了域配置，这与更简单的工作组配置在几个方面有所不同。其中最重要的是，域包括一个域控制器计算机，它管理域上所有计算机的账户。

如果你想让你的 Samba 服务器（或 Linux SMB/CIFS 客户端）使用 Windows 域，你必须设置几个 `smb.conf` 全局选项：

```
security = Domain
password server = 172.24.21.98
```

`security` 选项用于告知 Samba 及相关工具如何处理身份验证。默认值 `User` 会指示 Samba 针对本地账户数据库验证用户，如“设置基本 Samba 选项”中所述。在 Windows 域中可以使用以下三种不同的选项：

- `Server`：设置 `security = Server` 会使 Samba 使用 Windows NT 4 协议与域控制器通信，但不会完全加入域。此配置设置简单，但 Samba 开发者不建议使用。

- `Domain`：设置 `security = Domain` 会使 Samba 作为完整的域成员，使用 Windows NT 4 协议与域控制器通信。在首次访问控制器之前，你必须通过输入 `net join member -U adminuser` 来加入域，其中 `adminuser` 是域控制器上的一个账户，具有对域控制器账户数据库的管理访问权限，以便为 Linux 系统创建特殊账户。系统会提示你输入密码，如果一切顺利，随后你会看到一条消息，表示你已成功加入域。

- `ADS`：设置 `security = ADS` 的作用与 `security = Domain` 类似，不同之处在于系统使用的是更复杂的 Active Directory (AD) 协议，而不是较旧的 NT 4 协议。然而，此配置在 Linux 下可能比较棘手。

在设置了 `security` 选项，并配置指向域控制器计算机的 `password server`（可以指定 IP 地址或 NetBIOS 名称），以及根据需要为计算机创建域账户后，Samba 现在应当委托域控制器处理身份验证任务。

如果身份验证成功但用户没有本地 Linux 账户，用户将无法登录。如果你希望用户在域上存在且成功认证就足够了，可以使用 `add user script` Samba 选项：

```
add user script = /usr/sbin/useradd -m %u
```

此配置使得当域登录成功但不存在本地用户时，Samba 会运行带有 `-m` 选项（用于创建用户主目录）的 `useradd` 命令。（`%u` 选项是一个 Samba 变量，指代用户名。）

许多 Linux 系统仅将 Windows 域用于 Samba 身份验证。不过，也可以更综合地利用 Windows 域。`Winbind` 工具（有时称为 `winbind`，即服务器二进制文件的名称）可以将 Windows 域账户链接到主要的 Linux 账户系统中。完成此配置后，计算机将使用 Windows NT 4 域或 AD 控制器来验证普通文本模式和图形界面登录、电子邮件检索、FTP 访问等用户。配置 Winbind 可能很棘手，因为它需要设置 `smb.conf` 文件、`/etc/nsswitch.conf` 文件以及 `/etc/pam.d` 中一个或多个文件中的选项。配置错误可能导致系统无法接受任何登录。第 12 章“保护 Linux”更详细地描述了这些身份验证工具，但如果你想配置 Winbind，建议查阅更高级的文档，例如关于 Samba 或网络身份验证的书籍。

Samba 主要是一个用于与 Windows 客户端共享文件的工具。虽然它可以用于与 Linux 或 Unix 客户端共享文件，但 SMB/CIFS 并非为这些系统而设计。早期的 SMB/CIFS 版本不支持 Unix 风格的拥有者和权限。后续版本增加了此功能，但由于 Windows 和 Unix 的拥有者和权限模型往往相互冲突，其功能经常运行不完美。Linux 和 Unix 系统之间文件共享的更好选择是网络文件系统（NFS），它由 Sun 公司设计，作为 Unix 的网络文件共享工具。要使用 NFS，你必须配置要共享的目录（在 NFS 中称为导出），并启动服务器。你还可以使用工具在服务器运行期间修改或查看配置。

## 配置 NFS 服务器

在 Linux 中，NFS 服务器配置通过一个名为 `/etc/exports` 的文件进行处理。该文件包含以要共享的目录开头的行，后跟可以访问该目录的主机名或 IP 地址列表，选项放在括号内：

```
/home taurus(rw,async) littrow(ro)
/opt taurus(ro)
```

这些示例共享两个目录：`/home` 和 `/opt`。两台计算机（`taurus` 和 `littrow`）可以访问 `/home`，但只有 `taurus` 可以写入该目录（因为只有 `taurus` 的定义包含 `rw`（读/写）选项；`littrow` 的定义包含 `ro`（只读）指定。`taurus` 的 `/home` 描述还包含 `async` 选项，这可以提高性能，但如果在发生磁盘错误时，会略微增加数据丢失的风险。`/opt` 目录仅与 `taurus` 共享，且该系统不能写入该目录。

为了提供 NFS 支持，你必须运行一个 NFS 服务器程序。（大多数 Linux 的 NFS 服务器程序也依赖特殊的内核功能，但它们默认几乎总是编译进内核中。）通常，此程序由 SysV 启动脚本运行，通常称为 `nfsserver` 或类似名称。检查此启动脚本，并在修改 `/etc/exports` 文件后，如有必要，启动或重启它。

### 动态修改或查看 NFS 配置

除了 `/etc/exports`，NFS 还通过 `exportfs` 命令启用对其导出的非永久性更改。在没有选项的情况下使用时，`exportfs` 显示活动 NFS 导出的列表，类似于 `/etc/exports` 的内容，但每个导出占一行（因此，如果你列出一个目录导出到三个系统或网络，`exportfs` 输出中该目录会出现三行）。添加选项允许你修改系统的 NFS 导出。表 11.1 总结了这些选项中最重要的一些。`exportfs` 手册页提供了更不常见选项的详细信息。

#### 表 11.1 常见的 exportfs 选项

| 选项 | 说明 |
| :--- | :--- |
| `-a` | 读取 `/etc/exports` 并导出其中列出的所有目录。（与 `-u` 一起使用时，取消导出所有目录。） |
| `-r` | 重新导出所有目录。这具有取消导出未列在 `/etc/exports` 中的目录的效果。 |
| `-o options` | 实现指定的 `options`，其形式与 `/etc/exports` 中的形式相同。 |
| `-u` | 取消导出一个或多个目录。 |
| `-f` | 刷新并重建导出表。 |
| `-v` | 在程序输出中添加详细消息。 |

在使用 `exportfs` 添加或删除导出时，你以 `client:/export/directory` 的形式指定客户端和目录。在导出新目录时，你不需要指定表 11.1 中的任何选项，但你必须使用 `-u` 选项来取消导出目录。例如，假设你的 NFS 服务器当前正在导出 `/var/www` 到 `192.168.23.0/24`，作为让本地用户编辑 Web 服务器文件的一种手段。你想将此目录移动到 `/var/apache/websites`。你可以通过输入以下命令来实现这些更改：

```
# exportfs -u 192.168.23.0/24:/var/www
# exportfs 192.168.23.0/24:/var/apache/websites
```

然而，这种更改是临时的；你也应该编辑 `/etc/exports`。事实上，你可能更喜欢先编辑 `/etc/exports`，然后输入 `exportfs -r`，从而实现你的更改。

管理 NFS 的第二个工具是 `showmount`，它显示当前 NFS 活动的信息。在没有选项的情况下使用时，该工具显示当前使用服务器的计算机的 IP 地址。表 11.2 总结了 `showmount` 最常见的选项。

#### 表 11.2 常见的 showmount 选项

| 选项 | 选项缩写 | 说明 |
| :--- | :--- | :--- |
| `--all` | `-a` | 显示客户端的 IP 地址以及它们正在使用的目录 |
| `--directories` | `-d` | 显示服务器当前共享的目录，但不显示客户端身份 |
