

第二条过滤规则控制来自传出连接的返回数据包。例如，当你连接到某个网站时，你的浏览器会发出数据包，而 Web 服务器会对这些数据包做出响应。你可能会点击网站上的一个按钮，然后弹出一个新的显示窗口。点击按钮会发送一个数据包出去，Web 服务器则会发送数据包回来。你之前已经阻止了来自 Internet 的数据包。这条规则创建了一个例外，允许属于现有连接的数据包——例如代表你点击按钮的连接——通过防火墙返回到你的计算机。请注意，我们不允许建立新的传入连接（--state NEW），因为这会违背此防火墙的初衷。

6. **（可选）使用以下规则允许 SSH 连接进入你的 Linux 计算机：**

```bash
iptables -A INPUT -p tcp -m state --state NEW,ESTABLISHED -j ACCEPT -dport 22
```

此规则允许 22 端口上的 SSH 连接进入你的计算机。你可以登录为 root，挂载随附的 DVD，并运行以下命令来安装 OpenSSH 服务器：

```bash
rpm -ivh /mnt/cdrom/RedHat/RPMS/openssh-server*
```

运行以下命令启动 OpenSSH 服务器：

```bash
/etc/init.d/sshd start
```

你可以修改此规则以允许其他类型的传入连接进入你的计算机。例如，添加一条使用 -dport 80 的新规则，防火墙就会允许传入的 HTTP 数据包。你所需要做的只是安装 Apache Web 服务器（包含在本书的随附 DVD-ROM 中，并在第 16 章中有描述），你的工作站就会变身为一个 Web 服务器。

你刚刚创建了一个简单而有效的防火墙，保护你的计算机免受“网络领域”（Netdom）中“狼人”的攻击。（“它们会把你的心掏出来，吉姆！”）你的防火墙将保持活动状态，直到你关闭规则或重启计算机。下一节将展示如何显示你新的防火墙规则。

## 显示你的防火墙规则

配置好防火墙后，你自然会想验证过滤规则是否设置正确。要显示防火墙规则，请遵循以下步骤：

- 1. 通过右键点击桌面的任意空白区域并选择 **新终端** 菜单，打开一个 GNOME 终端仿真器窗口。
- 2. 如果你当前不是 root 用户，请在 GNOME 终端窗口中输入 su - 命令。
- 3. 输入 root 密码，并键入以下命令以显示防火墙规则：

```bash
iptables -L
```

完成这些步骤后，你会看到防火墙过滤规则在终端窗口中显示如下（使用前一条命令中的详细模式 -v 选项可以显示额外信息，包括网络接口——为了简洁起见，本示例中未使用该选项）：

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

第一条链，INPUT，用于处理传入的数据包。你可以看到默认策略是拒绝所有数据包。INPUT 链中的前几条规则指示 iptables 允许逻辑回环接口（lo）上的所有内部数据包；许多程序使用内部（lo）网络进行相互通信。第二条规则允许传出连接的返回数据包（RELATED 和 ESTABLISHED）进入。最后一条规则（可选的）允许传入的安全 Shell（SSH）连接进入你的计算机。

下一条链，FORWARD，拒绝所有数据包通过你的 Linux 计算机进行转发。只有当你的计算机用于路由或其他高级网络功能时，才需要转发。

最后一条链，OUTPUT，定义了哪些 IP 数据包允许离开你的计算机。同样，第一条规则允许通过回环（lo）接口进行无限制的交通。第二条也是最后一条规则允许任何及所有数据包离开你的防火墙。

下一节将描述如何保存你刚刚创建并显示的那些规则，以便它们可以自动启动。

## 启动你的防火墙（以及熄灭火焰）

前一节描述了如何显示你的防火墙过滤规则。然而，你肯定不希望每次重启计算机时都手动输入这些规则。本节将向你展示如何自动设置你的防火墙。我们将展示如何使用 Red Hat 实用工具来保存你刚刚创建的规则，并在每次启动计算机时启动防火墙。

以下说明假设你已按照前一节描述配置了防火墙，且该配置仍然有效。

### 将过滤规则保存到脚本中

创建防火墙后，你需要保存你的规则集。Red Hat 提供了一个专门用于此目的的工具。`iptables-save` 实用程序读取你当前的防火墙规则，并将其转换为脚本兼容的格式。Red Hat 还提供了一个脚本，用于在每次启动计算机时启动你的防火墙。每当启动计算机时都会运行 `/etc/init.d/iptables` 脚本，因此你的防火墙也会随之启动。请遵循以下步骤：

- 1. 如有必要，登录为 root，并打开一个 GNOME 终端窗口（参见第 4 章），如有必要。
- 2. 运行以下命令，如果你的防火墙规则被保存到脚本中：

```bash
iptables-save > /etc/sysconfig/iptables
```

### 关闭和开启你的防火墙

Red Hat 使用 `/etc/sysconfig/iptables` 脚本来启动 *Netfilter/iptables* 防火墙。`/etc/init.d/iptables` 脚本使用存储在 `/etc/sysconfig/iptables` 文件中的过滤规则来实现过滤规则。

你可以通过运行此 `iptables` 脚本启动 *Netfilter/iptables* 防火墙：

```bash
/etc/init.d/iptables start
```

当然，你必须以 root 身份登录。注意，你可以将 start 替换为 stop 来关闭你的防火墙：

```bash
/etc/init.d/iptables stop
```

你也可以使用图形化的 Red Hat 服务配置实用程序。以下说明展示如何使用该实用程序启动或停止你的防火墙：

- 1. **点击 GNOME 菜单按钮并选择 系统设置:: 服务器设置:: 服务。**

如果你未以 root 身份登录，将弹出一个输入窗口，要求你输入 root 密码。

- 2. **输入你在 Red Hat 安装过程中设置的 root 密码。**

服务配置窗口将出现。此窗口控制所有的 Linux 守护进程（提供服务的进程）。

- 3. **向下滚动服务配置窗口，直到找到 Iptables 服务。**

复选框中应打有勾。

- 4. **点击窗口左上角的 重新启动 按钮。**

你可以点击 启动 按钮，但我们建议你使用 重新启动 功能。启动和重新启动按钮产生相同的结果，但如果服务已经在运行，重新启动仍然有效。如果服务已经在运行，使用 启动 功能则无效。

点击 停止 按钮即可关闭你的防火墙。

服务重新启动后，你会看到一条确认消息。

- 5. **点击 确定。**

你的防火墙已重新启动，你可以退出服务配置窗口。

你也可以防止 Iptables 脚本在系统启动时自动运行。点击服务名称左侧的方框以移除勾选。点击 保存 按钮，指向启动脚本（/etc/init.d/iptables）的指针（/etc/rc.d/rc5.d/S08iptables）将被移除。你可以通过再次点击方框使勾选重新出现来恢复该指针。

