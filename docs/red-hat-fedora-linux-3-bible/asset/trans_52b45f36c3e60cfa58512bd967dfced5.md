

## 使用防火墙保护您的网络

什么是防火墙？在非计算机世界中，防火墙是一种防止火势蔓延的物理屏障。*计算机防火墙* 扮演着类似的角色，但它们试图阻挡的“火焰”是来自互联网上黑客的攻击。在此上下文中，防火墙（也称为*数据包过滤器*）是一台位于您的网络和互联网之间的计算机硬件设备，用于调节和控制信息流。

当今使用最常见的防火墙类型是过滤型防火墙。过滤型防火墙会过滤在您的网络和互联网之间流动的数据流量，阻止那些可能使您的网络面临风险的内容。它可以将互联网到以及来自互联网的访问限制为仅针对您网络中的特定计算机。它还可以限制通信类型，有选择地允许或拒绝各种互联网服务。

要使 Fedora 充当过滤型防火墙，您可以使用 iptables 功能。iptables 功能在几个版本之前取代了 ipchains，成为 Red Hat Linux 的默认防火墙。在 Fedora Core 2 中，ipchains 被完全弃用。iptables 机制在本章中进行了描述。

> **注意：** 您可以在位于 www.netfilter.org/documentation/HOWTO/packet-filtering-HOWTO-10.html 的 iptables HOWTO 中阅读关于 ipchains 和 iptables 之间差异的内容。

### 配置 iptables 防火墙

iptables 防火墙功能（也称为 netfilter）是安装 Fedora 时的默认防火墙软件。曾经随 Red Hat Linux 和 Fedora Core 1 提供的 ipchains 防火墙功能，在 Fedora Core 2 中不再可用。

如果您当前的 Red Hat Linux 系统（例如，如果您刚刚升级到 Fedora Core 2）正在使用 ipchains，并且希望转换为 iptables，您需要在使用 iptables 之前禁用 ipchains。实际上，如果 ipchains 模块已加载时，您尝试使用 iptables 脚本（`/etc/init.d/iptables`）启动 iptables，iptables 启动脚本会静默失败并退出。

虽然通常认为 iptables 比 ipchains 更难操作，但它也被认为更强大且更灵活。由于 ipchains 的开发已停止，现有的少数损坏的 ipchains 功能很可能会保持损坏状态。

本节介绍了如何启用 iptables 并为几种不同情况设置防火墙规则。它还说明了如何启用与防火墙相关的功能，使您的 iptables 防火墙能够执行网络地址转换（NAT）、IP 伪装、端口转发和透明代理。

> **注意**：如果您使用某些服务，Fedora 启动脚本会为您的防火墙“开一个洞”，因此即使它们在您的 `iptables` 配置中未被明确启用，它们也能正常工作。例如，NTP（通过网络时间服务器设置系统时间）和 DNS 解析（允许您联系 DNS 服务器来解析地址）都会打开防火墙中所需的端口。

### 启用 iptables

以下步骤描述了如何在您的 Fedora 系统上启动 iptables。

> **提示**：在您关闭 ipchains、启用 iptables 并配置 iptables 过滤规则期间，您的计算机可能未受到网络保护。您应在非关键计算机上测试防火墙规则，然后快速执行切换，或暂时关闭您的网络接口在关键计算机上执行切换。

- 1. 停止 ipchains 脚本在启动时自动运行：
  ```bash
  # chkconfig ipchains off
  ```

- 2. 设置 iptables 脚本在启动时自动运行：
  ```bash
  # chkconfig iptables on
  ```

- 3. 现在您可以重启 Fedora，或者停止 ipchains 并卸载 ipchains 模块，操作如下：
  ```bash
  # service ipchains stop
  # modprobe -r ipchains
  ```

- 4. 在启动 iptables 之前，您必须在 `/etc/sysconfig/iptables` 文件中拥有一组可用的规则。要创建这些规则，请参阅下一节中的示例。（如果没有放置配置文件，iptables 会静默失败。）

> **提示：** 如果您是 iptables 的新手，您可以通过在 Fedora 安装过程中配置防火墙来从一个可用的默认值集合开始。我建议选择一个中等安全级别的防火墙，并配置几个允许的服务。生成的 `/etc/sysconfig/iptables` 文件将让您研究 Fedora 如何创建其防火墙规则。

