

## RS-232 串行设备

连接到标准 RS-232 串行端口的打印机只需要启用该串行端口，并正确设置 printcap 条目即可。为了适应调制解调器和其他串行设备，串行支持通常默认内置在内核中，并且这些端口也支持打印功能。第 11 章讨论了 Linux 对 RS-232 串行连接的支持。

## USB 设备

在 Linux 中，USB 打印机需要特别注意，因为需要 USB 补丁版的 2.2.x 或 2.4.x 内核。特别是，您需要基本 USB 支持（包括支持 OHCI 或 EHCI USB 控制器，具体取决于您的 USB 端口使用哪一种）以及 USB 打印机支持。一旦编译好这些支持并安装了相应的设备文件，就可以使用 `/dev/usb/lp*n*` 设备访问 USB 打印机，其中 *n* 是从 0 开始的数字。（该文件可能位于 /dev 的子目录中，例如 /dev/usb。）第 11 章更详细地介绍了 USB 设备。

## 远程打印

在网络上，工作站可以配置为向连接到网络中另一台主机上的打印机打印，或者向带有内置网络接口卡（NIC）的独立打印机打印。在第一种情况下，主机可能是 Linux 或 Unix 机器，也可能是运行某种版本 Microsoft Windows 的机器。在第二种情况下，打印机运行自己的服务器软件，其功能与 Linux/Unix 或 Windows 打印服务器完全相同。

## Linux 到 Linux

对于 Linux 到 Linux 的打印，您需要在服务器（连接打印机的机器）和客户端（提交打印任务的机器）上配置打印。除了基本的网络设置外，整体配置有两个步骤：

- 1. 配置服务器以向其控制的打印机打印。您应该测试如本章前面所述的本地打印功能。您可以手动执行此配置，也可以通过 Printconf 或 Webmin 等 GUI 实用工具执行。
- 2. 配置客户端以向由服务器托管的网络打印机打印，如本章前面所述。您可以手动执行此配置，也可以通过 Printconf 或 Webmin 等 GUI 实用工具执行。

前面讨论中已经涵盖了这两个步骤。一旦您将打印服务器配置为本地打印，它就自动配置为接受远程打印任务，至少如果您使用的是随 Red Hat 7.3 提供的 LPRng。这使得打印机设置非常容易，但这也可能是一个巨大的风险，因为这意味着任何恶作剧者都可以向您的打印机发送大量打印任务。旧的 lpd 打印系统默认不那么“开放”。若要使用旧的 lpd 接受远程打印任务，您必须在 /etc/hosts.lpd 文件中（或在 /etc/hosts.equiv 中，但该文件授予使用一系列其他服务的权限，因此在大多数情况下最好不要使用它）输入 lpd 将接受任务的计算机的名称或 IP 地址。

要阻止随机互联网系统使用您的 LPRng 打印服务器，您应该编辑 /etc/lpd.perms 文件。该文件包含一大段描述其配置细节的注释。若要阻止除本地机器以外的所有连接，您可以使用两种形式之一的条目：

```
ACCEPT SERVICE=x REMOTEIP=127.0.0.1/255.0.0.0
```

或者

```
ACCEPT SERVICE=X REMOTEHOST=localhost
REJECT SERVICE=X NOT REMOTEHOST=*, three.com
```

这些示例分别阻止了不源自 192.168.98.0 IP 块或 three.com 域的通信连接，同时仍允许来自服务器本身的连接。与旧式 lpd 的 hosts.lpd 文件相比，lpd.perms 文件可以实现更多功能。例如，您可以基于远程用户允许或拒绝访问，并且可以允许或拒绝用户或机器访问特定的 LPRng 功能。默认的 lpd.perms 文件包含许多被注释掉的示例，因此如果您想微调配置，非常值得仔细查看。

**注意**：虽然 LPRng 默认让外部人员可以在您的打印服务器上进行打印，但其更高级的安全功能使得如果您正确配置，它将是一个更安全的打印软件包。

## 当涉及 Windows 时

当本地或目标机器运行某种版本的 Microsoft Windows 时，情况会变得稍微复杂一些。Windows 打印机使用称为服务器消息块（SMB）的协议，后更名为通用互联网文件系统（CIFS），以提供共享打印。试图让 Windows 和 Linux 计算机使用其原生工具共享打印机，就像试图让两个不懂同一种语言的人进行对话一样。幸运的是，Linux 包含一个教 Linux “说” Windows 文件和打印机共享语言 SMB/CIFS 的软件包：Samba。

