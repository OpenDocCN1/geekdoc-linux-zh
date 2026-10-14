
| --- | --- |
| IP Address | 10.0.2.15 |
| Netmask | 255.255.255.0 |
| Default Gateway | 10.0.2.254 |
| Primary Nameserver | 10.0.2.1 |
| Domain Name | redhat.com |
| Hostname | pooh.redhat.com |

图 5-3：示例网络信息

请注意：图 5-3 中的信息仅为示例！你应从你的网络管理员处获取适用于你的网络的正确信息。

第一个对话框要求你输入 IP 和其他网络地址（参见图 5-4）。输入你在安装期间使用的 IP 地址并按 `[Enter]`。安装程序会根据你的 IP 地址尝试猜测你的 Netmask；如果不正确你可以更改它。按 `[Enter]`。安装程序会根据你的 IP 地址和 netmask 猜测 Default gateway 和 Primary nameserver 地址；如果不正确你可以更改它们。

![](img/46f4935125ba89e12897afbe9d77a097_107_0.png)

## Figure 5-4: Configuring TCP/IP

选择 `Ok` 继续。

在第一个对话框之后，你可能会看到第二个对话框。它会提示你输入域名、主机名和其他网络信息（参见 Figure 5-5）。输入系统的域名并按 `[Enter]`；安装程序会将域名带到主机名字段。输入你在域名前使用的主机名以形成完全限定域名（FQDN）。如果你的网络有多个名称服务器，你可以在 Secondary nameserver 和 Tertiary nameserver 字段中输入其他名称服务器的 IP 地址。

选择 `Ok` 继续。

## Figure 5-5: Configuring Networking

请注意：如果您执行的是 FTP 安装，请转到 Installing via FTP 并从那里继续。如果您执行的是 NFS 安装，请继续阅读。

### Installing via NFS

如果您通过 NFS 安装 Red Hat Linux 6.0，现在需要配置您的 NFS 服务器信息。

#### NFS Server Information

下一个对话框请求有关 NFS 服务器的信息（参见 Figure 5-6）。输入 NFS 服务器的名称（必须是完全限定域名）或 IP 地址，以及包含 Red Hat Linux CD 的导出目录的名称。例如，如果 NFS 服务器将 Red Hat Linux CD 挂载在 `/mnt/cdrom` 上，请在 Red Hat directory 字段中输入 `/mnt/cdrom`。如果 NFS 服务器导出的是 Red Hat Linux 安装树的镜像而不是 CD，请输入包含 RedHat 目录的目录。例如，如果你的 NFS 服务器包含目录 `/mirrors/redhat/i386/RedHat`,

![](img/46f4935125ba89e12897afbe9d77a097_108_0.png)

输入 `/mirrors/redhat/i386`。

![](img/46f4935125ba89e12897afbe9d77a097_109_0.png)

Figure 5-6: Installing via NFS

短暂延迟后，下一个对话框将出现。

> 请注意：NFS 安装在安装过程中不需要支持软盘，除非您使用 PCMCIA 设备来完成安装。如果是这样，在提示时您将需要使用 PCMCIA 支持磁盘。

### Installing via FTP

您现在应该看到“FTP Setup”对话框。这里是您将安装程序指向您选择的 FTP 站点的地方（参见 Figure 5-7）。输入您安装来源的 FTP 站点的名称或 IP 地址，以及其中包含您架构的 RedHat 目录的目录名称。例如，如果 FTP 站点包含目录 `/pub/mirrors/redhat/i386/RedHat`,

输入 `/pub/mirrors/redhat/i386`。如果您未使用匿名 FTP，或者如果您需要使用代理 FTP 服务器（例如，如果您位于防火墙后面），请选中复选框，然后另一个对话框将请求 FTP 帐户和代理信息。

![](img/46f4935125ba89e12897afbe9d77a097_110_0.png)

Figure 5-7: Installing via FTP

如果一切都已正确指定，您应该会看到一个消息框，指示 base/hdlist 正在被检索。

继续 Upgrading or Installing 以获取升级或完整安装说明。

### Installing via HTTP

