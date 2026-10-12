

确认计算机能够互相识别后，您需要确保您的 Linux 机器能够连接到互联网。如果您对此有任何疑问，请参阅“在 Linux 下手动配置调制解调器”一节。

在您的 Linux 机器上连接到互联网后，您使用一个名为 ipchains 的程序来允许计算机通过 Linux 进行通信。请确认您已安装 ipchains。再次输入 `rpm -q ipchains` 命令以检查安装在您机器上的最新版本的 ipchains。如果未安装该程序，请从您的发行版 CD 中安装该程序，或从众多 RPM 发行版网站之一下载它。Red Hat 的发行商拥有许多镜像站点，托管所有可用和已更新的 RPM。ipchains 程序允许您的 Linux 机器充当通往互联网的网关和路由器。它取代了 ipfwadm，这是一个较旧的用于执行 IP 伪装（IP masquerading）的 IP 防火墙管理工具。

与 ipchains 相关的语法起初可能比较棘手。表 16.1 列出了与 ipchains 关联的系统目标（targets）。

### 表 16.1 ipchains 下可用的目标

| 参数 | 定义 |
| :--- | :--- |
| ACCEPT | 允许数据包通过 |
| DENY | 静默丢弃数据包 |
| REJECT | 通知发送者数据包已被丢弃 |
| MASQ | 对数据包进行伪装 |
| REDIRECT | 将数据包发送到防火墙或路由 Linux 机器上的端口。也可能接收后续指令将其发送到另一个端口 |
| RETURN | 将数据包转移到当前链的末尾，并根据链的默认目标进行处理 |

这些是 ipchains 下指定的一些主要目标。此外，还有许多您可以与目标配合使用的命令。表 16.2 解释了每个命令。

### 表 16.2 ipchains 下可用的命令

| 命令 | 定义 |
| :--- | :--- |
| -A chain | 向链添加一条规则 |
| -D chain rule_number | 从链中删除指定编号的规则 |
| -I chain rule_number | 在指定编号之前向链插入一条规则 |
| -R chain rule_number | 替换链中的指定编号规则 |
| -F chain | 清空链。使用此命令等同于逐个向每个链发送 -D 命令 |
| -L chain | 列出链中的规则 |
| -N chain | 创建一个新的用户自定义链 |
| -X chain | 删除一个链 |
| -P chain target | 设置默认目标 |

为了进一步自定义 ipchains，还有额外的选项可用。但对于本示例的目的而言，这些表格涵盖了大部分选项。

## 设置主机或网关

如果您要提供 IP 伪装，该功能的支持必须被编译到内核中。大多数 Red Hat 版本已经提供了 IP 伪装。但是，您可能需要启用某些自定义选项。如果您需要有关编译内核的帮助，请参阅第 14 章。

为了方便起见，列表 16.3 展示了编译启用 IP 伪装的内核所需的主要步骤。您需要自行提供内核中的 IP 伪装选项。

### 列表 16.3 编译启用 IP 伪装的内核所需的基本步骤

```
    cd /usr/src/linux
    make config                # 或选择以下两项之一
        make menuconfig
        make xconfig
    make dep
    make bzImage
        # 现在编辑您的 /etc/lilo.conf 文件。
    make modules
    make modules_install
    make install
    /sbin/lilo
    /sbin/shutdown now -r
```

在设置内核下的 IP 伪装时，您必须编译几个选项。由于内核开发的动态性质，最新内核中的选项可能与下列列出的有所不同。在配置例程提示时，您应该选择所有 IP 伪装选项。

下列列出的选项（如图 16.4 所示）是您输入 `make config` 命令时可能看到的一个示例。在 /usr/src/linux 目录下进行正常编译时，对于以下每个选项，您应该输入 Y（表示是）。随着内核不断成熟并变得不那么实验性，此列表中的选项可能会更加稳定。您还应该在内核配置的网络部分启用以太网支持，该部分在下文中未显示。再次提醒，务必了解您的网络接口卡的制造商。

