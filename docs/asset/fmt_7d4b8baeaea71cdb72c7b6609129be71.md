
```
~]# firewall-cmd --zone=external --remove-masquerade
```

要使此设置持久化，请添加 `--permanent` 选项并重复执行该命令。

## 5.11. 管理 ICMP 请求

互联网控制消息协议（ICMP）是一种支持协议，被各种网络设备用来发送错误消息和操作信息，以指示连接问题，例如所请求的服务不可用。与 TCP 和 UDP 等传输协议不同，ICMP 不用于系统间的数据交换。

不幸的是，可以利用 ICMP 消息（尤其是 echo-request 和 echo-reply）来泄露有关您网络的信息，并出于各种欺诈目的滥用这些信息。因此，防火墙可以通过阻止 ICMP 请求来保护您的网络信息。

### 5.11.1. 列出 ICMP 请求

ICMP 请求由位于 `/usr/lib/firewalld/icmp types/` 目录下的独立 XML 文件描述。您可以阅读这些文件以查看请求的描述。`firewall-cmd` 命令用于控制 ICMP 请求的操作。

要列出所有可用的 ICMP 类型：

```bash
~]# firewall-cmd --get-icmptypes
```

ICMP 请求可以由 IPv4、IPv6 或两者同时使用。要查看 ICMP 请求用于哪种协议：

```bash
~]# firewall-cmd --info-icmptype=<icmptype>
```

如果当前阻止了请求，则 ICMP 请求的状态显示为 yes；如果未阻止，则显示为 no。要查看当前是否阻止了某个 ICMP 请求：

```bash
~]# firewall-cmd --query-icmp-block=<icmptype>
```

### 5.11.2. 阻止或取消阻止 ICMP 请求

当您的服务器阻止 ICMP 请求时，它将不再提供通常会提供的信息。但这并不意味着完全没有提供信息。客户端会接收到该特定 ICMP 请求正在被阻止（拒绝）的信息。应该谨慎考虑阻止 ICMP 请求，因为这可能会导致通信问题，特别是对于 IPv6 流量。

要查看当前是否阻止了某个 ICMP 请求：

```bash
~]# firewall-cmd --query-icmp-block=<icmptype>
```

要阻止某个 ICMP 请求：

```bash
~]# firewall-cmd --add-icmp-block=<icmptype>
```

要移除对某个 ICMP 请求的阻止：

```bash
~]# firewall-cmd --remove-icmp-block=<icmptype>
```

### 5.11.3. 在不提供任何信息的情况下阻止 ICMP 请求

通常，如果你阻止 `ICMP` 请求，客户端会知道正在阻止它。因此，正在嗅探活跃 IP 地址的潜在攻击者仍然可以看到你的 IP 地址在线。为了完全隐藏此信息，你必须丢弃所有 `ICMP` 请求。

要阻止并丢弃所有 `ICMP` 请求：

1. 将你的区域的目标设置为 `DROP`：

```bash
~]# firewall-cmd --set-target=DROP
```

2. 使新设置持久化：

```bash
~]# firewall-cmd --runtime-to-permanent
```

现在，除了你明确允许流量外，所有流量（包括 `ICMP` 请求）都会被丢弃。

要阻止并丢弃特定的 `ICMP` 请求并允许其他请求：

1. 将你的区域的目标设置为 `DROP`：

```bash
~]# firewall-cmd --set-target=DROP
```

2. 添加 ICMP 阻止反转以一次性阻止所有 `ICMP` 请求：

```bash
~]# firewall-cmd --add-icmp-block-inversion
```

3. 添加你想允许的 `ICMP` 请求的 ICMP 阻止：

```bash
~]# firewall-cmd --add-icmp-block=<icmptype>
```

4. 使新设置持久化：

```bash
~]# firewall-cmd --runtime-to-permanent
```

`block inversion` 反转了 `ICMP` 请求阻止的设置，因此所有之前未被阻止的请求现在都会被阻止，而之前被阻止的请求现在不再被阻止。这意味着如果你需要取消阻止某个请求，必须使用阻止命令。

要恢复为完全允许的设置：

1. 将你的区域的目标设置为 `default` 或 `ACCEPT`：

```bash
~]# firewall-cmd --set-target=default
```

2. 移除所有已添加的 `ICMP` 请求的阻止：

```bash
~]# firewall-cmd --remove-icmp-block=<icmptype>
```

3. 移除 `ICMP` 阻止反转：

```bash
~]# firewall-cmd --remove-icmp-block-inversion
```

4. 使新设置持久化：

```bash
~]# firewall-cmd --runtime-to-permanent
```

### 5.11.4. 使用 GUI 配置 ICMP 过滤器

要启用或禁用 `ICMP` 过滤器，请启动 `firewall-config` 工具并选择要过滤消息的网络区域。选择 `ICMP Filter` 选项卡，并勾选你想过滤的每种 `ICMP` 消息类型的复选框。清除复选框以禁用过滤器。此设置是按方向进行的，默认允许所有内容。

要编辑 `ICMP` 类型，请启动 `firewall-config` 工具，并从标记为 `Configuration` 的菜单中选择 `Permanent` 模式。`Services` 窗口底部会出现额外的图标。在后续对话框中选择 `Yes` 以启用 masquerading 并使转发到另一台机器生效。

要启用反转 `ICMP Filter`，请单击右侧的 `Invert Filter` 复选框。现在仅接受标记的 `ICMP` 类型，所有其他类型都被拒绝。在使用 `DROP` 目标的区域中，它们会被丢弃。

## 5.12. 使用 FIREWALLD 设置和控制 IP 集合

要查看 `firewalld` 支持的 IP 集合类型列表，请以 `root` 身份输入以下命令。

```bash
~]# firewall-cmd --get-ipset-types
hash:ip hash:ip,mark hash:ip,port hash:ip,port,ip hash:ip,port,net
hash:mac hash:net hash:net,iface hash:net,net hash:net,port
hash:net,port,net
```

### 5.12.1. 使用命令行客户端配置 IP 集合选项

IP 集合可以用作 `firewalld` 区域中的源，也可以用作 rich 规则中的源。在 `Red Hat Enterprise Linux 7` 中，推荐的方法是在直接规则中使用由 `firewalld` 创建的 IP 集合。

要列出永久环境中 `firewalld` 已知的 IP 集合，请以 `root` 身份使用以下命令：

```bash
~]# firewall-cmd --permanent --get-ipsets
```

要以 `root` 身份使用永久环境添加新的 IP 集合，请使用以下命令：

```bash
~]# firewall-cmd --permanent --new-ipset=test --type=hash:net
success
```

上面的命令创建了一个名为 `test` 且类型为 `hash:net` 的 `IPv4` IP 集合。要创建用于 `IPv6` 的 IP 集合，请添加 `--option=family=inete6` 选项。要使新设置在运行时环境中生效，请重新加载 `firewalld`。以 `root` 身份使用以下命令列出新的 IP 集合：

```bash
~]# firewall-cmd --permanent --get-ipsets
test
```

要以 root 身份获取更多关于 IP 集合的信息，请使用以下命令：

```bash
~]# firewall-cmd --permanent --info-ipset=test
test
type: hash:net
options:
entries:
```

注意目前该 IP 集合没有任何条目。要以 root 身份向测试 IP 集合添加条目，请使用以下命令：
