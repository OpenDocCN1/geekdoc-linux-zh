
`xinetd` 0:off 1:off 2:on 3:on 4:on 5:on

6:off

`xinetd` based services:

`charg-dgram`: off

`charg-stream`: off

`daytime-dgram`: off

`daytime-stream`: off

`discard-dgram`: off

`discard-stream`: off

`echo-dgram`: off

`echo-stream`: off

`tcpmax-server`: off

`tftp`: on

`time-dgram`: off

`time-stream`: off

你在这里看到 `xinetd` 服务被设置为在启动时启动，且 TFTP 服务是它将启动启动的服务。

## 第 10 步

为了在不重启系统的情况下让服务运行起来，只需调整你需要的任何配置选项并重启 `xinetd` 服务即可：

```bash
# service xinetd restart
Stopping xinetd:      [ OK ]
Starting xinetd:     [ OK ]
```

## 第 11 步

验证 `xinetd` 服务现在正在系统上运行，并监听 UDP 端口 69 以待连接：

```bash
# netstat -a | grep tftp
udp 0 **:tftp
```

424 Red Hat® 考试实战指南：RHCSA® 和 RHCE® 认证指南与实验手册

> 考试提示
请记住，尽管这里提到了 TFTP 服务器，但实际上是 `xinetd` 服务在运行，并代表任何 TFTP 请求在 UDP 端口 69 上提供所有功能。

> 考试提示
同样请记住，对于你设置在 `xinetd` 下运行的任何服务，都需要制作防火墙规则来允许入站连接。

`xinetd` 服务识别来自 `/etc/services` 的服务和来自 `/etc/rpc` 的端口。这两个文件定义了系统可以用来通过 `xinetd` 主服务为客户端提供网络服务的所有服务和端口。`xinetd` 服务的配置非常简单，但你应该确保在 `/etc/xinetd.d` 目录下为你你想要使用的服务定义配置文件，并在使用前重启服务。对于任何 `xinetd` 服务的故障排除，你可以检查 `/var/log/messages` 文件，该文件是 `/etc/xinetd.conf` 文件定义要发送的所有日志的地方。虽然默认选项通常可以，但你也可以通过编辑主配置文件来编辑发送到日志文件的信息。以下是日志日志选项：

- Attempt（尝试）
- Duration（持续时间）
- Exit（退出）
- Pid（进程 ID）
- Host（主机）
- Userid（用户 ID）

你还有以下主机访问选项：

- `only_from`（仅来自）
- `no_access`（无访问）
- `access_times`（访问时间）

它们可以在主配置文件中定义以进行安全限制。通常情况下，让防火墙和 TCP Wrappers 来限制某些客户端更好。

> 考试提示
请记住，尽管这里提到了 TFTP 服务器，但实际上是 `xinetd` 服务在运行，并代表任何 TFTP 请求在 UDP 端口 69 上提供所有功能。

> 迁移提示
RHEL5，你配置了：

- 第 1 步。查询布尔值：
```bash
getsebool -a | grep tftpd_disable
```

- 第 2 步。禁用 SELinux：
```bash
setsebool -P tftpd_disable
```

- 第 3 步。验证已更改的：
```bash
getsebool -a | grep tftpd_disable
```

### 动态主机协议 (Dynamic Host Protocol)

基础知识之一是动态主机协议 (DHCP) 服务器，在你开始安装之前，检查你的接口：

```bash
# /etc/sysconfig/network-scripts/ifcfg-eth1
DEVICE=eth1
ONBOOT=yes
NM_CONTROLLED=no
BOOTPROTO=static
```

#### 安装 DHCP 服务器

实际上，软件包名为 `dhcp`，而服务名为 `dhcpd`。

- 第 1 步。首先安装 `dhcp` 包：
```bash
yum install -y dhcp
```

- 第 2 步。验证软件包已安装：
```bash
rpm -qa | grep dhcp
dhcp-4.1.1-12.P1.x86_64
```

- 第 3 步。安装软件包后，确保 `dhcpd` 服务在启动时启动：
```bash
chkconfig dhcpd on
```

- 第 4 步。验证 `dhcpd` 服务在启动时启动：
```bash
chkconfig dhcpd --list
dhcpd 0:off 1:off 2:on 3:on 4:on 5:on
6:off
```

#### 配置 DHCP 服务器

为了开始配置，让我们查看处理服务选项的重要文件：

- `/etc/dhcp/dhcpd.conf` 使用 IPv4 地址的 DHCP 主配置文件
- `/etc/dhcp/dhcpd6.conf` 使用 IPv6 地址的 DHCP 主配置文件
- `/var/lib/dhcpd/dhcpd.leases` IPv4 客户端文件
- `/var/lib/dhcpd/dhcpd6.leases` IPv6 客户端文件

主配置文件通常除了一两个注释外是空的。好消息是软件包提供了一个示例配置文件供你使用。该示例文件提供了如何配置你的 DHCP 服务器选项的示例和注释。

使用以下命令拷贝示例文件：

```bash
# /usr/share/doc/dhcpd-4.1.1/dhcpd.conf.sample /etc/dhcp/dhcpd.conf
```

# 全局选项
`ddns-update-style none;`
`authoritative;`

# 子网定义

```
subnet 172.168.1.0 netmask 255.255.255.0 {
  # 本地子网参数
  option routers 172.168.1.1;
  option subnet-mask 255.255.255.0;
  option domain-name "example.com";
  option domain-name-servers 172.168.1.1;
  default-lease-time 21600;
  max-lease-time 43200;
  # IP 范围
  range dynamic-bootp 172.168.1.100 172.168.1.200;
}
```
