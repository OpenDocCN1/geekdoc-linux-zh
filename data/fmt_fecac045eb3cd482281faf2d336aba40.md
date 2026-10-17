
| time | bread/s | lead/s | tcrcache | bwrit/s | lwrit/s | twcache | pread/s | pwrit/s |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 19:08:32 | 46 | 100 | 0 | 5 | 100 | 0 | 0 | 0 |
| 19:08:37 | 28 | 100 | 1 | 4 | 80 | 0 | 0 | 0 |
| 19:08:42 | 13 | 100 | 0 | 0 | 0 | 0 | 0 | 0 |
| 19:08:47 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 19:08:52 | 0 | 37 | 100 | 0 | 0 | 0 | 0 | 0 |
| 19:08:57 | 0 | 6 | 100 | 1 | 2 | 50 | 0 | 0 |
| 19:09:02 | 29 | 100 | 0 | 0 | 50 | 0 | 0 | 0 |
| 19:09:07 | 27 | 100 | 2 | 4 | 59 | 0 | 0 | 0 |
| 19:09:12 | 13 | 100 | 0 | 0 | 0 | 0 | 0 | 0 |
| 19:09:17 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Average | 20 | 100 | 0 | 2 | 77 | 0 | 0 |

性能交换空间是一个经常被忽视的领域。如果交换空间配置得当，你可以获得比配置不当时更好的性能。

运行 `swapinfo -at` 和 `swapinfo -m`。交换空间有时以随机方式添加到系统中。以下示例显示了 `/dev/dsk/c0t6d0` 上的两个交换分区，这是一种糟糕的做法：

![](img/6969df54e516231f8e64fd1177ac1127_1050_0.png)

### swapinfo -at

| TYPE | Kb AVAIL | USED | Kb FREE | USED | PCT | START/LIMIT | RESERVE | PRI | NAME | ( disk ) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| dev | 512000 | 0 | 512000 | 0 | 0% | 0 -0 | | 1 | /dev/vg00/lvol2 | c0t6d0 |
| dev | 274432 | 0 | 274432 | 0 | 0% | 0 -0 | | 0 | /dev/vg00/lvol8 | c0t6d0 |
| dev | 262144 | 0 | 262144 | 0 | 0% | 0 -0 | | 0 | /dev/vg03/lvol2 | c0t6d0 |
| dev | 512000 | 0 | 512000 | 0 | 0% | 0 -0 | | 1 | /dev/vg00/lvol2 | c0t6d0 |

## 补丁 (Patches)

无论你的系统中是否安装了适当的补丁，你都需要在审计中包含补丁清单。补丁很难维护，但它们对于系统的正常运行至关重要。你已安装的每个补丁的前几行都包含了该补丁的描述，包括它的编号。良好的审计程序会读取这些信息并将其保存到文件中，这样你就可以将其与其他重要文件放在同一个目录中。

## 网络 (Networking)

系统管理员花费大量时间来配置网络。如果你遇到了某种类型的系统灾难，拥有一个详尽记录网络设置的章节将非常有帮助。以下项目符号描述了需要检查的一些常见网络区域：

- 检查你的系统是否为 NFS 服务器，并检查 `/etc/exports` 查看导出的文件系统。

```
# grep err /var/adm/syslog/syslog.log
```

![](img/6969df54e516231f8e64fd1177ac1127_1056_0.png)

### 第 14 章 HP-UX 系统审计与系统配置库

- 使用以下命令检查 rpc 注册：

```
# rpcinfo -p
```

- 使用 DNS 检查你的系统信息：

```
# nslookup $HOSTNAME
```

- 检查 `/etc/resolv.conf` 是否存在，这表明你的系统使用了 DNS：

```
# cat /etc/resolv.conf
```

- 使用以下命令查看局域网（LAN）设备：

```
# ls -l /dev/lan*
```

- 通过运行 `lanscan` 所有接口的 LAN 卡。

- 使用以下命令检查内核中的 LAN 卡配置：

```
# ioscan -funC lan
```

- 使用以下命令显示路由：

```
# netstat -r
```

- 使用以下命令检查 SNA：

```
# snapshownet
```

- 使用以下命令检查 uucp：

```
# /usr/lib/uucp/uucheck -v
```

随着你对系统进行更改，审计你的系统变得越来越重要。在本节中涵盖的审计甚至没有涉及你运行的应用程序。拥有一个文档良好的系统并努力审查审计结果，从长远来看将获得丰厚的回。修复审计发现的小问题可能防止未来出现更大的问题。

## 一些示例脚本 (Some Example Scripts)

你最终希望有一个可以定期在你在你所有 HP-UX 系统上运行的完整审计程序。在本章中建议的主题是一个很好的起点。你可能还有系统的其他方面也应该定期审计。

接下来的章节包含几个可以运行的短脚本，以便让你了解通过审计脚本可以产生什么类型的输出。随后，可以将许多此类短脚本组合起来，产生一个更大、更全面的审计程序。你编写的短脚本可以作为主程序的子程序使用。

接下来的章节展示了示例脚本及其运行结果。本章之前的讨论已经涵盖了审计系统的主题，因此在后续章节中我不会包含过多的解释。

每个系统都是不同的，因此你可能需要修改脚本以满足你的需求。任何检查系统相关信息的程序在不同系统之间都会有所不同。

## 内核 (Kernel)

以下名为 `audker.sh` 的脚本判断现有内核是否是用 `/stand/system` 构建的。该程序运行 `system_prep -s` 并与文件 `/stand/system` 进行比较。

```
#!/bin/ksh

DESTF=$HOME/audit.ker.out

export DESTF

{
  /usr/sbin/sysadm/system_prep -s system.tmp
  diffs=`diff system.tmp /stand/system`
  if [ ! -z "$diffs" ]
  then
    echo "the system file is different: $diffs"
    echo "/stand/vmunix WAS NOT built with /stand/system"
  else
    echo "/stand/vmunix was built with /stand/system"
  fi
}
```

## 一些示例脚本 (Some Example Scripts)

这是运行 `audker.sh` 后获得的输出。

```
# audker.sh
the system file is different: 51a0
spt0
/stand/vmunix WAS NOT built with /stand/system
```
