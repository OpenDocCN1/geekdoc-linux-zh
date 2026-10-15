
## 启用允许去碎片的保护

如果你将 Linux 服务器作为网关将内部流量伪装到互联网（IP 伪装），则必须启用此保护。

### RedHat Linux 6.1

```bash
root @deep ~# echo 1 > /proc/sys/net/ipv4/ip_frag
```

将上述命令添加到 `etc/rc.d/rc.local` 脚本中，这样在下次重启系统时你就不需要再次输入它们。

### RedHat Linux 6.2

编辑 `etc/sysctl.conf` 文件并添加以下行：

```bash
## 启用始终去碎片保护
net.ipv4.ip.always_defrag = 1
```

你必须重启网络使更改生效。重启内核的命令如下：

- 在你的系统上手动重启所有网络设备，使用以下命令：

`root @deep ~# /etc/rc.d/init.d/network restart`

Setting network parameters

Bringing up interface lo [ OK ]

Bringing up interface eth0 [ OK ]

Bringing up interface eth1 [ OK ]

## Linux 通用安全 第3 章

## 启用错误的错误消息保护

此选项将通过你网络中所有错误的错误消息。

### 在 RedHat Linux 6.1 下

```bash
[root@deep /# echo 1 > /proc/sys/net/ipv4/icmp_ignore_bogus_error_responses
```

将上述命令添加到 `etc/rc.local` 脚本文件中，这样在下次重启系统时你就不需要再次输入它们。

### 在 RedHat Linux 6.2 下

编辑 `etc/sysctl.conf` 文件并添加以下行：

```bash
## 启用错误的错误消息保护
net.ipv4.icmp_ignore_bogus_error_responses = 1
```

你必须重启网络使更改生效。重启内核的命令如下：

- 在你的系统上手动启动所有网络设备，使用以下命令：`[root@deep /# /etc/rc.d/init.d/network restart]`

Setting network parameters

Bringing up interface lo [ OK ]

Bringing up interface eth0 [ OK ]

Bringing up interface eth1 [ OK ]

## 启用 IP 欺骗保护

欺骗保护可以防止你的网络成为欺骗（即伪造）通信的源头，这些通信通常用于 DoS 攻击。

### 在 RedHat Linux 6.1 下

```bash
[root@deep /# for i in /proc/sys/net/ipv4/conf/*/rp_filter; do
echo 1 > $i
done
[root@deep /#]
```

将上述命令添加到 `etc/rc.local` 脚本文件中，这样在下次重启系统时你就不需要再次输入它们。

### 在 RedHat Linux 6.2 下

编辑 `etc/sysctl.conf` 文件并添加以下行：

```bash
## 启用 IP 欺骗保护，开启源地址验证
net.ipv4.conf.all.rp_filter = 1
```

你必须重启网络使更改生效。重启内核的命令如下：

- 在你的系统上手动启动所有网络设备，使用以下命令：`[root@deep /# /etc/rc.d/init.d/network restart]`

Setting network parameters

Bringing up interface lo [ OK ]

Bringing up interface eth0 [ OK ]

Bringing up interface eth1 [ OK ]

## Linux 通用安全 0 第3 章

## 记录欺骗包、源路由包、重定向包

此保护将将欺骗包、源路由包和重定向包记录到你的日志文件中。

### 在 RedHat Linux 6.1 下

```bash
[root@deep #] for i in /proc/sys/net/ipv4/conf/*.log_martians; do
> echo 1 > $i
done
[root@deep #]
```

将上述命令添加到 `/etc/rc.local` 脚本文件中，这样在下次重启系统时你就不需要再次输入它们。

### 在 RedHat Linux 6.2 下

编辑 `etc/sysctl.conf` 文件并添加以下行：

```bash
# 记录欺骗包、源路由包、重定向包
net.ipv4.conf.all.martians = 1
```

你必须重启网络使更改生效。重启内核的命令如下：

- 在你的系统上手动重启所有网络设备，使用以下命令：`root@deep # network restart`

Setting network parameters

Bringing up interface lo [ OK ]

Bringing up interface eth0 [ OK ]

Bringing up interface eth1 [ OK ]

## Linux通用安全

第3章

你可以使用 `cron` 任务定期检查、报告内容并删除 `HOME/.hosts` 文件。此外，用户应该知晓你根据策略要求会定期执行此类审计。

- 若要使用 `cron` 任务定期检查并通过邮件报告所有 ".rhosts" 文件，请执行以下操作：

以 "`root`" 身份在 `/etc/cron.daily/` 目录下创建 `find_rhosts_script` 文件（执行 `touch /etc/cron.daily/find_rhosts_files`），并在该脚本文件中添加以下行：

```sh
#!/bin/sh
/usr/bin/find -name .rhosts /home/ | cat <<EOF
这是一个由 find 命令生成的关于服务器 deep.opens.com 上可能存在的 ".rhosts" 文件的自动报告。

在 "home" 目录下新检测的 ".rhosts" 文件包括：
EOF
/bin/mail -s "Content of .rhosts file audit report" root
```

现在将该脚本设为可执行权限，验证所有者，并将组更改为 "`root`"：

`[root@deep #]# chmod 755 /etc/cron.daily/find_rhosts_files`

`[root@deep #]# chmod 000 /etc/cron.daily/find_rhosts_files`

每天都会向 "`root`" 发送邮件，主题为：Content of .rhosts file audit report，其中包含潜在的新型 ".rhosts" 文件。

## 系统已被攻破

如果你认为你的系统已被攻破，请联系 CERT © 协调中心或你在 FIRST（事件响应与安全小组论坛）的代表。

电子邮箱：`cert@cert.org`

CERT 热线：(+1) 412-268-7090

传真：(+1) 412-268-6989

CERT 人员在工作日的东部时间上午 8:00 (GMT -5)/东部夏令时间 (GMT -4) 回答，其他时段和节假日提供值服务。

## 第4章 系统优化

### 概述

在配置的这一阶段，你现在应该拥有一台配置良好且安全的 Linux 服务器。我们的服务器已包含了正常工作所需的核心软件包。在继续后续步骤并开始安装我们与客户共享的服务之前，对 Linux 服务器进行调至关重要。以下部分将引导你通过不同的步骤，针对你的特定处理器、内存和网络优化 Linux 服务器。通常情况下，如果你没有开箱即用 RedHat Linux，它并没有针对你的特定架构进行优化。

### "/etc/profile" 文件

"//etc/profile" 文件包含环境变量和启动程序。你在该文件中进行的所有自定义都将应用到整个系统环境，因此在该文件中放置优化标志是一个很好的选择。为了压榨 x86 程序的性能，你可以在编译时使用 `-O2` 标志进行全优化，这是最高级别的优化。注意注意：`-O` 标志并不总是能为你的处理器带来最佳性能。如果你是 x86 及以上版本，那么肯定可以，但低于 x86 的则不一定。编译时，对任何类型的处理器都使用 `-fomit-frame-pointer` 选项。这将使用堆栈来访问变量。遗憾的是，调试几乎是不可能的。你还可以使用 `-mcpu=cpu_type` 和 `-march=cpu_type` 选项针对 GCC 能力列表中列出的 CPU 优化程序。然而，生成的代码将仅运行在指定的 CPU 或更高版本的 CPU 上。

以下是根据你的 CPU 建议放在你的 "/etc/profile" 文件中的优化标志。这些优化标志仅在我们从服务器上编译并安装新程序时生效。这些优化对已有的程序没有作用。

第1步
