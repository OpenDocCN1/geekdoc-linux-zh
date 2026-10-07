

# v.4.33
作为数字取证平台的的 Linux 全方位入门指南

通过更改权限。如果一个 rc 脚本是可执行的，它就会运行。如果它不可执行，则会被跳过。作为一个例子，让我们来看 rc.inet2 中的 OpenSSH（安全外壳）部分：

```
root@forensic:~# cat /etc/rc.d/rc.inet2
...
# Start the OpenSSH SSH daemon:
if [ -x /etc/rc.d/rc.sshd ]; then
echo "Starting OpenSSH SSH daemon: /usr/sbin/sshd"
/etc/rc.d/rc.sshd start
fi
...
```

再次，rc.inet2 的这个位置检查 `rc.sshd` 是否可执行。如果是，它就会运行命令 `/etc/rc.d/rc.sshd start`。请注意，在大多数情况下，rc 服务可以接收 `start`、`stop` 或 `restart` 作为参数传递。因此，在这个特定的示例中：

- `/inittab` 调用 `/etc/rc.d/rc.M`
- `/etc/rc.d/rc.M` 调用 `/etc/rc.d/rc.inet2`（如果 `rc.inet2` 可执行的）
- `/etc/rc.d/rc.inet2` 传递命令 `/etc/rc.d/rc.sshd start`（如果 `rc.sshd` 可执行）。

之前我们讨论了文件权限。现在让我们来看一个更改权限的实际示例，目的是防止某些服务在启动时自动启动。查看 `/etc/rc.d/rc.sshd` 的权限显示它是可执行的，因此当 `rc.inet2` 运行时，它会启动：

```
root@forensic:~# ls -l /etc/rc.d/rc.sshd
-rw-xr-x- 1 root 1726 Mar 10 2016 /etc/rc.d/rc.sshd*
```

为了更改权限以防止 SSH 服务在启动时运行，我执行了以下命令：

```
root@forensic:~# chmod 644 /etc/rc.d/rc.sshd
root@forensic:~# ls -l /etc/rc.d/rc.sshd
-rw-r--r-- 1 root 1726 Mar 10 2016 /etc/rc.d/rc.sshd
```

目录列表显示我已更改了脚本的可执行状态，从而防止了服务在系统启动时启动。根据你的终端颜色设置，你可能还会看到文件颜色发生变化。

你可以使用这种技术遍历你的 `/etc/rc.d/` 目录，关闭你不需要的服务。由于我没有使用笔记本电脑，不需要 PCMCIA 服务，我的工作站也没有无线网络支持，我将确保它们相应的不再启动。

```
root@forensic1:~# chmod 644 /etc/rc.d/rc.pcmcia
root@forensic1:~# chmod 644 /etc/rc.d/rc.wireless
```

你可能也会考虑对其他服务执行相同的操作：

```
root@forensic1:~# chmod 644 /etc/rc.d/rc.gpm-sample
```

如果你想知道每个脚本的作用，或者你不确定由某个特定 rc 脚本启动服务的用途，只需用你的分页程序（例如 `less`）打开脚本并阅读注释。关闭你需要的服务等同于让一个不需要的服务运行。学习每个脚本启动了什么、以及何时启动，并相应地启用它们。

例如，这里是 `/etc/rc.d/rc.yp` 开头的注释：

```
root@forensic1:~# less /etc/rc.d/rc.yp
#!/bin/sh
# /etc/rc.d/rc.yp
# Start NIS (Network Information Service). NIS 提供全网络范围的
# 主机名、用户名和其他信息数据库的发布。
# 在配置 NIS 后，你将需要取消脚本中
# 你想要运行的部分。
# 注意：有关设置 NIS 的详细信息，请参阅
# /usr/doc/yp-tools, /usr/doc/ypbind
# /usr/doc/yperv, 以及 /usr/doc/NIS-HOWTO.
```

我建议运行 ssh（通过 `/etc/rc.d/rc.ssh` 脚本）。如果你认为自己不会使用 SSH，随着你变得精通 Linux，你会发现“安全外壳”将成为你工具箱中重要的一部分。

## 基于主机的访问控制

我们继续关于基于主机的访问控制讨论。请注意，这**不是**防火墙。这是主机级别的访问控制。简单来说，我们可以通过两个文件 `/etc/hosts.deny` 和 `/etc/hosts.allow` 来决定谁可以访问我们的系统。为此，我们使用 TCP wrappers。

基本上，TCP wrappers 的工作原理如下：当配置为通过 TCP wrappers 运行的服务器接收连接请求时，`inetd` 守护进程调用封装服务 `/usr/sbin/tcpd`。`tcpd` 程序检查 `/etc/hosts.allow` 文件查看是否允许连接，并相应运行请求的服务。

如果只想看到那些未被注释的行，我可以这样做：

```
root@forensics:~# cat /etc/inetd.conf | grep -v ^
time      stream tcp wait root internal
time      dgram wait   root internal
comsat    dgram wait   /usr/sbin/tcpd in.comsat
auth      stream wait   /usr/sbin/in.ident in.ident
```

显示的命令显示了 `/etc/inetd.conf` 的内容并将输出传递给 `grep`。我们将使用 `grep` 显示不以 `#` 开头的行。字符 `^` 意味着“行首”。运行上面的命令只给了我配置中实际使用的那些行。为了理解这些服务如何工作，并找到关于我们系统上运行的特定信息，让我们更详细地查看：

```
comsat    dgram wait   /usr/sbin/tcpd in.comsat```

由于此行没有被注释，我们知道该服务被允许在系统上运行。为了了解这些服务如何工作并找到特定的信息，我们将禁用它并确认它已禁用。出于教学目的，在课程结束时，我们可能会保持启用。如果你正在运行 Linux（任何发行版），并且不知道哪些服务在运行以及为什么，那么你需要重新考虑保护你工作站的方法。

那么 `comsat` 服务是做什么的？我们可以对该程序运行 `man` 命令。在这种情况下，程序是 `in.comsat`。如果我们运行 `man in.comsat`，我们会看到该服务用于通知用户（邮件（biff）。

