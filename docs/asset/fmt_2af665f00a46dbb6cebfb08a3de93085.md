
```bash
$ sudo smbpasswd sam
New SMB password:
Retype new SMB password:
```

此示例假设在安装 Samba 之前，Sam 已经是 Linux 系统上的一个用户。如果你安装了 Samba，它会将所有 Linux 用户复制到 Samba 用户列表中。如果你在安装 Samba 之后添加用户，需要使用 `-a` 选项指示 `smbpasswd` 将该用户添加到 Samba 用户列表中。以下操作将新的 Linux 用户 Max 添加到 Samba 用户列表中，并为 Max 分配一个 Samba 密码：

```bash
$ sudo smbpasswd -a max
New SMB password:
Retype new SMB password:
Added user max.
```

一旦用户拥有 Samba 密码，就可以不带任何参数使用 `smbpasswd` 来更改密码。

如果用户在 Linux 和 Windows 系统上的用户名不同，你必须将 Windows 用户名映射到 Linux 用户名（参见第 811 页的 `username map`）。确保所有将登录 Samba 的 Linux 用户都有 Samba 密码。

你现在应该能够从 Windows 机器访问新的共享内容（第 814 页）。不需要重启 Samba 服务器。

## swat: 配置 SAMBA 服务器

备份 `/etc/samba/smb.conf`

在安装状态下，`/etc/samba/smb.conf` 文件包含大量的注释（第 807 页）。`swat` 工具会覆盖此文件并移除注释。在第一次运行此工具之前，请备份 `smb.conf` 副本以防万一。

`swat`（Samba 网页管理工具，`swat` 软件包）工具是一个针对 `/etc/samba/smb.conf` 文件的基于浏览器的图形编辑器。对于每个可配置参数，它都提供了帮助链接、默认值和一个用于更改值的文本框。`swat` 工具是一个设计良好的工具，它保留了你所编辑的 `smb.conf` 文件的行：你可以使用并学习 `swat`，因此，如果你想使用文本编辑器修改 `smb.conf`，这种过渡将非常顺畅。

`swat` 工具通过 `inetd`（`openbsd-inetd` 软件包）运行。当你安装 `swat` 软件包时，它会安装 `openbsd-inetd` 作为依赖项，并在 `/etc/inetd.conf` 中放置以下行：

```bash
swat stream tcp nowait root /usr/sbin/tcpd /usr/sbin/swat
```

这在 `inetd` 运行时启用 `swat`。如有必要，执行以下命令重启 `inetd` 以使其读取其配置文件：

```bash
$ sudo service openbsd-inetd restart
```

- `重启互联网服务器 inetd`

![](img/c8ae2cd4d550a81142a3ed64b0f61f6a_854_0.png)

图 23-5 本地 `swat` 主页

## 设置 Samba 服务器

现在你应该可以使用 `swat` 了：从本地系统开始，打开浏览器并在地址栏中输入 `http://127.0.0.1:901` 或 `http://localhost:901`。在提示时，输入用户名 `root` 和 `root` 密码（你必须设置 `root` 密码才能配置 Samba 配置；请参第 43 页的说明）。如果你提供了 `root` 以外的用户名，将能够查看某些配置信息但无法进行更改。从远程系统访问，将 `127.0.0.1` 替换为服务器的 IP 地址（但使用旁边的提示）。如果本地系统运行着防火墙且你想从远程系统访问 `swat`，请使用 `gufw` 打开 TCP 端口 `901`（第 876 页）。

## 不允许对 swat 进行非加密远程访问

不要允许从不安全网络上的远程系统访问 `swat`。当你这样做时，`root` 密码将以明文形式通过你正在使用的任何连接传输，并很容易被嗅探。如果你想在不安全的网络上访问，请使用 `ssh` 转发端口 `901`（第 681 页）。

浏览器显示本地的 Samba/`swat` 主页（图 23-5）。这包括指向本地 Samba 文档的链接以及下方列出的按钮。

- 指向本地 Samba 文档的链接。当你点击 Samba 单词（不是图标，而是 Samba/`swat` 主页中 Documentation 单词之前的那个词），`swat` 会切换 Samba 手页，该页定义了每个 Samba 程序。

