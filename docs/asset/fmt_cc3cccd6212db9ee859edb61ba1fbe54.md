
`auth [success=1 default=ignore] pam_succeed_if.so user in user1:user2:user3`

要查看每个用户的失败尝试次数，请以 root 身份运行以下命令：

```
[root@localhost -]# faillock
```

```
John:

When             Type Source               Valid

2013-03-05 11:44:14 TTY pts/0                  V
```

要解锁用户的账户，请以 root 身份运行以下命令：

```
faillock --user <username> --reset
```

当使用 `authconfig` 工具修改身份验证配置时，`system-auth` 和 `password-auth` 文件将被来自 `authconfig` 的设置覆盖。为了同时使用这些文件和 `authconfig`，你必须按照以下步骤配置账户锁定：

- 1. 创建以下链接：

```
ln -s /etc/pam.d/system-auth /etc/pam.d/system-auth-local
ln -s /etc/pam.d/password-auth /etc/pam.d/password-auth-local
```

- 2. `/etc/pam.d/system-auth-local` 文件应包含以下行：

```
auth required pam_failock.so preauth silent audit deny=3
unlock_time=600 include system-auth-ac
auth [default:] pam_failock.so authfail audit deny=3
unlock_time=600
account required pam_failock.so include system-auth-ac
password include system-auth-ac
session include system-auth-ac
```

- 3. `/etc/pam.d/password-auth-local` 文件应包含以下行：

```
auth required pam_failock.so preauth silent audit deny=3
unlock_time=600 include system-auth-ac
auth [default:] pam_failock.so authfail audit deny=3
unlock_time=600
account required pam_failock.so include system-auth-ac
password include system-auth-ac
session include system-auth-ac
```

关于 `pam_failock` 配置的更多信息，请参阅 `faillock(8)` 手页。

## 第 2 章 保护网络安全

### 2.1. 会话锁定

在日常操作中，用户由于各种原因可能离开工作站无人看。这可能为攻击者访问机器提供机会，特别是在物理安全不足的环境中（见第 2.1.3 节，“物理控制”）。笔记本电脑特别容易受到影响，因为移动性干扰了物理安全。你可以使用锁定功能防止在输入正确密码之前访问系统，从而缓解这些风险。

> 与注销相比，锁定屏幕的主要优势是，锁定允许用户的进程（如文件传输）继续运行。注销会停止这些进程。

#### 2.1.9.1. 使用 gnome-screensaver-command 锁定 GNOME

Red Enterprise Linux 6 的默认桌面环境 GNOME 包含一个允许用户随时锁定屏幕的功能。有几种方法可以激活锁定：

- 按系统 → 偏好 → 键盘快捷键 → 桌面 → 锁定屏幕中指定的组合键。默认组合键为 Ctrl+Alt+L。
- 在面板上选择 系统 → 锁定屏幕。
- 从命令行界面执行以下命令：

```
gnome-screensaver-command -
```

所有描述的技术具有相同的结果；屏幕保护程序被激活且屏幕被锁定。用户随后可以按任意键取消屏幕保护程序，输入密码并继续工作。

请记住，此功能需要 `gnome-screensaver` 进程正在运行。你可以使用任何提供进程信息的命令来检查是否如此。例如，在终端执行以下命令：

```
pidof gnome-screensaver
```

如果 `gnome-screensaver` 进程当前正在运行，执行命令后屏幕上将显示表示其标识符 (PID) 的数字。如果进程当前未运行，命令将不会任何输出。

更多信息请参阅 `gnome-screensaver-command(1)` 手页。

> 重要：上述描述的锁定屏幕方法依赖于手动激活。因此，管理员应该建议用户在每次离开电脑时都锁定电脑，即使只离开一会。

#### 2.1.9.1. 使用 gnome-screensaver-command 锁定 GNOME

Red Enterprise Linux 6 的默认桌面环境 GNOME 包含一个允许用户随时锁定屏幕的功能。有几种方法可以激活锁定：

