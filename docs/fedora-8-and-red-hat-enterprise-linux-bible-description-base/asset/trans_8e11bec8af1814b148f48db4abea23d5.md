

Samba 服务器在本地广播域内控制工作组浏览器列表的机会。

如果值为 0，通常会选择一台 Windows 机器。值为 65 通常会确保 Samba 服务器优先于 NT 服务器被选中。默认值为 20。

- **preferred master** — 如果您希望强制选择主浏览器，请将其设置为“是”。将其设置为“是”可以增加 Samba 服务器被选中的机会。（将此选项与将域主设置为“是”相结合，应确保 Samba 服务器会被选中。）默认设置为自动，这会使 Samba 在承担该职责之前尝试检测当前的主浏览器。
- **local master** — 如果您希望 Samba 服务器成为本地浏览器主，请将其设置为“是”。（这并非保证，但会增加其被选中的机会。）如果您不希望您的 Samba 服务器被选为本地主，请将值设置为“否”。本地主默认为自动。
- **domain master** — 如果您希望 Samba 服务器（nmbd 守护进程）将其自身标识为所在工作组的域主浏览器，请将其设置为“是”。此列表将允许分配给该工作组的客户端计算机使用来自其自身子网之外的子网中的 SMB 共享文件和打印机。此选项默认为否。

## WINS 选项

如果您希望特定的 WINS 服务器为 SMB 客户端使用的 NetBIOS 名称提供名称到地址的转换，请使用 WINS 选项。如前所述，如果您的 SMB 工作组中的所有客户端和服务器都在同一子网上，您可能不需要使用 WINS 服务器。这是因为可以通过广播地址获取 NetBIOS 名称。可以让您的 Samba 服务器提供 WINS 服务。

- **wins server** — 如果您的网络中有一个您想用来解析工作组 NetBIOS 名称的 WINS 服务器，您可以在此输入该服务器的 IP 地址。再次强调，如果您的工作组扩展到了本地子网之外，您可能需要选择一个 WINS 服务器。
- **wins support** — 如果您希望您的 Samba 服务器充当 WINS 服务器，请将此值设置为“是”。（默认为否。）再次强调，如果工作组中的所有计算机都在同一子网上，则不需要此设置。您的网络上只能有一台计算机被指定为 WINS 服务器。

除了这里描述的值之外，您可以通过点击高级视图按钮访问数十个其他选项。填写完您需要的所有字段后，点击提交。更改屏幕上的内容以将更改写入 `/etc/samba/smb.conf` 文件。

## 使用 SWAT 配置共享目录

为了使您的 Samba 共享（共享目录）对其他用户可用，您可以向 SWAT 窗口添加一个条目。若使用 SWAT 设置 Samba 以共享目录，请执行以下操作：

**注意**：在此过程中，您可能会看到一个或多个安全警告。这些消息警告您，有人可能会查看您发送到 SWAT 的数据。如果您在本地主机或私有 LAN 上工作，风险极小。