- `Globals` 编辑 `smb.conf` 中的参数（变量）。

- `SHARES` 编辑 `smb.conf` 中的共享信息。

- `PRINTERS` 编辑 `smb.conf` 中的打印机信息。

- `WIZARD` 重写 `smb.conf` 文件，移除所有注释行和指定默认值的行。

- `STATUS` 显示活跃的连接、活跃的共享和打开的文件。停止并重启 `smbd` 和 `nmbd` 守护进程。

- `VIEW` 显示子集（点击）。

- `PASSWORD` 管理 Samba 密码。

- `Help` 提供有关参数的信息。

当 Ubuntu 在 `smb.conf` 中设置全局参数时，你只需为 Windows 系统添加一个共享，使其能够访问 Linux 服务器上的目录。将以下简单的共享配置添加到 `smb.conf` 文件的末尾，即可允许 Windows 系统上的用户读写本地的 `/tmp` 目录：

```
[tmp]
comment = temporary directory
path = /tmp
writable = YES
guest ok = YES
```

在 Windows 下的共享名称为 `tmp`；Linux 下的路径为 `/tmp`。任何可以登录 Samba 的 Windows 用户（包括访客 `guest`）都可以读取和写入此目录，前提是 Linux 权限允许。若要允许用户登录 Samba，你必须运行 `smbpasswd`（第 803 页）。由于 `browseable` 默认为 `NO`，该共享会显示为服务器上的一个共享，但不会显式地变为可浏览。适用于使用 Samba 的 Windows 用户的权限与映射到该用户的 Linux 用户拥有的权限相同。

## smbd.conf 文件中的参数

`smb.conf` 页面和 `swat list` 帮助功能列出了所有可以在 `smb.conf` 中设置的参数。以下章节列出了一些你可能想要更改的参数：

### 全局参数

- `interfaces`: Samba 使用的以空格分隔的网络列表。以接口名称（如 `eth0`）或 IP 地址/子掩码对（第 462 页）的形式指定。

  默认：除 `127.0.0.1` 之外的所有活动接口。

- `server`: Windows 机器在各处显示的字符串。在字符串内部，Samba 将 `%v` 替换为 Samba 版本，将 `%h` 替换为主机。

  默认：`Samba %v`

  Ubuntu：`%h server (Samba, Ubuntu)`

- `workgroup`: Samba 所属的工作组。设置为与使用服务器的 Windows 客户端所相同的工作组。当 `security`（第 810 页）设置为 `DOMAIN` 时，此参数控制 Samba 使用的域名。

  默认：`WORKGROUP`

### 安全参数

- `encrypt`: `YES` 仅接受来自客户端的加密密码。Windows 98 和 Windows NT 密码 4.0 Service Pack 3 及更高版本默认使用加密密码。此参数使用 `smbpasswd` 验证密码，除非将 `security` 设置为 `SERVER` 或 `DOMAIN`，以防 Samba 使用其他服务器进行验证。

  默认：`YES`

### 设置 Samba 服务器

- `guest account`: 分配给以访客身份登录或映射为访客的用户名；仅在 `guest ok`（813 页）设置为 `YES` 时有效。此用户名应存在于 `/etc/passwd` 中但不应能够登录系统。通常 `guest account` 被赋值为 `nobody`，因为 `nobody` 用户只能访问任何用户都可以访问的文件。如果你在 Linux 系统的其他用途中使用 `nobody` 账户，请将此参数设置为 `nobody` 的其他名称。

  默认：`nobody`

- `hosts allow`: 类似于 `/etc/hosts.allow` 文件（第 465 页）；指定允许连接到服务器的主机。覆盖 `hosts deny` 中指定的主机。良好的策略是在 `hosts deny` 中指定 `ALL`，并在文件中指定你想要授予访问权限的主机。以与 `hosts.allow` 相同指定主机。

  默认：`none`（允许所有主机访问）

- `hosts deny`: 类似于 `/etc/hosts.deny` 文件（第 465 页）；指定不允许连接到服务器的主机。被 `hosts allow` 中指定的主机覆盖。如果你在此文件中指定了 `ALL`，请记住在 `hosts allow` 中包含本地系统 (`127.0.0.1`)。以与 `hosts.deny` 相同指定主机。

  默认：`none`（未排除任何主机）

