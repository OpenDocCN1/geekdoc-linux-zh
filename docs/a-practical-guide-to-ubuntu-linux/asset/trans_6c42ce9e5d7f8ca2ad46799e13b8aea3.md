

# 812 第 23 章 SAMBA：LINUX 与 Windows 文件和打印机共享

max log size 一个整数，指定日志文件以字节（KB）为单位的最大大小。0（零）表示不限制大小。当文件达到此大小时，Samba 会向文件名添加 .old 并开始新日志，同时删除旧的日志文件。

默认：5000
Ubuntu：1000

## 浏览器参数 (BROWSER PARAMETERS)

域主浏览器（domain master browser）是负责维护网络机器列表的系统，该列表用于浏览 Windows“网络”或“我的网络位置”时。SMB（第 1172 页）每 11–15 分钟进行一次加权选举，以确定哪台机器作为域主浏览器。

Samba 服务器是否能赢得此选举取决于两个参数：

- 将 *domain master* 设置为 YES 可指示 Samba 服务器参加选举。
- os level（操作系统层级）决定了 Samba 服务器的票数所获得的权重。

将 os level 设置为 2 应该使 Samba 服务器胜过任何 Windows 9x 机器。NT 服务器域控制器——包括 Windows 2000、XP 和 2003——使用的 os level 为 32。os level 的最大设置为 255，尽管将其设置为 65 应该就能确保 Samba 服务器赢得选举。

domain master YES：nmbd 尝试成为域主浏览器。如果存在域主浏览器，本地域主会将其浏览列表的副本转发给它。如果没有域主，则浏览查询可能无法跨边界。Windows PDC（主域控制器）将始终尝试成为域主，如果失败，它将表现出意料之外的行为。
更多信息请参考前述的讨论。

local master YES：nmbd 为子网内的本地主进行选举。本地主浏览器会存储本地子网内实体的 NetBIOS（第 1161 页）名称的缓存，以便进行浏览。Windows 机器会自动参加选举；为了使浏览正常工作，网络必须至少有一台 Windows 机器或 local master 设置为 YES 的 Samba 服务器。将 local master 设置为 NO 不是良好的做法。如果你不希望某台计算机充本地主，请将其 os level 设置为较低数字，以便在其他情况失败时将其用作本地主。

默认：20

os level 一个整数，控制 Samba 在选举中宣传自己的程度，以及 nmbd 成为其所在组本地主浏览器的概率。数字越高，本地服务器成为本地主浏览器的机会越大。更多信息请参考本节开头的讨论。

默认：20

preferred master YES：nmbd 为本地主举行选举，并以轻微优势进入本地系统。当 domain master 设置为 YES 时，这有助于确保本地 Samba 服务器成为域主。在多台服务器上将此参数设置为 YES 会允许服务器竞争成为主节点，从而产生大量的网络流量，有时会导致不可预知的结果。Windows PDC 会自动像设置了此参数一样运行。

默认：AUTO

## 通信参数 (COMMUNICATION PARAMETERS)

- **dns proxy** 当作为 WINS 服务器（第 1181 页）时，YES 导致 nmbd 在 DNS Net-BIOS（第 1161 页）解析失败时使用 DNS。
默认：YES
Ubuntu：NO

- **socket options** 调整与客户端交换数据时使用的网络参数。在此参数中添加 SO_RCVBUF=8192 SO_SNDBUF=8192 可能会提高网络性能。
默认：TCP_NODELAY

- **wins server** nmbd 应该注册的 WINS 服务器的 IP 地址。
默认：未启用

- **wins support** YES 指定 nmbd 充当 WINS 服务器。
默认：NO

## 共享参数 (SHARE PARAMETERS)

以下每个参数都可以在 smb.conf 中出现多次，每个共享定义中出现一次。

- **available** YES 指定该共享为活动状态。将此参数设置为 NO 可禁用共享，但继续记录该共享的请求。
默认：YES

- **browseable** 决定共享是否可以被浏览，例如在 Windows“网络位置”中。
默认：YES
Ubuntu：YES（打印机除外）

- **comment** 共享的描述，从 Windows 浏览网络时显示。
默认：无
Ubuntu：各异

- **guest ok** 允许以访宾登录的用户访问此共享。
默认：NO

- **path** 被共享目录的路径。
默认：无
Ubuntu：多种

- **read only** 不允许写访问权限。使用 writable 允许读写访问。
默认：YES

## [HOMES] 共享：共享用户的主目录

用户经常希望将其 Linux 主目录与 Windows 机器共享。为了让此任务更容易，Samba 提供了 [homes] 共享，Ubuntu 通常会包含它。当你定义此共享时，每个用户的主目录将根据指定的参数进行共享。在大多数情况下，以下参数就足够了：

```
[homes]
comment = Home Directories
browseable = NO
writable = YES
```

这些设置防止了所有者以外的用户浏览主目录，同时允许登录的所有者完全完全访问。

## 从 Windows 访问 Linux 共享

本节描述了如何从 Windows 机器访问 Linux 目录。

## 浏览共享 (BROWSING SHARES)

要从 Windows 访问 Samba 服务器上的共享，请在 Windows 系统上打开“我的电脑”或“资源管理器”，并在标记为地址的文本框中输入 Samba 服务器的 \NetBIOS 名称（如果你没有分配不同的 NetBIOS 名称，只需输入主机名）。Windows 随后将显示 Linux 系统共享的目录。例如，要查看名为 dog 的 Linux 系统上的共享，输入 \dog。从此窗口...

