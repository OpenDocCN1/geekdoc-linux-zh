
在现实世界中，你会不断地处理防火墙规则。一个需要记住的重要点是，在测试防火墙规则时，你并不总是处于正在操作的系统面前。在调整或创建规则时，你需要小心，不要创建一个会将你锁在系统之外的规则！最糟糕的事情莫过于调整了一条规则并保存，结果后来发现你已经把自己锁在系统之外了，必须开车三个小时去灾难恢复中心，因为你无法访问你的服务器！

# 排查防火墙规则

在排查防火墙规则和连接时，你可以临时禁用防火墙，以确保防火墙确实是导致你问题的根源。你还可以使用 `service` 命令的状态选项来查看 `iptables` 的当前状态。

```
# service iptables status
```

表：filter

Chain INPUT (policy ACCEPT)

| num | target | opt | source | destination |
| :--- | :--- | :--- | :--- | :--- |
| 1 | ACCEPT | all | 0.0.0.0/0 | 0.0.0.0/0 | RELATED,ESTABLISHED |
| 2 | ACCEPT | icmp | 0.0.0.0/0 | 0.0.0.0/0 |
| 3 | ACCEPT | all | 0.0.0.0/0 | 0.0.0.0/0 |
| 4 | ACCEPT | tcp | 0.0.0.0/0 | 0.0.0.0/0 | state NEW tcp dpt:22 |
| 5 | REJECT | all | 0.0.0.0/0 | 0.0.0.0/0 | reject-with-icmp-host-prohibited |

```
Chain FORWARD (policy ACCEPT)
```

| num | target | opt | source | destination | match |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | ACCEPT | all | 0.0.0.0/0 | 0.0.0.0/0 | PHYSDEV match --physdevdev-is-bridged |
| 2 | REJECT | all | 0.0.0.0/0 | 0.0.0.0/0 | reject-with-icmp-host-prohibited |

```
Chain OUTPUT (policy ACCEPT)
```

| num | target | opt | source | destination |

你也可以检查 `/var/log/messages` 文件以查找 `iptables` 产生的任何消息，因为这是默认的日志文件。如果系统运行非常频繁，可能很难挑选出消息，因为该文件记录了许多不同服务的日志。虽然这个主题不在考试范围内，但在现实世界中获取仅来自防火墙服务的稳健反馈非常有帮助。

# 使用 NAT

`iptables` 的最后一个用途是网络地址转换 (NAT)。这允许你将服务器作为子网的网关，本质上控制进入和离开网络的流量。你实际上在实验中使用了这一点，以便所有系统可以使用 `RHEL01` 作为网关进出私有网络。

之前我们讨论了 `iptables` 的语法：

```
Syntax: iptables [options] [chain] [target]
```

然而，这里还有一个额外部分，即表类型：

```
Syntax: iptables -t [table-type] [chain] -j [target]
```

我最初漏掉了表类型是因为有两种类型的过滤器：filter 和 nat。默认情况下使用 filter，你需要指定它。因为你想使用 NAT，你需要知道表类型。目标 NAT (DNAT) 使用 `PREROUTING` 链。源 NAT (SNAT) 使用 `ROUTING` 链。

- 步骤 1. 使用以下规则实现 NAT：

```
# iptables -t nat -I PREROUTING -o eth0 -s 172.168.1.0/24 -j MASQUADE
```

- 步骤 2. 对内核进行以下更改：

```
# echo 1 > /proc/sys/ipv4/ip_forward
```

上述更改有效直到系统重启。如果你希望 IP 转发更改持久化，在 `/etc/sysctl.conf` 中添加该行：

```
net.ipv4.ip_forward = 1
```

# 可插认证模块

可插认证模块 (PAM) 包含一组用于在系统中实施安全的可加载库。它通过使用一组配置文件来检查不同的标准（取决于调用的应用程序或服务）。这些配置文件位于 32 位系统的 `/lib/security` 和 64 位系统的 `/lib64/security` 目录下。以下是一些可用的库模块：

```
# ls /lib/security
pam_access.so pam_mkhomedir.so
pam_creds.so pam_passwdqc.so
pam_chroot.so pam_permit.so
pam_console.so pam_pkcs11.so
pam_cracklib.so pam_postgresql.so
pam_debug.so pam_whistory.so
pam_deny.so pam_rosthosts_auth.so
pam_echo.so pam_rosthosts.so
```

# 访问安全

每个配置文件包含使用以下内容的四列：

```
module_type control_flag module_name [arguments]
```

进一步细分不同的选项，有四种不同的模块类型作为安全机制：

## Red Hat® 考试实战指南：RHCSSA™ 和 RHCE® 认证指南与实验手册

| 类型 | 功能 |
| :--- | :--- |
| auth (认证) | 建立身份 |
| account (账户) | 允许或拒绝访问 |
| password (密码) | 管理密码策略 |
| session (会话) | 将设置应用于应用程序 |

还有五种不同的控制标志，根据成功或失败决定要执行的操作：

- required (强制) | 如果通过则继续；即使失败也继续
- requisite (必须) | 失败时停止
- sufficient (足够) | 如果为真，则不需要其他验证
- optional (可选) | 忽略成功或失败
- include (包含) | 包含另一个文件的模块类型指令