- `invalid users`: 不允许使用 Samba 登录的用户。

  默认：`none`（允许所有用户登录）

  Ubuntu：`none`（允许所有用户登录）

- `map to guest`: 定义当登录失败时何时映射到访客账户。仅当 `security`（第 810 页）未设置为 `SHARE` 时有用。

  - `Never`（从不）：仅当用户显式提供 `guest` 作为用户名和空密码时，才允许访客登录。

  - `Bad User`（错误用户）：将任何尝试以不存在的用户身份登录的行为视为访客登录。此参数存在安全风险，因为它允许恶意用户快速获取系统上的用户列表。

  - `Bad Password`（错误密码）：对于错误输入密码的用户静默地以访客身份登录。当用户输错密码并在不知情的情况下以访客身份登录时，可能会误导用户，因为他们突然发现共享比以前少。

  默认：`Never`

  Ubuntu：`Bad User`

- `passdb backend`: 指定 Samba 存储密码的方式。设置为 `ldapswd` 用于 LDAP，`passmbswd` 用于 Samba，或 `tdams` 用于 TDB（简单数据库）密码存储。参见第 803 页关于使用 `smbpasswdd` 修改 Samba 密码的说明。

  默认：`smbpasswd`

  Ubuntu：`tdams`

- `passwd chat`: Samba 用于与 `passwd` 程序交互的脚本。如果不遵循此脚本，Samba 将不会更改密码。仅在 `unix sync`（第 810 页）设置为 `YES` 时使用。

  默认：`%new*password* %n*n*new*password* %n\n*changed*`

  Ubuntu：`*Enter*new*s\/password:* %*n\u*Retype*new*s\/password:* %*n%n*updatedasssuccessfully*.`

- `passwd program`: Samba 用于设置 Linux 密码的程序。Samba 将 `%u` 替换为用户用户名。

  默认：`none`

  Ubuntu：`/usr/bin/passwd %u`

- `security`: 指定客户端如何向服务器传输用户和密码信息。选择以下内容之一：

  - `USER`：导致 Samba 要求...

  - `SHARE`：导致 Samba 要求...

  - `SERVER`：导致 Samba 使用...

  - `DOMAIN`：导致 Samba 使用...

  - `ADS`：指示 Samba 使用...

  - `UPDATE`：允许用户迁移...

- `username map`: 映射文件的名称（通常为 `/etc/samba/smbusers`），将 Windows 客户端的用户名映射到服务器上的用户名。此参数仅在 `security`（第 810 页）设置为 `USER` 时有效。

`max log size` 一个整数，指定以 KB 为单位的日志文件最大大小。`0`（零）表示不限制。当文件达到此大同时，Samba 会在文件名后添加 `.old` 并启动新日志，同时删除旧日志文件。

默认: `5000`

Ubuntu: `1000`

### 浏览器参数 (BROWSER PARAMETERS)

域主（`domain master`）是负责维护网络列表的系统，用于浏览 Windows 网络邻域或“我的网络位置”。SMB（第 1172 页）每 11–15 分钟进行一次选举，以确定哪台机器作为域主。

Samba 是否赢得选举取决于两个参数：

- 将 `domain master` 设置为 `YES` 会指示 Samba 服务器参与选举。

- `os level`（操作系统级别）决定了 Samba 服务器投票的权重大小。

将 `os level` 设置为 `2` 应该让 Samba 服务器能够胜过任何 Windows 9x 机器。NT 服务器域控制器——包括 Windows 2000、XP 和 2003——使用的 `os level` 为 `32`。`os level` 的最大设置为 `255`，尽管将其设置为 `60` 就能确保 Samba 服务器赢得选举。

`domain master` 设置为 `YES` 会导致 `nmbd` 成为域主浏览器（`domain master browser`）。如果存在域浏览器，本地主浏览器（`local master browser`）将其列表副本转发给它。如果没有域主浏览器，浏览查询可能无法跨子网边界。Windows PDC（主域控制器）将始终尝试成为域主，如果失败，可能会出现意料之外的行为。更多信息请参考前述讨论。

