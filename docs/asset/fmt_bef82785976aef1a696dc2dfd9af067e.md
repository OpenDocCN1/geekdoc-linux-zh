
`dmesg | grep eth0 /etc/modprobe.conf | cut -d ' ' -f 3`

此命令在消息中搜索任何包含以太网卡名称的行（反引号内——`grep eth0 /etc/modprobe.conf | cut -d ' ' -f 3` 从 `/etc/modprobe.conf` 文件中提取 `eth0` 设备的别名）。`grep` 的 `A` `2` 选项会导致它为匹配搜索标准的行打印两行内容。

在我的 PC 上，我安装了一块 3Com PCI 3c905 以太网卡，因此当我在系统上输入命令时，我得到如下输出：

```
3cx59: Donald Becker and others,, www.scylid.com/network/vortex.html

0000:02:01:0:3Com PCI 3c905 Tornado at 0x3000. Vers LKI.1.1

divert: allocating divert_blk for eth0
```