- 按系统 → 偏好 → 键盘快捷键 → 桌面 → 锁定屏幕中指定的组合键。默认组合键为 Ctrl+Alt+L。
- 在面板上选择 系统 → 锁定屏幕。
- 从命令行界面执行以下命令：

```
gnome-screensaver-command -
```

所有描述的技术具有相同的结果；屏幕保护程序被激活且屏幕被锁定。用户随后可以按任意键取消屏幕保护程序，输入密码并继续工作。

请记住，此功能需要 `gnome-screensaver` 进程正在运行。你可以使用任何提供进程信息的命令来检查是否如此。例如，在终端执行以下命令：

```
pidof gnome-screensaver
```

如果 `gnome-screensaver` 进程当前正在运行，执行命令后屏幕上将显示表示其标识符 (PID) 的数字。如果进程当前未运行，命令将不会任何输出。

更多信息请参阅 `gnome-screensaver-command(1)` 手页。

> 重要：上述描述的锁定屏幕方法依赖于手动激活。因此，管理员应该建议用户在每次离开电脑时都锁定电脑，即使只离开一会。

#### 2.1.9.1. 屏幕保护程序激活自动锁定

正如 `gnome-screensaver` 名称所示，屏幕保护程序激活功能与屏幕保护程序相关。在你可以访问的机器上，可以使用 ssh 锁定屏幕，只要目标机器接受此协议。执行以下命令：

```
ssh <username>@server> "export DISPLAY=:0; gnome-screensaver-"
```

缓冲区溢出攻击 — 连接到 0 到 2023 号端口的服务必须以管理员用户身份运行。如果应用程序存在可利用的缓冲区溢出漏洞，攻击者就可以以运行守护进程的用户身份访问系统。由于存在可利用的缓冲区溢出，黑客使用自动化工具来识别漏洞，一旦获得访问权限，他们就会使用自动化 rootkit 来维持对系统的访问。

## 注意事项

Red Hat Enterprise Linux 通过 ExecShield 缓解了缓冲区溢出漏洞的威胁，ExecShield 是一种由 x86 单元支持的可执行内存分段保护技术。ExecShield 通过将虚拟内存分为可执行段和不可执行段来降低缓冲区溢出的风险。任何尝试在可执行段之外执行程序的代码（例如从缓冲区溢出注入的恶意代码）都会触发段错误并终止。

ExecShield 还包括对 AMD64 平台上的无执行（NX）技术和 Intel® 系统上的 Execute XD 技术的支持。这些技术与 ExecShield 协同工作，防止恶意代码以 4KB 可执行代码的粒度在虚拟内存的可执行部分运行，从而降低来自缓冲区溢出攻击的风险。

## 重要

为了限制受到网络攻击的风险，请禁用所有未使用的服务。

### 2.1.10.2. 识别和配置服务

为了增强安全性，大多数通过 Red Hat Enterprise Linux 安装的网络服务默认都是关闭的。然而，还有一些显著的例外：

- `cupsd` — Red Hat Enterprise Linux 的默认打印服务器
- `lpd` — 一种替代打印服务器。
- `xinetd` — 一个超级服务器，用于控制到一系列从服务器（如 `gssftp` 和 `telnet`）的连接。
- `sendmail` — SendMail 传输代理 (MTA) 默认启用，但仅监听来自本地主机（localhost）的连接。
- `sshd` — OpenSSH 服务器，是 Telnet 的安全替代方案。

在决定是否保持这些服务的运行时，最好根据常识判断并避免风险。例如，如果没有打印机可用，就不要让 `cupsd` 运行。`portmap` 也是如此。如果您没有挂载 NFS3 卷或使用 NIS（`ypbind` 服务），则应该禁用 `portmap`。

## 服务配置

![](img/fa49fe194038627f7baabbe849816a0e_58_0.png)

图 2.3. 服务配置工具

如果您不确定特定服务的用途，服务配置工具有一个描述字段（如图 2.3，“服务配置工具”所示），该字段可提供额外信息。

