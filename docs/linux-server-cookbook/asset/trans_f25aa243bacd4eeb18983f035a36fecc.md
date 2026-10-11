

### 伪装（Masquerading）

在*第 7 章 网络配置*中，我们学习了如何配置 Linux 服务器作为路由器。使用**IP 转发**，可以将 Linux 系统用作网关来访问其他网络。但这仅在未涉及**网络地址转换 (NAT)** 时才可行。例如，在节点具有 IP `192.168.122.10` 且网关为 `192.168.122.1`，并且网络 `192.168.122.0/24` 中的节点使用网关 `192.168.122.10` 且启用了 **IP 转发** 的场景下，这种通信是可能的。
如果涉及**一对一多网络地址转换**，即来自一个网络的连接被重定向到另一个网络，则需要执行**伪装**来进行该连接。**图 8.14** 展示了流量流动和*IP 伪装*过程：

![](img/863afa537de4eed7deb11978bfbfa90e_258_0.png)

图 8.14：IP 伪装示意图

上述两种防火墙解决方案，**firewalld** 和 **ufw**，都允许为区域或接口启用伪装。图 8.15 展示了如何使用 **firewall-cmd** 命令的 `--add-masquerade` 选项来启用它：

```sh
[root@rhel ~]# firewall-cmd --list-all |grep -i masquerade
    masquerade: no
[root@rhel ~]# firewall-cmd --add-masquerade --permanent
success
[root@rhel ~]# firewall-cmd --reload
success
[root@rhel ~]# firewall-cmd --list-all |grep -i masquerade
    masquerade: yes
```

图 8.15：使用 firewall-cmd 启用伪装

使用 **ufw** 需要手动编辑两个文件，并禁用/启用防火墙：

-   *   编辑文件 `/etc/default/ufw`，并将键 `DEFAULT_FORWARD_POLICY` 的值设置为 **ACCEPT**。
-   *   编辑文件 `/etc/ufw/before.rules` 以添加以下行（在 **COMMIT** 行之前）：
    -   `-A POSTROUTING -s 192.168.122.0/24 -o eth0 -j MASQUERADE`
-   *   执行命令：`ufw disable && sudo ufw enable`。

### 服务安全性

确保系统在谁可以访问服务方面保持安全非常重要。防火墙是安全的第一道屏障，指示在网络连接中谁拥有访问权限以及访问什么。以下是一些与服务相关的安全建议：

-   *   禁用不需要服务的。某些服务在安装过程中被启用，建议监控系统正在运行的服务并禁用那些不需要的服务。
-   *   配置服务以监听特定接口。应用程序通常监听所有可用接口，这可能因防火墙接受通过其中一个接口的所有通信而导致安全线程问题。
-   *   如果未使用 IPv6，请将其关闭。某些网络不使用 IPv6，在这种情况下，建议不在服务上使用它，以避免非预期的访问。
-   *   启用日志记录和审计。对于用户将连接和操作的服務，启用日志记录和审计至关重要。建议使用集中式日志服务，以便创建报告和警报通知。
-   *   使用**入侵检测系统 (IDS)**。此服务检测对系统的潜在入侵。
-   *   使用安全模型。像 SELinux 和 AppArmor 这样的软件通过缓解未授权的访问和攻击来保护系统。

### 禁用不需要的服务

要列出已启用的服务，可以使用带有 `list-unit-files` 参数的命令 `systemctl`，并使用选项 `--type=service` 和 `--state=enabled` 进行过滤，如`图 8.16`所示：

```
root@ubuntu:~# systemctl list-unit-files --state=enabled --type=service
UNIT FILE                    STATE  VENDOR PRESET
apparmor.service             enabled enabled
atop.service                 enabled enabled
atopacct.service             enabled enabled
blk-availability.service     enabled enabled
cloud-config.service         enabled enabled
cloud-final.service          enabled enabled
cloud-init-local.service     enabled enabled
cloud-init.service           enabled enabled
console-setup.service        enabled enabled
cron.service                 enabled enabled
dmesg.service                enabled enabled
e2scrub_reap.service         enabled enabled
```

图 8.16：使用 systemctl 列出系统中已启用的服务

要列出系统中正在运行的服务，请使用参数 **list-units** 以及选项 `--type=service` 和 `--state=running`，如图 8.17 所示。

