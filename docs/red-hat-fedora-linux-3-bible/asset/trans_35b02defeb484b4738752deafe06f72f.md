
除了在此描述的数值外，你可以通过点击“高级视图”按钮访问数十个其他选项。当填写完所有需要的字段后，点击屏幕上的“提交更改”按钮，即可将更改写入 `/etc/samba/smb.conf` 文件。

## 使用 SWAT 配置共享目录

要使你的共享目录对其他用户可用，你可以向 SWAT 窗口添加一个条目。若要使用 SWAT 设置 Samba 以共享目录，请执行以下操作：

> **注意：** 在此过程中，你可能会看到一个或多个安全警告。这些消息警告你，有人可能会查看你发送给 SWAT 的数据。如果你正在本地主机或私有局域网上工作，风险极小。

1. 从主 SWAT 窗口，点击 **SHARES** 按钮。
2. 在 **Create Share** 框中输入你要共享的目录名称，然后点击 **Create Share**。
3. 点击 **Advanced** 切换到高级视图。
4. 有几十个选项可供选择。以下是一些可能特别感兴趣的选项：
   - **comment** — 用于描述共享目录的几个字（可选）。
   - **path** — 你要共享的目录的路径名。
   - **read only** — 如果选择 Yes，则只能从此文件系统读取文件，但远程用户无法在文件系统中保存或修改文件。如果希望允许用户通过网络将文件保存到此目录，请选择 No。
   - **guest ok** — 选择 Yes 以允许任何人无需密码即可访问此目录。
   - **hosts allow** — 添加允许访问此文件系统的计算机名称。你可以使用逗号、空格或制表符分隔主机名。以下是一些输入主机名的有效方式：
     - **localhost** — 允许访问本地主机。
     - **192.168.74.18** — IP 地址。输入单个 IP 地址。
     - **192.168.74.** — 输入网络地址以包含网络上的所有主机。（务必在网络数字末尾加点，否则无效！）
     - **maple, pine** — 通过名称启用对单独主机的访问。
     - **EXCEPT host** — 如果你允许访问一组主机（例如通过输入网络地址），使用 EXCEPT 来专门拒绝该组中某一台主机的访问。
   - **hosts deny** — 在此处放置特定计算机的名称以拒绝其访问。默认情况下，没有排除任何特定计算机。输入主机名的方式应与 hosts allow 中使用的格式相同。
   - **browseable** — 指示你共享目录列表上是否可以看到此目录。默认为开启（Yes）。
   - **available** — 允许你保留此条目，但关闭服务。如果你希望暂时关闭对目录的访问，这将很有用。默认为开启（Yes）。
5. 选择提交更改。

此时，共享文件系统应该对能够访问你的 Linux Samba 服务器的 Samba 客户端计算机（Windows 9x、Windows NT、Windows 2000、OS/2、Linux 等）可用。然而，在尝试之前，你可以检查关于你的 Samba 配置的一些事项。

## 使用 SWAT 检查你的 Samba 设置

从 SWAT 窗口，选择 STATUS 按钮。

在此窗口中，你可以重启 smbd 和 nmbd 进程。同样，你也可以看到活动连接、活动共享和打开文件的列表。（启动 smbd 和 nmbd 守护进程的推荐方式是设置 smb 服务自动启动。输入 `chkcconfig smb on` 以服务在启动时启动。）

## 处理 Samba 文件和命令

虽然你可以通过 Samba 服务器配置窗口或 SWAT 设置 Samba，但许多管理员喜欢直接编辑 `/etc/samba/smb.conf` 文件。作为 root 用户，你可以查看此文件的内容并进行必要的更改。如果你选择了用户安全（推荐），你也会对其中的 *smbusers* 和 *smbpasswd* 文件（也在 `/etc/samba` 目录中）感兴趣。这些文件以及诸如 *testparm* 和 *smbstatus* 等命令将在以下章节中描述。

## 编辑 smb.conf 文件

