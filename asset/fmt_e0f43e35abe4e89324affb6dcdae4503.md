
```
# semodule -l
abrt 1.2.0
accountsd 1.0.0
acct 1.5.0
...
xserver 3.5.6
zabbix 1.3.1
zarafa 1.0.0
zebra 1.12.0
zoosremote 1.1.0
```

# 第 24 章：使用 SELinux 增强 Linux 安全

一些工具可以帮助你管理甚至创建自己的策略模块。表 24.3 显示了 Fedora 系统上提供的各种策略规则包工具。

## 表 24.3 SELinux 策略包工具

| 策略工具 | 描述 |
| --- | --- |
| `audit2allow` | 从拒绝操作的日志生成允许/不审计规则 |
| `audit2why` | 从拒绝操作的日志生成关于为什么访问被拒绝的描述 |
| `checkmodule` | 编译策略模块 |
| `checkpolicy` | 编译 SELinux 策略 |
| `load_policy` | 将新策略加载到内核 |
| `semodule` | 管理策略模块 |
| `semodule_deps` | 列出策略包之间的依赖关系 |
| `semodule_expand` | 扩展策略模块包 |
| `semodule_link` | 将策略模块包链接在一起 |
| `semodule_package` | 创建策略模块包 |

以下是一个通常作为创建本地策略规则框架的策略示例。该示例相当长，所以只显示了部分。

```
# cat /usr/share/selinux/dev/example.te

policy_module(myapp, 1.0.0)
#################################################
# 声明
#

type myapp_t;
type myapp_exec_t;
domain_type(myapp_t)
domain_entry_file(myapp_t, myapp_exec_t)

type myapp_log_t;
logging_log_file(myapp_log_t)
...
type myapp_tmp_t;
files_tmp_file(myapp_tmp_t)
...
allow myapp_t myapp_tmp_t:file manage_file_perms;
files_tmp_filetrans(myapp_t, myapp_tmp_t,file)
#
```

# 第五部分：学习 Linux 安全技术

从前面的代码示例中你可以看到，策略代码中使用了一种特殊的语法。要创建和修改策略规则，你需要学习这种策略规则语言语法；学习如何将 SELinux 策略规则链接起来形成模块，并且可能需要参加几天的课程。你现在可能想放弃 SELinux。然而，使用布尔值（Booleans）修改策略要简单得多。

## 使用布尔值管理 SELinux

SELinux 策略规则编写和模块创建是一个更复杂且耗时的活动。创建错误的策略规则可能会危及你 Linux 系统的安全性。坦率地说，SELinux 提供了布尔值。

布尔值是一个开启或关闭设置的开关。布尔开关允许你在不了解策略编写的情况下更改 SELinux 策略规则的一部分。这些策略更改可以在不重启系统的情况下完成！

要查看 SELinux 中使用的所有布尔值，请使用 `getbool` 命令。以下是 Fedora Linux 系统上带有布尔值的 SELinux 策略规则示例：

```
# getbool -a
abrt_anon_write -- off
abrt_handle_event -- off
```

```
xserver_object_manager -- off
zabbix_can_network -- off
```

要查看可以通过布尔值修改的策略，再次使用 `getbool` 命令。在以下示例中，传递了策略名称：

```
# getbool httpd_can_ftp
httpd_can_ftp -- off
```

要切换策略，可以使用 `setbool` 命令或 `toggleboolean`。这两个命令都会定期更改策略状态。当系统重启时，布尔值将恢复原始设置。要永久生效，你需要使用 `setbool` 并配合 `-P` 参数。

`toggle` 命令会将你指定的布尔值开启或关闭。`setbool` 命令有六种设置：三个开启策略（on, 1, true），三个关闭策略（off, 0, false）。

对于 `setbool` 的示例，请记住 22 允许用户从主目录执行程序是不安全的。通常执行在该位置的程序是恶意软件。为了防止这种情况发生，需要关闭 `allow_user_exec_content` 策略。下面的示例显示了使用 `setbool` 命令。注意使用了 `-P` 参数来永久生效。

```
# setbool -P allow_user_exec_content
```

`getbool` 命令将验证布尔值设置是否正确：

```
# getbool allow_user_exec_content
allow_user_exec_content --> off
```

# 第五部分：学习安全技术

## 在审计日志中查看 SELinux auditd

如果你正在运行审计守护进程（audit daemon），可以使用 `aureport` 命令快速查看是否记录了任何 AVC 拒绝。下面的示例显示了如何使用 `aureport` 和 `grep` 搜索 AVC 拒绝记录。`/var/log/audit/audit.log` 中至少记录了一个拒绝记录。

```
# aureport | grep AVC
Number of AVC's: 1
```

一旦你发现 `audit.log` 中记录了 AVC 拒绝，就可以使用 `ausearch` 来审查拒绝信息。下面的示例显示了使用 `ausearch` 命令来查看已记录的 AVC 拒绝。

```
# ausearch -m avc
---
time=Sat Feb 25 09:18:07 2015:
type=SYSCALL syscall=226 msg=audit(133179487.213:250):
arch=40000003 success=no exit=-22
a0=8c8d88 a1=4c6db88 a2=c6ec90 a3=1f items=0
pid=2586 pid=30553 uid=1000 gid=0 euid=0
sid=0 suid=0(fuid=0 sgid=0 tty=pts0
sess=2 comm="chcon" exe="/usr/bin/chcon"
subj=unconfined:unconfined_r:unconfined_t:s0-s0:c0.c1023
key=(null)
type=AVC msg=audit(1330179487.213:250): avc denied
[ mac_admin ] for pid=30553 comm="chcon" capability=33
context=unconfined:unconfined_r:unconfined_t:s0-s0:c0.c1023
target=unconfined:unconfined_r:unconfined_t:s0-s0:c0.c1023
class=capability\002	class=capability2
```

显示内容将提供尝试访问的对象的信息，以及它们尝试访问时的安全上下文。在 AVC 拒绝消息中需要查找的关键词有：

- `avc=AVC`
- `avc: denied`
- `pid=`
- `exe=`
- `subj=`

这可以为你提供修复问题或追踪恶意活动的数据。

## 在 messages 日志中查看 SELinux 消息

如果你正在运行 `rsyslog`，可以通过 `grep` 搜索 `/var/log/messages` 文件来查找 AVC 拒绝。下面的示例显示了搜索 SELinux 拒绝信息。

```
# grep "SELinux is preventing" /var/log/messages
Feb 25 09:18:08 localhost retrousethooks: SELinux is preventing
/usr/bin/chcon from mac_admin access on the None . For complete
SELinux messages.
run sealert -1 b1d86ca2-6e83-4c29-b0db8-a5470a34f3f5
```
