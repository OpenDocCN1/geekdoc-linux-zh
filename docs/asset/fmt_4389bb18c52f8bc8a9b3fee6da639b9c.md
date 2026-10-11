
Feb 3 12:08:25 localhost systemd[1]: Reloading.

## 第 22 章：理解基础 Linux 安全

要回审查审计日志，请使用审计守护进程的 `ausearch` 命令。所需的选项是 `-f` 审计日志，它指定了你想从审计日志中查看哪些记录。以下是 `/etc/passwd` 审计信息的示例：

```bash
# ausearch -f /etc/passwd

time->PATH msg=audit(1328612221.365:572):

item=0 name="/etc/passwd" inode=170549

fd=01 mode=0100644 uid=0 ogid=0

rdev=00 obj=system:u_object:r_t:0

type=CWD msg=audit(1328612221.365:572): cwd="/"

time->PATH Feb 3 04:27:01 2014

type=PATH msg=audit(1328612634.558:574):

item=0 name="/etc/passwd" inode=170549

fd=01 mode=0100644 uid=0 ogid=0

rdev=00 obj=system:u_object:r_t:0

type=CWD msg=audit(1328612634.558:574):

cwd="/johnndoe"

type=SYSCALL msg=audit(1328612634.558:574):

arch=x86(600) syscall=5 success=yes exit=3

asid=3bc2b9 aid=ae5000 a2=a1b6 items=3 ppid=3891

pid=21696 uid=1000 auid=1000 euid=1000

suid=1000 fsuid=1000 sgid=1000 fsid=1000

tty=pts1 ses=2 comm="vi" exe="/bin/vi"

subj=unconfined:unconfined:r_unconfined_t:s0:s0:c0.c123"
```

这里有很多需要审查的信息。几项内容可以帮助你看到发生了什么审计事件触发了底部记录。

- `time`: 活动发生的时间
- `name`: 文件名，`/etc/passwd` 在此文件系统上的 inode 节点号
- `inode`: 运行程序的 inode 节点号
- `uid`: 用户 ID (User ID)
- `exe`: 在 `/etc/passwd` 文件上使用的程序，即 `/bin/vi`

要确定哪个用户账户被分配了 UID 100，请查看 `/etc/passwd` 文件。在这种情况下，UID 100 属于用户 `johnndoe`。因此，通过上面显示的审计记录，你可以确定 `johnndoe` 尝试使用 `vi` 编辑器处理 `/etc/passwd` 文件。这很不是一个无意的行为，需要进一步调查。

# 第五部分：学习 Linux 安全技术

> 注意
> 如果文件没有触发任何监视事件，`search` 命令将返回空结果。

审计守护进程及其相关工具非常丰富。要了解更多信息，请查看以下审计守护进程工具和配置文件的帮助页（man pages）：

- `auditd`
- `auditd.conf` — 审计守护进程配置文件
- `auditctl` — 控制审计系统
- `audit.rules` — 启动时加载的配置规则
- `ausearch` — 在审计日志中搜索指定项目
- `aureport` — 审计守护进程的报告生成
- `audisp` — 将审计信息发送到其他程序

审计系统是监控重要文件的一种方法。你应该定期通过“肉眼”审查你的账户和组文件，以查看是否有任何异常。

重要文件（如 `/etc/passwd`）确实需要监控以防止未经授权的账户创建。然而，一个新的未经授权的用户账户可能只是一个坏密码的授权用户账户。

## 检测弱账户密码

为了使用 John the Ripper 测试用户账户名和密码，你必须首先使用 `shadow` 命令提取账户名。这些信息需要重定向到文件中供 `john` 使用，如下：

```bash
# unshadow /etc/passwd /etc/shadow > password.file
```

## 第 22 章：理解基础 Linux 安全

现在，使用你喜欢的文本编辑器编辑 `password.file`，移除任何没有密码的账户。明智的做法是将 John the Ripper 限制为一次测试几个账户，因此移除任何你目前不需要的账户。

> 警告
> `john` 工具非常消耗 CPU 资源。它将其 `nice` 值设置为 19 以降低优先级。然而，在非生产系统上或在非峰期间运行它，并且一次仅运行几个账户是明智的。

现在，使用 `john` 命令尝试破解密码。要对密码运行 john，请执行命令 `john filename`。在下面的代码段中，你可以看到运行 `john` 处理示例 `password.file` 时的输出。为了演示，示例中只留了一个账户。该账户 `Samantha` 被赋予了一个坏密码 `password`。你可以看到 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32]

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

## 监控文件系统

为了演示，你可以看到 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32]

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32]

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32]

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32])

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32])

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32])

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32])

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32])

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32])

password (Samantha)

guesses: 1 time: 00:00
```

查看 John Ripper 破解这个密码花了多短的时间。

```bash
# password.file

Loaded 1 hash (generic crypt(3) [?/32])

password (Samantha)

guesses: 1 time: 00:00
```
