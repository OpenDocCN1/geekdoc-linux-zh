
## 允许追加访问

通常，程序只需要对诸如 /var/log/messages 或 /var/log/secure 等关键系统日志进行追加访问。您可以使用以下命令为这两个文件启用追加模式：

```
/sbin/lids -A -o /var/log/messages -j APPEND
/sbin/lids -A -o /var/log/secure -j APPEND
```

## 允许仅写访问

若要允许名为 /usr/local/apache/bin/httpd 的程序能够向名为 /home/httpd 的保护目录写入数据，请运行以下命令：

```
/sbin/lids -A -o /home/httpd -j DENY
/sbin/lids -A -s /usr/local/apache/bin/httpd -o /home/httpd -j READ
```

## 删除 ACL

若要删除所有 ACL 规则，请运行 /sbin/lidsadm -Z 命令。若要删除单独的 ACL 规则，只需指定该 ACL 的主体（如果有）和/或对象。例如，如果您运行 /sbin/lidsadm -D -o /bin 命令，则以 /bin 为对象的所有 ACL 规则都会被删除。但是，如果您运行 /sbin/lidsadm -D -s /bin/login -o /bin 命令，则只有指定 /bin/login 为主体且 /bin 为对象的 ACL 会被删除。

> **注意** 不带任何参数指定 -Z 或 -D 选项会删除您所有的 ACL 规则。

## 一种良好的文件和目录保护方案

在本节中，我将向您展示一种您可以与 LIDS 配合使用的良好保护方案。该方案允许您将 /boot 目录（或分区）设为只读，这意味着内核不能被入侵者修改；它还将系统库目录 /lib、root 用户的家庭目录 /root、系统配置目录 /etc、系统守护程序二进制文件目录 /sbin 和 /usr/sbin，以及标准二进制文件目录 /usr/bin 和 /bin 设为只读。它还仅允许对 /var/log 目录中的文件进行追加操作，从而确保日志文件不会被任何入侵者破坏。该配置如下所示：

```
# 将 /boot 目录或分区设为只读
/sbin/lidsadm -A -o /boot -j READ

# 将系统库目录设为只读
# 这也保护了 lib/modules
/sbin/lidsadm -A -o /lib -j READ

# 将 root 用户的家庭目录设为只读
/sbin/lidsadm -A -o /root -j READ

# 将系统配置目录设为只读
/sbin/lidsadm -A -o /etc -j READ

# 将守护程序二进制文件目录设为只读
/sbin/lidsadm -A -o /sbin -j READ

# 将其他守护程序二进制文件目录设为只读
/sbin/lidsadm -A -o /usr/sbin -j READ

# 将通用二进制文件目录设为只读
/sbin/lidsadm -A -o /bin -j READ

# 将其他通用二进制文件目录设为只读
/sbin/lidsadm -A -o /usr/bin -j READ

# 将通用库目录设为只读
/sbin/lidsadm -A -o /lib -j READ

# 将系统日志目录设为追加模式
/sbin/lidsadm -A -o /var/log -j APPEND

# 将 X Windows 二进制文件目录设为只读
/sbin/lidsadm -A -o /usr/X11R6/bin -j READ
```

除了使用上述技术保护您的文件和目录外，LIDS 还可以使用 Linux Capabilities（能力）来限制正在运行的程序（即进程）的能力。在传统的 Linux 系统中，root 用户（即 UID 和 GID 设置为 0 的用户）拥有所有的“能力”或执行任何任务（通过运行任何进程）的能力。LIDS 使用 Linux Capabilities 将 root 的所有权力（或由 root 用户运行的进程）分解为碎片，以便您可以精确调整特定进程能做或不能做什么。要了解可用的 Linux Capabilities，请参见 /usr/include/linux/capability.h 头文件。表 23-5 列出了所有 Linux Capabilities 及其在默认 LIDS Capabilities 配置文件 /etc/lids/lids.cap 中的状态（开启或关闭）。