Samba 对于混合网络来说是如此重要的工具，以至于它成为 Craig Hunt Linux 系列书籍中的一本配套书 Roderick W. Smith 所著的《Linux Samba 服务器管理》（Sybex, 2001）的主题。本书第 12 章简要介绍了 Samba。简而言之，Samba 是一个开源软件套件，为可能运行 Windows、OS/2 或若干其他操作系统任何版本的客户端提供 SMB/CIFS 文件和打印服务。Samba 运行在 Linux、其他版本的 Unix、VMS 和几种其他操作系统上。有关 Samba 的其他信息源包括优秀的 SMB  HOWTO 文档和多个 Samba 邮件列表。Samba 的主网页是 http://www.samba.org/。

由于本章讨论的是打印，接下来的两个部分展示了如何使用 Samba 从 Windows 机器向连接到 Linux 主机的打印机打印，以及如何从 Linux 机器向连接到 Windows 主机的打印机打印。

### 从 Windows 打印到 Linux 打印机

假设您已配置 Linux 计算机以向本地打印机打印，您只需设置一个 Samba 共享，以允许 LAN 上的 Windows 计算机向其打印。您将在这在安装 Samba 时创建的 smb.conf 文件中执行此操作。（在 Red Hat 7.3 中，该文件位于 /etc/samba，但在其他发行版中可能位于 /etc、/etc/samba.d 或其他地方。）按照清单 10.2 所示，将打印配置添加到您的 smb.conf 中：

**清单 10.2：允许联网的 Windows 计算机向 Linux 打印机打印的示例 smb.conf 文件**

```
[global]
workgroup = ARBORETUM
printing = bsd
encrypt passwords = Yes

load printers = Yes
log_file = /var/log/samba-log.%m
lock_directory = /var/lock/samba

[printers]
comment = All Printers
security = Server
path = /var/spool/samba
browseable = No
printable = Yes
public = Yes
create mode = 0700
```

Samba 配置涉及设置适用于所有共享的全局选项（在 smb.conf 文件的 [global] 部分中）以及特定共享或共享类型的选项。清单 10.2 仅显示一个共享——[printers] 共享。这个共享很特别，因为它为 /etc/printcap 中定义的每个打印机创建了一个单独的打印机共享。此选项依赖于 [global] 部分中的 load printers = Yes 参数。（或者，您可以通过为每个打印机单独创建共享定义来共享部分打印机。）另一个至关重要的全局参数是 workgroup = ARBORETUM。这将 Samba 服务器的 *NetBIOS 工作组* 名称设置为类似于域名的值。如果此选项设置不正确，您将无法在 Windows 计算机的网络资源管理器中查看 Samba 服务器。在清单 10.2 的情况下，该服务器是 ARBORETUM 工作组的成员。

另一个关键的 Samba 配置问题与身份验证有关。与 Linux 到 Linux 的打印不同，SMB/CIFS 打印在机器之间发送密码以授权打印。默认情况下，Samba 接受 *明文*（未加密）密码，并将其与常规的 Linux 登录密码进行比对。然而，自 Windows 95 OSR2 和 Windows NT 服务包 3 以来，Microsoft 已编程使 Windows 计算机默认发送加密密码。由于 SMB/CIFS 使用的密码编码方法与 Linux 不同，当使用加密密码时，Samba 无法依赖常规的 Linux 密码数据库。因此，您必须使用 Samba 的 smbpasswd 实用程序创建一个新的密码数据库，该程序允许您设置 Samba 的加密密码，就像 Linux passwd 实用程序允许您设置 Linux 登录密码一样。若要使用此实用程序添加用户，请传入 -a 参数和您希望添加的用户名（此用户名必须对应于现有的 Linux 用户）：

```
# smbpasswd -a someone
New SMB password:
Retype new SMB password:
```

当您输入密码时，密码不会回显。如果您以前从未使用该实用程序，它会抱怨无法打开 smbpasswd 文件，但尽管有这个错误，它仍会创建一个新的文件。若要使用加密密码，您必须向 smb.conf 的 [global] 部分添加 encrypt passwords = Yes 参数，如清单 10.2 所示。

**警告**：Windows 9x 和 Me 系统会在本地存储您发送到服务器的密码。这可能是一个重大的安全问题，特别是当用户的 Samba 和 Linux 登录密码相同时。有许多方法可以减轻 Windows 在本地存储密码所带来的风险。其中最简单的一种方法是确保 Samba 加密密码与常规的 Linux 登录密码不对应。您还可能将 Samba 服务器与其他 Linux 服务器和工作站隔离，或使用单独的

