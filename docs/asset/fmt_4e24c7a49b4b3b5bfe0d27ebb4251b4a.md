
| 5005 4 root 19 0 SW | 0.0 0.0 | 00:33 | swapp |

| 5005 5 root 9 0 SW | 0.0 0.0 | 00:00 | creclaim |

| 5005 6 root 9 0 SW | 0.0 0.0 | 00:00 | bdflush |

| 5005 7 root 9 0 SW | 0.0 0.0 | 00:00 | |

| 5005 8 root 9 0 SW | 0.0 0.0 | 00:05 | updated |

| 5005 9 root -1:20 SW-C | 0.0 0.0 | 00:01 | recovery |

| 5005 13 root 9 0 SW | 0.0 0.0 | 00:00 | journald |

| 5005 89 root 9 0 SW | 0.0 0.0 | 00:00 | bud |

| 5005 219 root 9 0 SW | 0.0 0.0 | 00:00 | journald |

| 5005 220 root 9 0 SW | 0.0 0.0 | 00:00 | journald |

`uptime` 命令的第一行包含了 `uptime` 命令显示的相同信息：

```
jeff:-> uptime
3:30pm, 12 days, 23:29, 6 users, load average: 0.01, 02
```

这些程序的数据在 `/var/run/utmp`（当前连接用户的信息）和虚拟文件系统 `/proc/loadavg`（平均负载信息）中共享。有各种图形应用程序可以查看这些数据，例如 Gnome System Monitor 和 apps。在 [FreshMeat](https://www.freshmeat.net) 和 [SourceForge](https://www.sourceforge.org) 上，你会找到许多类型的应用程序可以将此信息与其他服务器数据以及多个服务器（一个 Web 服务器）集中，从而从一个工作站监控整个基础设施。

进程之间的关系可以使用 `pstree` 命令进行可视化：

```
sophie:-> pstree
init--+amd
|--apmd
+-2*[artsd]
+-atd
+-crond
+-deskguide_apple
+-eth0
+-gdm--gdm--+X
|--gnome-session--+Gnome
| |--ssh-agent
| |--true
+-geyes_applet
+-gkb_applet
+-gnome-name-serv
+-gnome-smproxy
+-gnome-terminal--+bash--vim
+-bash
+-bash---pstree
+-bash---ssh
+-bash---mozilla-bin--mozilla-bin--3*[mozilla-bin]
|--gnome-pty-helper
+-gpm
+-weather
+-kapm-idled
+-3*[kdeinit]
+-keeventd
+-khubd
+-5*[kjournal]
+-klogd
+-lockd---rpciod
+-lpd
+-mdrecoveryd
+-6*[mingetty]
+-8*[nfsd]
+-nscd---nscd--5*[nscd]
+-ntpd
+-3*[oafd]
+-panel
+-portmap
+-rhnsd
+-rpc.mountd
+-rpc.quotad
+-rpc.statd
+-sawfish
+-screenshooter_a
+-sendmail
+-sshd--+sshd---su---bash
+-syslog
+-tasklist_applet
+-vmnet-bridge
+-xfs
+-+xinetd-ipv6
```

## 进程

`-u` 和 `-a` 选项提供了额外信息。更多选项及其功能，请参考 Info 页面。

在下一节中，我们将看到一个进程如何创建另一个。

## 进程的生存与死亡

### 进程创建

新进程的创建是因为现有进程创建了自身的精确拷贝。这个子进程与其父进程具有相同的环境，只是进程 ID 不同。这种过程被称为分支（forking）。

在分支进程之后，子进程的地址空间会被新进程数据覆盖。这是通过对系统进行 `exec` 调用实现的。

`fork-and-exec` 机制将旧命令切换为新命令，而新程序中的环境保持不变，并配置了输入输出设备、环境变量和优先级。这种机制用于创建所有 UNIX 进程，因此也适用于 Linux 操作系统。第一个进程 `init`（进程 ID 为 1）是在启动过程中通过所谓的引导（bootstrapping）程序被分支产生的。

### 进程结束

当进程正常结束（即没有被杀死或没有以意外方式中断）时，进程会将其退出状态返回给父进程。该退出状态是由程序返回的数字，用于提供程序执行的结果。这种在执行作业时返回信息的机制源于 C 语言语言，而 UNIX 一直在使用这种语言。

返回码可以被父进程或在脚本中解释。返回码的值取决于具体的程序。这些信息通常可以在指定程序的 man 页面中找到，例如 `grep` 的返回码：如果没有找到匹配项，则返回 -1，并打印出类似“未找到文件”的消息的消息。另一个例子是 Bash 内置命令 `true`，它除了返回退出状态 0（表示成功）之外什么都不做。

## 信号

进程结束是因为它们接收到了信号。你可以向进程发送多个信号。使用 `kill` 命令向进程发送信号。命令 `kill -1` 显示信号列表。大多数信号供系统内部使用，或供程序员在编写代码时使用。作为用户，你需要以下信号：

### 表 4.2. 常用信号

| 信号名称 | 信号数字 | 含义 |
|---|---|---|
| SIGTERM | 15 | 以有序的方式终止进程。 |
| SIGINT | 2 | 中断进程。进程可以忽略此信号。 |
| SIGKILL | 9 | 中断进程。进程无法忽略此信号。 |
| SIGHUP | 1 | 用于守护进程：读取配置文件。 |

你可以在 `man 7` 中阅读更多关于向进程发送信号时所采取默认操作的信息。

## SUID 和 SGID

正如上一章中承诺的，我们现在将详细讨论 SUID 和 SGID 特殊模式。这些模式的存在是为了让普通用户能够执行某些由于 UNIX 系统文件权限方案而无法执行的任务。在理想情况下，应尽量使用特殊模式，因为它们包含了风险。Linux 开发者通常会尽可能避免它们。例如，Linux 的 `ps` 版本存储在 `/proc` 文件系统中的信息是所有人可见的，但避免了向公众暴露敏感系统数据。在此之前，以及在旧的 UNIX 系统上，`ps` 程序需要访问 `/dev/mem` 和 `/dev/kmem` 等文件，但由于这些文件的权限和所有权问题，这存在缺点：

```bash
rita->$ ls -1 /dev/*mem
crw-r------ 1 root kmem 1, 2 Aug 30 22:30 /dev/kmem
crw-r------ 1 root kmem 1, 1 Aug 30 22:30 /dev/mem
```

在旧版本的 `ps` 中，除非对程序应用了特殊模式，否则无法以普通用户启动程序。

### 进程

虽然我们通常尝试避免任何特殊模式，但有时必须使用 SUID。例如更改密码。比如，用户会希望自己设置密码，而不是由系统管理员设置密码。正如我们所知，用户名和密码列在 `/etc/passwd` 文件中，该文件具有访问权限和所有者：

```bash
bea-> ls -l /etc/passwd
-rw-r--r-- 1 root root 1267 Jan 16 14:43 /etc/passwd
```

尽管如此，用户需要更改该文件中的所有者信息。这是通过给密码赋予特殊权限来实现：

```bash
mia-> which passwd
passwd is /usr/bin/passwd
```

```bash
mia-> ls -l /usr/bin/passwd
-r-xr-xr-x 1 root root 13476 Aug 7 06:03 /usr/bin/passwd*
```

当被调用时，命令将使用 `root` 的访问权限运行，从而允许普通用户编辑由系统管理员拥有的密码文件。

SGID 通常涉及额外的组。在某些情况下，你可能会担心这个问题——必要的组通常在安装时创建。这是为了 `write` 和 `wall` 程序，它们用于向其他用户的终端（ttys）发送消息。`write` 命令向单个用户写入消息，而 `wall` 向所有已连接的用户写入。

通常不允许向另一个用户的终端或图形显示器发送文本。为了解决这个问题，会创建一个拥有所有设备的组。当 `write` 和 `wall` 命令被授予 SUID 权限时，命令将使用相应的访问权限运行（示例所示）。由于该组具有访问目标终端的权限，因此即使是没有权限使用终端的用户也可以向其发送消息。
