
除了使用上述技术保护您的文件和目录外，`LIDS` 还可以使用 Linux Capabilities（能力）来限制正在运行的程序（即进程）的能力。在传统的 Linux 系统中，`root` 用户（即 `UID` 和 `GID` 设置为 0 的用户）拥有所有的“能力”或执行任何任务（通过运行任何进程）的能力。`LIDS` 使用 Linux Capabilities 将 `root` 的所有权力（或由 `root` 用户运行的进程）分解为碎片，以便您可以精确调整特定进程能做或不能做什么。要了解可用的 Linux Capabilities，请参见 `/usr/include/linux/capability.h` 头文件。表 23-5 列出了所有 Linux Capabilities 及其在默认 `LIDS` Capabilities 配置文件 `/etc/lids/lids.cap` 中的状态（开启或关闭）。

| Capability ID | Capability Name | Meaning | Status in /etc/lids/lids.cap |
| :-- | :-- | :-- | :-- |
| 0 | `CAP_CHOWN` | 允许/禁止更改文件所有权 | 允许 |
| 1 | `CAP_DAC_OVERRIDE` | 允许/禁止覆盖所有 DAC 访问限制 | 允许 |
| 2 | `CAP_DAC_READ_SEARCH` | 允许/禁止覆盖所有有关读取和搜索的 DAC 限制 | 允许 |
| 3 | `CAP_FOWNER` | 允许/禁止以下限制：在文件中设置 `S_ISUID` 和 `S_ISGID` 位时，有效用户 ID 必须与文件所有者 ID 匹配；在文件中设置该位时，有效组 ID 必须与文件所有者 ID 匹配 | 允许 |
| 4 | `CAP_FSETID` | 允许/禁止在有效用户 ID 不等于所有者 ID 时访问 | 允许 |
| 5 | `CAP_KILL` | 允许/禁止向属于其他用户的进程发送信号 | 允许 |
| 6 | `CAP_SETGID` | 允许/禁止更改 `GID` | 允许 |
| 7 | `CAP_SETUID` | 允许/禁止更改 `UID` | 允许 |
| 8 | `CAP_SETPCAP` | 允许/禁止将当前集合的转移和移除给任何 `PID` | 允许 |
| 9 | `CAP_LINUX_IMMUTABLE` | 允许/禁止修改不可变文件和追加文件 | 禁止 |
| 10 | `CAP_NET_BIND_SERVICE` | 允许/禁止绑定到 1024 以下的端口 | 禁止 |
| 11 | `CAP_NET_BROADCAST` | 允许/禁止广播/监听组播 | 允许 |
| 12 | `CAP_NET_ADMIN` | 允许/禁止网络管理以执行接口配置、管理 `IP` 防火墙、设置伪装、设置 `IP` 记账、在套接字上设置调试选项、修改路由表、在套接字上设置任意进程/进程组所有权、为透明代理绑定任何地址、设置服务类型 (`TOS`)、设置混杂模式等 | 禁止 |
| 13 | `CAP_NET_RAW` | 允许/禁止使用原始套接字 | 禁止 |
| 14 | `CAP_IPC_LOCK` | 允许/禁止锁定共享内存段 | 允许 |
| 15 | `CAP_IPC_OWNER` | 允许/禁止 `IPC` 所有权检查 | 允许 |
| 16 | `CAP_SYS_MODULE` | 允许/禁止插入和移除内核模块 | 禁止 |
| 17 | `CAP_SYS_RAWIO` | 允许 `ioperm(2)`/`fiopl(2)` 访问 `CAP_SYS_CHROOT` `chroot(2)` | 禁止 |
| 18 | `CAP_SYS_CHROOT` | 允许/禁止 `chroot` 系统调用 | 禁止 |
| 19 | `CAP_SYS_PTRACE` | 允许/禁止 `ptrace` | 允许 |
| 20 | `CAP_SYS_PACCT` | 允许/禁止配置进程记账 | 允许 |
| 21 | `CAP_SYS_ADMIN` | 允许/禁止各种系统管理任务 | 允许 |
| 22 | `CAP_SYS_BOOT` | 允许/禁止重新启动 | 允许 |
| 23 | `CAP_SYS_NICE` | 允许/禁止使用 `nice` 命令更改进程优先级 | 允许 |
| 24 | `CAP_SYS_RESOURCE` | 允许/禁止设置系统资源限制 | 允许 |
| 25 | `CAP_SYS_TIME` | 允许/禁止设置系统时间 | 允许 |
| 26 | `CAP_SYS_TTY_CONFIG` | 允许/禁止伪终端 (`TTY`) 配置 | 允许 |
| 27 | `CAP_MKNOD` | 允许/禁止 `mknod()` 系统调用的特权方面 | 允许 |
| 28 | `CAP_LEASE` | 允许/禁止获取文件租约 | 允许 |
| 29 | `CAP_HIDDEN` | 允许/禁止将进程对系统的其余部分隐藏 | 允许 |
| 30 | `CAP_INIT_KILL` | 允许/禁止程序终止 `init` 进程（`PID` = 1）的子进程的能力 | 允许 |

