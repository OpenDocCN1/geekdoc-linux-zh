
# systemctl enable smb.service
# systemctl start smb.service

虽然通常不需要，但在修改 `smb` 配置文件后，你可以再次运行第二条命令，将 `start` 替换为 `reload` 以使 `smb` 重新读取这些文件。

## 启用并启动 nmb

运行 `systemctl` 使 `nmb` 服务（`nmbd` 守护进程）在系统每次进入多用户模式时启动，然后启动 `nmb` 服务。使用 `systemctl status` 命令确保服务正在运行。

```bash
# systemctl enable nmb.service
# systemctl start nmb.service
```

虽然通常不需要，但在修改 `nmb` 配置文件后，你可以再次运行第二条命令，将 `start` 替换为 `reload` 以使 `nmb` 重新读取这些文件。

## 服务器防火墙

`Samba` 服务器使用 UDP 端口 137 和 138，以及 TCP 端口 139 和 445。如果服务器正在运行防火墙或位于防火墙之后，你需要打开这些端口。运行以下命令以在系统每次启动时（永久地）以及在正在运行的系统上打开这些端口；有关 `firewall-cmd` 的信息请参阅第 906 页。

```bash
# firewall-cmd --add-port=137/udp
# firewall-cmd --permanent --add-port=137/udp
# firewall-cmd --add-port=138/udp
# firewall-cmd --permanent --add-port=138/udp
# firewall-cmd --add-port=139/tcp
# firewall-cmd --permanent --add-port=139/tcp
# firewall-cmd --add-port=445/tcp
# firewall-cmd --permanent --add-port=445/tcp
```

## SELinux

当 `SELinux` 设置为使用目标策略时，`Samba` 受 `SELinux` 保护。如有必要，你可以使用 `system-config-selinux`（第 475 页）来禁用此保护。如果你希望允许用户共享其主目录，请参阅第 840 页的“SELinux”。`smb.conf` 文件中包含关于为 `Samba` 配置 `SELinux` 的大量注释。

## 打印机

默认的 `smb.conf` 配置文件会共享 `Samba` 服务器上的打印机；无需额外配置。

![](img/243613168ac865b539f12460d966088e_893_0.png)

图 23-1 `Samba` 服务器配置窗口

## 主目录

默认的 `smb.conf` 配置文件会共享 `Samba` 服务器上用户的主目录；无需额外配置。

配置 `/etc/sysconfig/samba` 文件使 `smbd` 和 `nmbd` 均以 `-D` 选项启动，从而使 `smbd` 和 `nmbd` 进程作为守护进程运行。

### 快速入门：使用 system-config-samba 配置 Samba 服务器（Fedora）

`system-config-samba` 实用程序在 `RHEL` 下不可用，它只能设置 `Samba` 服务器的基本功能。然而，如果你不熟悉 `Samba` 并希望快速设置一个简单的 `Samba` 服务器，这是最佳工具。`system-config-samba` 实用程序执行三个基本功能：配置服务器、配置用户以及设置导出到 `Windows` 机器的共享（目录层级）。

要显示 `Samba` 服务器配置窗口（图 23-1），请从终端仿真器或输入命令窗口（`Alt+T2`）输入 `system-config-samba`。

#### 配置服务器

选择菜单栏：`首选项 => 服务器设置`，以显示“服务器设置”窗口的“基本”选项卡（图 23-2）。将工作组更改为 `Windows` 中正在使用的那个。

![](img/243613168ac865b539f12460d966088e_893_1.png)

图 23-2 服务器设置窗口，基本选项卡

## 添加或修改 Samba 用户

机器。如果您愿意，可以更改服务器的描述。单击 `Security`（安全性）选项卡，并确保将 `Authentication Mode`（身份验证模式）设置为 `User`（用户）；您无需指定身份验证服务器或 `Kerberos` 域。如果您使用的是 `Windows` 98 或更高版本，请将 `Encrypt Passwords`（加密密码）设置为 `Yes`（是）。当您在 `Guest Account`（来宾账户）中指定用户名时，任何以 `guest`（来宾）身份登录 `Samba` 服务器的人都将映射到该用户的 ID。单击 `OK`（确定）。

