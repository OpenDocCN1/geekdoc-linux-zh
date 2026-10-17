
```bash
[root@rhel ~]# firewall-cmd --list-all |grep -i masquerade
masquerade: no
[root@rhel ~]# firewall-cmd --add-masquerade --permanent
success
[root@rhel ~]# firewall-cmd --reload
success
[root@rhel ~]# firewall-cmd --list-all |grep -i masquerade
masquerade: yes
```

## 图 8.15：使用 `firewall-cmd` 启用伪装

使用 `ufw` 需要手动完成编辑两个文件以及禁用/启用防火墙的任务：

- 编辑文件 `/etc/default/ufw`，并将 `DEFAULT_FORWARD_POLICY` 键的值设置为 `ACCEPT`。

- 编辑文件 `/etc/ufw/before.rules` 以添加以下行（在 `COMMIT` 行之前）：

  ```
  -A PREROUTING -s 192.168.122.0/24 -o eth0 -j MASQUERADE
  ```

- 执行命令：`ufw disable && sudo ufw enable`。

## 服务安全

保持系统访问服务方面的安全性至关重要。防火墙是安全的第一道屏障，指示了在网络连接中谁可以访问什么内容。与服务相关的一些建议如下：

- 禁用不需要的服务。某些服务在安装期间会被启用，建议监控系统中运行了哪些服务，并禁用不需要的服务。

- 配置服务在特定接口上监听。

- 使用入侵检测系统 (`IDS`)。

- 使用工具。

- 一对多网络地址转换 (`NAT`) 被用于重定向连接。

- 进程需要伪装。

可以使用 `app list` 参数列出定义的应用程序并使用 `app info` 获取信息。图 8.13 显示了用法示例：

```bash
root@ubuntu:~# ufw app list
Available applications:
OpenSSH
root@ubuntu:~# ufw info OpenSSH
Profile: OpenSSH
Title: Secure shell server, a rshd replacement
Description: OpenSSH is a free implementation of the Secure Shell.
Port:
22/tcp
```

图 8.13：使用 `ufw` 列出应用程序并获取信息

## 禁用服务

要列出运行的服务，使用 `systemctl list-units` 命令参数 `type=service`，如图 8.16 所示：

```text
UNIT                 LOAD ACTIVE DESCRIPTION
apparmor.service     active running AppArmor
atop.service         active running Atop
cron.service          active running Regular program
dbus.service         active running D-Bus System
getty1.service       active running Getty on tty1
irqbalance.service   active running irqbalance daemon
modemmanager.service  active running Modem Manager
multathd.service      active running Device-Mapper
network-dispatcher.service active running Dispatcher for systemd
ovswitch.service     active running OpenSwitch Unit
```

图 8.16：列出 `ufw` 中的服务

要列出运行的服务，使用 `systemctl list-units` 参数 `type=service` 和 `state=running`，如图 8.17 所示：

```text
UNIT                 LOAD ACTIVE DESCRIPTION
apparmor.service     active running AppArmor
atop.service         active running Atop
cron.service          active running Regular program
dbus.service         active running D-Bus System
getty1.service       active running Getty on tty1
irqbalance.service   active running irqbalance daemon
modemmanager.service  active running Modem Manager
multathd.service      active running Device-Mapper
network-dispatcher.service active running Dispatcher for systemd
ovswitch.service     active running OpenSwitch Unit
```

图 8.17：列出 `ufw` 中的服务

# 在所有接口上列出服务

可以使用 `ss` 命令列出在所有接口上监听的服务。要在所有接口上监听，`IPv4` 使用特殊 IP `0.0.0.0`，`IPv6` 使用 `[::]`。图 8.18 显示了针对这些 IP 进行过滤的示例：

```bash
root@ubuntu:~# ss -tunlp src = 0.0.0.0 or src = [::]
Netid State    Recv-Q Send-O Local Address:Port      Peer Address:Port
Process
tcp    LISTEN      128                   0.0.0.0:22             0.0.0.0:*
users:("sshd",pid=874,fd=3))
tcp    LISTEN      511                               *:*
users:("apache2",pid=2416,fd=4), ("apache2",pid=2415,fd=4), ("apache2",pid=2414,fd=4))
tcp    LISTEN      128                   [::]:22               [::]:*
users:("sshd",pid=874,fd=4))
```

图 8.18：`ss` 命令的输出示例

## 服务日志

传统上，服务使用自己的日志文件来存储与过程、访问或其他相关的信息。例如，`Apache2` 使用 `/var/log/httpd/` 或 `/var/log/apache2/` 目录记录 Web 服务器，用于分析对服务的非法访问。其他服务使用系统中的日志服务来存储日志。Linux 上用于该用途更流行的服务是 `syslog-ng`。

现代基础设施使用集中式日志聚合服务，系统将系统日志和服务日志流到该服务。流行的日志收集器有 `logstash`、`fluentd` 项目。使用集中式日志系统可以方便网络中所有 Linux 系统和服务的日志过滤和告警创建。`Grafana` 和 `Kibana` 项目是日志可视化的流行解决方案。

## 侵入检测系统

Linux 提供了几个流行的入侵检测系统（`IDS`）选项，用于检测文件完整性、连接攻击或对系统的未经授权访问。其中一些选项如下：

- `Tripwire`: 检测文件系统未经授权的更改。

- `Fail2ban`: 保护 Linux 系统免受暴力破解攻击。它通过读取日志并配置防火墙来阻止尝试攻击的 IP 地址。

- `Snort`: 一种网络入侵检测系统，用于检查所有入站和出站网络活动，并识别可能指示攻击的嫌疑模式。

安装 `tripwire`（使用软件存储库中的 `tripwire` 包）后，需要使用 `tripwire` 命令的 `--init` 选项启动数据库。图 8.19 显示了输出示例：
