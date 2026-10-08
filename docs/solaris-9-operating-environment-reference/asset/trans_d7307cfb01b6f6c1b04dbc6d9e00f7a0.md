

## crle 189

以下示例为 ELF 可执行文件创建一个备用对象缓存。

```
example$ crle -c /local/$HOST/.xterm/ld.config -f RTLD_REL_REL
-o /usr/openwin/bin/xterm
example$ in -s /usr/local/$.xterm/xterm /local/$HOST/xterm
example$ ldd /usr/local/$HOST/xterm
libXaw.so.5 => /local/$HOST/.xterm/libXaw.so.5 (alternate)
libXmu.so.4 => /local/$HOST/.xterm/libXmu.so.4 (alternate)
ibc.so.1 => /local/$HOST/.xterm/libc.so.1 (alternate)
```

通过此配置，将创建一个新的 xterm 及其依赖项。这些新对象已完全重定位到自身，其启动速度比原始对象更快。

> 注意 — 该应用程序的执行使用了它自己的配置文件。使用这种模型通常比使用环境变量 LD_CONFIG 更灵活，因为配置文件不会被 ldd(1) 或 truss(1) 等其他应用程序误用。

以下示例创建一个备用对象缓存以替换一个 ELF 对象。

```
example$ ldd /usr/sbin/bin/vold
libthread.so.1 => /usr/lib/libthread.so.1

example$ crle -a /usr/lib/libthread.so.1 -o /usr/lib/lwp
example$ crle
```

配置文件 [2]: /var/ld/ld.config
默认库路径 (ELF): /usr/lib（系统默认）
信任目录 (ELF): /usr/lib/secure（系统默认）

```
Directory: /usr/lib
libthread.so.1 (alternate: /usr/lib/lwp/libthread.so.1)
...
example$ ldd /usr/sbin/bin/vold
libthread.so.1 => /usr/lib/lwp/libthread.so.1 (alternate)
...
example$ .
```

通过此配置，任何通常会解析到 /usr/lib/libthread.so.1 的依赖项现在将解析到 /usr/lib/lwp/libthread.so.1。详见 threads(3)。

## 退出状态

创建或显示配置文件返回 0；否则，任何错误情况都将伴随诊断消息并返回非零值。

## 190

## crontab

### 文件

- /var/ld/ld.config
32 位应用程序的默认配置文件。

- /var/ld/64/ld.config
64 位应用程序的默认配置文件。

- /var/tmp
临时配置文件的默认位置（参见 tempnam(3)）。

- /usr/lib/ldstub
ldd(3) 用于 32 位对象的存根程序（Stub application）。

- /usr/lib/64/ldstub
ldd(3) 用于 64 位对象的存根程序（Stub application）。

- /usr/lib/libc.so.1
ldd(3) 用于 32 位对象的审计标准库。

- /usr/lib/64/libcle.so.1
ldd(3) 用于 64 位对象的审计标准库。

### 属性

参见 attributes(5) 获取以下属性的描述。

| 属性类型 | 属性值 |
|---|---|
| 可性 | SUNWfoo |

## 另请

ld(1), ld.so.1(1), ldd(3), tempnam(3), threads(3), attributes(5)。

## crontab — 用户时间表文件

### 概要

/usr/bin/crontab [filename]
/usr/bin/crontab [-elr] username

### 描述

使用 crontab 命令通过复制、创建、列出和删除 crontab 文件来管理用户对 cron 的访问。如果未带选项调用，crontab 将指定的文件（或在未指定文件时为标准输入）复制到存放所有用户 crontab 的目录中。

## crontab 访问控制

允许用户访问 cron：

- * 如果用户名出现在 /etc/cron.d/cron.allow 中。
- * 如果 /etc/cron.d/cron.allow 不存在且用户名不在 /etc/cron.d/cron.deny 中。

拒绝用户访问 crontab：

- * 如果 /etc/cron.d/cron.allow 存在且用户名不在其中。
- * 如果 /etc/cron.d/cron.allow 不存在且用户名在 /etc/cron.d/cron.deny 中。
- * 如果两个文件都不存在，从 Solaris 8 版本开始，只有具有 solaris.jobs 授权的用户允许提交作业。

请注意，只有当允许/拒绝文件存在时，这些这些规则才适用于 root。允许/拒绝文件每行一个用户名。

## crontab 格式

crontab 文件由每行六字段的行组成。字段之间用空格或制表符分隔。前五个字段是整数模式，指定以下内容：

- 分钟 (0-59)。
- 小时 (0-23)。
- 日 (1-31)。
- 月份 (1-12)。
- 星期 (0-6=星期日)。

这些模式中的每一个都可以是星号（表示所有合法值）或由逗号分隔的元素列表。

元素是一个数字或两个由连字符分隔的数字（表示闭区间范围）。注意，日期可以通过两个字段（日期和星期）来指定。如果作为元素列表指定，则两者都将被遵守。

crontab 行的第六个字段是一个字符串，将在指定时间由 shell 执行。该字段中的 % 字符（除非用 \ 转义）会被转换为换行符。

shell 仅执行命令字段的第一部分（直到百分比 % 处或行尾）。其他行作为标准输入提供给命令。任何以井号 (#) 开头的行都是注释并被忽略。文件不包含空行。

shell 从 HOME 目录通过 arg sh 参数被调用。想要加载 .profile 的用户必须在 crontab 文件中显式地这样做。cron 为每个 shell 提供默认环境，定义了 HOME、LOGNAME、SHELL(/bin/sh)、TZ 和 PATH。

## 192

## crontab

当 cron 被 crontab 通知要更新用户的 crontab 文件时会发生这种情况，它首先会重建 crontab 和事件。最后这一步需要时间，特别是当 crontab 文件很大时，可以在计划事件完成后完成。

### 选项

-e 编辑当前用户 crontab 文件的副本，如果 crontab 不存在则创建一个空文件。编辑完成后，将该文件安装用户的 crontab 文件。如果给了用户名，则编辑指定用户的 crontab 文件而不是当前用户的；此操作只能由超级用户执行。环境变量 EDITOR 决定了用 -e 选项调用哪个编辑器。默认编辑器是 ed(1)。注意，所有 crontab 作业应通过 crontab 提交，而不是通过直接编辑 crontab 文件添加作业，如果你删除了 crontab 文件中的所有行，旧的 crontab 文件将恢复。删除所有行的正确方法是使用 -r 选项移除 crontab 文件。

-1 列出调用用户的 crontab 文件。只有超级用户可以指定用户名来移除或列出指定用户的 crontab 文件。

-r 从 crontab 目录移除用户的 crontab。

### 示例

以下示例每天凌晨3:15 清理 core 文件。

```
15 3 * * 5 find $HOME -name core 2>/dev/null | xargs
rm -f
```

以下示例发送生日邮件。

```
0 12 14 2 * mailx Happy Birthday!%Time for lunch.
```

以下示例在每月的第一和十五以及每个星期一运行命令。

```
0 0 1, 15 *
```

要仅通过一个字段指定日期，将另一个字段设为 *。以下示例仅在每个星期一运行命令。

```
0 0 * * 1
```