第三列是应该调用的动态库文件名称，也包括任何可选参数。让我们来看其中一个配置文件作为示例：

```bash
# cat /etc/pam.d/reboot
#%PAM-1.0
auth      sufficient pam_rootok.so
auth      required pam_console.so
#auth     include   system-auth
account   required pam_permit.so
```

此 PAM 配置文件处理谁可以重启系统。`pam_rootok.so` 模块在用户以 root 用户身份调用命令时返回真。如果你由于“sufficient”控制标志而身份是 root 用户，则不需要任何其他要求，系统将重启。如果你不是 root 用户，下一行是：它检查你是否已在控制台中登录。这里的逻辑是，如果你不想在没有获得物理控制台访问权限的情况下重启系统并进入不稳定状态。如果是这种情况，则会调用最后一行（`pam_permit.so`），它始终返回真，因此系统将将重启。

PAM 模块及其配置文件并不难使用，但了解如何阅读以及它们的含义可能需要一些练习。确保你理解模块类型和控制标志。

这里是另一个常用调用模块的示例：

```bash
# cat /etc/pam.d/system-auth
#%PAM-1.0
# 此文件是自动生成的。
# 下次运行 authconfig 时，用户的更改将被销毁。
auth      required pam_env.so
auth      sufficient pam_unix.so nullock try_first_pass
auth      requisite pam_succeed.if uid >= 500 quiet
auth      required pam_deny.so
```

```bash
account   required pam_unix.so
account  sufficient pam_succeed.if.so uid < 500 quiet
account   required pam_permit.so
```

```bash
password  requisite pam_cracklib.so try_first_pass retry=3
password sufficient pam_unix.so md5 shadow nullock try_first_pass
password  required pam_deny.so
```

```bash
session   optional pam_keyinit.so revoke
session   required pam_limits.so
session   [success=1] default pam_succeed_if.so service in crond
quiet_use_id
session   required pam_unix.so
```

在不通过整个文件的情况下，我想指出第三行。在这里，你使用使用参数的使用作为模块名。此行要求用户具有一个大于或等于 500 的 UID（一个无意义的用户）。你可以对 `/etc/pam.d` 中的配置文件进行更改，但要确保其中某些文件由其他系统命令重新生成（如第三行注释所示）。

## PAM 故障排除

人们应该记住 PAM 模块的作用或它们的选项是什么。在需要对 PAM 进行故障排除时，知道去哪里查看将帮助你快速解决或自定义任何你与 PAM 工作所需的内容。首先，你应该知道 `/usr/share/doc/pam-<version>/txt` 目录包含 readme 文件，这些文件为你使用的每个 PAM 模块提供了详细信息和参数。这些信息可以帮助你准确判断某个特定模块的作用。其次，你应该知道 PAM 日志记录在独立的日志文件中。`/var/log/secure` 日志提供了与 PAM 事件相关的信息。如果你在进行故障排除或自定义某些内容，可以使用此日志文件作为参考，以确保一切运行正常。关于 PAM 的最后一个要检查的问题是查看是否对系统限制了访问。检查 `/etc/nologin` 文件是否存在。如果存在，则允许普通用户登录系统控制台；相反，将向用户显示 `/etc/nologin` 文件的文本。这对于控制台的系统加固很常见，但可能是你需要很好地如何检测和故障排除的内容。

## 管理密码策略

确保实施良好的密码策略有助于系统的于管理。它可以防止账户密码被破入和暴力破解。你有几种不同的方法可以管理系统上的密码策略。

- **步骤 1.** 查看 `/etc/login.defs` 文件，它控制密码长度、年龄和过期时间：

```bash
# cat /etc/login.defs
# 密码年龄控制：
# PASS_MAX_DAYS 密码允许使用的最大天数。
# PASS_MIN_DAYS 允许更改密码的最少天数。
# PASS_MIN_LEN 最小接受密码长度。
# PASS_WARN_AGE 密码过期前的警告天数。
PASS_MAX_DAYS 99999
PASS_MIN_DAYS 0
PASS_MIN_LEN 5
PASS_WARN_AGE 7
```

接下来，将你的注意力转转向 PAM。`cracklib` 和 `pwquality` 模块都用于强制。

- **步骤 2.** 查看当前的密码策略：

```bash
password  requisite pam_cracklib.so try_first_pass retry=3
```

你可以对 `/etc/pam.d` 中的配置文件进行更改，但要确保其中某些文件由其他系统命令重新生成（如第三行注释所示）。

- **步骤 3.** 查看 `/etc/login.defs` 文件，它控制密码长度、年龄和过期时间：

## 总结

处理 Red Hat 的安全并非易事。在第一部分，我们描述了 Wrapper。接下来，我们查看了防火墙规则和 NAT。最后，我们讨论了 PAM，它提供了系统的部分功能。

### 习题

