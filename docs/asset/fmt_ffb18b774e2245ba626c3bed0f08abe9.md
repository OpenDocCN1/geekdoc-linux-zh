
有时用户列表语法很严格；在某些情况下，逗号后或行尾的额外空格可能导致认证失败。

组常以特殊符号如 `@` 或 `+` 前缀包含在用户列表中。

有时允许访问系统的用户配置在单独的认证数据库中，如与 Samba 服务器关联的数据库，用 `smbpasswd` 命令配置。

### 控制台安全

如第 8 章所述，控制台安全在 `/etc/securetty` 和 `/etc/security/access.conf` 文件中管控。可帮助管控对 `root` 和普通用户的本地控制台访问。

但控制台访问不仅限于本地。要全面了解控制台安全，需能配置远程控制台访问限制。两个主要选项是前面讨论的 `SSH` 和 `Telnet`。`telnet` 命令如第 2 章所述有其用途，但对 Telnet 服务器的通信本质上不安全。用户名、密码以及与 Telnet 服务器的通信以明文传输。这意味着网络协议分析器如 `Ethereal` 可读取这些用户名、密码及任何其他关键信息。

即使 Telnet 服务器有基于 Kerberos 的选项，大多数安全专业人员几乎在所有情况下都避免使用 Telnet 进行远程控制台。这与 NSA 的建议一致。

### 美国国家安全局的建议

NSA 对 Linux 尤其是 Red Hat Enterprise Linux 特别感兴趣。NSA 不仅花费时间开发 SELinux，还创建了指南帮助像你这样的管理员创建更安全的 RHEL 配置。是的，“超级保密”的 NSA 已以开源许可证发布 SELinux 代码供所有人查看。他们认识到 Linux 在计算机网络基础设施中的重要性。RHEL 观察者可能会注意到 RHEL 5 与 RHEL 6 之间的变化遵循 NSA 的建议。

The NSA includes five general principles for securing operating systems in general and RHEL in particular.

- **尽可能加密传输的数据** NSA 关于加密的建议包括在应为私密且安全的网络上进行通信。`SSH`, with the security options described in Chapter 11, are an excellent step in this process.
- **最小化软件以最小化漏洞** As suggested by the NSA, “The simplest way to avoid vulnerabilities in software is to avoid installing that software.” The NSA pays special attention to any software that can communicate over a network, including the Linux GUI. The minimal installation of RHEL 6 includes far fewer packages than the comparable installation of RHEL 5.
- **在不同的系统上运行不同的网络服务** This is consistent with the concept of bastion servers described earlier in this chapter. Implementation is made easier by the flexibility afforded by virtual machine technologies such as `KVM`.
- **配置安全工具以提高系统健壮性** The RHCSA and RHCE objectives have this well covered, with the use of `iptables`-based firewalls, `SELinux`, and appropriate log collection services.
- **最小权限** In principle, you should give users the minimum privileges required to accomplish their tasks. Not only does that mean minimize access to the `root` administrative account, but also careful use of the `sudo` command privileges. `SELinux` options such as the `user_u` role for confinement described in Chapter 4 may also be helpful to that end.

## PolicyKit

The PolicyKit is one more security mechanism designed to help protect different administrative tools. When starting an administrative tool in the GUI from a regular account, most tools prompt for the `root` administrative password with a window similar to Figure 10-1.

Alternatively, you might see a slightly different window similar to that shown in Figure 10-2. Functionally, the effect is the same. As described in the window, authentication by the superuser is required. In this case, you'd still have to enter the `root` administrative password. However, there's a difference, as shown under details.

### 图 10-1

GUI 中访问管理工具需要 `root` 密码。

![](img/9139201cfcaf4292284a0eed074928e5_565_0.png)

The action specifies the policy required by the "vendor," in this case, the `system-config-firewall` command.

The action noted is "`org.fedoraproject.config.firewall.auth`," which is associated with a policy file in the `/usr/share/polkit-1/actions` directory. Policy configuration files are stored in this directory; the corresponding file for the `system-config-firewall` tool is `org.fedoraproject.config.firewall.policy`

These policy files are configured in XML format and may be modified further to support fine-grained control by individual users. However, since the PolicyKit only works within the GUI, its fine-grained controls do not affect the use of administrative tools from the console. It certainly does not prevent administrators from configuring or otherwise controlling important services. If fine-grained control is required, the better tool is the `/etc/sudoers` file described in Chapter 8.

### 图 10-2

PolicyKit 可能会限制对管理工具的访问。

![](img/9139201cfcaf4292284a0eed074928e5_565_1.png)

## 认证目标 10.02

## 防火墙和网络地址转换

通常，防火墙位于内部局域网和外部不安全网络（如互联网）之间。防火墙可以配置为检查进入或离开您局域网的每个网络数据包。当配置适当的规则时，它可以过滤掉可能对局域网上的系统构成安全风险的数据包。

然而，为了遵循 NSA 建议的精神，您将在每台系统上配置防火墙。虽然网络地址转换使用相同的 `iptables` 命令，但其使用通常仍最适用于局域网和外部网络之间的网关或路由器上的系统。

### 定义

基于 `iptables` 命令的防火墙通过读取每个网络数据包的头部工作。根据头部包含的信息，可以使用基于 `iptables` 的规则来过滤每个数据包。要了解数据包过滤的工作原理，您需要了解有关信息如何在网络上传输的一些知识。

在消息通过网络发送之前，该消息会被分解为称为数据包的较小单元。管理信息，包括数据类型、源地址和目标地址，会添加到每个数据包的头部。数据包在到达目标计算机时重新组装。防火墙检查每个头部中的字段。根据现有规则，防火墙随后可能对该数据包采取以下四种操作之一：

- 允许数据包进入系统。
- 如果当前系统是网络之间的网关或路由器，则将数据包转发到其他系统。
- 拒绝数据包并向源 IP 地址发送消息。
- 丢弃数据包而不发送任何消息。

无论结果如何，决策都可以被记录。如果有大量数据包被拒绝或丢弃，日志文件可能很有用。

RHEL 6 提供了配置系统为防火墙所需的一切，包括用于 IPv4 和 IPv6 网络的 `iptables` 和 `ip6tables` 命令。

相比之下，NAT 隐藏了连接到外部网络的局域网计算机的 IP 地址。NAT 用带防火墙的网关或路由器系统的 IP 地址替换内部源地址。该内部源地址缓存在网关上，因此它知道哪个计算机发出了请求。

当防火墙接收到网页等数据时，过程会反转。当数据包通过防火墙时，原发计算机在缓存中被识别。在数据包被发送出去之前，每个数据包的头部会相应地被修改。

这种方法有几个好处。隐藏内部 IP 地址使得黑客更难知道使用哪个 IP 地址入侵内部网络。NAT 支持具有私有 IP 地址的系统与外部网络（如互联网）之间的连接。这就是 IPv4 地址能够长期存活的原因。在 Linux 世界中，此过程称为 IP 伪装。

### iptables 命令的结构

`iptables` 命令组装成防火墙的方式基于“链”。一组防火墙规则可以按顺序应用于每个网络数据包。每条链中的规则做两件事：它指定数据包必须满足的条件以匹配规则，并指定数据包匹配时的操作。

The `iptables` command uses the following basic format:

```
