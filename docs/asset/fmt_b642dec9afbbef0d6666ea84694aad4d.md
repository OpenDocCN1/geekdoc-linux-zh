
在本节中，你将设计一个基于 `Iptables` 的防火墙，关闭调制解调器上的所有传入连接，同时允许你建立到互联网的传出连接。然后，你会放宽对传入通信的完全限制，以允许传入的安全 shell 连接。（安全 shell 提供加密通信。）

![](img/8c094d1b36276212c03d10d898508a6e_125_2.png)

不要通过远程连接执行这些指令！你必须从你的电脑控制台运行这些命令。也就是说，你必须坐在你的电脑前，而不是通过网络连接操作它。原因是这些防火墙规则在恢复外部网络连接之前会切断它们。

这些指令描述了如何逐块构建你的防火墙：

1. 以 `root` 身份登录你的计算机，然后通过右键点击桌面的任何空白区域并从菜单中选择“新建终端”来打开一个 GNOME 终端窗口。

2. 通过在终端窗口中的命令提示符下输入以下规则，确保你尚未运行防火墙：

```
iptables --flush
iptables --flush -t nat
```

`iptables` 条目移除了任何现有的过滤或网络地址转换（`NAT`）规则。*`NAT` 规则*将你的网络地址伪装成另一个地址，使你的计算机看起来像是被别人使用。`NAT` 经常用于使你的计算机看起来像是来自你的 `ISP`，这样你就无需为计算机注册正式的互联网协议（`IP`）地址。

3. **通过输入以下规则过滤所有进出及通过你计算机的网络通信：**

```
iptables --policy INPUT  DROP
iptables --policy OUTPUT DROP
iptables --policy FORWARD DROP
```

这些命令将你的防火墙默认策略设置为不允许任何网络流量进入（`INPUT` 规则）或离开（`OUTPUT` 规则）任何网络接口；如果你有任何网络接口，也不允许任何流量通过它们之间的传递（`FORWARD` 规则）。此时，你拥有一个极其安全的网络。然而，你的计算机在用于任何网络相关任务方面是无用的。下一步稍微打开防火墙，以便你可以安全地访问互联网（或你连接的任何网络）。

4. **输入以下规则允许网络流量通过回环设备：**

```
iptables -A OUTPUT -j ACCEPT -o lo
iptables -A INPUT  -j ACCEPT -i lo
```

Linux 计算机使用内部网络，称为*回环接口*（`lo`）。回环不是物理设备，而是虚拟设备。Linux 使用 `lo` 进行内部通信。（Linux 计算机幕后发生了很多事情。）

5. **打开你计算机的所有传出通信：**

```
iptables -A OUTPUT -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A INPUT  -m state --state RELATED,ESTABLISHED -j ACCEPT
```

这些规则没有指定任何特定的网络接口。然而，由于过滤器是有状态的，这些规则实际上在你的以太网、无线或拨号点对点（`PPP`）接口上有效。

第一个过滤规则允许所有传出通信。`--state NEW, RELATED, ESTABLISHED` 选项告诉防火墙允许新连接和已建立连接的数据包通过。（数据包是所有网络通信的基本部分。）与现有连接相关但使用不同端口的数据包（如 `FTP` 数据传输）也被允许。

第二条过滤规则控制来自传出连接的返回数据包。例如，当你连接到某个网站时，你的浏览器会发出数据包，而 Web 服务器会对这些数据包做出响应。你可能会点击网站上的一个按钮，然后弹出一个新的显示窗口。点击按钮会发送一个数据包出去，Web 服务器则会发送数据包回来。你之前已经阻止了来自 Internet 的数据包。这条规则创建了一个例外，允许属于现有连接的数据包——例如代表你点击按钮的连接——通过防火墙返回到你的计算机。请注意，我们不允许建立新的传入连接（`--state NEW`），因为这会违背此防火墙的初衷。

6. **（可选）使用以下规则允许 SSH 连接进入你的 Linux 计算机：**

```bash
iptables -A INPUT -p tcp -m state --state NEW,ESTABLISHED -j ACCEPT -dport 22
```

此规则允许 `22` 端口上的 `SSH` 连接进入你的计算机。你可以登录为 `root`，挂载随附的 `DVD`，并运行以下命令来安装 `OpenSSH` 服务器：

