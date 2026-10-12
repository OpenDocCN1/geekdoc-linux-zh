

## 使用拨号守护进程

另一个您可以在 `rp3` 和 `kppp` 中使用的有用实用程序是 `diald`，即拨号守护进程程序。当您对正常内网之外的 Web 页面、服务或服务器连接发起请求，且您的调制解调器已开启时，diald 将自动拨打您的默认 ISP 号码或在您的任何拨号程序中指定的服务提供商号码。它还会在两台计算机之间建立 PPP 会话。diald 程序可以让您看起来像全天候通过 SLIP 或 PPP 链路连接到互联网，每周 7 天，每天 24 小时。您可以配置该程序，使其在面对电话线问题时保持链路全天候连接，或者在需要连接时让调制解调器拨号，或者在不再需要时挂断线路。

一些 ISP 不赞成使用重新拨号程序或滥用电话特权，因此在实施任何此类协议之前，请先联系您的 ISP。

diald 再次表明，对于任何在 Windows 或其他系统下存在的程序，Linux 都有等效或更优的对应程序。

> **注意**
>
> 有关 diald 的更多信息以及下载此程序，请访问其网站 [http://diald.unix.ch/](http://diald.unix.ch/) 或在互联网上进行快速搜索。

## 配置机器作为独立 PPP 服务器

除了将您的 Linux 机器设置为与 ISP 的调制解调器进行 PPP 通信外，您还可以配置自己的机器与另一台 Linux 机器进行 PPP 通信，从而为另一台机器和网络提供连接及其带宽访问权限。虽然一些 ISP 提供大量设备来连接到互联网，包括路由器、交换机、租用线路以及各种其他机制以确保客户获得最快的连接，但您也可以为自己提供相同的条件。

如果您拥有专用的互联网连接并且有一条可用的模拟线路，您可以在任何 Red Hat Linux 机器上设置一个调制解调器，让它接听来自您的家庭计算机或任何其他带有调制解调器的计算机的有效电话呼叫，从而建立有效的拨号连接并访问互联网。由于 Linux 上的许多工具都允许其作为服务器运行，您还可以配置 Linux 以授予个别拨号用户 PPP 访问权限，并给予这些机器与 Linux 相同的访问权限。Linux 可以为任何知道如何运行 PPP 和 TCP/IP 的机器充当 PPP 服务器。

![](img/a0884097af3186d9b4f616aaa3f065b0_622_0.png)

例如，在我的办公室，我有一条通往互联网的专用 OC3 线路，我的 Linux 机器可以从中获取带宽。在家，我有一条简单的 33.6 调制解调器连接——速度很慢但极其可靠的连接。绕过我的 ISP 直接拨打办公地点的 Linux 机器，就能获得一条通往互联网的专用线路，并防止我通过 ISP 可能遇到的任何忙音。然而，在您尝试设置任何类似配置之前，请先确保您的线路可以成功用于此目的。

![](img/a0884097af3186d9b4f616aaa3f065b0_622_1.png)

要创建一个独立 PPP 服务器，请按照以下步骤操作：

- 1. 收集必要的硬件，如调制解调器、串行电缆、模拟电话线等。
- 2. 正确配置您的调制解调器以接听来电。确保它不与传真机等另一设备竞争。
- 3. 验证您的系统包含某种线路监控设备，如 getty 或 mgetty。
- 4. 配置 Linux，使其在机器接听电话后启动 pppd 守护进程。
- 5. 正确配置您的 /etc/inittab 文件以监听来电。

下一节将详细描述这些要求的每一步。

此过程涉及两台机器：服务器和客户端。您将最为详细地查看服务器。这是通过局域网或高速连接连接到互联网的 Linux 机器。客户端可以是您希望授予互联网连接的家庭 Linux 或 Windows 机器。

在充当独立 PPP 服务器的服务器机器或 Linux 机器上，请确保您完成以下步骤：

- 1. 验证已安装 PPP 守护进程。简单的 rpm 查询可以确认这一点：`rpm -q ppp`。
- 2. 检查确保您的内核中编译了 PPP 支持。如果您使用的是随 Red Hat 安装附带的默认内核，您应该已经启用了模块化 PPP 支持。
- 3. 如果您使用的是自定义内核，请开启 PPP 支持。如果 SLIP 是您首选的连接方式，您还可以启用 SLIP 支持。
- 4. 确保所有用户都可以使用 pppd。输入以下命令：`chmod u+s /usr/sbin/pppd`。
- 5. 在 /etc/bashrc 文件中添加此行：`alias ppp="exec /usr/sbin/pppd -detach"`。启用此选项后，PPP 守护进程可以分叉并作为与发起它的终端分离的后台进程运行。
- 6. 确保已安装 mgetty。在 /etc 目录中检查是否有一个 `mgetty+sendfax/` 目录。此目录包含您可能需要修改的几个配置文件。

## 设置拨号服务器

现在，您可以开始在服务器上建立物理连接。将您的调制解调器插入可用的内部插槽，或将外部调制解调器连接到相应的 COM 端口。我的外部调制解调器连接到 COM1。使用 Red Hat 控制面板中的 modemtool 命令，选择您的调制解调器将使用的 COM 端口。此选择会在设备名称和调制解调器之间创建一个符号链接。您也可以通过在命令行输入以下内容来实现同样效果：`ln -s /dev/ttyS0 /dev/modem`。

接下来，进入 /etc/ppp 目录并检查其内容。应该有一个名为 options 的文件。您应该将此文件复制为更具可配置性和标识性的名称，例如 options.ttyS0。您可以开始编辑这个新文件。

在我自己的 /etc/ppp/options.ttyS0 文件中，如果您希望获得真正的互联网访问权限，这些必须是有效的 IP 地址。

您需要在第一个字段中放置 Linux 服务器的 IP 地址，然后在冒号后放置您将要分配给拨号客户端机器的 IP 地址：

`205.82.148.21:205.82.148.20`

接下来，检查您的 /etc/mgetty+sendfax/login.config 文件。确保输入了以下一行，并根据您的特定文件名进行自定义：

`/autoPPP/ - ppp /usr/sbin/pppd file /etc/ppp/options.srv`

现在，检查您的 /etc/ppp/options.srv 文件的内容。清单 16.1 展示了您输入内容的示例。请更改值以反映您自己的系统。

### 清单 16.1 指定调制解调器需求的 options.srv 文件示例

```
auth
-chap
\*pap
login
asyncmap 0
:205.82.148.20
debug
modem
crtcts
ms-dns 205.82.148.253
ms-dns 205.82.148.254
proxyarp
```

最后，检查您的 /etc/inittab 文件，并确保输入清单 16.2 中显示的最后一行。

### 清单 16.2 包含生成调制解调器连接条目的 /etc/inittab 文件

```
# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3

4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
# \# 0:2345:respawn:/sbin/mgetty ttyS0 -D /dev/ttyS0
# \# 0:2345:respawn:/sbin/ugetty -d /etc/default/ugetty.ttyS0 ttyS0
\#115200 vtl00
d1:345:respawn:/sbin/mgetty -n 1 ttyS0
```

倒数第二行和倒数第三行被注释掉了，但它们也能实现必要的连接。最后一行可能是您的最佳选择，因为我使用它的成功率比其他两个高。描述相同方法的 Web 页面引用了这两个被注释的行作为它们的示例条目。

接下来，创建一个名为 dialup 或 remon 或能够识别该新用户的其他名称的用户。使用 `/usr/sbin/adduser` 命令创建此用户，然后使用 `passwd` 命令为该新用户分配唯一密码。使用一个不易被识别的名称。

`/etc/ppp/options.srv` 文件包含一个 `+pap` 条目，因此您必须在 `/etc/ppp/pap-secrets` 文件中为该用户添加一行。以下是一个示例条目的样子：

```
# Secrets for authentication using PAP
# client       server       secret               IP addresses
dialup   *          password   *
```

如果您希望允许其他拨号用户通过调制解调器连接访问您的机器，也请将他们的用户名和密码输入此处。用客户端相应的用户名和密码替换 `dialup` 和 `password` 字样。

## 启用 IP 转发

最后一项业务是确保开启 IP 转发。此选项应存在于您的内核中，但如果您在内核重新编译期间没有定义它，可能需要手动启动该模块。在 Red Hat 下，您需要编辑的文件位于 `/etc/sysconfig/network`。您的配置可能如下所示：

```
NETWORKING=yes
FORWARD_IPV4=yes
HOSTNAME=quasi.astronomy.org
GATEWAY=205.82.148.1
GATEWAYDEV=
```

第二行应该设置为 `yes`。同样，为了安全目的，网关的 IP 地址已被更改，尽管对该名称进行一次简单的 `nslookup` 应该会显示完整的地址。

您可能还需要开启 `proxy_arp` 设置：

```
echo 1 >/proc/sys/net/ipv4/conf/default/proxy_arp
```