您现在应该看到“HTTP Setup”对话框。这里是您将安装程序指向您选择的 HTTP 站点的地方。输入您安装来源的 HTTP 站点的名称或 IP 地址，以及其中包含您架构的 RedHat 目录的目录名称。例如，如果 HTTP 站点包含

目录 `/pub/mirrors/redhat/i386/RedHat`，输入 `/pub/mirrors/redhat/i386`。如果您未使用匿名 HTTP，或者如果您需要使用代理 HTTP 服务器（例如，如果您位于防火墙后面），请选中复选框，然后另一个对话框将请求 HTTP 帐户和代理信息。

![](img/46f4935125ba89e12897afbe9d77a097_111_0.png)

Figure 5-8: Installing via HTTP

如果一切都已正确指定，您应该会看到一个消息框，指示 base/hdlist 正在被检索。继续 Upgrading or Installing 以获取升级或完整安装说明。

## Upgrading or Installing

在您选择安装方法后，安装程序会提示您进行安装或升级（参见 Figure 5-9）。

## 图 5-9：升级或安装

### 安装

你通常在干净的磁盘分区或一组分区上安装 Red Hat Linux，或覆盖另一份 Linux 安装。

> 请注意： 在另一份 Linux 安装（包括 Red Hat Linux）上安装 Red Hat Linux 不会保留任何来自先前安装的信息（文件或数据）。请确保保存任何重要文件！如果你担心保存现有系统上的当前数据（而不自行备份），你应考虑执行升级。

如果你希望执行完整安装，请选择 `Install`，然后跳至 Installation Class。

### 升级

Red Hat Linux 6.0 的安装过程包括从基于 RPM 技术的前期版本 Red Hat Linux（2.0 及更高版本）升级的能力。升级你的系统会安装

![](img/46f4935125ba89e12897afbe9d77a097_112_0.png)

模块化的 2.2.x 内核以及当前安装在你的机器上的软件包的更新版本。升级过程通过使用 `.rpmsave` 扩展名重命名它们来保留现有配置文件（例如，`sendmail.cf.rpmsave`），并在 `/tmp/upgrade.log` 中留下记录其所采取操作的日志。随着软件的演进，配置文件格式可能会发生变化，因此在整合你的更改之前，你应仔细比较原始配置文件和新文件。如果你希望升级你的 Red Hat Linux 系统，请选择 `Upgrade`。

> 请注意：某些升级的软件包可能需要安装其他软件包才能正常运行。升级程序会处理这些依赖关系，但它可能需要安装额外的软件包。

> 请注意：如果你机器上已安装 X Window System（以及可能较旧版本的 GNOME），你可能会看到一个屏幕提示你安装本发行版中包含的最新版本的 GNOME。

## Installation Class

如果你选择执行完整安装，安装程序会要求你选择一个安装类别（见图 5-10）。如果你选择执行升级，则不会看到此屏幕。你可以从以下安装类别中选择：

## 图 5-10：安装类别

- **Workstation** — 工作站类安装将自动擦除你计算机硬盘上的所有 Linux 分区。此类安装将尝试自动设置双启动环境。

- **Server** — 服务器类安装将自动擦除你计算机硬盘上的所有分区。

- **Custom** — 自定义类安装会让你完全控制与分区相关的问题。如果你过去安装过 Red Hat Linux，自定义类安装与过去的安装最相似。

**请注意：** 如果你选择 `Workstation` 或 `Server`，你计算机上所有驱动器上的部分（或全部）存储数据将被擦除！系统会要求你确认你的决定；然而，请记住，一旦安装程序收到你的确认，擦除就是不可逆的。

**请注意：警告** — 如果你选择执行工作站类或服务器类安装，数据擦除将是不可逆的。

根据安装类型，被擦除数据的严重程度各不相同：

- Workstation-class — 系统上任何硬盘上任何现有的 Linux 分区上的数据将被擦除。

- Server-class — 所有驱动器的所有分区上的数据将被完全擦除，无论是否在现有的 Linux 分区上。

如果你选择工作站类或服务器类安装，你将能够跳过自定义类安装所需的某些步骤。

## SCSI 支持