[/content]

译文：

[content]

# 812 第 23 章 SAMBA：LINUX 与 Windows 文件和打印机共享

max log size 一个整数，指定日志文件以字节（KB）为单位的最大大小。0（零）表示不限制大小。当文件达到此大小时，Samba 会向文件名添加 .old 并开始新日志，同时删除旧的日志文件。

默认：5000
Ubuntu：1000

## 浏览器参数 (BROWSER PARAMETERS)

域主浏览器（domain master browser）是负责维护网络机器列表的系统，该列表用于浏览 Windows“网络”或“我的网络位置”时。SMB（第 1172 页）每 11–15 分钟进行一次加权选举，以确定哪台机器作为域主浏览器。

Samba 服务器是否能赢得此选举取决于两个参数：

- 将 *domain master* 设置为 YES 可指示 Samba 服务器参加选举。
- os level（操作系统层级）决定了 Samba 服务器的票数所获得的权重。

将 os level 设置为 2 应该使 Samba 服务器胜过任何 Windows 9x 机器。NT 服务器域控制器——包括 Windows 2000、XP 和 2003——使用的 os level 为 32。os level 的最大设置为 255，尽管将其设置为 65 应该就能确保 Samba 服务器赢得选举。

domain master YES：nmbd 尝试成为域主浏览器。如果存在域主浏览器，本地域主会将浏览列表的副本转发给它。如果没有域主，则浏览查询可能无法跨边界。Windows PDC（主域控制器）将始终尝试成为域主，如果失败，它将表现出意料之外的行为。
更多信息请参考前述的讨论。

local master YES：nmbd 为子网内的本地主进行选举。本地主浏览器会存储本地子网内实体的 NetBIOS（第 1161 页）名称的缓存，以便进行浏览。Windows 机器会自动参加选举；为了使浏览正常工作，网络必须至少有一台 Windows 机器或 local master 设置为 YES 的 Samba 服务器。将 local master 设置为 NO 不是良好的做法。如果你不希望某台计算机充本地主，请将其 os level 设置为较低数字，以便在其他情况失败时将其用作本地主。

默认：20

os level 一个整数，控制 Samba 在选举中宣传自己的程度，以及 nmbd 成为其所在组本地主浏览器的概率。数字越高，本地服务器成为本地主浏览器的机会越大。更多信息请参考本节开头的讨论。

默认：20

preferred master YES：nmbd 为本地主举行选举，并以轻微优势进入本地系统。当 domain master 设置为 YES 时，这有助于确保本地 Samba 服务器成为域主。在多台服务器上将此参数设置为 YES 会允许服务器竞争成为主节点，从而产生大量的网络流量，有时会导致不可预知的结果。Windows PDC 会自动像设置了此参数一样运行。

默认：AUTO

## 通信参数 (COMMUNICATION PARAMETERS)

- **dns proxy** 当作为 WINS 服务器（第 1181 页）时，YES 导致 nmbd 在 DNS Net-BIOS（第 1161 页）解析失败时使用 DNS。
默认：YES
Ubuntu：NO

- **socket options** 调整与客户端交换数据时使用的网络参数。在此参数中添加 SO_RCVBUF=8192 SO_SNDBUF=8192 可能会提高网络性能。
默认：TCP_NODELAY

- **wins server** nmbd 应该注册的 WINS 服务器的 IP 地址。
默认：未启用

- **wins support** YES 指定 nmbd 充当 WINS 服务器。
默认：NO

## 共享参数 (SHARE PARAMETERS)

以下每个参数都可以在 smb.conf 中出现多次，每个共享定义中出现一次。

- **available** YES 指定该共享为活动状态。将此参数设置为 NO 可禁用共享，但继续记录该共享的请求。
默认：YES

- **browseable** 决定共享是否可以被浏览，例如在 Windows“网络位置”中。
默认：YES
Ubuntu：YES（打印机除外）

- **comment** 共享的描述，从 Windows 浏览网络时显示。
默认：无
Ubuntu：各异

- **guest ok** 允许以访宾登录的用户访问此共享。
默认：NO

- **path** 被共享目录的路径。
默认：无
Ubuntu：多种

- **read only** 不允许写访问权限。使用 writable 允许读写访问。
默认：YES

## [HOMES] 共享：共享用户的主目录

用户经常希望将其 Linux 主目录与 Windows 机器共享。为了让此任务更容易，Samba 提供了 [homes] 共享，Ubuntu 通常会包含它。当你定义此共享时，每个用户的主目录将根据指定的参数进行共享。在大多数情况下，以下参数就足够了：

```
[homes]
comment = Home Directories
browseable = NO
writable = YES
```

这些设置防止了所有者以外的用户浏览主目录，同时允许登录的所有者完全访问。

## 从 Windows 访问 Linux 共享

本节描述了如何从 Windows 机器访问 Linux 目录。

## 浏览共享 (BROWSING SHARES)

要从 Windows 访问 Samba 服务器上的共享，请在 Windows 系统上打开“我的电脑”或“资源管理器”，并在标记为地址的文本框中输入 Samba 服务器的 \NetBIOS 名称（如果你没有分配不同的 NetBIOS 名称，只需输入主机名）。Windows 随后将显示 Linux 系统共享的目录。例如，要查看名为 dog 的 Linux 系统上的共享，输入 \dog。从此窗口...

