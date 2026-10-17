
## sestatus

SELinux status: enabled

SELinux mount: SELinux

Current mode: enforcing --- 当前运行模式

Mode from config file: permissive --- 通过 `/etc/sysconfig/selinux` 设置的模式

要临时更改，设置 `setenforce 0` (permissive) 或 `setenforce 1` (enforcing) —— 或 `echo 1 > /selinux/enforce`

要设置持久模式，编辑 `/etc/selinux/config`（`/etc/sysconfig/SELinux` 的软链接）

```bash
>>> cat /etc/sysconfig/config
```

### SELinux 可以取以下三个值之一：

`enforcing` - 强制执行 SELinux 安全策略。

`permissive` - SELinux 打印警告而非执行。

`disabled` - 加载 SELinux 策略。

`SELinux=enforcing`

### SELinux=可以取以下值之一：

`targeted` - 保护目标进程。

`minimum` - 目标策略的修改。仅保护选定的进程。

`mls` - 多层级安全保护。

`SELINTYPE=targeted`

通常建议禁用 SELinux。某些安装可能会调用它，但通常 `permissive` 模式就足够了。
如果禁用，临时或为了对非关键项进行更改，通常建议在 `/etc/sysconfig/selinux` 中设置 `selinux` 后重启，以便它会影响检查/重新加载（系统从 `enforcing` 切换到 `disabled`）
在启动时，`service` 也会读取该开关，因此对 SELinux 关键的是 `grub` 中：
`kernel/vmlinux-2.6.32-279.x86_64 root=/dev/md3 selinux=1 enforcing=0`
`Linux=0` 表示禁用，`1` 表示启用，并配合 `enforcing` 设置，`permissive` 为 `0`，`1` 为 `enforcing`

SELinux 模式更改命令：`setforce`, `getforce`, `sestatus`

## 查看文件的 SELinux 上文：标签

有几个命令可以使用 `-Z` 显示 SELinux 上文；针对文件/目录（对象）：

`$ ls -Z`
`-rw-r-- user group1 unconfined u:object:user_home_t:s0`
`ls -Z /var/www/html/`
`-rw-r-- root root unconfined u:object:httpd_sys_content_t:s0`
`-ls -Z /var/www/`
`drwxr-xr-x root apache system_u u:object:httpd_sys_content_t:4096 Dec 23 20:47:`

这些示例显示了用户、组、DAC 和权限，但通过添加 `-Z`，我们可以看到 SELinux 上文：一个用户 (`unconfined,u`)，一个角色 (`object,r`)，一个类型 (`user_home_t`) 和一个级别 (`s0`)。

- 用户：非特权用户=`u` 特权用户=`r`
- 角色：非特权和用户= `system_u`
- 类型/域标签：12 默认值：`httpd`, `dbd`, `mysqld`, `nfs`, `portmap`, `postfix`, `smpd`, `squid`, `windbind`, `swigold`。
- 级别 (`s0`) 是 MCS/MLS 策略的一部分，我将它们保存在最后以便保留

- `id -Z`
- `ps -Z`
- `cp -Z`
- `mdir -Z`
- `netstat -ss -Z`
显示用户的上下文
显示运行进程（用户和主体/域/命名空间）的上下文
在复制文件时维护/保持上下文
显示新创建的域的上下文
显示网络信息的上下文。

## 使用 semanage 配置 SELinux

- 常用选项：`-a`, `-d`, `-delete`, `-m`, `-modify`, `-t`, `-import` 和 `-export <filename>` 用于导入或输出你的配置
Web 中的所有
网络类型文件定义 `semanage_a -t httpd_sys_content_t -w <file__t>="/*"`
网络接口类型 列出所有接口
网络端口定义 `semanage_a -t httpd_sys_content_t -w <file__t>="/*"`

# SELinux 布尔值 (Boolean)

布尔值允许在运行时对 SELinux 进行调整，而无需修改或重新加载策略，并能无缝激活特定的功能进程。

| 布尔值 - 包含描述、开启或关闭状态以及默认值的列表 | 状态 | 默认 | 描述 |
| :--- | :--- | :--- | :--- |
| SELINux boolean | (off, off) | 允许 ftp 在用户主目录读写文件 |
| ftp_home_dir | (off, off) | 允许 xdm 作为 systemd 登录 |
| xdm_system_login | (off, off) | 允许 wen 管理 nfs 文件 |
| ssh_root_rw_homedirs | (off, off) | 允许 root 通过 ssh 在用户主目录读写文件 |
| postgresql_can_rsync | (off, off) | 允许 postgres 使用 ssh 进行同步时间恢复 |
| authlogin_shadow | (off, off) | 允许用户登录程序访问 /etc/shadow |
| httpd_can_relay | (off, off) | 允许 httpd 作为中继站 |
| openvpn_enable_homedirs | (off, off) | 允许 openvpn 读取主目录 |

`getsebool - | grep http` 提供不同的值

`httpd_scripting_-> on`

`httpd_network_connect -> on`

使用 `setboolean` 更改值：`setboolean httpd_enable_cgi off` - 持久化 `-P` (开启和关闭可以为 `0` 或 `1`)

更改布尔值不是通过 `selinux` 完成的，因此请使用 `setboolean -P`

## 在运行期间禁用特定的（目标）策略

我们需要编辑 `/booleans` 目录下的项目并切换布尔值：
`echo "1" > /etc/selinux/booleans/disable_trans`
SELinux 需要重启系统以检查是否需要刷新策略
`echo "1" > /sbin/service/pending_boots`
重启受影响的服务：`service httpd restart`
Apache 现在在 `undefined_domain` 域运行

## MLS/MCS 级别详解

SELinux 的操作顺序如下：
1. DAC（自主访问控制，由主机操作系统允许 Linux 权限）
2. TE（类型强制，最基本的 SELinux 操作）进行检查
3. MLS（多级敏感性标签允许访问控制，例如：秘密、绝密）
4. MCS（基于类别的多分类访问控制）

### SELinux 用户 MLS/MCS 范围

`_default unconfined_u s0:s0:c0-23`

`root unconfined_u s0:s0:c0-23`

`system_u system_u s0:s0:c0-23`
