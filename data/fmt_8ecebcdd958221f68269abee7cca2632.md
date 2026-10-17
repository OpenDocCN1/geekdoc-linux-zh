
注意：并不是每个 Linux 发行版（例如 `Ubuntu`）都拥有 `authconfig` 工具，该工具会覆盖 PAM 配置文件。要检查你的发行版是否拥有 `authconfig` 工具，请在命令行中输入 `authconfig`。如果没有返回内容，说明你的 Linux 发行版没有该工具。

在某些发行版中，`pam-auth-config` 在覆盖配置文件的能力与 `authconfig` 工具类似。如果在命令行输入命令 `pam-auth-config --force`，就会发生这种情况。如果你的系统上安装了该工具，请阅读 `pam-auth-config` 手页以了解更多关于该工具的信息。

`authconfig` 工具不使用也不会修改符号链接。因此，你可以创建一个新的 PAM 系统事件配置文件，并将符号链接指向它。这将允许你的系统实现所需的安全修改，并让你避免配置文件被 `authconfig` 工具覆盖。基本步骤如下，包括执行这些步骤的示例（针对“local”文件）：

1. 将 PAM 系统事件配置文件复制为名为“local”的文件。
   ```bash
   # cp system-auth-ac system-local
   ```
2. 对文件进行必要的更改。
   ```bash
   # vi system-local
   ```
3. 删除旧的符号链接。
   ```bash
   # ls -l system-auth
   lrwxrxr-x. 1 root root 14 Feb 28 01:36
   system-auth -> system-auth-ac
   ```
4. 创建一个指向新配置文件的符号链接。
   ```bash
   # ln -s system-local system-auth
   # ls -l system-auth
   lrwxrxr-x. 1 root root 17 Feb 28 01:36
   system-auth -> system-local
   ```

# 第五部分：学习 Linux 安全技术

一旦完成了这些更改，你就可以对“local”PAM 系统事件配置文件进行任何修改，而无需担心被 `authconfig` 工具覆盖。

## 使用 PAM 实现资源限制

资源管理不仅是一项系统管理任务，也是一项安全任务。设置资源限制可以避免 Linux 系统出现问题。限制创建进程的数量可以防止炸弹（fork bombs）。炸弹是指进程递归地产生自身直到耗尽系统资源。

`pam-limits` 模块使用配置文件设置这些限制。配置文件通常是 `/etc/security/limits.conf`。该文件的项格式为：

`<domain> <type> <item> <value>`

其中：
- `domain` 限制所属的用户或组。如果域为 `*`，则适用于所有用户。
- `type` 硬限制（hard）不能被超过。软限制（soft）可以被超过，但只是暂时的。
- `item` 可以是以下之一：
  - `core` 限制核心转储大小 (KB)
  - `data-max` 限制数据大小 (KB)
  - `filesize` 限制文件大小 (KB)
  - `memlock` 限制锁定在内存中的地址空间 (KB)
  - `nofile` 限制打开的文件数
  - `rss` 限制驻存内存大小 (KB)
  - `stack` 限制堆栈大小 (KB)
  - `cpu` 限制 CPU 时间 (分钟)
  - `nproc` 限制进程数
  - `as` 限制地址空间 (KB)
  - `maxlogins` 限制该用户的登录次数
  - `maxsyslogs` 限制整个系统的登录次数
  - `priority` 运行优先级
  - `locks` 限制用户可以持有的锁
  - `sigpending` 限制挂起的信号数
  - `mssque` 限制 POSIX 消息队列使用的内存 (字节)
  - `nice` 允许提高优先级的范围 [-20, 19]
  - `rtprio` 限制实时优先级
- `value` 限制的值。

注意：软限制是默认值。硬限制只能由 root 用户设置。

以下是 `limits.conf` 文件的示例：

```bash
$ cat /etc/security/limits.conf

* soft core 0

* hard rss 10000

*student hard nproc 20

*faculty soft nproc 20

*faculty hard nproc 50

*ftp hard nproc

*student maxlogins 4
```

