
## GNOME 桌面配置

2. 选中“互联网（Internet）”菜单旁边的向下箭头，选择“GNOME PPP”，并选中“添加（Add）”。面板上会出现一个 GNOME PPP 电话图标。

3. 选中面板上的新图标。系统会询问您是否要使用调制解调器启动连接。

4. 填写用户名、密码和电话号码，然后选中“连接（Connect）”以开始连接。

## 从 KDE 桌面配置

从 KDE 桌面（安装 `kPPP` 软件包后）：

1. 右键点击面板，然后选择“向面板添加应用程序（Add Application to Panel）→ 互联网（Internet）→ KPPP”。

2. 选中面板上的 KPPP 图标（如果提示，请输入 root 密码）。将显示 KPPP 窗口。

3. 选中您添加的拨号接口（可能是 `ppp0`）并点击“连接（Connect）”进行连接。

从此刻起，您的桌面上将出现图标，您可以选中它们通过您配置的拨号连接立即连接到您的 ISP。

## 按需启动您的 PPP 连接

代替每次想要联系 Internet 时手动启动拨号 PPP 连接，您可以设置您的拨号连接在应用程序（如 Web 浏览器或电子邮件程序）尝试使用连接时自动启动。按需拨号在以下情况下特别有用：

- 您的 Linux 系统上的拨号连接充当家庭或办公室中其他计算机的网关。当另一台计算机需要拨号连接时，您不必跑到您的 Linux 机器旁去启动连接。
- 您在非工作时间运行需要 Internet 连接的程序（如远程备份）。
- 您只是想在 Web 上浏览一点内容，不想麻烦去点击额外的图标。

按需拨号的风险在于，拨号连接可能会在您不希望它启动时启动，因为连接是自动开始的。（有些人担心他们的电脑在半夜自己开始拨号。）

## 检查您的 PPP 连接

为了调试您的 PPP 连接或更好地理解其工作原理，您可以执行以下步骤。这将有助于您理解信息存储在哪里，以及如何使用工具来跟踪这些信息。

### 检查您的调制解调器是否被检测到

您的调制解调器可能不受 Linux 支持。如果是这种情况，您的 PPP 连接可能会失败，因为根本没有检测到调制解调器。要扫描串行端口以查看您的调制解调器可能在哪里，请输入以下命令（作为 root 用户）：

```
$ wvdialconf /etc/wvdial.conf.new
```

`wvdialconf` 命令实际上是用于构建配置文件（`/etc/wvdial.conf` 文件），该文件由拨号器命令（`wvdial`）使用。如果成功，您可以将 `wvdial.conf.new` 文件复制到 `/etc/wvdial.conf`。然而，它的第一个操作是扫描计算机上的串行端口并报告它在哪里发现调制解调器。如果它告诉您未检测到调制解调器，则很可能您的调制解调器未正确连接，或者没有可用的驱动程序来支持该调制解调器。

如果未检测到调制解调器，您应该确定它是否是 Linux 支持的调制解调器。您可以通过查明调制解调器中使用的芯片组类型来做到这一点。这甚至比查明调制解调器的制造商更重要，因为相同的制造商可以使用来自不同公司的芯片。（这主要适用于内部基于软件的调制解调器，因为大多数外部串行调制解调器、内部 PCI 控制器基于的调制解调器以及许多 USB 调制解调器都在 Linux 中得到支持。）

在确定所使用的芯片组后，检查网站 `linmodems.org`。该网站包含有关所谓“Win-modem”的信息。从该网站搜索您调制解调器上的芯片组。它将告诉您是否有可用的调制解调器驱动程序。

一个用于确定您拥有的 Win-modem 类型以及如何使其正常工作的良好工具是 `scanModem`。如果您可以从另一台机器访问 Internet，您可以从此地址下载 `scanModem`：

`http://linmodems.technion.ac.il/packages/scanModem.gz`

