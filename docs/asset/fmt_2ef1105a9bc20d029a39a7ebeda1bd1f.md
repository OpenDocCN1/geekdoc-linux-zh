
笔记本大多数时候连接到公司局域网（LAN）。有时，笔记本所有者要去公司的一个部门，并希望在该部门的局域网上使用笔记本。此外，在晚上，笔记本所有者希望将笔记本连接到家中的局域网。

过去，这种情况需要花费大量的精力来适应。有了克隆接口，只需为原始以太网接口创建两个克隆，并给它们提供适当的信息。这通过选择要克隆的接口并按下克隆按钮来实现。在为克隆设备命名（例如“home”）后，你将看到一个与图 1.4 类似的窗口。

![](img/8ae7f5fad98006e6a164a7db64fb5e18_23_0.png)

图 1.4：克隆接口设置

如你所见，你可以指定备用 IP 地址和子网掩码（网络和广播地址会自动计算），或使用 `bootp` 或 `dhcp` 来配置接口。此外，克隆设备可以配置为启动时启动、在启动时自动启动，并可以设置为任何用户都可以启用或禁用该接口。

## 1.3 系统管理相关增强

### 1.3.6 新的磁盘组

Red Hat Linux 5.0 还包含了一个组，系统管理员可以使用该组赋予某些用户访问系统磁盘驱动器的权限。这可以通过显式完成，也可以通过 `pam.env` 模块完成。

### 1.3.7 sendmail 反垃圾邮件更改

Red Hat Linux 5.0 包含了 `sendmail` 8.8.7。还包含了抑制分发未经请求的商业电子邮件（也称为“垃圾邮件”）的规则。这些规则集由 Claus Aßmann 创建。虽然下面包含了一些信息，但请参阅 Claus 记录其更改的网页，地址为：

`http://www.informatik.uni-kiel.de/~7Eca/email/check.html`

**注意：** 在此 Red Hat Linux 中，`sendmail` 默认不进行中继。正因如此，如果你的 Red Hat Linux 系统必须作为中继，请查看以下信息。

### 概述

此版本已配置为利用 send-mail 的最新更改，通过添加新的 `sendmail` 规则集来防止垃圾邮件。

以下规则集已添加到 `/etc/sendmail.cf` 的 S98（本地添加）部分：

- - `junk`
- `check.mail`
- `check.rcpt`
- `remove_local`
- * `junkIP`
- `check_relay`

这些规则集的作用由 `/etc/mail/` 目录下的以下文件控制：

- * `ip_allow`
- `name_allow`
- `relay_allow`
- `deny`

让我们来看这里的每一个文件。

### ip_allow

这是一个扁平文本文件，包含了允许使用此主机作为中继的主机地址或网络。

该文件的格式为：

```
hhh.hhh.hhh.hhh
ccc.ccc.ccc
bbb.bbb
aaa
```

这些行分别代表主机主机地址、C 类网络、B 类网络和 A 类网络。

### name_allow

这是一个扁平文本文件，包含了允许使用此主机作为中继的主机名或域名。

该文件的格式为：

```
hostname.domain.com
domain.com
```

这些行代表一个主机名和一个域名。

**注意：** 未“包含”在 `ip.allow` 或 `name.allow` 中的主机将收到错误信息“551: xxx, we do not relay”，其中 xxx 是给定的 RCPT 地址。

### relay.allow

这是一个扁平文本文件，包含了此机器将要中继的主机名、域名、主机地址网络：

该文件的格式为：

```
hostname.domain.com
domain.com
hhh.hhh.hhh.hhh
ccc.ccc.ccc
bbb.bbb
aaa
```

该文件的格式与之前描述的 `ip.allow` 和 `name.allow` 文件相同。

**注意：** 由于 `ip.allow`、`name.allow` 和 `relay.allow` 是纯文本文件，对它们的任何更改都必须重启 `sendmail`。这可以通过执行以下命令完成：

```
/etc/rc.d/init.d/sendmail stop; /etc/rc.d/init.d/sendmail start.
```

这是一个扁平文本文件，在使用之前必须通过 `smap(6)` 转换为哈希数据库文件。该文件包含一组电子邮件地址、主机名、域名、主机地址或网络地址，用制表符与错误消息分开。