1. 从主要的 SWAT 窗口，点击 **SHARES** 按钮。
2. 在创建共享框中输入您想要共享的目录名称，然后点击创建共享。
3. 如果您想切换到高级视图，请点击 **Advanced**。
4. 这里有几十个选项可供选择。以下是几个可能特别引起您兴趣的选项：
    - **comment** — 用于描述共享目录的几句话（可选）。
    - **path** — 您正在共享的目录的路径名。
    - **invalid users** — 允许您添加一个用户列表，这些用户不允许登录到 Samba 服务。除了直接识别用户名（来自您的 /etc/passwd 文件）外，通过在名称前添加 + 或 &，可以分别通过 Linux 组或 NIS 网络组来识别无效用户。在名称前添加 @，以便 Samba 首先检查 NIS 网络组，然后检查 Linux 组中是否包含该名称。
    - **valid users** — 在此处添加名称以标识哪些 Linux 用户帐户可以访问 Samba 服务。与无效用户一样，名称前可以加上 +、& 或 @ 字符。
    - **admin users** — 允许您标识在特定共享上具有管理特权的用户。这仅在 `security` = `share` 类型的安全模式下可用。
    - **read list** — 如果您只想向共享授予读访问权限（即使共享具有读写访问权限），请将用户添加到此列表。这仅在 `security` = `share` 类型的安全模式下可用。
    - **write list** — 将用户添加到此列表以向这些用户授予对共享的写访问权限，即使该共享对其他所有人只有只读访问权限。这仅在 `security` = `share` 类型的安全模式下可用。
    - **read only** — 如果为是，则只能从此文件系统读取文件，但远程用户无法在文件系统中保存或修改文件。如果您希望允许用户通过网络将文件保存到此目录，请选择否。
    - **guest ok** — 选择是，以启用任何人无需密码即可访问此目录。
    - **hosts allow** — 添加允许访问此文件系统的计算机名称。您可以使用逗号、空格或制表符分隔主机名。以下是一些输入主机名的有效方式：
        - **localhost** — 允许访问本地主机。
        - **192.168.74.18** — IP 地址。输入一个单独的 IP 地址。
        - **192.168.74.** — 输入一个网络地址，以包含网络上的所有主机。（请务必在网络地址末尾加上一个点，否则它将无法工作！）
        - **maple, pine** — 按名称启用对单独主机的访问。
        - **EXCEPT *host*** — 如果您允许访问一组主机（例如通过输入网络地址），请使用 EXCEPT 来明确拒绝从该组中的一个主机访问。
    - **hosts deny** — 通过将计算机名称放在此处来拒绝特定计算机的访问。默认情况下，不排除任何特定计算机。以与 hosts allow 相同的格式输入主机名。
    - **browsable** — 指示您是否可以在共享目录列表中查看此目录。默认为开（是）。
    - **available** — 允许您保留此条目，但关闭该服务。如果您想暂时关闭对目录的访问，这将很有用。默认为开（是）。选择否以将其关闭。
5. 选择提交更改。

此时，共享文件系统应该对具有访问您 Linux Samba 服务器权限的 Samba 客户端计算机（Windows 9x, Windows NT, Windows 2000, Windows Vista, Mac OS X, OS/2, Linux 等）可用。然而，在尝试之前，您可以检查关于 Samba 配置的一些事项。

## 使用 SWAT 检查您的 Samba 设置

从 SWAT 窗口，选择 STATUS 按钮。

从该窗口，您可以重启您的 smbd 和 nmbd 进程。同样，您可以查看活动连接、活动共享和打开文件的列表。（启动 smbd 和 nmbd 守护进程的推荐方式是设置 smb 服务以自动启动。在终端窗口中输入 `chkconfig smb on` 以设置服务在启动时启动。）

## 处理 Samba 文件和命令

虽然您可以通过 Samba 服务器配置窗口或 SWAT 设置 Samba，但许多管理员更喜欢直接编辑 `/etc/samba/smb.conf`。作为 root 用户，您可以查看此文件的内容并进行必要的更改。如果您选择了 *user* 安全（如推荐的那样），您也会对 *smbusers* 和 *smbpasswd* 文件（也在 `/etc/samba` 目录中）感兴趣。这些文件，以及诸如 *testparm* 和 *smbstatus* 之类的命令，将在以下章节中描述。

# 第 18 章：设置文件服务器 779

## 编辑 smb.conf 文件

您使用 Samba 服务器配置窗口或 SWAT Web 界面所做的更改将反映在您的 `/etc/samba/smb.conf` 文件中。以下是一个 `smb.conf` 文件的示例（已移除注释）：

```ini
[global]
workgroup = ESTREET
server string = Samba Server on Maple
hosts allow = 192.168.0.
printcap name = /etc/printcap
load printers = yes
printing = cups
log file = /var/log/samba/%m.log
max log size = 0
smb passwd file = /etc/samba/smbpasswd
security = user
encrypt passwords = Yes
unix password sync = Yes
passwd program = /usr/bin/passwd %u
passwd chat = *New*password* %\n *Retype*new*password* %\n *passwd:*all*authentication*tokens*updated*successfully*
pam password change = yes
obey pam restrictions = yes
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
username map = /etc/samba/smbusers
dns proxy = no

[homes]
comment = Home Directories
browseable = no
writable = yes
valid users = %S
create mode = 0644
directory mode = 0775

[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest ok = no
writable = no
printable = yes
```

在 `[global]` 部分，工作组设置为 **ESTREET**，服务器被标识为位于 Maple 上的 Samba 服务器，并且仅允许本地网络 `(192.168.0.)` 上的计算机访问 Samba 服务。您必须更改 `'hosts allow ='` 参数以匹配您的网络。