检查网络服务是否可以在启动时启动运行是不够的。建议检查哪些端口是开放并监听状态的。更多信息请参阅第 2.2.9 节“验证哪些端口正在监听”。

### 2.10.03. 不安全的服务

从潜在角度来说，任何网络服务都是不安全的。这就是为什么关闭未使用的服务如此重要的原因。服务的漏洞利用经常被发现并修补，因此定期更新与任何网络服务相关的包非常重要。更多信息请参阅第 1.5 节“安全更新”。

某些协议在本质上比其他协议更不安全。这些包括以下变体：

- 在网络上以明文传输用户名和密码 — 许多协议（如 Telnet 和 FTP）不对身份验证会话进行加密，应尽可能避免使用。
- 在网络上以明文传输敏感数据 — 许多协议在未加密的网络上传输数据。由于这些协议包括 Telnet、FTP、HTTP 和 SMTP。许多文件系统（如 NFS 和 SMB）也会在未加密的网络上传输信息。在使用这些协议时，限制传输的数据类型是用户的责任。

远程转储服务（如 `netdump`）通过网络以明文传输内存内容。内存转储可能包含密码，甚至更糟糕数据库条目和其他敏感信息。

其他服务如 **finger** 和 **rhod** 会暴露有关系统用户的信息。

本质上不安全服务的示例包括 **login、rsh、telnet、** 和 **vsftpd**。

所有的远程登录和 shell 程序（**login、rsh 和 telnet**）都应避免使用，改为使用 SSH。有关 **sshd** 的更多信息请参阅第 2.1.12 节“安全增强通信工具”。

FTP 在系统安全方面不像远程 shell 那样危险，但必须对 FTP 服务器进行仔细配置和监控以避免问题。有关保护 FTP 服务器的更多信息，请参阅第 2.2.6 节“保护 FTP”。

应该仔细实现并置于防火墙后的服务包括：

- finger
- authd（在之前的 Red Hat Enterprise Linux 版本中称为 ident）
- netdump
- netdump-server
- nfs
- rhod
- sendmail
- smb (Samba)
- yppasswdd
- pyserv
- pyxfrd

有关保护网络服务的更多信息请参阅第 2.2 节“服务器安全”。

下一节将讨论用于设置简单防火墙的工具。

### 2.1.11. 个人防火墙

在配置了必要的网络服务后，实施防火墙非常重要。

> **重要**：在连接到互联网或任何你不信任的网络*之前*，请配置必要的服务并实施防火墙。

防火墙防止数据包访问系统的网络接口。如果对被防火墙拦截的端口发送请求，该请求将被忽略。如果服务正在监听这些被拦截的端口之一，它将无法接收数据包并实际上被禁用了。为此，请确保在在使用防火墙时阻止对未使用端口的访问，同时不要阻止对已配置服务端口的访问。

对于大多数用户来说，配置简单防火墙的最佳工具是具有图形界面的 Red Hat Enterprise Linux **防火墙配置工具 (system-config-firewall)**。该工具创建 `iptables` 规则。

对于高级用户和服务器管理员，手动使用 **iptables** 配置防火墙是更好的选择。参阅第 2.8.2 节“基本防火墙配置”获取更多信息。参阅第 2.8.9 节“IPTables”获取 `iptables` 命令的全面指南。

### 2.1.12. 安全增强通信工具

随着互联网规模和流行的增长，通信拦截的威胁也随之增加。多年来，开发了一些工具在网络传输时进行加密。

Red Hat Enterprise Linux 具有两种使用公密钥加密算法保护网络传输的基本工具：

- **OpenSSH** — 用于加密通信的 SSH 协议的免费实现。
- **Gnu Privacy Guard (GPG)** — PGP（良好隐私）加密应用的免费实现。

OpenSSH 是一种更安全的远程访问方式，并取代了旧的不安全服务 **telnet** 和 **rsh**。OpenSSH 包括一个名为 **sshd** 的网络服务以及三个命令行应用程序：

- **ssh** — 安全远程访问客户端。
- **scp** — 安全远程复制命令。
- **sftp** — 允许交互式文件传输会话的伪 FTP 客户端。

