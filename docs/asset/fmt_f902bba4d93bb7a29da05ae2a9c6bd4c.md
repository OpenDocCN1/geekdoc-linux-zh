
接下来，你可以通过在 `/etc/selinux/config` 文件中配置以下 SELINUX 类型之一来选择 SELinux 策略：

- `SELINUXYPE` = `targeted`（目标策略，保护所有网络守护进程）
- `SELINUXYPE` = `minimum`（仅保护关键网络守护进程）
- `SELINUXYPE` = `mls`（使用 MLS 属性代替分类）

大多数 Linux 系统都使用 SELinux，它对 `targeted` 策略有定义，保护系统免受可能损坏文件或破坏安全的恶意应用程序的影响。在修改 `/etc/selinux/config` 文件启用 SELinux 后，你必须重启以对系统上的现有文件进行重新标记。之后，你可以使用 `sestatus` 命令查看当前的 SELinux 状态：

```
[root@server1 ~]# sestatus -v
SELinux status: enabled
SELinux mount: /sys/fs/selinux
SELinux root directory: /etc/selinux
Loaded policy name: targeted
Current mode: enforcing
Mode from config file: enforcing
Policy MLS status: enabled
Policy deny_unknown status: allowed
Memory protection checking: actual (secure)
Max kernel policy version: 31
```

## 778 第 14 章 安全、故障排除与性能

进程上下文：

当前上下文：

`unconfined_u:unconfined_r:unconfined_t:s0-s0:c1023`

`system_u:system_r:init_t:s0`

`system_u:system_r:sshd_t:s0-s0:c1023`

当前上下文：

`system_u:system_r:init_t:s0`

`system_u:system_r:sshd_t:s0-s0:c1023`

文件上下文：

`/etc/passwd`

`/etc/shadow`

`/bin/bash`

`/bin/sh`

`/bin/login`

`/dev/tty`

`/dev/pts/0`

`/dev/pts/1`

上下文：

`unconfined_u:unconfined_r:unconfined_t:s0-s0:c1023`

`system_u:system_r:init_t:s0`

`system_u:system_r:sshd_t:s0-s0:c1023`

文件上下文：

`/etc/passwd`

`/etc/shadow`

`/bin/bash`

`/bin/sh`

`/bin/login`

`/dev/tty`

`/dev/pts/0`

`/dev/pts/1`

当前上下文：

`unconfined_u:unconfined_r:unconfined_t:s0-s0:c1023`

`system_u:system_r:init_t:s0`

`system_u:system_r:sshd_t:s0-s0:c1023`

文件上下文：

`/etc/passwd`

`/etc/shadow`

`/bin/bash`

`/bin/sh`

`/bin/login`

`/dev/tty`

`/dev/pts/0`

`/dev/pts/1`

当前上下文：

`unconfined_u:unconfined_r:unconfined_t:s0-s0:c1023`

`system_u:system_r:init_t:s0`

`system_u:system_r:sshd_t:s0-s0:c1023`

文件上下文：

`/etc/passwd`

`/etc/shadow`

`/bin/bash`

`/bin/sh`

`/bin/login`

`/dev/tty`

`/dev/pts/0`

`/dev/pts/1`

当前上下文：

`unconfined_u:unconfined_r:unconfined_t:s0-s0:c1023`

`system_u:system_r:init_t:s0`

`system_u:system_r:sshd_t:s0-s0:c1023`

文件上下文：

`/etc/passwd`

`/etc/shadow`

`/bin/bash`

`/bin/sh`

`/bin/login`

`/dev/tty`

`/dev/pts/0`

`/dev/pts/1`

当前上下文：

`unconfined_u:unconfined_r:unconfined_t:s0-s0:c1023`

`system_u:system_r:init_t:s0`

`system_u:system_r:sshd_t:s0-s0:c1023`

文件上下文：

`/etc/passwd`

`/etc/shadow`

`/bin/bash`

`/bin/sh`

`/bin/login`

`/dev/tty`

`/dev/pts/0`

`/dev/pts/1`

注意：并不是你遇到的 SELinux 问题都与错误的标记有关。例如，默认 SELinux 策略不允许 Apache 读取用户主目录中的内容。结果，如果你启用了主目录，SELinux 将阻止该功能工作。要解决此问题，你可以通过修改 `/etc/selinux/targeted` 目录中的适当文件来更改策略设置。或者，你可以

## 803 第 14 章 安全、故障排除与性能

移动一个具有 SELinux 标签的文件到新目录，该文件将保留其原始标签，因为并没有创建新文件。这在以下输出中所示， `index.html` 被移动到了根目录：

```
[root@server1 ~]# ls -z index.html
unconfined_u:object_r:admin_home_t:s0 index.html
[root@server1 ~]# mv index.html /var/www/html
[root@server1 ~]# ls -z /var/www/html/index.html
unconfined_u:object_r:admin_home_t:s0 /var/www/html/index.html
[root@server1 ~]#
```

由于之前的输出中 `index` 在移动后保留了其原始分类，因此 SELinux 阻止 Apache 读取。因此，客户端尝试访问网页时将收到 403 Forbidden 错误。要解决此问题，你可以使用 `chcon` 命令将 `/var/www/html/index.html` 文件的分类手动更改为正确的分类（`httpd_sys_content_t`），如下文所示：

```
[rootserver1 ~]# chcon -t httpd_sys_content_t /var/www/html/index.html
[rootserver1 ~]# ls -z /var/www/html/index.html
unconfined_u:object_r:httpd_sys_content:t:s0 /var/www/html/index.html
[root@server1 ~]#
```

你也可以使用 `restorecon` 命令强制 SELinux 使用正确的分类重新重新标记文件。例如，在之前的输出中，可以使用 `restorecon /var/www/html/index.html` 命令代替 `chcon` 来为 `/var/www/html/index.html` 文件设置正确的分类。

> 注意 要下次启动时强制 SELinux 对系统上的所有文件进行重新标记，你可以使用 `touch /.autorelabel` 命令创建一个 `/.autorelabel` 文件。

## 第 14 章 安全、故障排除与性能

使用 `getsebool` 命令允许 Apache 读取用户主目录内网络内容的策略，并使用 `setsebool` 命令修改该设置。下方的输出演示了这一点：

```
[root@server1 ~]## getsebool -a | grep httpd
http_enable_homedirs -- off
[root@server1 ~]## getsebool -P httpd_enable_homedirs on
[root@server1 ~]## getsebool -a | grep httpd
http_enable_homedirs -- on
[root@server1 ~]##
```

在使用 SELinux 的系统中，审计守护进程（audit daemon）监听内核调用并将 SELinux 相关的事件记录到 `/var/log/audit/audit.log`。你可以查看此日志以识别与 SELinux 强制执行相关的问题。此外，你可以使用 `audit2 < /var/log/audit/audit.log` 命令在 `/var/audit/audit.log` 内部生成易于读的 SELinux 事件描述。这些描述对于确定 SELinux 限制的原因非常有帮助。

## 配置 AppArmor
