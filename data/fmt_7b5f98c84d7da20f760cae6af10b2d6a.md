
PROFDIR 指定由分析程序创建的文件目录。如果未设置 `PROFDIR`，则在当前目录产生 `mon.out`。如果设置 `PROFDIR=string`，则产生 `string/progname.pid`，其中 `progname` 包含去除了任何前缀的 `argv[0]`，`pid` 是程序的进程 ID。如果 `PROFDIR` 设置为 `null`，则不产生性能输出。

## 文件

`mon.out` 默认性能文件。

`a.out` 默认列表文件。

### 属性

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 | SUNwb |

### 相关

`gprof(1)`, `cc(1)`, `exit(2)`, `profil(2)`, `psample(2)`, `malloc(3)`, `MALLOC(3M)`, `monitor(3C)`, `attributes(5)`, `prof(5)`

## 1125 profiles — 打印用户的执行性能

### 概要

```
/bin/profiles [-l] [user...]
```

### 描述

使用 `profiles` 命令（于 Solaris 8 中引入）在标准输出上打印指定用户或角色执行特定功能所需的命令和权限。权限是基于角色的访问控制 (RBAC) 封装机制，列出每个可执行文件的属性，以及有效用户和组 ID。性能 shell 是 `pfsh`、`pfksh` 和 `pfexec`。

你可以组合多个 profiles 来构建相应的访问控制。当分配 profiles 时，权限会被添加到现有集合中。如果同一命令在多个 profiles 中出现，则根据 profiles 的顺序使用第一个出现项。为了方便起见，你可以指定通配符来匹配所有命令。

从 Solaris 9 发布开始，如果在 `/etc/security/policy.conf`（参见 `policy.conf(4)`）中定义了任何默认策略，则默认策略将被添加到从 `user_attr(4)` 加载的列表中。`prof_attr(4)` 中的匹配项提供了命令列表。

### 选项

- `-l` 列出每个 profile 中的命令，随后是用户和组 ID 等特殊进程属性。

### 示例

以下示例显示了 `profiles` 命令的输出。在没有选项的情况下，`profiles` 显示当前用户的性能。

```
profiles
Primary Administrator
Basic Solaris User
All
```

以下示例显示了三个用户的 `profiles` 命令输出。`winsor` 拥有 Primary Administrator 权限，`ray` 拥有 System Administrator 权限，`des` 拥有默认的 Basic Solaris User 和 All 权限。确定一组权限是否停止另一组的方法是使用 All 权限，它始终是列表中的最后一个。

```
profiles winsor ray des
Primary Administrator
Basic Solaris User
```

## 1126 profiles

- All
System Administrator
Audit Review
Printer Management
Cron Management
Device Management
File System Management
Mail Management
Maintenance and Repair
Media Backup
Media Restore
Name Service Management
Network Management
Object Access Management
Process Management
Software Installation
User Management
All
Basic Solaris User
Basic Solaris User
All
m%

以下示例使用列表选项显示具有 Primary Administrator 权限的用户的命令和属性。

```
profiles -l winsor
```

```
Primary Administrator:
* uid=0, gid=0
All:
*
```

```
%
```

以下示例使用列表选项显示具有 System Administrator 权限的用户的命令和属性。

```
profiles -l ray
```

```
Audit Review:
/usr/sbin/praudit euid=0
/usr/sbin/auditreduce euid=0
/usr/sbin/auditstat euid=0
Printer Management:
/usr/sbin/accept euid=1lp
/usr/ucb/lpq euid=0
/etc/init.d/lp euid=0
/usr/bin/lpstat euid=0
/usr/lib/lp/lpsched uid=0
/usr/sbin/lpfilter euid=1lp
/usr/bin/lpset egid=14
/usr/sbin/lpadmin egid=14
/usr/sbin/lpsystem uid=0
/usr/sbin/lpmove euid=1lp
*
```

# 配置文件

## 1127

```
/usr/sbin/lpsut uid=lp
/usr/bin/cancel uid=0
/usr/bin/disable uid=lp
/usr/sbin/reject uid=lp
/usr/sbin/lpforms uid=lp
/usr/ucb/lprm uid=0
/usr/bin/enable uid=lp
/usr/sbin/lusers uid=lp
Cron 管理:
/etc/init.d/cron uid=0, gid=sys
/usr/bin/crontab uid=0
设备管理:
/usr/sbin/allocate uid=0
/usr/sbin/deallocate uid=0
文件系统管理:
/usr/sbin/mount uid=0
/usr/sbin/dfshares uid=0
/usr/sbin/format uid=0
/usr/sbin/devinfo uid=0
/usr/sbin/mkfs uid=0
/etc/init.d/standardmounts uid=0, gid=sys
/usr/sbin/shareall uid=0, gid=root
/usr/sbin/clir uid=0
/usr/bin/rmdir uid=0
/usr/lib/autofs/automountd uid=0
/usr/sbin/unshare uid=0, gid=root
/etc/init.d/buildmtab uid=0, gid=sys
/usr/lib/fs/autofs/automount uid=0
/usr/sbin/share uid=0, gid=root
/usr/bin/mkdir uid=0
/usr/lib/fs/ufs/tunef uid=0
/usr/sbin/fstype uid=0
/usr/sbin/ff uid=0
/usr/sbin/fuser uid=0
/usr/sbin/fsck uid=0
/usr/bin/eject uid=0
/usr/sbin/umountall uid=0
/usr/sbin/mountall uid=0
/usr/sbin/unshare uid=0, gid=root
/etc/init.d/ufs_quota uid=0, gid=sys
/usr/sbin/fsdb uid=0
/usr/lib/fs/ufs/newfs uid=0
/usr/lib/fs/ufs/fsirand uid=0
/usr/sbin/swap uid=0
/usr/sbin/umount uid=0
/etc/init.d/autofs uid=0, gid=sys
/usr/lib/bin/nfs/showmount uid=0
/usr/sbin/mkfile uid=0
/usr/sbin/dfmounts uid=0
邮件管理:
/usr/bin/mconnect uid=0
/usr/bin/sendmail uid=0
/usr/bin/mailq uid=0
/usr/bin/newaliases uid=0
```
