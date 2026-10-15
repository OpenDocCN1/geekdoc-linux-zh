
第 10 章“配置网络服务器 I”开始探索 Linux 网络服务器。本章继续这一探索，深入查看另外几种服务器。具体而言，本章涵盖了多种文件共享和交换服务器（网络文件系统、Samba、文件传输协议以及 Apache Web 服务器）、Windows 远程访问工具（`rdesktop` 和虚拟网络计算）以及结构化查询语言数据库工具。

注意：目标 2.7 部分在本章中涵盖，部分在第 6 章“管理磁盘”中涵盖。目标 3.2 部分在本章中涵盖，部分在第 10 章中涵盖。

## 通过网络传递文件

许多网络协议以某种形式涉及文件传输。文件共享和文件传输协议（如服务器消息块/通用互联网文件系统（`SMB/CIFS`）、网络文件系统（`NFS`）和文件传输协议（`FTP`））最直接地体现了这一点。万维网（`WWW`）的协议——超文本传输协议（`HTTP`）是另一种常见的文件传输协议。自然，Linux 可以充当这些协议中任何一种的服务器。

注意：按照我的术语定义，“文件共享协议”用于以这样一种方式共享文件，使得客户端可以像挂载本地分区一样轻松地挂载共享文件目录。`SMB/CIFS` 和 `NFS` 都是文件共享协议。另一方面，文件传输协议缺乏一些对文件共享有帮助的低层功能，因此很少用于此目的。相反，文件传输协议（如 `FTP` 和 `HTTP`）通常借助专门程序（如 `ftp` 客户端程序或 Web 浏览器）来传输完整文件。

## 使用 Samba 传递文件

`Samba` 服务器套件（`http://www.samba.org`）实现了 `SMB/CIFS` 协议套件，该套件用于共享文件和打印机。它通过主配置文件 `smb.conf` 进行控制，该文件通常存储在 `/etc/samba` 中（有时也可能出现在 `/etc`、`/etc/samba.d` 或其他位置）。实际上，`Samba` 套件由两个主要服务器 `smbd` 和 `nmbd` 以及若干辅助程序和服务器组成。通过一个或多个 SysV 启动脚本来启动 `Samba`。通常，要么是一个名为 `samba`（或类似名称）的脚本同时启动 `smbd` 和 `nmbd`，要么这些服务器有以自身命名的独立 SysV 启动脚本。

> 非 Windows 计算机（包括 Linux）可以作为 `Samba` 客户端运行。第 6 章描述了如何使用 Linux 作为 `SMB/CIFS` 客户端。

### 设置基本的 Samba 选项

主要的 `smb.conf` 文件由若干部分组成，每部分都以方括号内的关键字开头。第一部分是 `[global]` 部分，它设置全局选项。随后的部分定义了文件或打印机共享项——`SMB/CIFS` 服务器上命名资源，可用于共享文件或打印机。每个部分都以共享项名称命名；例如，`[common]` 定义了一个名为 `COMMON` 的共享项。在每个部分内部，Samba 参数看起来是这样的：

```text
parameter = value
```

`parameter` 是一个关键字，例如 `security` 或 `netbios name`。它本质上是一个被设置为指定 `value` 的变量名称。这个 `value` 可以是数值（如以秒为单位的时间）、文件名、主机名、布尔值（`Yes` 或 `No`；`True` 或 `False`；1 或 0），或某种其他类型的值。其意图是让 `smb.conf` 文件的含义相当自明，前提是你了解服务器的基本功能。不幸的是，功能如此之多，除非你是专家，否则你可能无法理解所有内容，更不用说生成新条目了。大多数默认的 `smb.conf` 文件包含大量注释以帮助你完成此过程，或者你可以查阅 `smb.conf` man 页，该页面异常完整。

`[global]` 部分中的两个参数特别重要：`workgroup` 和 `encrypt passwords`。`workgroup` 参数设置 NetBIOS 工作组或域的名称。默认值通常是 `WORKGROUP`，但大多数网络都有自己的工作组名称，因此你应该相应调整此参数。如果你不这样做，客户端可能难以通过网络浏览器找到 `Samba` 服务器。`encrypt passwords` 参数是一个布尔值，决定 `Samba` 是使用其自己的加密密码数据库，还是要求使用未加密的密码，并使用标准的 Linux 密码数据库进行身份验证。对于 `Samba` 2.x，默认值是 `No`，但对于 `Samba` 3.0 及更高版本，默认值是 `Yes`。在大多数情况下，`encrypt passwords = Yes` 是最合适的选择，因为自 20 世纪 90 年代中期以来，所有版本的 Windows 都默认要求使用加密密码。