上述 Linux Capabilities 的默认存储在 `/etc/lids/lids.cap` 文件中，如列表 23-8 所示。

### 列表 23-8: /etc/lids/lids.cap

```
+0:CAP_CHOWN
+1:CAP_DAC_OVERRIDE
+2:CAP_DAC_READ_SEARCH
+3:CAP_FOWNER
+4:CAP_FSETID
+5:CAP_KILL
+6:CAP_SETGID
+7:CAP_SETUID
+8:CAP_SETPCAP
-9:CAP_LINUX_IMMUTABLE
-10:CAP_NET_BIND_SERVICE
+11:CAP_NET_BROADCAST
-12:CAP_NET_ADMIN
-13:CAP_NET_RAW
+14:CAP_IPC_LOCK
+15:CAP_IPC_OWNER
-16:CAP_SYS_MODULE
-17:CAP_SYS_RAWIO
-18:CAP_SYS_CHROOT
+19:CAP_SYS_PTRACE
+20:CAP_SYS_PACCT
-21:CAP_SYS_ADMIN
+22:CAP_SYS_BOOT
+23:CAP_SYS_NICE
+24:CAP_SYS_RESOURCE
+25:CAP_SYS_TIME
+26:CAP_SYS_TTY_CONFIG
+27:CAP_MKNOD
+28:CAP_LEASE
+29:CAP_HIDDEN
+30:CAP_INIT_KILL
```

加号 (`+`) 启用该能力，减号 (`-`) 禁用该能力。例如，在上述列表中，最后一个名为 `CAP_INIT_KILL` 的 Linux Capability 是启用的，这意味着由 `root` 拥有的进程可以终止由 `init` 进程创建的任何子进程（通常是守护程序）。您可以使用文本编辑器来启用或禁用 Linux Capabilities。

## 通过使用 LIDS 管理的 Linux Capabilities 保护您的系统

您可以使用 `LIDS` 提供的能力来保护您的系统。在本节中，我将向您展示如何利用由 `LIDS` 管理的 Linux Capabilities。您将了解如何保护守护程序（例如 Apache Web 服务器）不被 `root` 用户终止，如何从 `ps` 等程序中隐藏进程，如何禁用对设备的原始访问，以及如何保护 `ext2` 不可变标志。

## 保护守护程序不被 root 终止

通常，守护进程（例如 Sendmail 邮件传输代理和 Apache Web 服务器）是由 `init` 进程启动的。如果您希望保护它们不被 `root` 用户终止，请将 `/etc/lids/lids.cap` 中的 `CAP_INIT_KILL` 设置修改为：

```
-30:CAP_INIT_KILL
```

重载 `LIDS` 配置（使用 `/sbin/lidsadm -S - + RELOAD_CONF` 命令）或重启系统并密封内核（在 `/etc/rc.d/rc.local` 脚本中使用 `/sbin/lidsadm -i` 命令）之后，你（作为 `root`）将无法终止 `init` 的子进程。这确保了即使系统被入侵且入侵者获得了 `root` 权限，入侵者也无法终止守护进程并用特洛伊木马版本替换它们。

## 向所有人隐藏进程

默认情况下，`CAP_HIDDEN` 能力在 `/etc/lids/lids.cap` 配置文件中是开启的。你可以使用以下命令将进程对所有人隐藏：

```
lidsadm -A -s /path/to/binary -t -o CAP_HIDDEN -j INHERIT
```

其中 `/path/to/binary` 是你希望隐藏时运行的可执行文件的完全限定路径。例如，要隐藏正在运行的 Apache 服务器进程 `/usr/local/apache/bin/httpd`，只需运行以下命令：

```
lidsadm -A -s /usr/local/apache/bin/httpd -t -o CAP_HIDDEN -j INHERIT
```

这将把进程标记为内核中的隐藏状态，无法使用任何用户空间工具（如 `ps` 或 `top`）找到它，甚至无法通过探索 `/proc` 文件系统中的文件来发现它。

## 禁用进程对原始设备的访问

通常，只有特殊进程才需要访问原始设备。因此，禁用对原始设备的访问并在需要时启用它们是个好主意，这符合“全部关闭，仅开放所需”的整体安全概念。

