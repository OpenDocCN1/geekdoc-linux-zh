
```
cp booi.schot.zone /var/named/chroot/etc/
```

然后追加到 `named.conf` 中

```
cat named.conf >> /var/named/chroot/etc/named.conf
```

我按照以下步骤操作：`namedhowto4.txt`

```
vi /etc/init.d/named   [在 start() 之后之后添加了两个 export 行]
chmod a+r /usr/local/samba/private/dns.keytab
cp kb5 /usr/local/samba/private/dns.keytab
```
（等待，原文中有一个截断的 `kb5`，我将尽可能保持 OCR 上下文整洁）。

实际上，查看 OCR：`cp kb5 /usr/local/samba/private/dns.keytab` 可能是意图所在，但 OCR 显示为 `cp kb5 /usr/local/samba/private/dns.keytab`。我将坚持提供的文本但修复格式。

```
vi /etc/init.d/named   [在 start() 之后之后添加了两个 export 行]
chmod a+r /usr/local/samba/private/dns.keytab
cp kb5 /usr/local/samba/private/dns.keytab
```

（省略重复内容）

## 第 VII 部分 SELinux

### 19. SELinux 简介

Security 或 SELinux 是美国国家安全局 (NSA) 开发的一系列修改，旨在为 Linux 提供多种安全策略。SELinux 于 2000 年底作为开源发布。由于内核版本 2.6 是 Linux 的组成部分。

SELinux 提供安全性！SELinux 可以控制用户对文件和进程的访问类型。即使文件接收了 `chmod 777`，SELinux 仍然可以阻止应用程序访问它（Unix 文件权限首先被检查！）。SELinux 通过将用户置于代表安全上下文的角色中来实现这一点。管理员对授予角色的访问权限有非常严格的控制。

#### 19.1. selinux 模式

selinux 有三种模式：强制模式（`enforcing`）、允许模式（`permissive`）和禁用模式（`disabled`）。强制模式会执行策略，并可能根据 selinux 规则拒绝访问。允许模式不会执行策略，但可以记录在强制模式下会被拒绝的操作。禁用模式下表示完全禁用了 selinux。

#### 19.2. 日志 (logging)

验证 `syslog` 是否正在运行并在启动时已激活，以便在 `/var/log/messages` 中记录被拒绝的消息。

```
[root@rhel55 ~]# chkconfig --list syslog
syslog 0:off 1:off 2:on 3:on 4:on 5:off
```

验证 `auditd` 是否正在运行并在启动时已激活，以便在 `/var/log/audit/audit.log` 中记录更易读的日志。

```
[root@rhel55 ~]# chkconfig --list auditd
audit 0:off 1:off 2:on 3:on 4:on 5:off
```

如果未激活，运行 `chkconfig --levels 2345 auditd` 并启用 audit 图表。

```
[root@rhel55 ~]# service auditd status
audd (1660) is running...
[root@rhel55 ~]# service syslog status
syslog (2188) is running...
klog (1691) is running...
```

`/var/log/messages` 文件会告诉你 selinux 是否已禁用。

```
root@deb503:~# grep selinux /var/log/messages | grep -i Init
Jun 25 15:59:34 deb503 kernel: [ 0.084083] SELinux: Disabled at boot.
```

或者显示它已启用。

```
root@deb503:~# grep SELinux /var/log/messages | grep -i Init
Jun 25 15:09:52 deb503 kernel: [ 0.084094] SELinux: Initializing.
```

#### 19.3. 激活 selinux

在 RHEL 上，你可以使用 GUI 工具激活 selinux；在 Debian 上则有 `selinux-activate` 命令。激活需要重启系统。

```
root@deb503:~# selinux-activate
Activating SE Linux
Searching for GRUB installation directory ... found: /boot/grub
Searching for default file ... found: /boot/grub/default
Testing for an existing GRUB menu-list file ... /boot/grub/menu.list
Searching for splash image ... none found, skipping
Found kernel: /boot/vmlinuz-2.6.26-2-686
Updating /boot/grub/menu.list done
```

SE Linux 已激活。你现在可能需要重启。

#### 19.4. getenforce

使用 `getenforce` 验证 selinux 是处于强制模式、禁用模式还是允许模式。

```
[root@rhel55 ~]# getenforce
Permissive
```

`/selinux/enforce` 文件在强制模式激活时包含 1，在允许模式激活时包含 0。

```
root@fedoral3 -# cat /selinux/enforce
root@fedoral3 -#
```

#### 19.5. setenforce

一旦 selinux 激活，你可以使用 `setenforce` 在允许模式（`Permissive`）或强制模式（`Enforcing`）之间切换。

```
[root@rhel55 ~]# setenforce Enforcing
[root@rhel55 ~]# getenforce
Enforcing
[root@rhel55 ~]# setenforce Permissive
[root@rhel55 ~]# getenforce
Permissive
```

你也可以直接使用 0 和 1 作为参数。

```
[root@centos65 ~]# setenforce 1
[root@centos65 ~]# getenforce
Enforcing
[root@centos65 ~]# setenforce 0
[root@centos65 ~]# getenforce
Permissive
[root@centos65 ~]#
```

#### 19.6. sestatus

你可以使用 `sestatus` 命令查看当前的 selinux 状态和策略。

```
[root@hel55 ~]# sestatus
SELinux status:         enabled
SELinuxuxfs mount:       /selinux
Current mode:            permissive
Mode from config file:  permissive
Policy version:          21
Policy from config file:  targeted
```

#### 19.7. 策略 (policy)

大多数红 Hat 服务器将使用目标策略（`targeted policy`）。只有 NSA/FBI/CIA/DOD/HLS 使用多级安全策略（`mls policy`）。

目标策略会保护数百个进程，但允许其他进程以“无限制”（`unconfined`）模式运行（它们可以做任何事）。

#### 19.8. /etc/selinux/config

selinux 的主配置文件是 `/etc/selinux/config`。在允许模式下，该文件内容所示。

策略在 `/etc/selinux/config` 中被选中。