选择 `menubar: Preferences→Samba Users`（菜单栏：首选项→Samba 用户）以显示 `Samba Users`（Samba 用户）窗口（图 23-3）。如果您想要以特定用户身份登录且该用户未列在此窗口中，请单击 `Add User`（添加用户）。当您拥有适当的权限时，创建新 `Samba` 用户（`Create New Samba User`）窗口将显示一个标记为 `Unix Username`（Unix 用户名）的组合框，允许您选择一个 `Linux` 用户；否则，您的用户名将作为 `Unix` 用户名显示。`Windows` 用户名是您希望映射到指定 `Linux`（`UNIX`）用户名的 `Windows` 用户名。`Samba` 密码是此用户或 `Windows` 系统为访问 `Samba` 服务器而输入的密码。

如果 `Sam` 在 `Linux` 和 `Windows` 系统上的用户名均为 `sam`，您将从 `Unix` 用户名组合框中选择 `sam`，并在 `Windows` 用户名文本框中输入 `sam`。如果他在 `Linux` 下的用户名为 `sls`，而在 `Windows` 下为 `sam`，您将从 `Unix` 用户名组合框中选择 `sls`，并在 `Windows` 用户名文本框中输入 `sam`。最后，您将 `Sam` 的 `Windows` 密码输入到两个 `Samba` 密码文本框中。单击 `OK`（确定）关闭创建新 `Samba` 用户窗口，然后单击 `OK`（确定）关闭 `Samba` 用户窗口。

### 用户映射

如果您将一个 `Windows` 用户名映射到另一个 `Linux` 用户名，您必须向 `/etc/samba/smb.conf`（第 839 页）的 `[global]` 部分添加以下 `username map`（用户名映射，第 843 页）参数：

```
username map = /etc/samba/smbusers
```

如果 `smb.conf` 中没有这一行，`Samba` 将不会咨询用户映射文件。

### Linux 共享

接下来，您需要添加一个共享（`share`），即您从服务器（`Linux`）系统导出到客户端（`Windows`）系统的目录层次结构。单击工具栏上的加号（`+`）以显示“创建 `Samba` 共享”（`Create Samba Share`）窗口的“基本”（`Basic`）选项卡（图 23-4）。在

![](img/243613168ac865b539f12460d966088e_895_0.png)

图 23-4 “创建 `Samba` 共享”窗口，“基本”选项卡

标记为 `Folder`（文件夹）的文本框中，输入您要共享的目录的绝对路径名（`/tmp` 是一个适合练习的目录）。如果您愿意，可以输入描述。在此处输入 `Linux` 主机名和您共享的目录路径名可能很有用。如果您希望能够从客户机向该目录写入，请勾选标记为 `Writable`（可写）的复选框；勾选标记为 `Visible`（可见）的复选框允许从客户机看到（浏览）该共享。单击“访问”（`Access`）选项卡，并指定您是否希望将访问限制为指定用户，或者是否允许任何人访问此共享。单击 `OK`（确定）。关闭 `Samba Server Configuration`（Samba 服务器配置）窗口。

现在，您应该能够访问来自 `Windows` 机器（第 835 页）的共享。无需启动或重启 `Samba` 服务器。

**故障排除** 如果服务器工作不正常，请参阅第 846 页的“故障排除”。

## 修改 smb.conf 时，您无需重启 Samba

每当客户端连接时，`Samba` 都会重新读取其配置文件。除非您更改 `security`（安全性）参数（第 843 页），否则在更改 `smb.conf` 时无需重启 `Samba`。

## smb.conf：手动配置 SAMBA 服务器