不幸的是，使用加密密码意味着你必须维护一个 Samba 专用的密码数据库。原因是 `SMB/CIFS` 的加密密码交换工具与 Linux 在 `/etc/shadow` 中存储密码的方法不兼容。要创建和维护加密密码数据库，可以使用 `smbpasswd` 实用工具，它默认将数据存储在 `/etc/samba/smbpasswd` 文件中。（此文件有时位于其他位置，特别是如果你自己编译 Samba 时更是如此。你还可以使用 `smbd` 后端选项来更改 Samba 存储加密密码的方式；有关详情，请参阅 `smb.conf` 手册页。）要将用户添加到 Samba 密码数据库中，请将 `smbpasswd` 命令与 `-a` 参数和用户名一起使用：

```bash
# smbpasswd -a john
```

如果本地 Linux 用户 `john` 已经存在，该命令将为 `john` 创建一个条目。（`smbpasswd` 程序只会为那些已经拥有标准 Linux 账户的用户创建条目。）当你输入此命令时，系统会提示你两次输入密码，就像使用 `passwd` 命令更改密码时一样。事实上，你随后可以使用 `smbpasswd` 来更改现有用户的 Samba 密码。

![](img/a78bc63f22351f522ba5ec1fa0c060d2_515_0.png)

> 第一次使用 `smbpasswd` 命令时，它会抱怨缺少 `/etc/samba/smbpasswd` 文件。这种抱怨看起来像错误消息，但该实用程序会创建该文件，因此没有任何问题或需要您关注。

### 在 Samba 中解析主机名

`SMB/CIFS` 最初是围绕非 `TCP/IP` 网络构建的，但如今的实现通常使用 `TCP/IP`。这在名称解析方面可能会带来一些混淆，因为不同实现解析名称的方式各不相同——有些使用 `TCP/IP` 主机名，有些使用 NetBIOS 名称，即使在通过 `TCP/IP` 工作时也是如此。

为了最大化灵活性，Samba 支持一个名为 `lmhosts` 的文件，通常存储在 `/etc/samba` 中。此文件类似于 `Unix /etc/hosts` 文件，因为它提供了主机名到 IP 地址的映射。它每行代表一个主机，包含 IP 地址和主机名：

```
172.24.21.34 DANCE
```

这一行将 NetBIOS 名称 `DANCE` 映射到 `172.24.21.34`。如果你在使用 Samba 客户端查找 Windows 服务器时遇到问题，编辑 `lmhosts` 可能会解决该问题。不过，有时这个文件可能毫无用处。特别是如果你的服务器 IP 地址经常变化（例如，因为你使用带有动态 IP 地址的 DHCP 来配置它们），那么静态的 `lmhosts` 文件会很快过时。在这种情况下，应使用标准的 NetBIOS 名称解析。Samba 默认会尝试这样做，但为了保险起见，请检查 `smb.conf` 文件的 `[global]` 部分中的 `name resolve order` 指令：

```
name resolve order = host lmhosts wins bcast
```

每个子系统按列出的顺序依次尝试。如果列表中省略了某个子系统，则不使用它。在此示例中，`host` 使用 Linux 的标准 DNS 查找，`lmhosts` 使用 `lmhosts` 文件，`wins` 使用 NetBIOS 的 DNS 服务器等效物，而 `bcast` 使用 `SMB/CIFS` 特有的低级别广播查找。尝试这四种选项的不同顺序，直到找到一个有效的组合为止。

要通过 Samba 共享文件，你必须创建文件共享定义。这些定义可以非常简单，只需在 `smb.conf` 文件中用方括号包含一个共享名称即可：

```ini
[sample]
```

这一行创建了一个名为 `SAMPLE` 的共享。如果在文件末尾或下一个共享定义之前没有其他行，该共享是只读的，并提供对 `/tmp` 目录的访问。为了使该共享有用，你很可能需要更改这些默认值中的至少一些：

