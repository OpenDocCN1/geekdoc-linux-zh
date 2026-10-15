

### IP 转发

然后手动打开 IP 转发，如下所示，使用 sysctl（第 33 章），或使用 redhat-config 工具（可在系统工具下的 Extras 菜单中访问的内核调优工具），并在网络下的 IP 条目中 IP 面板中检查 IP 转发。这将设置 /etc/sysctl.conf 文件中的 net.ipv4.ip_forward 变量（如果愿意，您也可以手动更改此文件）。默认情况下 IP 转发处于关闭状态。

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

### 伪装选定主机

与其将所有本地主机伪装成防火墙/网关主机的单个 IP 地址，您可以使用 NAT 表重写少数选定主机的地址。这种方法通常应用于您希望多个本地主机作为 Internet 服务器出现的设置中。使用 DNAT 和 SNAT 目标，您可以将数据包定向到特定的本地主机。您将在 PREROUTING 和 POSTROUTING 链上使用规则来定向输入和输出数据包。

例如，前一个示例中描述的 Web 服务器本可以配置为本地主机，DNAT 目标可以将原本接收到 10.0.0.2 的任何数据包重定向到该主机。假设 Web 服务器设置在 192.168.0.5 上。它可以在 Internet 上显示为具有地址 10.0.0.2。发送到 10.0.0.2 的数据包将被重写并由 NAT 表定向到 192.168.0.5。您将使用 PREROUTING 链和 -d 选项来处理传入数据包，并使用 POSTROUTING 和 -s 选项处理传出数据包。

```
iptables -t nat -A PREROUTING -d 10.0.0.2 \
    --to-destination 192.168.0.5 -j DNAT
iptables -t nat -A POSTROUTING -s 192.168.0.5 \
    --to-source 10.0.0.2 -j SNAT
```

> 提示：请记住，使用 iptables 时，伪装不再与 FORWARD 链结合，如 ipchains 所做的那样。因此，如果您为 FORWARD 链指定 DROP 策略，您还必须专门为正在被伪装的网络启用 FORWARD 操作。您需要同时具有 POSTROUTING 规则和 FORWARD 规则。

## Part: Red Hat 服务器

- CHAPTER 20: Server Management
- CHAPTER 21: FTP Servers
- CHAPTER 22: Web Servers: Apache
- CHAPTER 23: Proxy Servers: Squid
- CHAPTER 24: Mail Servers: SMTP, POP, and IMAP
- CHAPTER 25: Print Servers
- CHAPTER 26: News and Search Servers

## 服务器管理

单个 Linux 系统可以提供多种不同的服务，例如邮件、Web 或 FTP 服务器。每个服务都作为一个持续运行的守护进程，寻找远程用户对其特定服务的请求。您可以通过启动或关闭其守护进程来打开或关闭服务。启动或关闭服务的流程由服务脚本处理，本章将详细介绍。

### 系统启动文件：/etc/rc.d 和 /etc/sysconfig

每次启动系统时，它都会从位于 /etc/rc.d 目录中的系统初始化文件读取一系列启动命令。这些初始化文件根据不同的任务组织。有些位于 /etc/rc.d 目录本身，而其他则位于名为 init.d 的子目录中。您不应更改这些文件中的任何一个。系统初始化文件的组织方式因 Linux 发行版而异。这里描述的是 Red Hat 的组织方式。您在 /etc/rc.d 中找到的一些文件列在表 20-1 中。

### /etc/rc.d/rc.sysinit

/etc/rc.d/rc.sysinit 文件包含用于初始化系统的命令，包括挂载和卸载文件系统。用于专门功能或设备的内核模块可以在 rc.modules 文件中加载。/etc/rc.d/rc.local 文件是执行的最后一个初始化文件。您可以在此处放置自己的命令。当您关闭系统时，系统会调用 halt 文件，其中包含关机命令。然后调用 init.d 中的文件以关闭守护进程，并卸载文件系统。在当前版本的 Red Hat 中，halt 位于 init.d 目录中。

### /etc/rc.d/init.d

/etc/rc.d/init.d 目录主要用于存放启动和关闭不同专用守护进程的脚本，例如网络和打印机守护进程以及字体和 Web 服务器的守护进程。这些文件具有双重功能，在系统启动时启动守护进程，在系统关闭时关闭守护进程。