`/etc/samba/smb.conf` 文件控制 `Samba` 工作方式的大多数方面，并分为多个部分。每个部分以一行文本开头，该行文本包含在方括号（`[...]`）中。方括号内的文本标识该部分。典型部分包括

- `[global]` 定义全局参数
- `[printers]` 定义打印机
- `[homes]` 定义用户主目录中的共享
- `[share name]` 定义一个共享（您可以拥有多个此类部分）

`smb.conf` 在 `Fedora/RHEL` 下安装时，`smb.conf` 示例配置文件包含大量注释和被注释掉的示例。注释行以井号（`#`）或分号（`;`）开头。示例文件使用井号来开始旨在保留为注释的行。分号开始您可能希望模仿或通过使用（即移除分号）的行。

### 基本 smb.conf 文件

以下是一个基本的 `smb.conf` 文件。它依赖于许多参数的默认值。为了使代码更清晰，重要的默认值就像在默认 `smb.conf` 文件中那样，作为以分号开头的注释写入。为了使系统更安全，更改默认的 `server string`（服务器字符串）以消除 `Samba` 版本号；该值可能会帮助黑客渗透系统。`hosts allow`（允许主机）和 `hosts deny`（拒绝主机）参数不是必需的。当包含它们时，它们会阻止未列出的系统联系 `Samba` 服务器。如果您取消注释这些行，请将 `192.168.206.180` 替换为您希望允许连接到 `Samba` 服务器的系统的 IP 地址。在客户端能够联系服务器之前，您必须打开防火墙（第 836 页）并启动 `smb` 和 `nmb` 服务（第 836 页）。

```bash
$ cat /etc/samba/smb.conf

[global]
    workgroup = MGS
    server string = Samba Server Version %v
    log file = /var/log/samba/log.%m
    max log size = 50
    ;   hosts allow = 127.0.0.1, 192.168.206.180
    ;   hosts deny = ALL
    ;   security = user
    ;   encrypt passwords = YES
    ;   guest ok = NO
    ;   guest account = nobody

[homes]
    comment = Home Directories
    read only = NO
    browsable = NO

[tmp]
    comment = Temporary Directory
    path = /tmp
    read only = NO
    guest ok = YES
    ;   available = YES
    ;   browsable = YES
```

### [homes] 共享

示例 `smb.conf` 文件包含 `[homes]` 共享，它允许用户与 `Windows` 机器共享其 `Linux` 主目录。默认的 `smb.conf` 文件包含相同的共享。此共享导致每个用户的主目录根据指定参数进行共享。共享的路径名是 `username`（用户名）；`Sam` 在 `plum` 上的共享将是 `/plum/sam`。上述文件中使用的默认设置可防止除所有者以外的用户浏览或访问主目录，同时允许登录的所有者拥有完全访问权限。

### SELinux

如果系统运行带有目标化策略的 `SELinux`，并且您希望允许用户共享其主目录（如本节所述），您必须修改 `SELinux` 策略以允许此访问。您可以使用 `system-config-selinux`（第 475 页）来允许此访问：在 `Booleans` 选项卡中，`samba` 模块，在 `Allow samba to share users home directories`（允许 `Samba` 共享用户主目录）旁边打勾。

### 定义共享

前面 `smb.conf` 文件中的 `tmp` 共享使 `Windows` 系统上的用户能够读取并写入服务器上的 `/tmp` 目录。该共享在 `Windows` 下的名称为 `tmp`；在 `Linux` 下的路径为 `/tmp`。任何能够登录 `Samba` 的 `Windows` 用户，包括 `guest`（来宾），都可以读写此目录，假设该用户的 `Linux` 权限允许这样做。要允许用户登录 `Samba`，您必须运行 `smbpasswd`（第 831 页）。`browsable`（可浏览）参数默认为 `YES`（是），使共享出现在服务器上的共享列表中。适用于使用 `Samba` 的 `Windows` 用户的 `Linux` 权限与适用于该 `Windows` 用户登录或映射到的 `Linux` 用户的权限相同。

