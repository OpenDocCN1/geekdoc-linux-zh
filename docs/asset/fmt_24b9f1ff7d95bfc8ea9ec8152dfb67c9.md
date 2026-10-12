
```
[root@centos65 ~]# cat /etc/selinux/config
# This file controls the state of SELinux on the system.
# SELINUX=can take one of these three values:
# enforcing - SELinux security policy is enforced.
# permissive - SELinux prints warnings instead of enforcing.
# disabled - SELinux is fully disabled.
SELINUX=permissive
# SELINUXTYPE= of policy in use. Possible values are:
# targeted - Only targeted network daemons are protected.
# strict - Full SELinux protection.
SELINUXTYPE=targeted
```

## 19.9. DAC 或 MAC

标准的 Unix 权限使用自主访问控制（DAC）来设置文件权限。这意味着拥有一个文件的用户可以通过输入 `chmod 777 $file` 使其变为对所有用户可读。

使用 `selinux` 后，内核将执行强制性访问控制（MAC），它严格控制进程或线程可以执行的操作（取代了 DAC）。进程被内核限制在它们所需的最小访问范围内。

SELinux MAC 关乎标签标记和类型强制执行！文件、进程等都被标记了 SELinux 上下文（context）。对于文件，这些是扩展属性；对于进程，则由内核管理。

标签的格式如下：

```
user:role:type:(level)
```

在目标策略中，我们只使用类型（type）标签。

## 19.10. ls -Z

要查看文件的 DAC 权限，使用 `ls -l` 显示用户、组所有者和权限。

对于 MAC 权限，`ls` 新增加了 `-Z` 选项。输出显示 `/root` 下的文件具有 `admin_home_t` 的 XXTypepol。

```
[root@centos65 #] ls -Z
-rw-r--r root root system_u:object:radmin_home_t:s0 anaconda-ks.cfg
-rw-r--r root root system_u:object:radmin_home_t:s0 install.log
-rw-r--r-- root root system_u:object:radmin_home_t:s0 install.log.syslog

[root@centos65 #] useradd -m -s /bin/bash pol
[root@centos65 #] ls -Z /home/pol/.bashrc
-rw-r--r pol unconfined:object:user_home_t:s0 /home/pol/.bashrc
```

## 19.11. -Z

还有其他一些工具带有 `-Z` 选项：

```
mkdir -Z
cp -Z
ps -Z
netstat -Z
```

## 19.12. /selinux

当 `selinux` 激活时，会有一个名为 `selinux` 的新文件（你可以将其与 `/proc` 和 `/dev` 进行比较）。

```
[root@centos65 ~]# ls -l /selinux
-rw-rw----- root root 0 Apr 12 19:40 access
dr-xr-xr-x. root root 0 Apr 12 19:40 avc
dr-xr-xr-x. root root 0 Apr 12 19:40 Booleans
-rw-rw--r-- root root 0 Apr 12 19:40 checkport
dr-xr-xr-x. root root 0 Apr 12 19:40 class
-rw-rw--r-- root root 0 Apr 12 19:40 commit_pending
-rw-rw--r-- root root 0 Apr 12 19:40 context
-r--r--r-- root root 0 Apr 12 19:40 create
t--r--r-- root root 0 Apr 12 19:40 deny_unknown
dr-xr-xr-x. root root 0 Apr 12 19:40 class
...（此处省略部分重复输出，以保持格式一致）
```

## 19.16. 安全上下文 (security context)

身份、角色和领域或类型的组合形成了 `selinux` 安全上下文。

`id` 将以 `identity:role:domain` 的形式向你显示安全上下文。

```
paul@RHEL5 ~# id | cut -d' ' -f4
context=user_u:system_r:unconfined_t
```

`ls -z` 命令以 `identity:type` 的形式显示文件的安全上下文。

```
paul@RHEL5 ~# ls -z test
-rw-rw-r-- paul paul user_u:object_r:user_home_t test
```

`/proc` 中进程的安全上下文同时定义了类型（`/proc` 中对应文件的类型）和领域（运行中进程的领域）。让我们来看 `init` 进程和 `/proc/1`。

`init` 进程在 `init_t` 领域中运行。

```
root@RHEL5 ~# ps -ZC init
LABEL                 PID TTY TIME CMD
system_u:system_r:init_t  1    00:00:01 init
```

`/proc/1/` 目录标识了 `init` 进程的领域，其类型为 `init_t`。

```
paul@RHEL5 ~# ls -ld /proc/1/
-dr-xr-xr-x root root system_u:system_r:init_t      /proc/1/
```

`init` 进程的领域和 `/proc/1/` 的类型都是 `init_t` 并不是巧合。

不要尝试在 `/proc/1` 上使用 `chcon`。它不起作用。

## 19.17. 转换 (transition)

`selinux` 转换（也称为 `selinux` 标记）决定了将分配的安全上下文。执行一个进程时，会发生进程领域的转换。当你创建一个文件时，会发生文件类型的转换。

文件类型转换的示例。

```
pol@centos65 ~# touch test /tmp/test
pol@centos65 ~# ls -z test
-rw-rw-r-- pol pol unconfined_u:object_r:user_home_t:s0 test
pol@centos65 ~# ls -Z /tmp/test
-rw-rw-r-- pol pol unconfined_u:object_r:user_tmp:s0 /tmp/test
```

## 19.18. 扩展属性 (extended attributes)

扩展属性由 `selinux` 创建，用于存储安全上下文。当 `selinux` 运行时，可以使用 `ls` 查看这些属性。

```
[root@RHEL5]# ls --context
drwx-------
p paul user:object_r:user_home_dir_t paul
drwxr-xr-x root root user:object_r:user_home_dir_t project42
drwxr-xr-x root root user:object_r:user_home_dir_t project55
[root@RHEL5]# ls -d
drwx------paul user:object_r:user_home_dir_t paul
drwxr-xr-x root root user:object_r:user_home_dir_t project42
drwxr-xr-x root root user:object_r:user_home_dir_t project55
[root@RHEL5]#
```

当 `selinux` 未运行时，则应使用 `getattr` 工具。

```
[root@RHEL5 etc]# getattr -m -d hosts
# file: hosts
security.selinux="system_u:object_r:etc:s0\000"
```

## 19.19. 进程安全上下文

一种方法是使用 `ps` 查看进程的 `selinux` 安全上下文。
