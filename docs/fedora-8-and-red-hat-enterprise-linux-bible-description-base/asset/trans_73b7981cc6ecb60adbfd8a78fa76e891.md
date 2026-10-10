
将外部接口分配给公共网络，使其被信任。但是，你可能拥有专用的网络连接或小型本地局域网连接，并希望将其设置为信任状态。

**地址伪装（Masquerading）**——通过将某个接口识别为地址伪装接口，你可以允许 LAN 中拥有私有 IP 地址的其他计算机使用你的计算机作为通往互联网（或其他网络）的路由器。这假设你的 Fedora 系统拥有另一个具有通往互联网路由的网络接口。通过选择至少一个网络接口作为提供 IP 地址伪装的功能，包转发支持将自动开启。（关于地址伪装的描述请参见本章后面的内容。）

**自定义规则**——创建自定义规则可能比简单地开放端口访问要复杂一些。你可以在单独的文件中创建一个 iptables 规则（以本章后面描述的 iptables-save 格式），并将该规则分配到 filter、NAT 或 mangle iptables 表中。点击“添加”并指示地址类型（ipv4 或 ipv6）、表类型以及包含该规则的文件。点击“确定”以添加该规则。

在点击“应用”以保存你的设置之前，请考虑这样做会覆盖你现有的防火墙规则。如果你曾手动编辑过配置文件（/etc/sysconfig/iptables），那些更改将被覆盖。在继续之前，请备份该文件。

配置 iptables 以设置日志记录、端口转发、网络地址转换以及其他功能，都可以手动完成，详见以下章节。

## 配置 iptables 防火墙

本章中关于 iptables 的剩余部分描述了在 Linux 中更手动地与 iptables 防火墙交互的方式。我还涵盖了如何实现一些在防火墙配置窗口中不可用的特殊 iptables 功能（例如端口转发和 NAT）。

### 启用 iptables

iptables 防火墙功能（也称为 netfilter）是安装 Fedora 或 RHEL 时的默认防火墙软件。

本节描述了如何启用 iptables 并为几种不同的情况设置防火墙规则。它还介绍了如何启用与防火墙相关的功能，使你的 iptables 防火墙能够执行网络地址转换（NAT）、IP 地址伪装、端口转发和透明代理。

> 注意：如果你使用某些服务，Fedora 的启动脚本会在你的防火墙中“打个洞”，因此即使这些服务未在 iptables 配置中明确启用，它们也能正常工作。例如，NTP（通过网络时间服务器设置系统时间）和 DNS 解析（允许你联系 DNS 服务器以解析地址）都会打开防火墙中它们所需的端口。

以下步骤描述了如何在你的 Fedora 或 RHEL 系统上让 `iptables` 运行起来。

1. 设置 `iptables` 脚本在启动时自动运行：
   ```bash
   # chkconfig iptables on
   ```

2. 在启动 `iptables` 之前，你必须已将一组可用的规则放入 `/etc/sysconfig/iptables` 文件中。要创建这些规则，请参阅以下章节中的示例。（如果没有配置文件的设置，`iptables` 将静默失败。）

> 提示：如果你是 `iptables` 的新手，你可以在 Fedora 或 RHEL 安装期间配置防火墙，从而获得一组可用的默认值作为起点。我建议启用防火墙，并仅启用你准备好提供的服务。生成的 `/etc/sysconfig/iptables` 文件可以让你研究 Fedora 或 RHEL 如何创建其防火墙规则。

3. 如果你在进行 NAT 或 IP 地址伪装，请开启 IP 包转发。允许此功能的一种方法是在 `/etc/sysctl.conf` 文件中将 `net_ipv4.ip_forward` 的值更改为 1。以 root 用户身份使用任意文本编辑器打开该文件，并将该行更改为如下所示：
   ```bash
   net_ipv4.ip_forward = 1
   ```

4. 重启网络接口以使 IP 包转发生效。
   ```bash
   # /etc/init.d/network restart
   ```

5. 规则文件就位后，启动 `iptables`：
   ```bash
   # /etc/init.d/iptables start
   ```

6. 此时，`iptables` 已安装为你的防火墙。你可以使用 `lsmod` 命令检查 `iptables` 使用的模块是否已加载，如下所示：
   ```bash
   # lsmod | grep "ip"
   ipt_REJECT      4736    1
   ipt_state       1536    7
   ip_conntrack    24368    1  ipt_state
   iptable_filter  2176    1
   ip_tables       13568    3  ipt_REJECT,ipt_state,iptable_filter
   ```

