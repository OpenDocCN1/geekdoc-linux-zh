
从现在起，每当你重启或重启 `iptables` 时，都会读取这些规则。保存一份你用于创建规则的脚本副本，以防你以后再次需要它。

## 示例 1：用于共享 Internet 连接（外服务器）的防火墙

此示例展示了一个家庭或小型办公室的局域网，其中 Red Hat Linux 系统充当局域网和互联网之间的 `iptables` 防火墙。该防火墙计算机还充当了 Web 服务器、FTP 服务器和 DNS 服务器。图 14-1 显示了这种配置：

**图 14-1：** 使用 `iptables` 作为互联网和局域网之间的防火墙。如果你想使用接下来的示例防火墙脚本，你需要更改以下内容：

使用 `iptables` 作为互联网和局域网之间的防火墙。如果你想使用接下来的示例防火墙脚本，你需要更改以下内容：

# 第 14 章：计算机安全问题 523

3. 现在，你可以重启 Red Hat Linux，或者按照如下方式停止 `iptchains` 并卸载 `ipchains` 模块：

```
# /etc/init.d/iptchains stop

# modprobe -r iptables
```

4. 在启动 `iptables` 之前，你必须拥有一组已经配置并放置在你的 `/etc/sysconfig/iptables` 文件中的可以运行的规则。要创建这些规则，请参考接几个章节中的示例（如果没有准备好配置文件，`iptables` 将静默失败。）

5. 如果你正在进行 NAT 或 IP 伪装，则需要开启 IP 数据包转发功能。实现此功能的一种方法是将 `/etc/sysctl.conf` 文件中的 `net.ipv4.ip_forward` 的值改为 `1`。以 root 用户身份使用任何文本编辑器编辑此文件，并将该行修改如下所示：

```
net.ipv4.ip_forward = 1
```

6. 一旦规则就绪，启动 `iptables`：
```
# /etc/init.d/iptables start
```
