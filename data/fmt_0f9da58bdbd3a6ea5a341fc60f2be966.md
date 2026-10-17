
若无法通过名称或 IP 访问 DNS 服务的计算机，请确认客户端地址记录正确。也可用完整主机名或 IP ping 各客户端和服务器。

## 获取有关 BIND 的更多信息

本章未描述的其他 BIND 选项可参考：

- `/usr/share/doc/bind-*/arm`—含 BIND 9 管理员参考手册的 HTML 和 XML 版本。
- **手册页**—输入 `man` 后跟 `named` 或 `named.conf`。手册页简述 `named` 守护进程和 `named.conf` 文件的选项和变量。
- **互联网软件联盟** (`www.isc.org/products/BIND`)—ISC 网站提供 BIND 信息和下载，含邮件列表、安全公告和历史记录链接。

## 摘要

将 Red Hat Linux 服务器连入 Internet 不可轻率。若服务器关键且维护负担重，应考虑托管服务提供商。

若将 Red Hat Linux 服务器暴露到 Internet 提供 Web、FTP、邮件等服务，需评估安全影响并做好准备。利用本书其他部分描述的功能可创建防火墙、监控日志并跟踪系统文件更改以保护计算机。

控制公共暴露的一种方式是获取域名并配置自己的域名系统 (`DNS`) 服务器。可让 DNS 为从 Internet 请求信息的客户端及本地私有 LAN 用户解析主机名到 IP。

### 第 26 章

### 从 Mac 使用 Linux 服务器

- 本章内容
- Mac OS X 内部
- 使用 Mac OS X 网络服务
- 访问 Samba 服务器
- 访问 AppleTalk (`netatalk`) 服务器
- 在 Linux 中配置 AppleTalk (`netatalk`) 服务器

过去要从 Apple Mac 使用 Linux 服务器，需让 Linux 在 AppleTalk 网络上表现为文件和打印机服务器。旧 Mac（OS 8 或 9）仍如此，但配备 OS X 的新 iMac 则不同。因为 Mac OS X 内部与 Linux 很相似。

本章面向桌面用 Mac、服务器用 Linux 的人。第一部分面向 Mac OS 8/9 和 Mac OS X 桌面用户，第二部分面向 AppleTalk 网络管理员。特别是：

- **面向 Mac 桌面用户** — 说明如何从 Linux 服务器访问共享资源。
- **面向系统管理员** — 说明如何用 `netatalk` 在 Linux 中设置 AppleTalk 服务器。第 17-25 章说明可从 Mac 访问的其他原生 Linux 服务器配置。

本章应读者要求撰写，他们希望用 Linux 替代 Windows 服务器。希望本章帮助您充分利用从易用 Mac 桌面访问强大的网络化 Linux 功能。

### 查看 Mac OS X 内部

新 Apple 计算机内部运行的操作系统是 Mac OS X，也称 Jaguar。与 Linux 一样，OS X 核心是免费的类 UNIX 操作系统

但与 Linux 内核不同，OS X 基于开源项目 Darwin (`www.opendarwin.org`)。

尽管 Mac OS X 和 Linux 表面差异大，但有许多相似之处。Mac 终端可运行类似 Linux 的命令
此外，两者包含许多相同的开源项目。包括：

- `Samba` (Windows file/printer server)
- `Apache` (Web server)
- `CUPS` (Linux print service)
- `Sendmail` (mail transport agent)
- `BIND` (DNS server)

也有一些差异：

- OS X 默认使用 `*tcsh*` shell 而非 Linux 的 `*bash*` shell。环境变量设置方式不同，配置文件为 `~/.tcshrc` 而非 `~/.bashrc`。
- Red Hat Linux 主要受 General Public License 覆盖，OS X 受 Apple Public Source License (APSL) 覆盖。2003 年 8 月发布 APSL 2.0 (`www.opensource.apple.com/apsl`)，现获 Free Software Foundation 认证为自由软件许可。
- Red Hat Linux 使用 Linux 内核；Mac OS X 基于 `*FreeBSD*` 内核。
- 大多数 Linux 配置通过 Red Hat 配置窗口完成，通常从命令行或 GUI 应用创建文本配置文件（多在 `/etc` 目录）；Mac OS X 将配置文件存储在其 `*NetInfo*` 数据库中，主要通过 GUI 工具和 `niutil` 命令操作。
- Red Hat Linux 许多管理操作需 root 权限；OS X discourages 过度使用 root 登录，鼓励授予管理权限的用户账户。

本章示例使用运行 Mac OS X 10.2.6 的 iMac。10.1 到 10.2 有较大改进，若使用前者建议升级。可通过 Apple System Profiler 查看 Mac 的版本。

### 使用 Mac OS X 的网络服务

可通过配置 Network 窗口轻松将 Mac OS X 计算机连接到 LAN。若 Red Hat Linux 计算机配置为 DHCP 服务器（见第 23 章），Mac OS X 客户端可自动检测。也可手动配置 LAN 接口，如下：

- 1. 从 Finder 栏点击 Preferences 并选择 Network。Network 窗口出现以配置网络接口，如图 26-1 所示。

![](img/27a85d56d393921ced6412ae6e8336bf_972_0.png)

图 26-1：配置 Mac OS X 网络接口以连接 Linux 服务器。