7. 如果你希望允许来自 LAN 上计算机的被动 FTP 或 IRC 连接，可能需要通过将模块添加到 `/etc/modprobe.conf` 文件来加载这些模块。基本的连接跟踪模块 `ip_conntrack` 默认应已加载。（关于被动 FTP 和 IRC 的说明参见防火墙示例章节之后的内容。）

如果你的 `/etc/sysconfig/iptables` 文件中有错误，你可以复制该文件，然后尝试运行 `system-config-securitylevel` 并设置基本防火墙，以创建可用的配置。然后，你可以修改防火墙以添加你需要的功能。

> 提示：随着你添加 iptables 规则，将需要加载更多的模块。当输入新规则时，适当的模块应自动加载。在你添加几条规则后，再次运行 `lsmod | grep ^ip` 查看哪些模块已添加。请注意，如果你决定停止 iptables，这些模块不会被卸载。它们将保持加载状态，直到下次重启或你手动移除它们（`modprobe -r`）。

以下部分包含 iptables 防火墙规则的示例。

## 创建 iptables 防火墙规则

配置 iptables 的一种方式是从命令行开始，向内核添加和删除规则。然后，当你得到一套喜欢的规则时，你可以保存当前在系统上运行的规则。你用于创建防火墙规则并使其永久化的工具如下：

- **iptables** — 使用此命令来追加（-A）、删除（-D）、替换（-R）或插入（-I）规则。使用 -L 选项列出所有当前规则。
- **service iptables save** — 使用此命令从内核保存规则并将其安装到配置文件中。
- **/etc/sysconfig/iptables** — 这是包含通过 *service iptables save* 命令保存的规则的配置 文件。
- **/etc/sysconfig/iptables-config** — 你可以向 *iptables-config* 文件添加用于管理 iptables 规则的设置。例如，任何 iptables 模块，如 *ip_conntrack* 及本章后面描述的其他模块，都可以添加到 `IPTABLES_MODULES` 行中以便自动加载。你还可以设置当 iptables 停止时，是否将运行内核中的 iptables 表保存到文件。
- **/etc/init.d/iptables** — 这是 iptables 启动脚本，必须在 Fedora 每次重启时自动运行。启动时，它会清除所有 iptables 规则和计数器，并安装来自 `/etc/sysconfig/iptables` 文件的新规则。你还可以使用此脚本并附带不同的选项从命令行检查 iptables 的状态（*status*）或替你运行 *iptables-save* 以保存当前规则（*save*）。

为了帮助你入门，我提供了一组带有说明的 iptables 规则示例，这些说明描述了你可能如何根据不同情况修改这些规则。以下是如何加载并保存下面示例中描述的任何规则集：

1. 停止 iptables 并清除所有现有规则：
   ```bash
   # /etc/init.d/iptables stop
   ```
2. 使用任何文本编辑器将以下示例中显示的规则添加到文件中。根据你的情况修改规则并保存文件。
3. 作为 root 用户，将该文件作为 shell 脚本运行。例如，如果你将该文件命名为 `firesscript`，可以如下运行它：
   ```bash
   # sh firesscript
   ```
4. 查看规则如何被加载到内核中：
   ```bash
   # iptables -L
   ```
5. 如果一切正常，将现在位于内核中的规则保存到 `/etc/sysconfig/iptables` 文件中：
   ```bash
   # cp /etc/sysconfig/iptables /etc/sysconfig/iptables-old
   # service iptables save
   ```

从此以后，每次你重启或重启 iptables 时，都会读取这些规则。保存一份你用于创建规则的脚本副本，以防将来再次需要。

**示例 1：共享互联网连接的防火墙（加上服务器）**

由于防火墙配置根据你想实现的目标可能截然不同，我基于几种不同的示例配置展示了如何配置防火墙。这些配置结合了不同级别的安全要求。

本示例展示了一个家庭或小型办公室局域网，其中一台 Fedora 系统充当位于局域网和互联网之间的 iptables 防火墙。该防火墙计算机还充当 Web 服务器、FTP 服务器和 DNS 服务器。图 14-2 展示了此配置。

![](img/fb202c163797a743c3c6cf236316bc96_624_0.png)

图 14-2：使用 iptables 作为互联网和局域网之间的防火墙

如果你想使用接下来的示例防火墙脚本，你必须更改以下信息以匹配你的配置：