```ini
[sample]
  comment = Sample Samba Share
  path = /home/samba/sample
  read only = No
```

此示例设置了三个参数。`comment` 行设置一个与共享关联的注释字符串，该字符串在许多客户端的网络浏览器中显示。它不直接影响共享的功能，但提供描述性注释可以帮助用户找到他们所需的共享。`path` 参数告诉 Samba 共享哪个目录。默认值是 `/tmp`，但这通常不是很有用。此参数的同义词是 `directory`。最后，设置 `read only = No` 告诉 Samba 用户可能写入该共享。`writable` 和 `write ok` 参数是 `read only` 的反义词；也就是说，`writable = Yes` 等同于 `read only = No`。关于 Samba 写入权限的一个重要注意事项是，它们仍然在 Linux 文件权限的约束内工作，如第 2 章所述。每个访问 Samba 服务器的用户都以普通用户身份进行。如果该用户无法写入目录或文件，Samba 不会允许用户这样做（至少，在不使用更高级参数的情况下不会）。因此，如果你希望用户能够写入文件共享，你必须确保在文件共享中正确设置了权限。事实上，权限也必须设置以允许用户读取他们应该能够读取的共享中的文件。在大多数情况下，`0644` (`-rw-r--r--`) 权限对于只读共享中的文件非常合适，但管理读写共享中的权限可能很复杂。

一个重要的特殊 Samba 共享是 `[homes]` 共享。与大多数共享不同，这个共享不指向单个目录；它指向用户的家目录，如 `/etc/passwd` 中定义的。如果你想让用户能够在 Samba 服务器上存储他们的个人文件，`[homes]` 共享可能正是你需要的。大多数 `smb.conf` 示例文件都包含一个可工作的 `[homes]` 共享，因此你可能不需要做任何事来添加一个。在运行中，该共享显示为用户名\mdash例如，用户 `john` 看到一个名为 `JOHN` 的共享。

![](img/a78bc63f22351f522ba5ec1fa0c060d2_516_0.png)

> Samba 是一个非常复杂且功能强大的服务器，上述描述几乎只介绍了最基本的 Samba 信息。如果你需要用 Samba 做更多事情，你应该查阅其详尽的文档或关于该主题的书籍，例如我的 *Linux Samba Server Administration*（Sybex, 2001）。

### 通过 Samba 共享打印机

除了文件共享外，Samba 还支持打印机共享。共享打印机的最简单方法是使用 `[printers]` 共享，它与 `[homes]` 共享类似，因为两者都共享其类型的每个可用实例（分别是打印机或用户家目录）。典型的 `[printers]` 共享定义如下所示：

```ini
[printers]
    comment = 'All Printers'
    path = /var/spool/samba
    print ok = Yes
```

名为 `[printers]` 的共享会导致 Samba 服务器上定义的所有打印机与 `SMB/CIFS` 客户端共享。此定义依赖于 Samba 能够识别打印机。在使用 Common Unix Printing System (`CUPS`) 进行打印的 Linux 系统上，你通常应在 `[global]` 部分中包含一行 `printing = cups`，以告诉 Samba 如何与打印系统接口。

作为 `[printers]` 定义的替代或补充，你可以创建按打印机命名的定义。这些定义，与 `[printers]` 共享一样，必须包含 `print ok = Yes` 参数或其同义词 `printable = Yes`。默认情况下，Samba 查找与打印机共享同名的本地打印机；但是，你可以使用 `printer name` 参数将 Samba 指向不同的共享，例如使用 `printer name = laser` 打印到名为 `laser` 的本地队列。

Samba 接受的打印作业将提交给 Linux 打印系统，仿佛它们是本地生成的一样。在大多数情况下，这意味着即使打印机不是 PostScript 型号，客户端也应配置为似乎正在打印到 PostScript 打印机。通用 PostScript 驱动程序通常工作良好，Apple LaserWriter 打印机的驱动程序也是如此。对于彩色打印机，请尝试使用 QMS magicolor 打印机的驱动程序；这些驱动程序通常与 Samba 配合得很好。某些打印队列的智能过滤器识别原生打印机语言并原样传递此类文件。如果是这种情况，使用打印机制造商提供的驱动程序将起作用。最终，你可能需要实验以确定在客户端端什么工作得最好。

