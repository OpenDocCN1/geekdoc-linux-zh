
The NSA includes five general principles for securing operating systems in general and RHEL in particular.

- **尽可能加密传输的数据** NSA 关于加密的建议包括在应为私密且安全的网络上进行通信。SSH, with the security options described in Chapter 11, are an excellent step in this process.
- **最小化软件以最小化漏洞** As suggested by the NSA, “The simplest way to avoid vulnerabilities in software is to avoid installing that software.” The NSA pays special attention to any software that can communicate over a network, including the Linux GUI. The minimal installation of RHEL 6 includes far fewer packages than the comparable installation of RHEL 5.
- **在不同的系统上运行不同的网络服务** This is consistent with the concept of bastion servers described earlier in this chapter. Implementation is made easier by the flexibility afforded by virtual machine technologies such as KVM.
- **配置安全工具以提高系统健壮性** The RHCSA and RHCE objectives have this well covered, with the use of iptables-based firewalls, SELinux, and appropriate log collection services.
- **最小权限** In principle, you should give users the minimum privileges required to accomplish their tasks. Not only does that mean minimize access to the root administrative account, but also careful use of the sudo command privileges. SELinux options such as the user_u role for confinement described in Chapter 4 may also be helpful to that end.

## PolicyKit

The PolicyKit is one more security mechanism designed to help protect different administrative tools. When starting an administrative tool in the GUI from a regular account, most tools prompt for the root administrative password with a window similar to Figure 10-1.

Alternatively, you might see a slightly different window similar to that shown in Figure 10-2. Functionally, the effect is the same. As described in the window, authentication by the superuser is required. In this case, you'd still have to enter the root administrative password. However, there's a difference, as shown under details.

### 图 10-1

GUI 中访问管理工具需要 root 密码。

![](img/9139201cfcaf4292284a0eed074928e5_565_0.png)

The action specifies the policy required by the "vendor," in this case, the system-config-firewall command.

The action noted is "org.fedoraproject.config.firewall.auth," which is associated with a policy file in the /usr/share/polkit-1/actions directory. Policy configuration files are stored in this directory; the corresponding file for the system-config-firewall tool is org.fedoraproject.config.firewall.policy

These policy files are configured in XML format and may be modified further to support fine-grained control by individual users. However, since the PolicyKit only works within the GUI, its fine-grained controls do not affect the use of administrative tools from the console. It certainly does not prevent administrators from configuring or otherwise controlling important services. If fine-grained control is required, the better tool is the /etc/sudoers file described in Chapter 8.

### 图 10-2

PolicyKit 可能会限制对管理工具的访问。

![](img/9139201cfcaf4292284a0eed074928e5_565_1.png)

## 认证目标 10.02

## 防火墙和网络地址转换

通常，防火墙位于内部局域网和外部不安全网络（如互联网）之间。防火墙可以配置为检查进入或离开您局域网的每个网络数据包。当配置适当的规则时，它可以过滤掉可能对局域网上的系统构成安全风险的数据包。

然而，为了遵循 NSA 建议的精神，您将在每台系统上配置防火墙。虽然网络地址转换使用相同的 iptables 命令，但其使用通常仍最适用于局域网和外部网络之间的网关或路由器上的系统。

### 定义

基于 iptables 命令的防火墙通过读取每个网络数据包的头部工作。根据头部包含的信息，可以使用基于 iptables 的规则来过滤每个数据包。要了解数据包过滤的工作原理，您需要了解有关信息如何在网络上传输的一些知识。

在消息通过网络发送之前，该消息会被分解为称为数据包的较小单元。管理信息，包括数据类型、源地址和目标地址，会添加到每个数据包的头部。数据包在到达目标计算机时重新组装。防火墙检查每个头部中的字段。根据现有规则，防火墙随后可能对该数据包采取以下四种操作之一：

- 允许数据包进入系统。
- 如果当前系统是网络之间的网关或路由器，则将数据包转发到其他系统。
- 拒绝数据包并向源 IP 地址发送消息。
- 丢弃数据包而不发送任何消息。