限制设置是按登录设置的，且仅在登录会话期间有效。恶意用户可能会登录多次以创建 fork 弹（fork bomb）。因此，为这些账户设置最大登录次数也是一个好主意。

限制最大登录次数可以按用户进行。例如，`johndoe` 只需要登录 Linux 系统一次。为了防止他人使用 `johndoe` 的账户，请将其账户的 `maxlogins` 设置为 1。

| johndoe | maxlogins |
| :--- | :--- |
| 1 | 1 |

限制此资源的最后一步是确保 PAM 模块配置包含在 PAM 系统事件配置文件之一中。在接下来的部分列列表中，使用 `grep` 来验证系统事件配置文件是否使用了该 PAM 模块。

```bash
# grep "pam_session" /etc/pam.d/*
system-auth:session required pam_limits.so
system-auth-ac:session required pam_limits.so
system-auth-local:session required pam_limits.so
```

访问服务和账户的时间限制并不由 PAM 的 `/etc/security/limits.conf` 配置文件处理。相反，它由 `time.conf` 处理。

## 在 PAM 上实现时间限制

PAM 可以让你的整个 Linux 系统按照“PAM 时间”运行。时间限制，例如在一天中的某些时间访问特定应用程序，或仅允许在指定的星期几登录，都由 PAM 处理。

处理这些限制的 PAM 配置文件位于 `/etc/security` 目录。以下代码显示了文档良好的 `/etc/security/time.conf` PAM 配置文件。

```bash
$ cat /etc/security/time.conf
# 这是一个用于 pam_time 模块的示例配置文件
# 行的语法如下：
#
# services;tty;users;times
#
# services
# 是一个适用于此规则的 PAM 服务名称列表。
#
# tty
# 是适用于此规则的终端名称逻辑列表。
#
# users
# 是适用于此规则的用户或用户网络组（netgroup）的逻辑列表。
# 注意。对于这些项目，简单的通配符 '*' 只能使用一次。
# times
# 这里的格式是日期/时间范围条目的逻辑列表
# 日期由一组两个字符的条目指定指定，例如 MotUSa 表示周一、周二和周六。
# 注意重复的日期将取消设置，MoMo = 无日期，MoWk = 所有工作日除去周一。
# 接受的两个字符组合是：
# n# Mo Tu Th Fr Sa Su Wd Al
# n# 最后两个分别表示开始-结束日期以及一周的 7 天。
# 最后一个例子是，AlFr 表示除周五以外的所有日期。
# 每个日期/时间范围都可以带有 '!' 前缀
# 表示“任何时间”
# 时间范围部分是 24 小时制的时间 HHMM，用连字符隔开
# 表示开始和结束时间（如果结束时间小于开始时间，
# 则认为应用于第二天）。
# 要使规则生效，执行进程时必须满足
# 所有的 service+ttys+users。
...
# 示例文件结束。
```

注意，每个有效条目的格式遵循以下语法：`services:ttys:users:times`。每个字段之间用分号分隔。有效的字段值记录在 `time.conf` 配置文件中。

虽然 `time.conf` 文档详尽，但示例总是有帮助的。例如，你决定允许普通用户在工作日的终端上登录（仅周一至周五）。他们可以在这些工作日的早上 7 点到下午 7 点登录。该列表描述了需要设置的元素：

- services — `Login`（登录）
- ttys - `*`（指定包含所有终端）
- users — 除了 (`root`) 的所有人
- times — 允许在工作日 (`W`) 从早上 7 点 (`0700`) 到下午 7 点 (`1900`)

`time.conf` 中的条目看起来如下：

```bash
login; ; :root ; Wd0700-1900
```

实现此示例时间限制的最后一步是确保 PAM 模块正在使用 `time.conf`；即 `time.conf` 被包含在 PAM 系统事件配置文件中。使用 `pam_time` 的 PAM 模块。在接下来的部分列表中，`grep` 显示了 PAM 模块；任何系统事件文件中都没有使用 `pam_time`。

```bash
# grep *pam* /etc/pam.d/*
```
