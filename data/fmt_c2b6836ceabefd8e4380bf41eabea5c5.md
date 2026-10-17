
`[root@deep]# /etc/rc.d/init.d/firewall start`

# 拒绝某些地址的访问

假设你知道一个想要阻止访问你服务器的地址。你可以通过创建 rc.d 文件并取消你的防火墙规则脚本中以下行的注释来实现：

编辑你的防火墙脚本（`vi /etc/rc.d/init.d/firewall`）并取消以下行的注释：

```bash
if [ -f /etc/rc.d/init.d/firewall ]; then
```

创建一个 rc.d 文件，对于你想要阻止访问你服务器的地址：

`touch /etc/rc.d/init.d/firewall` 并取消防火墙规则脚本中以下行的注释：

```bash
假设你知道一个想要阻止访问你服务器的地址。
```

WHOIS 客户端 (`43`)

```bash
# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $ANYWHERE 43 \
-d $IPADDR $UNPRIPVPORTS -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! \
-s $IPADDR $UNPRIPVPORTS \
-d $ANYWHERE 43 -j ACCEPT
```

```bash
# 出站追踪路由

# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $TRACEROUT_SRC_PORTS \
-d $ANYWHERE $TRACEROUT_DEST_PORTS -j ACCEPT
```

# 本地网络内的无限制流量。
# 所有内部机器都可以访问防火墙机器。

```bash
ipchains -A input -i $LOCAL_INTERFACE_1 -s $LOCALNET_1 -j ACCEPT

ipchains -A output -i $LOCAL_INTERFACE_1 -d $LOCALNET_1 -j ACCEPT
```

# 伪装内部流量。
# 所有内部流量在外部进行伪装。

```bash
ipchains -A forward -i $EXTERNAL_INTERFACE -s $LOCALNET_1 -j MASQ
```

# 为选定的拒绝数据包启用日志

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-d $IPADDR -j DENY -l
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp
-d $IPADDR $PRIPVORTS -j DENY -l

ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-d $IPADDR $UNPRIVORTS -j DENY -I

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 5 -d $IPADDR -j DENY -I

ipchains -A input -i $EXTERNAL_INTERFACE -p icmp \
-s $ANYWHERE 13:255 -d $IPADDR -j DENY -I
```

```bash
stop)
echo -n "正在关闭防火墙服务:"

# 移除所有属于此过滤器的现有规则
ipchains -F

# 重置过滤器的默认策略为接受。
ipchains -P input ACCEPT
ipchains -P output ACCEPT
ipchains -P forward ACCEPT

# 重置 TCP SYN Cookie 保护为关闭。
echo 0 > /proc/sys/net/ipv4/tcp_syncookies

# 重置 IP 欺骗保护为关闭。
# 使用源地址验证
for i in /proc/sys/net/ipv4/conf/*/rp_filter; do
echo 0 > $i
done

# 重置 ICMP 重定向接受为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_redirects; do
echo 1 > $i
done

# 重置源路由包为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_source_route; do
echo 1 > $i
done

status)
echo -n "现在显示防火墙统计数据吗?"

restart(reload)
$0 stop
$0 start

)
echo "用法: firewall {start|stop|restart|reload}"
exit 1
esac
```

关于本页面的意见和建议请邮件至 `gnmouari@videotron.ca`

- 若要移动软磁盘中的 RPM 二进制文件，请使用命令：

`[root@deep] # mount /dev/fd0 /mnt/floppy/`

`[root@deep] # mv /bin/rpm /mnt/floppy`

`[root@deep] # umount /mnt/floppy/`

- 若将 RPM 二进制文件还原到原始目录，请使用命令：

`[root@deep] # mount /dev/td0 /mnt/floppy/`

`[root@deep] # cp /mnt/floppy/rpm /bin/`

`[root@deep] # umount /mnt/floppy/`

`注意：` 永远不要从系统中完全卸载 RPM 程序，否则你以后将无法重新安装 RPM 或其他软件所需的命令。

# 为什么我们选择使用 tar 包 (tarballs)？

Red Hat 发行版 以 RPM 文件的形式提供，也称为“软件包”，这是一种软件分发方式，可以方便地安装、升级、查询和删除。然而，在 Unix 世界，软件包分发的标准实际上仍然所谓的“tar 包”。tar 包是可以使用“tar”工具读取的简单文件。从 tar 包安装比使用 RPM 要琐琐得多。那么我们为什么要选择这样做呢？

- 1- 遗憾的是，开发者需要几周时间才能将最新版本的软件包转换为 RPM，因为许多开发者首先是以 tar 包的形式发布。
- 2- 当开发者发布新的 RPM 时，他们会包含许多不必要的选项。开发者不知道你可能哪些选项，哪些不需要，因此他们必须使用这种方法来满足每个人的需求。
- 3- RPM 并没有针对你特定的处理器进行优化，像 Red Hat Linux 这样的公司基于标准 PC 构建 RPM。这允许他们的 RPM 软件包安装在各种类型的计算机上，为 i386 机器编译的程序可以适用于所有系统。
- 4- 有时你下载并安装了 RPM，而世界上其他地方的人可能已经为了你的目的构建并提供了它。这可能会导致某些冲突（取决于软件包的构建方式）、错误、安全问题以及上述所有其他描述。

# 在你的系统上编译软件

粗略来说，程序是能够执行的计算机代码。有人用他/她理解的语言编写了“源代码”。那可能是 C 语言（很有可能）或其他某种语言。程序“源代码”对于编译器来说也有意义，编译器将这些指令转换为插入的任何处理器的二进制文件 - 例如 386 或类似的处理器。用于这些“可执行文件”的现代文件格式是 Elf。程序员将他的源代码展示给编译器并获得某种结果。早期的尝试编译失败或未按预期编译成功的情况完全并不罕见。编程的一半工作是追踪并修复这些问题（调试）。

与源代码编译相关的更多方面和新词汇你将在书中看到，包括但不限于：

多文件 (`The Multiple Files`)

© Copyright 1999 Open Network Architecture ®

关于本页面的意见和建议请邮件至 `gmournai@videotron.ca`

单文件程序很稀见。通常会有多个文件（例如 `*.c`），每个文件都被编译成对象文件 (`*.o`) 并链接成一个可执行文件。编译器通常用于执行链接（它在后台调用 `ld` 程序）。

# Makefile

这些文件旨在帮助保持一致性（确保你每次都以相同的方式构建程序）。它们也有助于提高速度。有些程序非常长——一个大型程序可能需要几十分钟。`make` 程序使用 `Makefile` 中的“依赖关系”来决定程序的哪些部分需要重新编译。如果你修改了五十个源文件中的一个，你只需要处理这并编译一个链接步骤，而不是从头开始。请注意，该格式在某些行的开头包含制表符（空格则不包含）。

# 库 (The Libraries)

程序不仅可以链接到对象文件 (`*o`)，还可以链接到库（对象文件的集合）。有时你必须链接到系统提供的库（例如，用于数学库的 `-lm`，如果没有它，你的数学 C 程序将产生无意义的结果）。链接库有两种形式：静态链接（代码进入可执行文件）和动态链接（代码在程序开始运行时被加载）。大型编译器手册通常会解释这二者的优缺点。

# 补丁 (The Patches)