### 使用 Windows 域

大多数严重依赖 `SMB/CIFS` 进行文件共享的网络都部署了域配置，这与更简单的工作组配置在几个方面有所不同。其中最重要的是，域包含一个域控制器计算机，它管理域上所有计算机的账户。

如果你想让你的 Samba 服务器（或 Linux `SMB/CIFS` 客户端）使用 Windows 域，你必须设置几个 `smb.conf` 全局选项：

```ini
security = Domain
password server = 172.24.21.98
```

### 设置 Samba 安全选项

`security`（安全）选项告诉 Samba 及相关工具如何处理身份验证。默认值 `user`（用户）指示 Samba 针对本地账户数据库验证用户，如“设置基本 Samba 选项”中所述。在 Windows 域中可以使用三种不同的选项：

- `Server`（服务器）：设置 `security = Server` 会导致 Samba 使用 Windows NT 4 协议与域控制器通信，但不会完全加入域。此配置易于设置，但 Samba 开发者不推荐使用。

- `Domain`（域）：设置 `security = Domain` 会导致 Samba 作为完整的域成员，使用 Windows NT 4 协议与域控制器通信。在首次访问控制器之前，必须通过输入 `net join member -U adminuser` 来加入域，其中 `adminuser` 是域控制器上具有管理域控制器账户数据库权限的账户，以便为 Linux 系统创建特殊账户。系统会要求输入密码，如果一切顺利，随后将看到一条提示已加入域的消息。

- `ADS`：设置 `security = ADS` 的工作原理与 `security = Domain` 非常相似，不同之处在于系统使用的是更复杂的活动目录（AD）协议，而不是较旧的 NT 4 协议。然而，此配置在 Linux 中可能比较挑剔（不稳定）。

设置好 `security` 选项，`password server`（密码服务器）指向域控制器计算机（可以指定 IP 地址或 NetBIOS 名称），并在必要时为计算机创建域账户后，Samba 现在应该将身份验证任务委托给域控制器。

如果身份验证成功，但用户没有本地 Linux 账户，则用户将无法登录。如果希望用户在域中的存在及成功验证就足够了，可以使用 `add user script`（添加用户脚本）Samba 选项：

```
add user script = /usr/sbin/useradd -m %u
```

此配置导致 Samba 在域登录成功但不存在本地用户时，运行带有 `-m` 选项的 `useradd`（用于创建用户主目录）。`%u` 选项是一个 Samba 变量，指代用户名。

许多 Linux 系统仅使用 Windows 域进行 Samba 身份验证。然而，也可以更全面地使用 Windows 域。Winbind 工具（有时称为 `winbindd`，即服务器二进制文件的名称）可以将 Windows 域账户链接到主要的 Linux 账户系统中。如此配置后，计算机将使用 Windows NT 4 域或 AD 控制器为普通文本模式登录、GUI 登录、电子邮件检索、FTP 访问等进行用户验证。配置 Winbind 可能比较棘手，因为它需要在 `smb.conf` 文件、`/etc/nsswitch.conf` 文件以及 `/etc/pam.d` 目录下的一个或多个文件中设置选项。配置错误可能导致系统无法接受任何登录。第 12 章“保护 Linux”更详细地描述了这些身份验证工具，但如果你想配置 Winbind，可能需要查阅更高级的文档，例如关于 Samba 或网络身份验证的书籍。

### 使用 NFS 传输文件

`Samba` 主要是用于与 Windows 客户端共享文件的工具。虽然它可以用于与 Linux 或 Unix 客户端共享文件，但 `SMB/CIFS` 并非针对这些系统设计。早期版本的 `SMB/CIFS` 不支持 Unix 风格的所有者和权限。后期版本增加了此功能，但由于 Windows 和 Unix 的所有者和权限模型往往相互冲突，该功能通常工作得不太完美。Linux 和 Unix 系统之间文件共享的更好选择是 *网络文件系统（NFS）*，这是 Sun 公司为 Unix 设计的网络文件共享工具。要使用 NFS，必须配置要共享的目录（在 NFS 中称为 *exports* 导出）并启动服务器。服务器运行后，还可以使用实用程序来修改或查看配置。