原始设备访问由 `CAP_SYS_RAWIO` 能力控制，该能力在 `/etc/lids/lids.cap` 配置文件中默认是禁用的。如果启用了它，进程就可以访问 `/dev/mem`、`/dev/port`、`/dev/mem`、`/dev/kmem` 以及其他原始块设备。例如，当此能力关闭时（如默认情况），`/sbin/lilo` 程序无法正常工作，因为它需要对硬盘进行原始设备级别的访问。

但是一些特殊程序，如 `XF86_SVGA`，可能需要此能力才能正常运行。在这种情况下，你可以按如下方式将该程序添加到例外列表中：

```
lidsadm -A -s /usr/X11R6/bin/XF86_SVGA -t -o CAP_SYS_RAWIO -j INHERIT
```

### 禁用网络管理任务

默认情况下，`CAP_NET_ADMIN` 能力是关闭的，这意味着网络管理员（通常是 `root` 用户）无法再执行以下网络管理任务：

- 配置以太网接口
- 管理 `IP` 防火墙、伪装（masquerading）和会计
- 设置套接字的调试选项
- 修改路由表
- 在套接字上设置任意的进程/进程组所有权
- 绑定到任何地址以进行透明代理
- 设置服务类型 (`TOS`)
- 设置混杂模式
- 清除驱动程序统计信息
- 组播
- 设置特定设备寄存器的读写

强烈建议保持默认设置。如果你确实需要执行上述任一任务，只需使用 `/sbin/lidsadm -S -- -LIDS` 命令临时关闭 `LIDS` 即可。

### 保护文件的 Linux 不可变标志

`ext2` 文件系统具有一个扩展功能，允许你将文件标记为不可变。这是通过 `chattr` 命令完成的。例如，`chattr +i /path/to/myfile` 会将 `/path/to/myfile` 变为不可变文件。具有不可变属性的文件不能被修改、删除或重命名，也不能创建符号链接。然而，`root` 用户可以使用 `chattr -i /path/to/myfile` 命令来更改该标志。你可以通过禁用 `CAP_LINUX_IMMUTABLE` 能力来保护不可变文件，使其即使对超级用户（`root`）也安全。请注意，`CAP_LINUX_IMMUTABLE` 在 `/etc/lids/lids.cap` 中默认是禁用的。

### 检测扫描器

如果你按照前面讨论的 `LIDS` 安装部分中的建议，在内核编译时启用了内置端口扫描器，就可以检测端口扫描器。该扫描器可以检测半开放扫描、`SYN` 隐蔽端口扫描、Stealth `FIN`、`Xmas` 或 `Null` 扫描等。诸如 `nmap` 和 Satan 或 Scan 等工具可以被检测器检测到。当原始套接字（`CAP_NET_RAW`）被禁用时，这是很有用的。

> **注意**
> 当 `CAP_NET_RAW` 关闭时，一些基于嗅探的用户空间扫描器将无法正常工作。但 `LIDS` 提供的基于内核的扫描器不使用任何套接字，这使其更加安全。你可能需要考虑使用 `LIDS` 提供的扫描器。

## 对入侵者的响应

当 `LIDS` 检测到任何 `ACL` 规则违规时，可以通过以下方法对该行为做出响应。

- **记录消息。** 当有人违反 `ACL` 规则时，`LIDS` 将使用内核日志守护程序 (`klogd`) 记录一条消息。
- **向适当的权限发送电子邮件。** 当发生违规时，`LIDS` 可以发送电子邮件。此功能由 `/etc/lids/lids.net` 文件控制，该文件在本章前面“编译、安装和配置 `LIDS`”部分的第 5 步中进行了讨论。
- **挂起控制台。** 如果你按照 `LIDS` 安装部分第 9 步中讨论的内容，在 `LIDS` 的内核补丁应用中启用了此选项，当用户违反 `ACL` 规则时，控制台将被断开。

`LIDS` 的另一个类似系统是 OpenWall 项目 (`www.openwall.com/linux`)。OpenWall 项目包含一些与 `LIDS` 中找到的不同的安全特性，其中一个特定的 OpenWall 补丁使进程的堆栈区域不可执行。你应该看看这个正在进行中的项目。

# HTTP 1.1 状态代码

对于来自 Web 客户端的每个请求，Web 服务器必须向客户端返回一个 `HTTP` 状态代码，由三位数字组成。Web 客户端可以通过查看 `HTTP` 状态行（Status-Line）头部中发送的此状态代码来尝试理解服务器的响应。代码附带一个简短的短语，称为原因短语，旨在为用户提供简要解释。例如，`HTTP` 状态行头部可能如下所示：

```
HTTP/1.1 404 Not Found
```