```
root@ubuntu:~# systemctl list-units --type=service --state=running
UNIT LOAD ACTIVE SUB DESCRIPTION
atop.service loaded active running Atop advanced performance mo
atopacct.service loaded active running Atop process accounting daem
cron.service loaded active running Regular background program p
dbus.service loaded active running D-Bus System Message Bus
getty@tty1.service loaded active running Getty on tty1
irqbalance.service loaded active running irqbalance daemon
ModemManager.service loaded active running Modem Manager
multipathd.service loaded active running Device-Mapper Multipath Devi
networkd-dispatcher.service loaded active running Dispatcher daemon for system
ovs-vswitchd.service loaded active running Open vSwitch Forwarding Unit
```

*图 8.17：使用命令 systemctl 列出系统中正在运行的服务*

### 列出监听所有接口的服务

命令 `ss` 可用于列出监听所有接口的服务。为了监听所有接口，对于 IPv4 使用特殊的本地 IP `0.0.0.0`，对于 IPv6 使用 `[::]`。*图 8.18* 展示了使用 `ss` 过滤这些 IP 的输出示例：

```
root@ubuntu:~# ss -tunlp 'src = 0.0.0.0 or src = [::]'
Netid State Recv-Q Send-Q Local Address:Port Peer Address:Port
Process
tcp LISTEN 0 128 0.0.0.0:22 0.0.0.0:*
users:("sshd",pid=874,fd=3))
tcp LISTEN 0 511 *:80 *:
users:("apache2",pid=2416,fd=4),("apache2",pid=2415,fd=4),("apache2",pid=2414,fd=4))
tcp LISTEN 0 128 [::]:22 [::]:*
users:("sshd",pid=874,fd=4))
```

*图 8.18：命令 `ss` 的输出示例*

在上面的示例中，服务 **sshd** 和 **apache2** 正在监听所有接口。每个服务定义了不同的配置文件和选项来指示在哪个接口上监听。例如，对于*SSH*服务器，选项名为 *ListenAddress*；对于 Apache2，选项为 *Listen*。

### 服务日志记录

传统上，服务使用自己的日志文件来存储与进程、访问或其他信息相关的信息。例如，**Apache2** 使用目录 `/var/log/httpd/` 或 `/var/log/apache2/` 来记录对 Web 服务器的访问，这对于分析对服务的非预期访问非常有用。其他服务使用系统中的*系统日志*服务来在其上存储*日志*。在 Linux 上用于此目的更流行的服务是 **syslog-ng**。

现代基础设施使用集中式日志聚合服务，系统将系统和日志流传输到该服务。流行的日志收集器包括 *logstash* 和 *fluentd* 项目。使用集中式日志系统简化了网络中所有 Linux 系统和服务的日志过滤和警报创建。项目 *Grafana* 和 *Kibana* 是日志可视化的流行解决方案。

### 入侵检测系统

Linux 提供了多种流行的*入侵检测系统*选项，例如检测文件完整性、连接攻击或对系统的未授权访问。这些选项的一些示例如下：

-   **Tripwire**：检测未授权的文件系统更改。
-   **Fail2ban**：保护 Linux 系统免受暴力破解攻击。它通过读取日志并配置防火墙来阻止尝试攻击的 IP 地址来工作。
-   **Snort**：**网络入侵检测系统**检查所有传入和传出网络活动，并识别可能表明攻击的可疑模式。

安装 *tripwire*（在软件仓库中使用 *tripwire* 包）后，需要使用命令 **tripwire** 的选项 **--init** 来启动数据库。*图 8.19* 展示了一个输出示例：

```
root@ubuntu:~# tripwire --init 2>/dev/null
Please enter your local passphrase:
Parsing policy file: /etc/tripwire/tw.pol
Generating the database...
*** Processing Unix File System ***
The object: "/dev/hugepages" is on a different file system...ignoring.
The object: "/dev/mqueue" is on a different file system...ignoring.
The object: "/dev/pts" is on a different file system...ignoring.
The object: "/dev/shm" is on a different file system...ignoring.
The object: "/proc/sys/fs/binfmt_misc" is on a different file system...ignoring.
Wrote database file: /var/lib/tripwire/ubuntux.example.com.twd
The database was successfully generated.
```

*图 8.19：命令 tripwire 的输出示例*

选项 **--check** 将显示自数据库创建以来在文件系统中所做的修改。例如，如果在 */usr/bin/* 中创建一个文件，该部分“Unix