- 5. 如果您正在执行 NAT 或 IP 伪装，请启用 IP 数据包转发。允许此操作的一种方法是将 `/etc/sysctl.conf` 文件中 `net.ipv4.ip_forward` 的值更改为 1。以 root 用户身份使用任何文本编辑器打开该文件，并将该行更改为如下所示：
  ```bash
  net.ipv4.ip_forward = 1
  ```

- 6. 重启您的网络接口以使 IP 数据包转发生效。
  ```bash
  # /etc/init.d/network restart
  ```

- 7. 一旦规则文件就位，启动 iptables：
  ```bash
  # /etc/init.d/iptables start
  ```

- 8. 此时，iptables 已安装为您的防火墙。您可以使用 `lsmod` 命令检查 iptables 使用的模块是否已加载，操作如下：
  ```bash
  # lsmod | grep ip
  ipt_REJECT		4736	1
  ipt_state		1536	7
  ip_conntrack	24368	1	ipt_state
  iptables_filter	2176	1
  iptables			13568	3	ipt_REJECT, ipt_state, iptable_filter
  ```

- 9. 如果您希望允许来自局域网计算机的被动 FTP 或 IRC 连接，您可能需要将这些模块添加到 `/etc/modules.conf` 文件中以加载它们。基本的连接跟踪模块 `ip_conntrack` 应该默认已经加载。
  （请参阅防火墙示例章节之后关于被动 FTP 和 IRC 的描述。）

如果您的 iptables 服务没有启动，请确保：

- 没有加载 ipchains 模块。（如上所示，使用 `modprobe -r` 卸载它。）
- `/etc/sysconfig/iptables` 文件存在。（如果安装 Fedora 时未为您创建一个文件，您需要创建一个。）

> **提示：** 随着您添加 iptables 规则，将需要加载更多的模块。当输入新规则时，合适的模块应自动加载。在添加了一些规则后，再次运行 `lsmod | grep ip` 以查看添加了哪些模块。请注意，如果您决定停止 iptables，这些模块不会卸载。它们将保持加载状态，直到下一次重启或您移除它们（modprobe -r）。

接下来的章节包含 iptables 防火墙规则的示例。

## 创建 iptables 防火墙规则

配置 iptables 的一种方法是从命令行开始，向内核添加和删除规则。然后，当您得到一组喜欢的规则时，保存当前在系统上运行的规则。用于创建防火墙规则并使其永久化的工具如下：

- **iptables** — 使用此命令来追加（-A）、删除（-D）、替换（-R）或插入（-I）规则。使用 -L 选项列出所有当前规则。
- **service iptables save** — 使用此命令从内核保存规则并将其安装到配置文件中。
- **/etc/sysconfig/iptables** — 这是包含从 iptables-save 命令保存的规则的配置文件的名称。
- **/etc/sysconfig/iptables-config** — 您可以向 iptables-config 文件添加用于管理 iptables 规则的设置。例如，任何 iptables 模块（如 ip_conntrack 以及本章后面描述的其他模块）都可以添加到 IPTABLES_MODULES 行中以自动加载。您还可以设置当 iptables 停止时，运行内核中的 iptables 表是否保存到文件。
- **/etc/init.d/iptables** — 这是每次 Fedora 重启时必须自动运行的 iptables 启动脚本。启动时，它会清除所有 iptables 规则和计数器，并从 /etc/sysconfig/iptables 文件安装新规则。您还可以使用此脚本从命令行使用不同的选项来检查 iptables 的状态（status）或为您运行 iptables-save 以保存当前规则（save）。

为了帮助您开始使用 iptables，我提供了一组示例 iptables 规则以及如何在不同情况下更改这些规则的描述。以下是如何加载和保存下列示例中描述的规则集的方法：

- 1. 如果您当前正在运行 ipchains，请完成上一节“启用 iptables”中的步骤。
- 2. 停止 iptables 并清除所有现有规则：
  ```bash
  # /etc/init.d/iptables stop
  ```
- 3. 使用任何文本编辑器将下例中显示规则添加到文件中。根据您的需求修改规则并保存文件。
- 4. 以 root 用户身份将该文件作为 shell 脚本运行。例如，如果您将文件命名为 firescript，可以按以下方式运行：
  ```bash
  # sh firescript
  ```
- 5. 查看规则如何加载到内核中：
  ```bash
  # iptables -L
  ```