使用 Samba 服务器配置窗口或 SWAT Web 界面所做的更改将反映在你的 `/etc/samba/smb.conf` 文件中。这是一个 *smb.conf* 文件的示例（已移除注释）：

```
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
encrypt passwords = yes
unix password sync = yes
passwd program = /usr/bin/passwd %u
passwd chat = *New*password* \n\n *Retype*new*password* \n\n *passwd:*all*authentication*tokens*updated*successfully*
pam_password_change = yes
obey pam restrictions = yes
socket options = TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192
username map = /etc/samba/smbusers
dns proxy = no

[homes]
comment = Home Directories
browseable = no
writable = yes
valid users = $$
create mode = 0664
directory mode = 0775

[printers]
comment = All Printers
path = /var/spool/samba
browseable = no
guest_ok = no
writable = no
printable = yes
```

在 **[global]** 部分中，工作组设置为 **ESTREET**，服务器标识为 Maple 上的 Samba 服务器，并且只允许位于本地网络（**192.168.0.**）上的计算机访问 Samba 服务。你必须更改本地网络以匹配你的网络。

本地共享打印机的定义取自 **/etc/printcap** 文件，打印机已加载（**yes**），并且使用了 cups 打印服务（这是 Fedora 使用的默认打印服务）。

为每个尝试使用该服务的主机创建单独的日志文件，位于 **/var/log/samba/%m.log**（%m 会自动替换为每个主机名）。日志文件大小没有限制（0）。

在这种情况下，我们使用的是用户级安全（**security = user**）。这允许用户登录一次，然后轻松访问 Linux 系统上的打印机和用户主目录。密码加密已开启（**encrypt passwords = yes**），因为大多数 Windows 系统默认开启密码加密。密码存储在 Linux 系统的 `/etc/samba/smbpasswd` 文件中。

**dns proxy = no** 选项防止 Linux 在 DNS 服务器上查找系统名称（用于 TCP/IP 查找）。

**（homes）** 部分允许每个用户从局域网上的 Windows 系统访问其 Linux 主目录。用户能够写入主目录。然而，其他用户将无法看到或共享此目录。
**（printers）** 部分允许所有用户向本地 Linux 系统配置的任何打印机打印。

## 添加 Samba 用户

执行用户样式的 Samba 安全意味着为使用其 Windows 工作站访问 Linux 文件系统和打印机的每个人分配一个 Linux 用户帐户。（你可以将用户分配给来宾帐户，但在此示例中，所有用户都有自己的帐户。）然后你需要为每个用户添加 SMB 密码。例如，这是如何添加一个 Windows 98 工作站登录名为 chuckp 的用户：

1. 在终端窗口中作为 root 用户输入以下内容，以添加 Linux 用户帐户：
   
   ```bash
   # useradd -m chuckp
   ```

2. 按如下方式为新用户添加 Linux 密码：
   
   ```bash
   # passwd chuckp
   Changing password for user chuckp
   New UNIX password: ********
   Retype new UNIX password: ********
   ```

3. 重复前面的步骤，为你希望授予访问权限的局域网中所有 Windows 工作站的 Linux 系统用户添加用户帐户。

4. 输入以下命令以创建 Samba 密码文件（smbpasswd）：
   
   ```bash
   # cat /etc/passwd | /usr/bin/mksmbpasswd.sh > /etc/samba/smbpasswd
   ```

5. 按如下方式为用户添加 SMB 密码：
   
   ```bash
   # smbpasswd chuckp
   New SMB password: ********
   Retype new SMB password: ********
   ```

对每个用户重复此步骤。稍后，每个用户可以登录 Linux 并重新运行 `passwd` 和 `smbpasswd` 命令以设置私有密码。

> **注意**：在最新版本的 Samba 中，`smb.conf` 文件中提供了选项，可以自动同步 SMB 和 Linux 密码。请参阅本章 SWAT 部分中关于 `passwd` 程序、`passwd` chat 和 UNIX 密码同步选项的描述。