1. Red Hat 中的所有服务都可以 Wrapper。对还是错？
2. 防火墙默认是禁用的。对还是错？
3. 当安装 Red Hat Enterprise 6 时，SELinux 以强制模式运行。对还是错？
4. 以下防火墙规则实现了什么：`iptables -I INPUT 5 -p tcp -m tcp --dport 80 -j ACCEPT`？
5. `iptables` 文件中的最后规则是什么？
6. PAM 用于什么？
7. 什么是 NAT？如何使用的？
8. 以下防火墙规则在 Red Hat Enterprise 6 下有效：`iptables -I RH-Firewall-1-INPUT -p tcp -m tcp --dport 22 -j ACCEPT`。对还是错？

### 习题答案

1. 错。服务需要支持才能使用。
2. 错。防火墙默认是启用的。
3. 对。对于 Red Hat Enterprise 6，SELinux 以模式启动。
4. 该防火墙规则插入到 `iptables` 规则的第五行，并允许防火墙上的 TCP 端口 80（HTTP 服务）。
5. 最后规则始终隐式拒绝语句，拒绝任何未被规则允许的内容。
6. PAM 用于一种模块化的方式来实现安全。在本章中，我们讨论的主要功能是管理密码策略和。
7. 网络地址转换 (NAT) 维护一个允许允许多个 IP 地址转换为多个公网 IP 地址（称为地址转换）。它也可以用于一对一或一对多关系。
8. 错。使用的 INPUT 链是 Red Hat Enterprise 5 下默认的。此规则在 Red Hat Enterprise 6 下会产生错误。

## 实验 12

## 任务 1 – TCP Wrappers

- **步骤 1.** 根据以下指南设置 TCP Wrappers：
  - a. `RHEL01` 应允许来自 `192.168.1.0/24` 和 `172.168.1.0/24` 网络的 SSH 访问。
  - b. `Client02` 应仅允许来自 `172.168.1.0/24` 网络的 SSH 访问。
  - c. 拒绝此处列出的两个系统上来自任何网络的所有其他访问。

当正确设置 TCP Wrappers 后，任务完成。

## 任务 2 – 防火墙规则

- **步骤 1.** 创建以下防火墙规则：
  - a. 允许访问 `RHEL02` 上的 TCP 端口 3306。
  - b. 允许访问实验室所有服务器上的 TCP 端口 22。
  - c. 拒绝 `Client02` 上的 80 端口和 3306 端口的访问。
  - d. 在 `Client01` 上拒绝来自 `Client02` 的 80 端口访问。

当所有防火墙规则成功生效后，任务完成。

本章涵盖了以下主题：

- SSH——本节介绍了使用 SSH 协议对系统进行远程管理。
- SSH 安全重温——本节再次查看 SSH 协议以及一些更高级的安全保护方法。
- VNC 服务器——本节介绍了使用 GUI 连接进行远程管理。

涵盖了以下 RHCSA 考试目标：

- 使用 SSH 和 VNC 访问远程系统
- 部署一个允许共享多个桌面的 VNC 服务器

涵盖了以下 RHCE 考试目标：

- 安装提供服务所需的软件包
- 配置 SELinux 以支持该服务
- 配置服务在系统启动时自动启动
- 配置服务以进行基本操作
- 为服务配置基于主机和基于用户的安全防护
- 配置基于密钥的认证
- 配置文档中描述的额外选项

## 第 13 章

## 远程访问

你进入服务器房并在你的新服务器上安装 Red Hat。安装完成后，你将需要配置许多软件包并设置用户。所有这些任务都需要时间，如果你在数据中心工作，很有可能你的办公室位于其他地方。对你正在管理和故障排除的任何系统进行远程访问要容易得多，因为你不需要物理上与系统处于同一个位置。在本章中，我们将讨论使用 SSH 进行命令行远程访问，以及使用 VNC 进行图形化远程访问。

## Secure Shell (SSH)

你知道在某个时刻你将远程管理服务器，而且你不希望在没有某种安全措施的情况下这样做，对吧？SSH 可以保护从你的计算机到远程计算机传输的流量，为管理创建一个隧道。SSH 用于通信的隧道是加密的，与 Telnet 等不采用任何加密的协议不同。SSH 是一个非常容易设置的服务，并在许多方面都有用。虽然它通常是默认安装的，但你仍需要验证。

- 步骤 1. 验证 SSH 服务器软件包是否已安装：

```bash
# rpm -qa | grep ssh
libssh2-1.2.2-70.el16.x86_64
openssh-5.3p1-20.el16.x86_64
openssh-server-5.3p1-20.el16.x86_64
openssh-clients-5.3p1-20.el16.x86_64
```

- 步骤 2. 如果未安装 SSH 服务器软件包，执行以下操作：

```bash
# yum install -y openssh-server
```

- 步骤 3. 确保再次验证：

```bash
# rpm -qa | grep ssh
openssh-server-5.3p1-20.el16.x86_64
```

- 步骤 4. 确保服务正在运行（如果未运行则启动它）：

```bash
# service ssh status
hd (pid 678) is running...
```

现在服务正在运行，你还应该确保服务被设置为系统启动时启动。

## 步骤 1. 在启动时启用服务：

```bash
# chconfig sshd on
```

- 步骤 2. 验证服务在启动时是否已启用：
