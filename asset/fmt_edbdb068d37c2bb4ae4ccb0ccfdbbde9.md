
输出的第 1 列（`Login Name`）显示 Linux 用户，第 2 列（`SELinux User`）显示 SELinux 用户。第 3 和 4 列显示相关的安全级别（`MLS/MCS Range`）以及 Linux 用户的上下文（`*` 代表所有服务）。默认情况下，所有非 root Linux 用户表示为 `__default__`，它映射到策略中的 `unconfined_u` 用户。

## 进程的 SELinux 上文

你可以使用带有 `-Z` 标志的 `ps` 命令确定进程的上下文。以下示例仅显示了命令输出的前两行：

```
[user1@server10 ~]$ ps -ez
LABEL PID TTY TIME CMD
system_u:system_r:init:s0 1 ? 00:00:04 systemd
```

在输出中，主体 (`system_u`) 是 SELinux 用户名（映射到 Linux 用户 root），对象是 `system_r`，域 (`init_t`) 揭示了应用于进程的保护类型以及安全级别 (`s0`)。任何不受保护的进程将在 `unconfined_t` 域中运行。

## 文件的 SELinux 上文

你可以查看文件和目录的上下文。为此，请使用带有 `-Z` 切换的 `ls` 命令。以下显示了设置在 `/etc/password` 文件上的四个属性：

```
[user8@server10 ~] ls -Z /etc/passwd
-rw-r--r-- 1 root root system object:passwd:s0 2809 Nov 11 07:24 /etc/passwd
```

结果指示了主体 (`system_u`)、对象 (`object_r`)、类型 (`passwd file_t`) 和安全级别 (`s0`)。

## 带 SELinux 上文的文件复制、移动和归档

如所述，三种常用操作——复制、移动和归档需要特别注意。默认情况下，文件会继承父目录的属性。

- 如果文件被复制到不同的目录，SELinux 会为目标文件设置上下文。
- 如果文件被移动到相同或不同的目录，SELinux 上文保持不变。
- 如果文件使用 `tar` 归档，SELinux 会为源文件设置上下文。

## 端口的 SELinux 上文

SELinux 上文定义了网络端口的安全属性，可以使用 `semanage` 命令查看。以下展示了输出中的几条记录：

| SELux Type | Proto | Port Number |
| :--- | :--- | :--- |
| chronyd_port_t | udp | 123 |
| dns_port_t | tcp | 53 |
| ftp_port_t | tcp | 21 |
| http_port_t | tcp | 80 |
| https_port_t | tcp | 443 |
| ntp_port_t | udp | 123
| syslog_port_t | udp | 514 |

输出显示在三列。第 1 列显示 SELinux 类型，第 2 列描述协议，第 3 列指示端口号。

## 域转换 (Domain Transitioning)

只要策略中存在规则，SELinux 允许运行在一个域中的进程进入另一个域。为了理解这是如何工作的，下面提供了一个基本示例，显示了用户尝试更改密码时发生的情况。

`passwd` 命令被标记为 `passwd_exec_t` 类型，可以通过如下确认：

```
[user8@server10 ~]$ ls -lz /usr/bin/passwd
-rwxr-xr-x. 1 root root system:u_object_passwd_exec_t:s0 34512 Aug 12 /usr/bin/pass
```

`passwd` 命令需要访问 `/etc/shadow` 文件以修改用户密码。影子文件的类型不同 (`shadow_t`)：

```
[user8@server10 ~]$ ls -lz /etc/shadow
-------- 1 root root system:u_object_shadow_t:s0 1613 Nov 11 07:25 /etc/shadow
```

SELinux 策略专门允许运行 `passwd_t` 中的进程读取并修改类型为 `shadow_t` 的文件，并允许它们进入 `passwd_exec_t` 的入口权限。该规则允许执行 `passwd` 命令的用户 shell 进程切换到 `passwd_t` 域并更新 `shadow` 文件。

打开两个终端窗口。在窗口 1 中，发出 `passwd` 命令并在提示符处等待：

```
[user8@server10 ~]$ passwd
Changing password for user user1.
Current password: _
```

在窗口 2 中，运行 `ps` 命令：

```
[user8@server10 ~]$ ps -eZ | grep passwd
unconfined u:unconfined_r:passwd_t:s0-s0:c0.c1023 14188 pts/1 00:00:00 passwd
```

可以看到，`passwd` 命令（进程）转换到了 `passwd_t` 域以更改用户密码。

在此领域中运行的进程允许修改 `/etc/shadow` 文件的内容。

# SELinux 布尔值 (Booleans)

布尔值是 SELinux 用于确定是否允许执行操作的开关。布尔值可以直接激活或禁用 SELinux 策略中的某些规则，而无需重新编译或重新加载策略。例如，开启 `ftpd_anon_write` 布尔值允许匿名用户上传文件。通过关闭此布尔值可以撤销该权限。布尔值存储在 `/sys/fs/selinux/booleans` 目录下的虚拟文件中。文件名与布尔值名称匹配。以下是该列表示例：

```
user1@server10 ~$ ls -l /sys/fs/selinux/booleans
total 0
-rw-r--r-- 1 root root Nov 30 20:20 abrt_anon_write
-rw-r--r-- 1 root root Nov 30 20:20 abrt_handle_event
-rw-r--r-- 1 root root Nov 30 20:20 abrt_upload_watch_anon_write
-rw-r--r-- 1 root root Nov 30 20:20 antivirus_can_scan_system
-rw-r--r-- 1 root root Nov 30 20:20 antivirus_use_jit
-rw-r--r-- 1 root root Nov 30 20:20 auditadm_exec_content
-rw-r--r-- 1 root root Nov 30 20:20 authlogin_nswitch_use_ldap
```

在典型的服务器上，你会在输出中看到数百个布尔文件。

布尔值的帮助页可以通过 `selinux-policy-doc` 软件包获取。安装后，使用 `man` 命令配合 `-K` 选项可以为特定布尔值绑定页面。例如，执行 `man -K abrt_anon_write` 来查看 `abrt_anon_write` 布尔值的帮助页。

布尔值可以被查看，也可以临时切换以永久生效。新值会立即生效。临时更改存储在 `/sys/fs/selinux/booleans` 目录下对应布尔文件中的“1”或“0”，而永久更改则保存在策略数据库中。

下一节的练习之一演示了如何显示和更改布尔值。

## SELinux 管理

管理 SELinux 涉及大量任务，包括控制激活模式、检查运行状态、在主体和对象上设置安全上下文以及切换布尔值。RHEL 提供了一系列命令来执行这些操作。通过多个软件包，例如 `libselinux-utils` 提供了 `getenforce`、`getsebool` 和 `getcon` 命令；`policycoreutils` 包含了 `sestatus`、`setsebool` 和 `restorecon` 命令；`policycoreutils-python-utils` 提供了 `semanage` 命令；`setools-console` 包含了 `seinfo` 和 `sesearch` 命令。

为了查看警告和调试 SELinux 问题，可以使用名为 SELinux Alert Browser 的图形工具，它是 `troubleshoot-server` 软件包的一部分。为了完全管理 SELinux，你需要确保系统安装了所有这些软件包。除了这个工具集外，还有其他实用程序可以完成特定的 SELinux 管理任务，但它们的使用频率并不高。

# 管理命令

SELinux 提供了多种命令以进行有效管理。表 21-1 列出并描述了上述命令以及各种管理类别下的其他命令。

| 命令 | 描述 |
| --- | --- |
| getenforce | 显示当前的运行模式 |
| sestatus | 显示 SELinux 运行状态和布尔值 |