- 2. 若从 LAN 连接 Linux 服务器，点击 Show 框并选择 Built-in Ethernet。
- 3. 点击 TCP/IP 选项卡。然后在 Show 框中选择 DHCP 或 Manually。若选择 Manually，可添加计算机的 IP 地址、网络掩码、路由器的位置、DNS 服务器的位置和搜索域。（家庭或小型企业可能有一台 Red Hat Linux 服务器同时作为路由器和 DNS 服务器。此例中 10.0.0.1 同时提供这两个功能。）
- 4. 点击 AppleTalk 选项卡。若已将 Red Hat Linux 服务器配置为 AppleTalk 文件和打印机服务器（使用 `netatalk`），请勾选以启用 AppleTalk 网络协议。
- 5. 点击 Proxies 选项卡。若需通过代理服务器访问 Internet 或其他广域网，点击 Proxies 选项卡并指定使用的代理。

最新 iMac 计算机内置以太网接口，可连接到网络集线器。将 iMac 插入 LAN 集线器后，即可从 Mac OS X 使用 Linux 服务器。

## 使用 AppleTalk（netatalk）从 Mac OS X

AppleTalk 是苹果电脑用于在局域网中共享文件和打印机的传统协议集。虽然 Mac OS X 可以支持 Samba 文件共享，但 AppleTalk 仍然是 Mac 用户访问网络打印机和文件的一种熟悉方式。

Red Hat Linux 内含一个名为 `netatalk` 的软件包，可用于将 Red Hat Linux 配置为 AppleTalk 文件和打印机服务器。对 Mac 客户端而言，`netatalk` 服务器与任何其他 AppleTalk 服务器看起来并无不同。

> **交叉引用：** 请参阅本章稍后部分的“设置 netatalk 服务器”。

要从 AppleTalk 服务器访问共享目录，请单击屏幕顶部 Finder 栏中的 Go，然后选择“连接服务器”。连接服务器窗口出现，如图 26-2 所示。

![](img/27a85d56d393921ced6412ae6e8336bf_973_0.png)

图 26-2：在 Mac OS X 中，可从“连接服务器”窗口查看 Samba 和 AppleTalk 共享。

上例中出现的共享包括一个 Samba 工作组（名为 ESTREET）、一个 AppleTalk 工作组（名为 WORKGROUP）以及一个本地 AppleTalk 组。本地组包含在本地局域网上广播可用性的 AppleTalk 服务器。

在此示例中，出现的 AppleTalk 文件服务器包括名为 duck 的计算机的文件服务器，以及我从同一台计算机配置的两个独立服务器（名为 Guest Volume 和 User Volume）。（请参阅本章稍后部分的“共享 netatalk 卷”以了解这些服务器是如何创建的。）

选择 User Volume 服务器后，会出现一个弹出窗口，要求输入用户名和密码。使用选项窗口设置登录服务器的首选项。您可以将密码添加到钥匙串中，这样每次访问服务器时就不必重复输入。您还可以选择以明文发送密码（这是默认值），并会收到相关警告。服务器会确定您需要输入明文密码还是加密密码。您还可以为登录请求通过 SSH 建立安全连接（这样做有助于防止他人从网络中嗅探您的密码）。

图 26-3 显示了登录窗口以及用于选择连接选项的窗口。

![](img/27a85d56d393921ced6412ae6e8336bf_974_0.png)

**图 26-3**：连接 AppleTalk（netatalk）服务器时选择身份验证选项。

用户名和密码被接受后，表示 AppleTalk 共享的图标会出现在桌面上。双击即可打开共享目录。您可以以登录权限允许的任何方式更改该目录的内容。

## 在 Mac OS 8 或 OS 9 中使用 AppleTalk

在 Mac OS X 之前，Mac 客户端通过“选择器”窗口访问 AppleTalk 共享。访问 `netatalk`（或其他 AppleTalk）服务器的步骤大致如下：

- 1. 单击 Apple 菜单并选择“选择器”。“选择器”窗口出现。
- 2. 单击 AppleShare。本地网络上可用的文件服务器会出现在“选择文件服务器”窗口中。
- 3. 单击要访问的文件服务器并单击“确定”。系统会提示您输入用户名和密码（或仅提供访客登录）。
- 4. 输入所需信息并单击“确定”。表示服务器的图标会出现在桌面上。

此时，您可以打开表示共享目录的图标并开始使用其中包含的文件和子文件夹。

## 使用 Windows/Linux 服务器（Samba）

从 Mac OS X 系统访问 Samba 服务器的步骤与 AppleTalk 步骤类似。与 AppleTalk 步骤一样，您从 Finder 栏打开“前往”菜单并选择“连接服务器”。从“连接服务器”窗口执行以下操作：

- 1. 单击包含您感兴趣的 Samba 服务器的工作组名称。

> **提示：** 如果不确定服务器是 Samba 还是 AppleTalk 服务器，请在单击服务器名称后查看窗口底部的地址。Samba（SMB）地址以 `smb://` 开头，而 AppleTalk 服务器以 `afp://` 开头。

- 2. 选择要打开的服务器并单击“连接”。您可能会在 SMB/CIFS 文件系统身份验证窗口中被提示输入 Samba 用户名和密码，如图 26-4 所示。

![](img/27a85d56d393921ced6412ae6e8336bf_975_0.png)

- 3. 输入用户名和密码（可选，您可以单击“添加到钥匙串”框）。钥匙串可让您存储用户名和密码，这样下次访问此 Samba 共享时就不必再次输入。表示 Samba 共享的图标应出现在桌面上。

如果 Samba 服务器未出现在“连接服务器”窗口中，您可以在窗口底部的地址框中输入服务器的名称或 IP 地址，后跟您想要的共享名称。以下是从“连接服务器”窗口访问 Samba 共享的地址示例：

```
```