有关 OpenSSH 的更多信息请参阅第 3.2.2 节“Secure Shell”。

![](img/fa49fe194038627f7baabbe849816a0e_60_0.png)

> **重要**：虽然 **sshd** 服务本质上是安全的，但*必须*保持更新以防止安全威胁。更多信息请参阅第 1.5 节“安全更新”。

GPG 是确保隐私通信的一种方式。它可以既用于在公共网络上发送敏感数据，也可用于保护硬盘上的敏感数据。

## 2.2. 服务器安全

当系统作为公共网络上的服务器使用时，它就成了攻击的目标。对于系统管理员来说，加固系统和锁定服务至关重要。

在研究特定问题之前，请查看以下增强服务器安全的建议：

- 保持所有服务最新，以防御最新的威胁。
- 尽可能使用安全协议。
- 尽可能每台机器仅运行一种网络服务。
- 仔细监控所有服务器以发现疑活动。

### 2.2.1. 使用 TCP Wrappers 和 xinetd 保护服务

TCP Wrappers 为各种服务提供了访问控制。大多数现代网络服务（如 SSH、Telnet 和 FTP）都使用 TCP Wrappers，它们守卫在传入请求与服务之间

以及请求的服务。

当 TCP Wrappers 与 **xinetd** 配合使用时，其优势会得到增强。`xinetd` 是一个提供额外的访问、日志、绑定、重定向和资源利用控制的超级服务器。

# 注意

将 `iptables` 防火墙规则与 TCP Wrappers 和 **xinetd** 结合使用，可以在服务访问控制中创建冗余。有关使用 `iptables` 命令实现防火墙的更多详细信息，请参阅第 2.8 节“防火墙”。

以下子节假设读者对每个主题都有基础知识，并将重点放在特定的安全选项。

#### 2.2.1.1. 使用 TCP Wrappers 增强安全性

TCP Wrappers 的功能不仅限于拒绝服务的访问。本节说明了如何使用它们发送连接横幅（banners）、警告来自特定主机的攻击以及增强日志功能。有关 TCP Wrapper 的功能和控制，请参阅 **hosts_options** 页面。请参阅在线上的 http://linuxdie.net/man/5/xinetd.conf **xinetd.conf** 页面以获取可用标志，这些标志可以作为您提供服务的选项。

#### 2.2.1.1. TCP Wrappers 与连接横幅

当用户连接到服务时显示横幅是让攻击者知道系统管理员正在访问的一种良好方法。您可以控制向用户展示哪些系统信息。要为服务实现 TCP Wrappers 横幅，请使用 **banner** 选项。

此示例为 **vsftpd** 实现了一个横幅。首先，创建一个横幅文件。它可以位于系统上的任何位置，但名称必须与守护进程相同。例如，该文件名为 **/etc/banners/vsftpd**，并包含以下内容：

```
220-Hello, %C
220-All activity on ftp.example.com is logged.
220-Inappropriate use will result in your access privileges removed.
```

%c 令牌提供了各种客户端信息，例如用户名和主机名，或用户名和 IP 地址，使连接更具威慑力。

为了让此横幅显示在入站连接中，请在 **/etc/hosts.allow** 文件中添加以下行：

```
vsftpd : ALL : banners /etc/banners/
```

#### 2.2.1.2. TCP Wrappers 与攻击警告

如果检测到特定主机或网络正在攻击服务器，可以使用 TCP Wrappers 通过 **spawn** 守护进程向管理员警告来自该主机或网络的后续攻击。

在此示例中，假设检测到一个一个来自 206.162.68.0/24 网络的破解者试图攻击服务器。在 **/etc/hosts.deny** 中放置以下行，以拒绝来自该网络的任何连接尝试，并将这些尝试记录到特殊文件中：

# 红帽企业级 Linux 6 安全指南

```
ALL : 206.186.68.0 : spawn /bin/echo `date` %c %d >> /var/log/intruder_alert
```