### 故障排除

- 遵循第 836 页“先决条件”中的步骤，并在必要时添加用户和密码（第 831 页）。现在，从 `Windows` 机器，您应该能够访问您刚刚创建的共享（第 835 页）。如果服务器工作不正常，请参阅第 846 页的“故障排除”。

## smb.conf 文件中的参数

`smb.conf` man 页列出了您可以在 `smb.conf` 中设置的所有参数。以下部分介绍您可能需要更改的一些参数。

### 全局参数

- `interfaces`（接口）：`Samba` 监听的网络列表，以空格分隔。指定为接口名称（如 `lo` 和 `eth0`）或 IP 地址/子网掩码对（第 483 页）。
    - 默认值：除 `127.0.0.1` 外的所有活动接口
- `server string`（服务器字符串）：客户端（`Windows`）机器在多处显示的字符串。在字符串内，`Samba` 将 `%v` 替换为 `Samba` 版本号，将 `%h` 替换为服务器的主机名。为了使系统更安全，消除 `Samba` 版本号；该值可能会帮助黑客渗透系统。
    - 默认值：`Samba %v`
    - `Fedora/RHEL`: `Samba Server Version %v`
- `workgroup`（工作组）：服务器所属的工作组。将其设置为与使用服务器的 `Windows` 客户端相同的工作组。此参数控制当安全性（第 843 页）设置为 `DOMAIN`（域）时 `Samba` 使用的域名。
    - 默认值：`WORKGROUP`
    - `Fedora/RHEL`: `MYGROUP`

### 安全性参数

- `encrypt passwords`（加密密码）：`YES` 仅接受来自客户端的加密密码。`Windows` 98 和 `Windows` NT 4.0 Service Pack 3 及更高版本默认使用加密密码。此参数使用 `smbpasswd` 来验证密码，除非您将 `security` 设置为 `SERVER` 或 `DOMAIN`，在这种情况下，`Samba` 使用另一台服务器进行身份验证。
    - 默认值：`YES`

## 来宾账户

分配给以**来宾**身份登录的用户或映射到**来宾**用户的用户名；仅当 `guest ok` 设置为 `YES` 时适用。该用户名应存在于 `/etc/passwd` 中，但不应能够登录系统。通常**来宾账户**被赋予 `nobody` 值，因为 `nobody` 用户只能访问任何用户都可以访问的文件。如果您在服务器系统上出于其他目的使用 `nobody` 账户，请将此参数设置为除 `nobody` 以外的名称。更多信息请参见第830页。

默认值：无（允许所有主机访问）

## hosts allow

类似于 `/etc/hosts.allow` 文件；指定允许连接到服务器的主机。覆盖 `hosts deny` 中指定的主机。良好的策略是在 `hosts deny` 中指定 `ALL`，并在此文件中指定您想要授予访问权限的主机。指定主机的方式与 `hosts.allow` 文件中相同。

默认值：无（允许所有主机访问）

## hosts deny

类似于 `/etc/hosts.deny` 文件；指定不允许连接到服务器的主机。被 `hosts allow` 中指定的主机覆盖。如果您在此参数中指定 `ALL`，请记得在 `hosts allow` 中包含本地系统（`127.0.0.1`）。指定主机的方式与 `hosts.deny` 文件中相同。

默认值：无（不排除任何主机）

## invalid users

列出那些不允许使用 `Samba` 登录的用户。

默认值：无（允许所有用户登录）

## map to guest

定义当登录失败时映射到**来宾账户**的时机。仅当 `security` 未设置为 `SHARE` 或 `SERVER` 时才有用。

- `Never`：仅当用户显式提供 `guest` 作为用户名且密码为空时，才允许**来宾**登录。
- `Bad User`：将任何尝试以不存在的用户身份登录的行为视为**来宾**登录。此参数存在安全风险，因为它允许恶意用户快速获取系统中的用户列表。