默认: `AUTO`

`local master` 设置为 `YES` 会导致 `nmbd` 进入子网的本地主浏览器状态。本地主浏览器存储本地子网内实体 NetBIOS（第 1161 页）名称的缓存，以便进行浏览。Windows 机器会自动选举；为了正常工作，网络必须至少有一台 Windows 机器或一个 `local master` 设置为 `YES` 的 Samba 服务器。作为本地主并将 `os level` 设置为较低数值，在所有其他尝试都失败时让其成为本地主，是一种不良的做法。

默认: `YES`

`os level` 一个整数，控制 Samba 在选举中的宣传程度，以及 `nmbd` 成为工作组本地主浏览器的概率。数字越大，本地服务器成为本地主浏览器的概率越高。更多信息请参考本节开头的讨论。

默认: `20`

`preferred master` 设置为 `YES` 会强制 `nmbd` 为本地主进行选举，并带有微弱优势进入本地系统。当 `domain master` 设置为 `YES` 时，此参数可确保本地 Samba 服务器成为域主。在超过一台服务器上设置此参数会导致服务器之间竞争成为主节点，产生大量网络流量，有时会导致不可预测的结果。Windows PDC 会自动像设置了此参数一样运行。

默认: `AUTO`

### 通信参数 (COMMUNICATION PARAMETERS)

- `dns` 当作为 WINS 服务器（第 1181 页）时，如果 Net-BIOS（第 1161 页）解析失败，`YES` 会导致 `nmbd` 使用 DNS。

  默认: `YES`

  Ubuntu: `NO`

- `socket options` 用于与客户端交换数据时使用的网络参数。通过此参数设置 `SO_RCVBUF=8192 SO_SNDBUF=8192` 可能会网络性能。

  默认: `TCP_NODELAY`

- `wins server` `nmbd` 应注册的 WINS 服务器 IP 地址。

  默认: 未启用

- `wins support` 设置为 `YES` 指定 `nmbd` 充当 WINS 服务器。

  默认: `NO`

### 共享参数 (SHARE PARAMETERS)

- 下述每个参数可以在 `smb.conf` 中出现多次，每个共享定义中出现一次。

- `available` 设置为 `YES` 指定该共享为活动状态。将此参数设置为 `NO` 可禁用共享，但继续对其请求进行记录。

  默认: `YES`

- `browseable` 决定共享是否可以被浏览，例如在 Windows 网络位置中查看。

  默认: `YES`

  Ubuntu: `YES`，打印机除外

- `comment` 共享的描述，当从 Windows 浏览网络时显示。

  默认: `none`

  Ubuntu: 各不相同

- `guest ok` 允许以访客身份登录的用户访问此共享。

  默认: `NO`

- `path` 被共享目录的路径。

  默认: `none`

  Ubuntu: 各种

- `read only` 不允许写入访问。使用 `writable` 允许读写访问。

  默认: `YES`

### [HOMES] 共享：共享用户的主目录

用户经常想将他们的 Linux 主目录与 Windows 机器共享。为了让此任务更简单，Samba 提供了 `[homes]` 共享，Ubuntu 对其进行了注释。当定义此共享时，每个用户的主目录将按照指定的参数进行共享。在大多数情况下，以下参数是足够的的：

```
comment = Home Directories
browseable = NO
writable = YES
```

这些设置防止了所有者以外的用户浏览主目录，同时允许登录的所有者拥有完全访问权限。

## 从 Windows 使用 Linux 共享

本节描述了如何从 Windows 机器访问 Linux 目录。

### 浏览共享 (BROWSING SHARES)

要从 Windows 访问 Samba 服务器上的共享，请在 Windows 系统上打开“我的电脑”或“资源管理器”，并在标记为“地址”的文本框中输入 `\` 后跟 Samba 服务器的 NetBIOS 名称（如果你没有分配不同的 NetBIOS 名称，只需输入主机名）。Windows 然后将显示 Linux 系统正在共享的目录。要查看 Linux 系统上的共享，例如输入 `\dog`。

### 映射共享 (MAPPING A SHARE)