由于您可能还没有工作的 Internet 连接，请找到一种方法将 `scanModem.gz` 复制到您的 Linux 系统（例如将其复制到软盘或刻录到 CD 上）。作为 root 用户，在 Terminal 窗口中，当该文件在当前目录时，输入这些命令：

```
# gunzip scanModem.gz
# chmod 755 scanModem
# ./scanModem
```

结果是一个 `Modem` 目录，其中包含描述您的调制解调器以及您可以如何配置它的文本文件。

> **注意：** 如果您是新的 Linux 用户，拥有 Win-modem，并且在参考 `linmodems.org` 网站后仍然感到困惑，您可能需要考虑获取一个串行或 USB 调制解调器。为了使您的 Win-modem 正常工作，您可能需要下载、编译并加载调制解调器驱动程序。特别是对于一些较旧的 Win-modem，驱动程序未更新以支持最新的内核。从二手电脑店挑选一个便宜的串行调制解调器（20 美元以下）可以节省数小时的挫败感，而这些挫败感最终仍可能导致失败。

### 检查您的 PPP 接口是否工作

检查 PPP 接口是否工作的一种方法是使用 `ping` 命令。从 Terminal 窗口，输入 `ping` 加上您知道的任何 Internet 地址。例如：

```
$ ping www.handsonhistory.com
PING handsonhistory.com (198.60.22.8) from 192.168.0.43 : 56(84) bytes of data.
64 bytes from handsonhistory.com (198.60.22.8) : icmp_seq=0 ttl=240 time=120 msec
64 bytes from handsonhistory.com (198.60.22.8) : icmp_seq=1 ttl=240 time=116 msec
64 bytes from handsonhistory.com (198.60.22.8) : icmp_seq=2 ttl=240 time=120 msec

--- www.handsonhistory.com ping statistics ---
```

#### 按需拨号配置示例

以下是您可以添加到您的拨号配置文件中（可能是 `/etc/sysconfig/network-scripts/ifcfg-???`，其中 `???` 被替换为您的提供商名称）以配置按需拨号的设置示例：

```
ONBOOT=yes
DEMAND=yes
IDLETIMEOUT=600
RETRYTIMEOUT=30
```

`ONBOOT=yes` 启动 `pppd` 守护进程（但由于 `DEMAND` 设置为 `yes`，因此不会立即开始拨号）。此外，由于 `DEMAND=yes`，每当流量试图使用您的拨号连接时，都会尝试拨号连接。设置 `IDLETIMEOUT` 为 `600` 后，如果在 600 秒（10 分钟）内没有流量通过连接，连接将断开。设置 `RETRYTIMEOUT` 为 `30` 后，断开的连接将在 30 秒后重试（除非连接是由空闲超时断开的，在这种情况下没有重试）。您可以根据需要更改超时值。

> 注意：由于建立拨号连接可能需要一点时间，在拨号过程中操作可能会失败。特别是，DNS 请求可能在 30 秒内超时，这可能不足以建立拨号连接。如果您为每个客户端配置了三个 DNS 服务器，您有一个 90 秒的超时期限。因此，在请求失败之前，调制解调器连接可能已经在运行。

```
4 packets transmitted, 3 packets received, 25% packet loss

round-trip min/avg/max/mdev = 116.816/119.277/120.807/1.779 ms
```

按 `Ctrl-C` 可结束 `ping` 命令。前面几行显示的是来自 `www.hansonhistory.com` 的响应。该服务器针对收到的每个数据包，从 IP 地址 `198.62.0.28` 发回了数据包。你可以看到数据包的序列号（`icmp_seq`）以及每个响应所花费的时间（以毫秒计）。如果你收到返回的数据包，你将得知两件事：第一，你的连接正在工作；第二，你的名称到地址的转换（来自 `/etc/resolv.conf` 中的 DNS 地址）正在正常工作。

## 检查默认路由

在建立拨号连接后，使用 `route -n` 检查默认路由是否已设置，如下例所示：
