
![](img/33fc180c04c8f96c022bce6e62ae12fd_34_0.png)

![](img/33fc180c04c8f96c022bce6e62ae12fd_35_1.png)

|---|---|

| 版本: 5 | 状态：已分配 (ASSIGNED) |

| Qs: Linux | 添加 CC |

| | ddomingo@redhat.com |

| isk@redhat.com |

| 分配给：ajax (ajason@redhat.com) | |

## Bug 注

我刚刚安装了 RHEL 5 客户端，注意到有时 X 分辨率会按照我的指定正确设为 1200x1024，但经常在重启 X 服务器后，它会将分辨率降级到 800x600。

`rss_lim`: 0

```
Backtrace was generated from '/usr/bin/yelp'
(no debugging symbols found)
Using host libthread_db library "lib/libthread_db.so."
(no debugging symbols found)
[Thread debugging using libthread_db enabled]
[New Thread -1208362396 (LWP 3961)]
[New Thread -1255040656 (LWP 4181)]
[New Thread -1243546736 (LWP 3963)]
[New Thread -1210463344 (LWP 3962)]
(no debugging symbols found)
(no debugging symbols found)
```

www.syngress.com

# 操作系统加固 • 第 23 章

```
0002ae402 in __kernel_vsyscall ()
#0 0002ae402 in __kernel_vsyscall ()
#1 00033dc5b in __waitpid_nocancel () from /lib/libthread.so.0
#2 0051d2c6 in gnome_gtk_module_info_get () from /usr/lib/libgnomeui-2.so.0
#3 <signal handler called>

#48 008051811 in g_cclosure_marshal_VOID_VOID ()

Thread 4 (Thread -1210426344 (LWP 3962)):
#0 0002ae402 in __kernel_vsyscall ()
(no debugging symbols found)
#0 0002ae402 in __kernel_v2

0000
)

Memory status: size: 147779584 vsize: 0 resident: 147779584 share: 0 rss: 68427776
rss_lim: 0
CPU usage: start_time: 1189756814 rtime: 0 utime: 2224 stime: 0 cutime: 2027 cstime: 197 it_real_value: 0 frequency: 93
```

![](img/33fc180c04c8f96c022bce6e62ae12fd_42_0.png)

现代 Linux 发行版已经增强了图形界面（GUI），以涵盖大多数管理任务，但对于优秀的管理员来说，知道在没有 GUI 的情况下如何执行这些任务至关重要。让我们讨论如何手动禁用某些存在漏洞的服务。

## 需要禁用的服务

Linux 从生上上就比大多数操作系统更安全。然而，每个新版本 Linux 内核的发布都存在不确定性，许多安全漏洞尚未被发现。大多数 Linux 服务不会受到这些攻击的影响。但是，管理员可以通过删除不必要的服务来降低风险。红帽 Linux（Red Hat Linux）包含了许多服务，因此管理员根据公司需求定制系统是合理的。请记住，当你移除不必要的服务时，你就是在移除风险。

## xinetd.conf 文件

虽然现代 Linux 发行版提供了更先进、更复杂的管理网络服务的方法，但 `/etc/xinetd.conf` 文件控制着许多 Unix 服务，包括文件传输协议（FTP）和 Telnet。它决定了系统可以使用哪些服务。`xinetd` 服务（类似于早期版本中的 `inet`）是一个“超级服务器”，负责监听一系列服务的入站网络活动。它确定所请求服务的实际性质并启动相应的服务。这种设计的主要由于是为了避免运行大量低流量的服务。此外，`xinetd` 根据需要启动服务的能力意味着只有在需要时运行相应数量的服务器。

`etc/xinetd.conf` 文件将 `xinetd` 服务的请求重定向到 `/etc/xinetd.d` 目录。每个 `xinetd` 服务在 `xinetd.d/` 中都有一个配置文件。如果某个服务在指定的配置中被注释掉，则该服务不可用。由于 `xinetd` 功能非常强大，`/etc/xinetd.d` 目录使得禁用系统未使用的服务变得非常简单。例如，你可以通过在各自的文件中注释 FTP 和 Telnet 服务并重启服务来禁用 FTP 和 Telnet 服务。如果服务被注释掉，它将不会重启。下一节将演示如何禁用 Telnet、FTP 和登录（login）服务。

## Telnet 和 FTP

大多数管理员发现，通过网络登录 Unix 机器进行管理是非常方便的。然而，在高度安全的环境中，可能允许通过物理访问来管理服务器。在这种情况下，你需要禁用 Telnet 交互式登录程序。一旦禁用，无人可以通过 Telnet 访问机器。

1. 要禁用 Telnet，你必须编辑 `/etc/xinetd.d/telnet` 文件。使用 `vi` 或你选择的编辑器打开 Telnet 文件。
2. 在 `service telnet` 之前添加井号（#）来注释掉服务 telnet 的行：

```
#service telnet
```

3. 保存并退出文件。
4. 接下来，你必须通过输入以下命令来重启 xinetd：

```
/etc/rc.d/init.d/xinetd restart
```

```
Stopping xinetd:      [OK]
Starting xinetd:     [OK]
```

5. 尝试使用 Telnet 登录系统。你应该会失败。
6. 请注意，在相应的 `xinetd.d` 目录中注释服务行可以禁用许多服务。

![](img/33fc180c04c8f96c022bce6e62ae12fd_43_0.png)

7. 使用相同的方法禁用 FTP 服务（例如，通过编辑 `xinetd.d/wu-fptd` 文件，注释掉 service ftp 行并重启 xinetd）。
8. 尝试通过 FTP 访问该服务。你将无法登录服务器。

## Rlogin 服务

远程登录（login）服务在 `/etc/xinetd.d/login` 文件中默认启用。`login` 存在安全漏洞，因为它可以绕过密码提示远程访问系统。与登录相关的关联有两个服务：`login` 和 RSH（远程外壳）。要禁用这些服务，请打开 `/etc/xinetd.d/login` 文件并注释掉服务行。然后，打开 `/etc/xinetd.d/rsh` 文件并注释掉服务行。重启 xinetd 以确保你的系统不再提供这些服务。

### 锁定端口

TCP/IP 网络为每个服务分配一个端口，例如 HTTP、简单邮件传输协议（SMTP）和邮局协议 3 版（POP3）。该端口被赋予一个数字，称为端口，用于连接到正确的服务。例如，如果客户端请求服务器的 Web 页面，请求将重定向到服务器上的 80 端口。Web 服务接收请求并将 Web 页面发送给客户端。每个服务都被分配一个端口号，每个端口都有一个 TCP 端口和一个 UDP 端口。例如，端口 53 用于域名系统（DNS）——将域名映射到 IP 地址。

TCP/IP 网络使用了两个范围的端口：已知端口和注册端口。已知端口是分配了特定端口号的网络服务（由 `/etc/services` 定义）。例如，SMTP 分配了 25 端口，HTTP 分配了 80 端口。注册端口是临时的，通常由客户端使用，且每次都可能不同。注册端口也称为临时端口（ephemeral ports），持续时间很短。随后该端口被遗弃，并可以被其他服务使用。端口号范围的分类如表所示：

| 类别 | 端口范围 |

|---|---|

（注：此处根据通用知识补充了表格逻辑，原文未提供完整表格内容，但描述了分类方式）

![](img/33fc180c04c8f96c022bce6e62ae12fd_47_0.png)

![](img/33fc180c04c8f96c022bce6e62ae12fd_47_1.png)

```
ps aux | grep portmap
```