### 列表 16.4 输入 make config 命令时可能看到的内容

```
CONFIG_EXPERIMENTAL
• 这将允许您选择编译到内核中的实验性 ip_masq 代码
CONFIG_MODULES
• 启用可加载模块支持
• 网络支持
CONFIG_NET
• 网络防火墙
CONFIG_FIREWALL
• TCP/IP 网络
CONFIG_INET
• IP：转发/网关
CONFIG_IP_FORWARD
• IP：防火墙
CONFIG_IP_FIREWALL
• IP：伪装 (EXPERIMENTAL?)
CONFIG_IP_MASQUERADE
• IP：始终碎片重组
CONFIG_IP_ALWAYS_DEFRAG
• 高度推荐
CONFIG_DUMMY
• 虚拟网络驱动器支持
• 推荐
```

成功编译内核、将其复制到正确位置并完成与新内核制作或修改现有内核相关的其他任务后，您可以开始配置网络设置：

- 创建一个回环设备并验证网络支持是否正常工作：
  - `# /sbin/ifconfig lo 127.0.0.1`
  - `# /sbin/route add -host 127.0.0.1 lo`
- 现在测试您自己的网络接口，以确保您可以 ping 自己：
  - `# ping 127.0.0.1`
  - 大多数系统已经设置了回环配置，但请检查和/或在必要时添加。如果您收到回复，您的内部网络是可操作的。
- 现在开始在您的 Linux 设置中添加您系统上的主机：
  - `# /etc/hosts`
  - `192.168.0.20 beta.astronomy.org beta`
  - `192.168.0.30 gamma.astronomy.org gamma`
  - `192.168.0.40 delta.astronomy.org delta`
- 为客户端机器创建路由。在此命令之后，您可以根据需要简单地添加更多客户端，而不需要更改（除非您的小型局域网中有超过 255 个客户端，这不太可能）。
  - `# /sbin/ifconfig eth0 192.168.0.20 netmask 255.255.255.0 up`
  - `# /sbin/route add -net 192.168.0.0 eth0`
- 配置您的 Linux 机器，使客户端机器在 Linux 机器内部“隐藏”其身份。所有数据包将通过您的 Linux 机器路由，然后到您的 ISP，再到互联网。

## 安装链（Chains）

我通过将正确的 ipchains 序列放置在我的 `/etc/rc.d/init.d/network` 文件末尾来实现这一点。虽然可以单独运行脚本，但我希望每次启动或重启网络配置时都能使用此功能。

![](img/a0884097af3186d9b4f616aaa3f065b0_634_0.png)

您也可以轻松地将一个 rc.masquerade 脚本添加到 /etc/rc.d 目录，然后让 rc.local 文件在启动时调用该脚本。将所有用于伪装的所需行复制到一个名为 /etc/rc.d/rc.masquerade.local 的文件中。使用 chmod 命令使该文件可执行，如下所示：

```
chmod 700 /etc/rc.d/rc.masquerade.local
```

将该文件放在 /etc/rc.d/rc.local 文件顶部的某一行。当 rc.local 文件启动时，它也将解析该脚本并启动伪装过程。

![](img/a0884097af3186d9b4f616aaa3f065b0_634_1.png)

如果您选择在 /etc/rc.d/init.d/network 文件中运行伪装脚本，列表 16.5 中显示的代码行应出现在文件末尾之前，紧接在 exit 0 行之前。此脚本使启动和停止网络连接变得非常容易。此示例文本还自动启动 ipchains。以井号或英镑符号（#）开头的行是注释，解释每个部分的功能。

### 列表 16.5 放置在 /etc/rc.d/init.d/network 文件中启用 IP 伪装的示例脚本

```
echo "1" > /proc/sys/net/ipv4/ip_forward
echo "1" > /proc/sys/net/ipv4/ip_dynaddr

# MASQ 超时
# TCP 会话超时的 2 小时超时
# TCP/IP "FIN" 数据包接收后流量 10 秒超时
# UDP 流量 60 秒超时（MASQ'ed ICQ 用户
```