```bash
rpm -ivh /mnt/cdrom/RedHat/RPMS/openssh-server*
```

运行以下命令启动 `OpenSSH` 服务器：

```bash
/etc/init.d/sshd start
```

你可以修改此规则以允许其他类型的传入连接进入你的计算机。例如，添加一条使用 `-dport 80` 的新规则，防火墙就会允许传入的 `HTTP` 数据包。你所需要做的只是安装 `Apache` Web 服务器（包含在本书的随附 `DVD-ROM` 中，并在第 16 章中有描述），你的工作站就会变身为一个 Web 服务器。

你刚刚创建了一个简单而有效的防火墙，保护你的计算机免受“网络领域”（`Netdom`）中“狼人”的攻击。（“它们会把你的心掏出来，吉姆！”）你的防火墙将保持活动状态，直到你关闭规则或重启计算机。下一节将展示如何显示你新的防火墙规则。

## 显示你的防火墙规则

配置好防火墙后，你自然会想验证过滤规则是否设置正确。要显示防火墙规则，请遵循以下步骤：

- 1. 通过右键点击桌面的任意空白区域并选择 **新终端** 菜单，打开一个 GNOME 终端仿真器窗口。

- 2. 如果你当前不是 `root` 用户，请在 GNOME 终端窗口中输入 `su -` 命令。

- 3. 输入 `root` 密码，并键入以下命令以显示防火墙规则：

```bash
iptables -L
```

完成这些步骤后，你会看到防火墙过滤规则在终端窗口中显示如下（使用前一条命令中的详细模式 `-v` 选项可以显示额外信息，包括网络接口——为了简洁起见，本示例中未使用该选项）：

```
Chain INPUT (policy DROP)
target     prot opt source       destination
ACCEPT     all  --  anywhere       anywhere
ACCEPT     all  --  anywhere       anywhere       state RELATED,ESTABLISHED
ACCEPT     tcp  --  anywhere       anywhere       tcp dpt:ssh
state NEW,ESTABLISHED

Chain FORWARD (policy DROP)
target     prot opt source       destination

Chain OUTPUT (policy DROP)
target     prot opt source       destination
ACCEPT     all  --  anywhere       anywhere
ACCEPT     all  --  anywhere       anywhere       state NEW,RELATED,ESTABLISHED
```

第一条链，`INPUT`，用于处理传入的数据包。你可以看到默认策略是拒绝所有数据包。`INPUT` 链中的前几条规则指示 `iptables` 允许逻辑回环接口（`lo`）上的所有内部数据包；许多程序使用内部（`lo`）网络进行相互通信。第二条规则允许传出连接的返回数据包（`RELATED` 和 `ESTABLISHED`）进入。最后一条规则（可选的）允许传入的安全 Shell（`SSH`）连接进入你的计算机。

下一条链，`FORWARD`，拒绝所有数据包通过你的 Linux 计算机进行转发。只有当你的计算机用于路由或其他高级网络功能时，才需要转发。

最后一条链，`OUTPUT`，定义了哪些 `IP` 数据包允许离开你的计算机。同样，第一条规则允许通过回环（`lo`）接口进行无限制的交通。第二条也是最后一条规则允许任何及所有数据包离开你的防火墙。

下一节将描述如何保存你刚刚创建并显示的那些规则，以便它们可以自动启动。

## 启动你的防火墙（以及熄灭火焰）

前一节描述了如何显示你的防火墙过滤规则。然而，你肯定不希望每次重启计算机时都手动输入这些规则。本节将向你展示如何自动设置你的防火墙。我们将展示如何使用 Red Hat 实用工具来保存你刚刚创建的规则，并在每次启动计算机时启动防火墙。

以下说明假设你已按照前一节描述配置了防火墙，且该配置仍然有效。

### 将过滤规则保存到脚本中

创建防火墙后，你需要保存你的规则集。Red Hat 提供了一个专门用于此目的的工具。`iptables-save` 实用程序读取你当前的防火墙规则，并将其转换为脚本兼容的格式。Red Hat 还提供了一个脚本，用于在每次启动计算机时启动你的防火墙。每当启动计算机时都会运行 `/etc/init.d/iptables` 脚本，因此你的防火墙也会随之启动。请遵循以下步骤：

- 1. 如有必要，登录为 `root`，并打开一个 GNOME 终端窗口（参见第 4 章），如有必要。
