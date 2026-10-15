
```
rootubuntu:~# tripwire --init >/dev/null
Please enter your local passphrase:
Parsing file: /etc/tripwire/tw.pol
Generating the database...
*** Processing Unix File ***
The object: "/dev/hugepages" is on a different file system...ignoring.
The object: "/dev/nque" is on a different file system...ignoring.
The object: "/dev/shm" is on a different file system...ignoring.
The object: "/proc/sys/fs/binfmt misc is on a different file system...ignoring.
Wrote database file: /var/lib/tripwire/ubuntu.example.com.twd
The database was successfully generated.
```

> 图 8.19: 文件系统修改的输出示例

`--check` 选项将验证数据库的创建。例如，如果在 `/usr/bin/` 中创建了一个文件，"Unix File System: will show this information" 部分将显示此信息：

```
=================================================================
=
Object Summary:
```

```
============================================================
=
------------------------------------------------------------
# Section: Unix File System
------------------------------------------------------------
-
--------------------------------------------
Rule Name: Other binaries (/usr/bin)
Severity Level: 66
------------------------------------------------------------
```

Added:

`"/usr/bin/malware"`

Modified:

`"/usr/bin"`

`fail2ban` 服务读取日志以检测可能的暴力破解攻击。保存配置的主目录是 `/etc/fail2ban`。例如，SSH 连接将读取日志 `/var/log/auth.log` 以检测可能的密码暴力破解攻击。使用带有 `status` 参数的 `fail2ban-client` 命令和服务将提供有关被禁 IP 的信息，如图 8.20 所示：

```
root@ubuntu:~# fail2ban-client status sshd
Status for the jail: sshd
```

- Filter

  - Currently failed: 1

  - Total failed: 5

  - File list: `/var/log/auth.log`

- Actions

  - Currently banned: 1

  - Total banned: 1

  - Banned IP list: `192.168.122.145`

图 8.20: 命令 `fail2ban-client` 的输出示例

被拒绝的 IP 将被系统的防火墙后端。图 8.21 显示了它是如何被添加到 `nft` 表的：

```
root@ubuntu:~# nft list chain filter f2b-sshd\ip filter {
    chain f2b-sshd {
        ip saddr 192.168.122.145 counter packets 29 bytes 1200 reject
        counter packets 713 bytes 49060 return
    }
}
```

图 8.21: 命令 `nft` 的输出示例

`Snort` 是一个强大的网络入侵检测与防御系统套件，使用不同的规则检测未经授权的访问。可用规则可以在官方网站 [https://www.snort.org/](https://www.snort.org/) 获取。运行带有 `-c` 选项指定配置的 `snort` 命令将处理入站和出站连接并显示可能的攻击。以下块显示了输出示例：

```
Commencing packet processing (pid=5993)
08/28-21:11:04.609587**] [1:421:11] SNMP Agent/tcp request [**]
[Classification: Attempted Information Leak [Priority: 2] {TCP}
192.168.122.145:43439 -> 192.168.122.101:705
08/28-21:11:04.71243**] [1:421:11] SNMP Agent/tcp request [**]
[Classification: Attempted Information Leak [Priority: 2] {TCP}
192.168.122.145:4340 -> 192.168.122.101:705
08/28-21:11:06.307016**] [1:418:11] SNMP request [**]
[Classification: Attempted Information Leak [Priority: 2] {TCP}
192.168.122.145:43439 -> 192.168.122.101:161
08/28-21:11:06.407381**] [1:418:11] SNMP request [**]
[Classification: Attempted Information Leak [Priority: 2] {TCP}
192.168.122.145:4340 -> 192.168.122.101:161
```

## 安全模型

安全模型提供了一种支持访问策略的机制。红帽企业 Linux 及其衍生版本使用 `SELinux`，Deb 及其衍生版本使用 `AppArmor`。两种解决方案都集成到 Linux 内核中以增加系统的安全性。

`SELinux`（增强型）为应用程序、进程和文件定义访问控制。通过安全策略，规则定义了哪些可以访问哪些不能访问。例如，`SELinux` 规则可以定义哪些目录可以被应用程序使用，哪些端口可以用于监听连接。

`SELinux` 有三种状态，如下：

- `enforcing`: 保护并确保遵守规则。
- `permissive`: 会显示警告但允许操作执行。
- `disabled`: 在系统中不使用策略。

定义状态的主配置是 `/etc/selinux/config`。命令 `getenforce` 显示当前状态，命令 `setenforce` 提供更多信息。图 8.22 显示了命令的输出：

```
[root@rel]# getenforce
Permissive
[root@rel]# setenforce Enforcing
[root@rel]# sestatus
SELinux status:               enabled
SELinux mounts:               /sys/fs/selinux /etc/selinux
Loaded policy name:            targeted
Current mode:                  enforcing
Mode from config file:        enforcing
Policy MLS status:            enabled
Policy deny checking:        allowed
Memory protection checking: actual (secure)
Max kernel policy version: 3
```

> 图 8.22: 命令 `getenforce` 的输出示例

`SELinux` 与上下文（也称为标签）工作，上下文包含多个字段：用户、角色、类型和安全级别。在接下来的图 8.23 中，具有 `httpd_t` 上文的 `Apache` 服务可以访问 `/var/www/` 目录。

![](img/bcd1b6709d1a6bc46b9b8587284794e258_0.png)

### 图 8.23 `SELinux` 上文权限