| Capability ID | Capability Name | Meaning | Status in /etc/lids/lids.cap |
| :-- | :-- | :-- | :-- |
| 0 | CAP_CHOWN | 允许/禁止更改文件所有权 | 允许 |
| 1 | CAP_DAC_OVERRIDE | 允许/禁止覆盖所有 DAC 访问限制 | 允许 |
| 2 | CAP_DAC_READ_SEARCH | 允许/禁止覆盖所有有关读取和搜索的 DAC 限制 | 允许 |
| 3 | CAP_FOWNER | 允许/禁止以下限制：在文件中设置 `S_ISUID` 和 `S_ISGID` 位时，有效用户 ID 必须与文件所有者 ID 匹配；在文件中设置该位时，有效组 ID 必须与文件所有者 ID 匹配 | 允许 |
| 4 | CAP_FSETID | 允许/禁止在有效用户 ID 不等于所有者 ID 时访问 | 允许 |
| 5 | CAP_KILL | 允许/禁止向属于其他用户的进程发送信号 | 允许 |
| 6 | CAP_SETGID | 允许/禁止更改 GID | 允许 |
| 7 | CAP_SETUID | 允许/禁止更改 UID | 允许 |
| 8 | CAP_SETPCAP | 允许/禁止将当前集合的转移和移除给任何 PID | 允许 |
| 9 | CAP_LINUX_IMMUTABLE | 允许/禁止修改不可变文件和追加文件 | 禁止 |
| 10 | CAP_NET_BIND_SERVICE | 允许/禁止绑定到 1024 以下的端口 | 禁止 |
| 11 | CAP_NET_BROADCAST | 允许/禁止广播/监听组播 | 允许 |
| 12 | CAP_NET_ADMIN | 允许/禁止网络管理以执行接口配置、管理 IP 防火墙、设置伪装、设置 IP 记账、在套接字上设置调试选项、修改路由表、在套接字上设置任意进程/进程组所有权、为透明代理绑定任何地址、设置服务类型 (TOS)、设置混杂模式等 | 禁止 |
| 13 | CAP_NET_RAW | 允许/禁止使用原始套接字 | 禁止 |
| 14 | CAP_IPC_LOCK | 允许/禁止锁定共享内存段 | 允许 |
| 15 | CAP_IPC_OWNER | 允许/禁止 IPC 所有权检查 | 允许 |
| 16 | CAP_SYS_MODULE | 允许/禁止插入和移除内核模块 | 禁止 |
| 17 | CAP_SYS_RAWIO | 允许 ioperm(2)/fiopl(2) 访问 CAP_SYS_CHROOT chroot(2) | 禁止 |
| 18 | CAP_SYS_CHROOT | 允许/禁止 chroot 系统调用 | 禁止 |
| 19 | CAP_SYS_PTRACE | 允许/禁止 ptrace | 允许 |
| 20 | CAP_SYS_PACCT | 允许/禁止配置进程记账 | 允许 |
| 21 | CAP_SYS_ADMIN | 允许/禁止各种系统管理任务 | 允许 |
| 22 | CAP_SYS_BOOT | 允许/禁止重新启动 | 允许 |
| 23 | CAP_SYS_NICE | 允许/禁止使用 *nice* 命令更改进程优先级 | 允许 |
| 24 | CAP_SYS_RESOURCE | 允许/禁止设置系统资源限制 | 允许 |
| 25 | CAP_SYS_TIME | 允许/禁止设置系统时间 | 允许 |
| 26 | CAP_SYS_TTY_CONFIG | 允许/禁止伪终端 (TTY) 配置 | 允许 |
| 27 | CAP_MKNOD | 允许/禁止 *mknod*() 系统调用的特权方面 | 允许 |
| 28 | CAP_LEASE | 允许/禁止获取文件租约 | 允许 |
| 29 | CAP_HIDDEN | 允许/禁止将进程对系统的其余部分隐藏 | 允许 |
| 30 | CAP_INIT_KILL | 允许/禁止程序终止 *init* 进程（PID = 1）的子进程的能力 | 允许 |

上述 Linux Capabilities 的默认设置存储在 */etc/lids/lids.cap* 文件中，如列表 23-8 所示。

### 列表 23-8: */etc/lids/lids.cap*

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

加号 (+) 启用该能力，减号 (-) 禁用该能力。例如，在上述列表中，最后一个名为 `CAP_INIT_KILL` 的 Linux Capability 是启用的，这意味着由 root 拥有的进程可以终止由 `init` 进程创建的任何子进程（通常是守护程序）。您可以使用文本编辑器来启用或禁用 Linux Capabilities。

## 通过使用 LIDS 管理的 Linux Capabilities 保护您的系统

您可以使用 LIDS 提供的能力来保护您的系统。在本节中，我将向您展示如何利用由 LIDS 管理的 Linux Capabilities。您将了解如何保护守护程序（例如 Apache Web 服务器）不被 root 用户终止，如何从 `ps` 等程序中隐藏进程，如何禁用对设备的原始访问，以及如何保护 ext2 不可变标志。

## 保护守护程序不被 root 终止

通常，守护进程（例如 Sendmail 邮件传输代理和 Apache Web 服务器）是由 `init` 进程启动的。如果您希望保护它们不被 root 用户终止，请将 `/etc/lids/lids.cap` 中的 `CAP_INIT_KILL` 设置修改为：

```
-30:CAP_INIT_KILL
```
