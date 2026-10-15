
这也可以帮助你确定资源冲突问题。确保你参考的是声卡制造商的信息。

## 174 附录 B：故障排除 SuSE Linux

此命令列出所有使用的 DMA 通道：
```bash
cat /proc/dma
```

你可以在 http://www.linuxdoc.org/HOWTO/Sound-HOWTO.html#toc4 找到声音 HOWTO。

## 网络接口卡

网卡（NIC）的配置非常简单，大多数驱动程序在 SuSE Linux 安装的内核中可用。我发现的一个问题是关于 PCI 卡配置的。这是一个孤案例，但为了方便他人，我会将其记录下来。在 10Base ISA 卡流行时期最初构建的旧机器上，其 BIOS 设置可能需要更改 PCI 设置。PCI 卡自动分配 IRQ 和 IO。这意味着如果 PCI 设置开启了“旧版兼容（legacy compatibility）”，系统要么能识别显卡但不为其分配 IRQ，或者它会分配 IRQ0 或 255，这些都不是有效地址。当设置调整为 PCI PnP 兼容模式时，问题应该就会消失。可以在 http://csdesis.gsfc.nasa.gov/linux/misc/irq-config.html 获取更详细的信息。查看 http://sdb.suse.de/cqi-bin/sdbsearch_en.q7stitchwort-PCI 数据库。

如果你在使用 ISA 卡时遇到问题，你需要使用上一节声卡部分列出的相同命令。这将帮助你确定是否存在系统冲突或其他问题。再次提醒，你需要手头有显卡的规格说明。

## 笔记本电脑与笔记本

如果你有一台笔记本电脑并安装了 SuSE，你可能会发现一些不同之处——特别是 PCMCIA 配置问题。如果你面临需要诊断的情况，这可能会有所帮助。

Linux 在安装后会自动探测 PCMCIA 设备并尝试在此时设置该设备。你还会被询问使用哪种网络设备；否则，你选择 PCMCIA，YaST 将尝试配置 PCMCIA 设备。当你重启时，启动过程无法启动 PCMCIA 设备，并提示“eth0 device not found”，或者设备初始化后 `/etc/route` 失败。该问题的由于是 Linux 和 YaST 试图做同一项工作。在互不感知的情况下，每个程序都必须配置 PCMCIA 设备。

你必须返回 YaST 并选择“网络配置（Network Configuration）”，取消勾选 YaST 设置的 PCMCIA 设备（在基础配置下）。不要删除已有的任何条目。接下来，你需要编辑 `/etc/pcmcia/network.opts` 文件——SuSE 在该文件中查找有关 PCMCIA 设备的网络信息。添加你的 IP 地址、子网掩码、广播地址和网络信息。还要添加你的主机名和 DNS 服务器以完成任务。

## 故障排除 SuSE Linux 175

如果系统在启动并尝试初始化 PCMCIA 设备时挂起，请查看此支持提示：http://sdb.suse.de/sdb/html/mnened_6.3_pcmia-start.html。

由于 PCI 技术差异，你可能在你的笔记本电脑上没有声音。标准声驱动程序和配置工具是针对 ISA 类型 PnP 的。如果你愿意尝试开发内核版本，这可能解决你无声的困境。

# SuSE Linux 177 故障排除

“管理网络设置。”如果你决定不在 SuSE 中使用防火墙功能（数据包过滤），你你仍然可以使用 IP Chains 的伪装功能。

执行以下命令以在拨号连接设备 `ppp0` 上激活 IP Chains：

```
ipchains -P forward DENY
ipchains -A forward -i ppp0 -j MASQ
echo 1 > /proc/sys/net/ipv4/ip_forward
```

在连接到定义为 `eth0` 的以太网网卡的机器上执行这些命令：

```
ipchains -P forward DENY
ipchains -A forward -i eth0 -j MASQ
echo 1 > /proc/sys/net/ipv4/ip_forward
```