无论结果如何，决策都可以被记录。如果有大量数据包被拒绝或丢弃，日志文件可能很有用。

RHEL 6 提供了配置系统为防火墙所需的一切，包括用于 IPv4 和 IPv6 网络的 iptables 和 ip6tables 命令。

相比之下，NAT 隐藏了连接到外部网络的局域网计算机的 IP 地址。NAT 用带防火墙的网关或路由器系统的 IP 地址替换内部源地址。该内部源地址缓存在网关上，因此它知道哪个计算机发出了请求。

当防火墙接收到网页等数据时，过程会反转。当数据包通过防火墙时，原发计算机在缓存中被识别。在数据包被发送出去之前，每个数据包的头部会相应地被修改。

这种方法有几个好处。隐藏内部 IP 地址使得黑客更难知道使用哪个 IP 地址入侵内部网络。NAT 支持具有私有 IP 地址的系统与外部网络（如互联网）之间的连接。这就是 IPv4 地址能够长期存活的原因。在 Linux 世界中，此过程称为 IP 伪装。

### iptables 命令的结构

iptables 命令组装成防火墙的方式基于“链”。一组防火墙规则可以按顺序应用于每个网络数据包。每条链中的规则做两件事：它指定数据包必须满足的条件以匹配规则，并指定数据包匹配时的操作。

The iptables command uses the following basic format:

```
iptables -t tabletype <action direction> <packet pattern> -j <what to do>
```

现在逐项分析此命令。第一个项目是 -t tabletype 开关。iptables 有三个基本 tabletype 选项值得关注：

- **filter** 设置用于过滤数据包的规则。
- **nat** 配置网络地址转换，也称为伪装，本章后面会讨论。
- **mangle** 修改数据包头部。

默认是 filter；如果您未指定 -t tabletype，iptables 命令假定您尝试创建过滤规则。

下一个项目是 <action direction>。iptables 规则有四个基本操作：

- **-A (--append)** 将规则追加到链的末尾。
- **-D (--delete)** 从链中删除规则。通过编号或数据包模式指定规则。
- **-L (--list)** 列出链中当前配置的规则。
- **-F (--flush)** 刷新当前 iptables 链中的所有规则。

如果您要向链追加 (-A) 或从链删除 (-D)，您希望将其应用于沿三个方向之一传输的网络数据。对于保护系统免受外部数据侵害的常规防火墙而言，在大多数情况下，适用的方向是 INPUT：

- **INPUT** 所有传入数据包都会对照此链中的规则进行检查。
- **OUTPUT** 所有传出数据包都会对照此链中的规则进行检查。
- **FORWARD** 所有发送到另一台计算机的数据包都会对照此链中的规则进行检查。

接下来，您需要配置 <packet pattern>。所有 iptables 防火墙都会将每个数据包与此模式进行检查。最简单的模式是按 IP 地址：

- **-s ip_address** 所有数据包都会检查特定的源 IP 地址。
- **-d ip_address** 所有数据包都会检查特定的目标 IP 地址。

数据包模式可以更复杂。在 TCP/IP 中，大多数数据包使用传输控制协议 (TCP)、用户数据报协议 (UDP) 或互联网控制消息协议 (ICMP) 协议传输。您可以使用 -p 开关指定协议，后跟目标端口 (--dport)。例如，-p tcp --dport 80 扩展影响尝试使用 HTTP 连接的网络外部用户。

一旦 iptables 命令找到数据包模式匹配，它需要知道对该数据包做什么，这就引出了命令的最后一部分 -j <what to do>。有三个基本选项：

- **DROP** 数据包被丢弃。不向请求计算机发送消息。
- **REJECT** 数据包被丢弃。向请求计算机发送错误消息。
- **ACCEPT** 数据包被允许按 -A 操作指定的方式继续：INPUT、OUTPUT 或 FORWARD。
