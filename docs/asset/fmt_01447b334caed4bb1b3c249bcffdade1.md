
```
[homes]
comment=Home Directories
browse=no
writable = yes
create mode = 0664
directory mode = 0775
max connections = 1
```

让我们学习 `[printers]`。

`[printers]`

它是为打印机提供配置的部分。它允许客户端为指定的目录设置打印选项。`[printers]` 中最重要的选项如下：

```
[printers]
comment = All printers
path=/var/spool/samba
browseable=yes
printable = yes
```

### 创建 Samba 用户

通过执行用户级 Samba 安全机制，为每个在 Windows 下使用 Linux 文件系统和打印机的人员分配 Linux 用户账户。你需要为每个用户提供一个 SMB 密码。要添加或创建新的 Samba 用户，你需要执行以下命令：

在终端窗口中以 root 用户身份输入命令：

```
useradd -m bob
```

这将添加一个名为 "bob" 的用户。为新用户添加 Linux 密码：

```bash
passwd bob
```

终端将提示你为用户 bob 修改密码：

```
Changing password for user bob
New password: ******
Retype new password: ******
```

> 重复上述命令，为来自 Windows 工作站的所有用户添加账户，以便其提供访问你的 Linux 系统的权限。

以下命令用于在 Fedora Linux 系统上创建用户账户或创建 Samba 密码文件 (`smbpasswd`)：

```bash
cat /etc/passwd | smbpasswd.sh > /etc/samba/smbpasswd
```

此命令仅创建了用户账户，而没有创建密码。你需要使用 `smbpasswd` 命令为你的用户创建密码，格式如下：

```bash
smbpasswd bob
New SMB password: ******
Retype new SMB password: ******
```

> 为每个用户重复上述命令。

让我们使用命令连接到 Samba 客户端。

### 将 Windows PC 连接到 Samba 服务器

你可以连接到任何运行 SMB 协议的计算机。可以通过两种方法通过命令行连接。以下是连接到 Samba 客户端的方法：

`smbclient` 工具提供了以下命令，

```
smbclient://computer name/share name
```

## 微软网络与网络服务导言

将 `computer name` 替换为想要连接的 Samba 服务器的主名或 IP 地址，将 `share name` 替换为想要浏览的目录名称。输入 `exit` 退出连接。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_78_0.png)

若要查询网络中的 Samba 服务器，请使用 `findsmb` 命令。

- `smbmount` 工具提供了以下命令，

```
smbmount //computerName/directory/mysystem/mount/point
```

将 `computer name` 替换为想要连接的 Samba 服务器的主名或 IP 地址，将 `directory` 替换为想要浏览的目录名称。输入 `exit` 退出连接。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_78_1.png)

通过在目录上执行 `ls` 命令来检查挂载是否成功。

要在 Windows PC 上测试连接，请执行以下步骤：

在计算机上，双击网络窗口。会出现一个包含 Linux 系统图标的列表。双击图标查看所有共享。会弹出一个提示输入用户名和密码以进入目录。在提供适当的登录凭据后，你可以在 Linux 和 Windows 计算机之间共享文件。

学习了连接微软网络后，让我们学习网络服务。

### 3.2 附加网络服务

任何管理员都可以持续控制对新或增强服务的请求。一个常用的请求服务是时间服务器。它提供权威时钟，局域网（LAN）上的其他系统通过它同步时钟。在下一节中，你将学习两种非本质局域网服务：基于 NTP 的时间服务器和缓存代理服务器。

让我们配置时间服务器。

### 配置时间服务器

时间服务器运行在某机器上的守护进程，供其他系统同步时钟。通常，你会将你的时间服务器与一个或多个位于局域网外的参考时间服务器同步。在某些情况下，时间服务器与专门设计的时钟同步时间。这种硬件时钟是一个特殊用途的独立设备，旨在保持准确性。它的主要目标是保持局域网内系统时间的一致性，以便时间敏感的操作。系统和服务器之间的时钟异常会导致影响。

最重要且广泛用于发布和同步时间的协议是网络时间协议 (`NTP`)。`NTP` 是一种用于同步你的 Linux 系统时钟与准确时间源的协议。`ntpd` 守护进程具有双重用途：它可以作为服务器监听时间同步请求并提供响应，也可以作为客户端与其他时间服务器通信以调整本地系统时间。

### 参考时钟

最重要且广泛用于发布和同步时间的协议是网络时间协议 (`NTP`)。`NTP` 是一种用于同步你的 Linux 系统时钟与准确时间源的协议。`ntpd` 守护进程具有双重用途：它可以作为服务器监听时间同步请求并提供响应，也可以作为客户端与其他时间服务器通信以调整本地系统时间。

# 第 3 章

涉及 `autokey`。它在 Fedora 核心默认配置中没有安装。要创建一个基础的 `autokey` 设置并配置到 `/etc/ntp` 服务器，请按照以下步骤操作：

- 将以下几行添加到 `/etc/ntp.conf` 中：

```
broadcast 224.0.1.1 autokey
crypto pw serverpassword
keysdir /etc/ntp
```

- 使用以下命令生成密钥文件和证书：

```
# cd /etc/ntp
# ntp-keygen -T -I serverpassword
```

输出显示了某些文件的生成。

如果 `ntp-daemon` 未在运行，请使用以下命令重启 `ntpd`：

```bash
# service ntpd restart
```

如果 `ntpd` 未在运行，请使用以下命令启动 `ntp-daemon`：

```bash
# service ntpd start
```

- 使用以下 `chkconfig` 验证 `ntp` 是否在启动时启动，以及是否在所有多用户运行级别下启动：

```bash
# chkconfig -level 0123465 ntpd off
# chkconfig -level 345 ntpd on
```

这些步骤都启用了 NTP 的 `autokey` 加密，并配置了在启动时启动和停止 NTP 服务。

让我们学习如何配置 NTP 客户端。

### 配置 NTP 客户端

`NTP` 客户端可以通过几个步骤进行配置。在 Fedora 中启动“日期/时间属性”工具，选择 `→` 管理 `→` 日期/时间；将打开日期/时间属性窗口（图 3.1）。您也可以通过终端窗口输入 `system-config-date` 打开此窗口。

如果 NTP 已经在系统上运行，则“日期/时间”选项卡将显示禁用（灰色）。点击“网络时间协议”选项卡来配置 NTP。选择“启用网络时间”选项来配置 NTP。这允许您更改“`NTP` 服务器”选项中的内容，如图 1 所示：

# 微软网络和网络服务介绍

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_82_0.png)

你可以从服务器列表中选择，通过点击“添加”按钮添加新服务器，并通过“删除”删除任何服务器。要配置高级 NTP 选项，点击“显示高级选项”。这些选项允许您使用系统时钟作为参考钟并使用 NTP 广播。在进行所需的更改后点击“确定”。

如果您的 NTP 服务器要使用 `autokey` 加密，您还需要配置 NTP 客户端使用 `autokey` 加密。请按照所需的步骤在 `/etc/ntp.conf` 中配置 NTP 客户端：

- 在客户端的 `/etc/ntp.conf` 中添加以下几行：

```
crypto pw clientpassword
keysdir /etc/ntp
timeserver autokey
```

将 `clientpassword` 替换为您选择的密码，将 `timeserver` 替换为配置为服务器的系统名称或 IP 地址。

- 使用以下命令生成客户端密钥和证书：

```bash
# cd /etc/ntp
# ntp-keygen -H -p clientpassword
```

输出显示了某些文件的生成。

- 使用 `ftp` 或 `scp` 导入服务器配置中创建的密钥。以下示例使用了 `scp`：
