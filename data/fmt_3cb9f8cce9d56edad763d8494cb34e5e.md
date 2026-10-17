
<-内部网络->

在这个示例中，我们关注的是 4 个计算机系统（推测最右侧有某个设备是你连接互联网的 IP 连接，且互联网上某个设备（页面之外）是你感兴趣交换信息的对象）。Linux 系统 `masq-gate` 是 `abox`、`bbox` 和 `cbox` 机器内部网络到互联网的伪装网关。内部网络使用分配的私网地址之一，在本例中为 C 类 `192.168.1.0`，`linux` 机器地址为 `192.168.1.1`，其他系统拥有该网络上的地址。

上述三台机器 `bbox` 和 `cbox`（只要它们支持 IP，可以运行任何操作系统——如 Windows 95、Macintosh MacTCP 甚至是另一个 `linux` 机器）可以连接到网络上的其他机器，然而伪装的 `masq-gate` 会转换所有连接，使其看起来源自 `masq-gate`，并安排返回数据直接路由到互联网，我们并不知道它们的数据正在被伪装。

## 2.6 在 Linux 2.x 上使用 IP Masquerade 的要求

请参考 IP Masquerade 资源 <http://ipmasq.home.ml.org/> 获取最新信息，因为很难频繁更新 HOWTO。

- 内核 2.0 源码可从 <http://ftp.funet.fb/pub/Linux/kernel/src/v2.0/> <http://ftp.funet.fi/Linux/kernel/src/v2.0> 获取。已知推荐使用最新的稳定内核。
- 可加载内核模块，优选从 <http://www.pi.se/biz/modules/modules-2.0.0.tar.gz> <http://www.pi.se/blox/modules-0.tar.gz> 获取（`modules-1.37` 是最低要求）。
- Linux NET-2 HOWTO <http://www.caldera.com/LDP/HOWTO-NET-2-HOWTO.html> 涵盖了配置良好的 TCP/IP 网络，管理员指南 <http://linuxww.db.erau.edu/nag/> 也包含了相关内容。
- Linux ISP Hook HOWTO <http://www.caldera.com/LDP/HOWTO/ISP-Hook-HOWTO.html>、Linux PPP HOWTO <http://www.caldera.com/LDP/HOWTO/PPP-HOWTO.html> 和 Linux PPP-over-ISDN mini-HOWTO <http://www.caldera.com/LDP/HOWTO/mini-PPP-over-ISDN> 涵盖了 Linux 主机的互联网连通性。
- Ipfwadam 2.0 源码来自 <http://ftp.zos.net/pub/linux/ipfwadam/ipfwadam-2.3.tar.gz> <http://ftp.zos.net/pub/linux/ipfwadam/>，关于版本要求的更多信息见 Linux ipfwadam 页面 <http://www.qos.nl/linux/ipfwadam/。
- 你可以选择应用一些 IP Masquerade 补丁来添加其他功能。IP Masquerade 资源 <http://ipmasq.home.ml.org/> 提供了更多信息（这些补丁适用于所有 2.0.x 内）。

## 3. 设置 IP Masquerade

如果你的私有网络包含任何重要信息，在使用 IP Masquerade 前请慎重考虑。这可能是

### 3.1 为 IP Masquerade 编译内核

请参考 IP Masquerade 资源 <http://ipmasq.home.ml.org/> 获取最新信息，因为很难频繁更新 HOWTO。

- 内核 2.0 源码可从 <http://ftp.funet.fb/pub/Linux/kernel/src/v2.0/> <http://ftp.funet.fi/Linux/kernel/src/v2.0> 获取。已知推荐使用最新的稳定内核。
- 可加载内核模块，优选 2.0.0 或更高版本，从 <http://www.pi.se/biz/modules/modules-2.0.0.tar.gz> <http://www.pi.se/blox/modules-0.tar.gz> 获取（`modules-1.37` 是最低要求）。
- NET-2 HOWTO <http://www.caldera.com/LDP/HOWTO-NET-2-HOWTO.html> 涵盖了配置良好的 TCP/IP 网络，管理员指南 <http://linuxww.db.erau.edu/nag/> 也包含了相关内容。
- Linux ISP Hook HOWTO <http://www.caldera.com/LDP/HOWTO/ISP-Hook-HOWTO.html>、Linux PPP HOWTO <http://www.caldera.com/LDP/HOWTO/PPP-HOWTO.html> 和 Linux PPP-over-ISDN mini-HOWTO <http://www.caldera.com/LDP/HOWTO/mini-PPP-over-ISDN> 涵盖了 Linux 主机的互联网连通性。
- Ipfwadam 2.0 源码来自 <http://ftp.zos.net/pub/linux/ipfwadam/ipfwadam-2.3.tar.gz> <http://ftp.zos.net/pub/linux/ipfwadam/>，关于版本要求的更多信息见 Linux ipfwadam 页面 <http://www.qos.nl/linux/ipfwadam/。
- 你可以选择应用一些 IP Masquerade 补丁来添加其他功能。IP Masquerade 资源 <http://ipmasq.home.ml.org/> 提供了更多信息（这些补丁适用于所有 2.0.x 内）。

（注：此处原文存在大量重复的“在使用 IP Masquerade 前请慎重考虑。这可能是”，根据指令要求不重复输出原文，翻译时仅保留核心逻辑或对应结构）

在使用 IP Masquerade 前请慎重考虑。这可能是

- 启用可加载模块支持 `CONFIG_MODULES` 允许你加载模块
- 网络支持 `CONFIG_NET`
- 网络防火墙 `CONFIG_FIREWALL`
- TCP/IP 网络 `CONFIG_IP_FORWARD`
- IP: 转发/网关 `CONFIG_IP_FORWARD`
- IP: 防火墙 `CONFIG_FIREWALL`
- IP: 伪装（实验性）`CONFIG_IP_MASQUERADE` - 虽然是实验性的，但是必须的
- IP: ipautofw 伪装（实验性）`CONFIG_IP_MASQUERADE_AUTOFW` - 推荐
- IP: ICMP 伪装 `CONFIG_IP_MASQUERADE_ICMP`
- 始终去碎片化 `CONFIG_ALWAYS_DEFRAG` - 高度推荐
- 虚拟驱动支持 `CONFIG_DUMMY` - 推荐

注意：这些只是 IP Masquerade 所需的组件，请根据设置选择任何其他选项。

- 编译内核后，你应该编译并安装模块：

```