该文件的格式为：

```
user@domain.com<tab>error message 0
hostname.domain.com<tab>error message 1
domain.domain.com<tab>error message 2
hhh.hhh.hhh.hhh<tab>error message 1
ccc.ccc.ccc<tab>error message 3
bbb.bbb<tab>error message 4
aaa<tab>error message 5
```

每一行代表一个垃圾邮件发送者的标识。可以使用以下命令创建该文件的哈希数据库：

```
smap -v /etc/mail/deny /etc/mail/deny
```

要使用该数据库，在 `sendmail.cf` 中添加以下行：

```
relay = /etc/mail/deny
```

如你所见，你可以指定备用 IP 地址和子网掩码（网络和广播地址会自动计算），或使用 `bootp` 或 `dhcp` 来配置接口。此外，克隆设备可以配置为启动时启动、在启动时自动启动，并可以设置为任何用户都可以启用或禁用该接口。

## 3 系统管理相关增强

### 1.4.1 模块化驱动

在 Red Hat Linux 5.0 中，标准 OSS 驱动已修改为模块化。这允许在不重新编译内核或重启的情况下加载和卸载各种驱动。这项工作由 Alan 完成并由 Red Hat 赞助。

更多信息请参阅 `sndconfig` 目录下的 README 文件。最新的信息可以在 `http://ftp.redhat.com/pub/sound/` 找到。

如果你对模块化驱动有任何问题，请发送邮件到 `sound-bugs@redhat.com`。还有一个与模块化驱动相关的列表（`sound-list@redhat.com`）。要订阅，请向 `sound-list-request@redhat.com` 发送邮件，主题为“subscribe”。

### 1.4.2 声卡配置工具

Red Hat Linux 5.0 还包含了 `sndconfig`，这是一个可以正确配置声卡驱动的界面工具。

关于 `sndconfig` 有几点需要注意：

即插即用——能够检测并配置即插即用卡，例如 Sound Blaster 16 PnP。但请注意当前版本的 `sndconfig` 会创建一个新的 `/etc/isapnp.conf` 文件，其中仅取消了声卡的设置。因此，如果你的系统中其他的即插即用设备，你必须执行以下两种操作之一：

- 将你的声卡 PnP 信息手动添加到现有的 `/etc/isapnp.conf` 中，并使用 `--nprobe` 运行 `sndconfig`。
- 不使用 `--nprobe` 选项运行 `sndconfig`，然后在 `sndconfig` 创建的 `/etc/isapnp.conf` 文件中取消其他 PnP 卡的配置。

无论如何，注意 `sndconfig` 将原始的 `/etc/isapnp.conf` 文件备份为 `/etc/isapnp.conf.bak`。

**修改** `/etc/conf.modules` —— `sndconfig` 修改模块配置文件 `/etc/conf.modules`，添加声卡所需的模块选项信息。注意 `sndconfig` 将原始的 `/etc/conf.modules` 文件备份为 `/etc/conf.modules.bak`。

要设置你的声卡，请运行 `/usr/sbin/sndconfig`。

### 1.4.3 窗口管理器增强

对提供的窗口管理器及其菜单进行了增强。

### 支持的声卡

目前支持以下声卡：

- Sound Blaster 1.0
- Sound Blaster 2.0
- Sound Blaster Pro
- Sound Blaster 16
- Sound Blaster 16 PnP
- Sound Blaster AWE32/AWE64（仅限 SB-16 模式）

# 2 安装准备

虽然安装 Red Hat Linux 是一个简单的过程，但在开始安装之前花一些时间可以使过程变得更加顺畅。在本章中，我们将讨论在开始安装之前应该执行的步骤。

如果您目前运行版本 2.0（或更高版本）的 Red Hat Linux 系统，可以进行升级。请跳过本章以回顾与安装相关的基本问题，并按照指示顺序阅读后续章节。升级过程起始与安装过程完全相同；在启动安装程序并回答几个问题后，系统将引导您选择进行安装或或升级。

在安装 Red Hat Linux 之前，您应该完成以下五件事：

- 1. 确保您拥有安装所需的 Red Hat Linux 组件访问。
- 2. 确保您了解计算机的硬件配置和网络信息。
