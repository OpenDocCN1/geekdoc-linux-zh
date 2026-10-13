
然后使用 `kill` 向 syslog 发送一个 SIGHUP 信号。现在你已经准备好通过尝试错误的密码或登录 ID 进行 telnet 登录来测试它。

# 16.5 为自动分页构建示例

你以那种特定的方式编写脚本，是因为它允许你轻松扫描其他事件并为它们生成自定义页面。在大型系统中，某些人的密码会很弱（除非你在第一部分中确保不讨论易于破解的密码）。

因此，一种常用技术是猜测某些用户的密码作为破入的第一步，然后尝试执行操作。（第一部分讨论了如何配置系统，使 root 仅能从物理安全的控制台登录，而不能通过破解机房的某处的 telnet 登录。）

当然，你可能会在失败的 `su` 尝试中需要分页显示。`su` 程序也会通过 `auth.notice` 记录尝试。因此，向你的脚本中添加几行代码并重启它。

```bash
#!/bin/csh -f

loop:

  set x="$$"

  echo "$x" | grep -q ' invalid password'

  if ($status == 0) then

    echo "$x"

    sed "s/\.*/.*\:\^([^ ]*)\*: invalid password for /BAD PW:\/"/\"

    Mail 1234567@skytel.com

  endif

  echo "$x" | grep -q 'su[:].*: Authentication failed'

  if ($status == 0) then

    echo "$x"

    sed "s/\.*/.*\^([^ ]*)\*: Authentication failed for /BAD SU:\/"/\"

    Mail 1234567@skytel.com

  endif

goto loop
```

这在对 root 执行 `su` 失败时将产生以下页面：

BAD SU:cavu:root

你不需要向 syslogd 发送消息，因为它的配置文件没有更改。

这第二个示例主要展示了如何为单个脚本添加消息处理句程序。如果你的助手再次在调整系统，那么知道哪个账户尝试 `su` 到 root 以及在哪个终端上操作，将非常有帮助。

`su` 程序会记录这些额外信息，但处于调试级别（debug level）。因为许多其他程序也会在此记录安全相关信息，请将所有这些信息通过你的脚本发送，你可以从中挑选要分页的消息。因此，编辑 `/etc/syslog.conf` 显示以下内容并向 syslogd 发送 SIGHUP 信号：

```
auth.* |/usr/local/etc/syslog_auth
```

（你也可以选择以其他方式处理某些信息，例如发送邮件到你的账户，可能在另一个系统上。在成功的破解中，你所有的“触丝线”（trip wires）都会失效，但通过将它们放置在所有入口处以便在系统被攻破之前获得“警告”，你仍然会收到警告，并希望在及时阻止破解者。）

原始日志消息如下所示：

```
Nov 24 13:13:18 cavu su[426]: tty2 bob-root
```

以下脚本将很好地处理此。（它可以从任何 shell 调用。）

```bash
#!/bin/csh -f

loop:

  set x="$$$"

  echo "$x" | grep -q ' : invalid password'

  if ($status == 0) then

    echo "$x"

    sed "s/\/.../...\\([^*]*\*: invalid password for /BAD PW:\" /\

    Mail 1234567@skytel.com

  endif

  echo "$x" | grep -q 'su[:].*: Authentication failed'

  if ($status == 0) then

    echo "$x"

    sed "s/\.*/.*\^([^ ]*)\*: Authentication failed for /BAD SU:\/"/\"

    Mail 1234567@skytel.com

  endif

goto loop
```

在 `su` root 失败将产生以下页面：

BAD SU:cavu:root

你不需要向 syslogd 发送消息，因为它的配置文件没有更改。

这第二个示例主要展示了如何为单个脚本添加消息处理程序。如果你的助手再次在调整系统，那么知道哪个账户尝试 `su` 到 root 以及在哪个终端上操作，将非常有帮助。

`su` 程序记录了这些额外信息，但处于调试级别。因为许多其他程序也会在此记录安全相关信息，请将所有这些信息通过你的脚本发送，你可以从中挑选要分页的消息。因此，编辑 `/etc/syslog.conf` 显示以下内容并向 syslogd 发送 SIGHUP 信号：

```
auth.* |/usr/local/etc/syslog_auth
```

（你也可以选择以其他方式处理某些信息，例如发送邮件到你的账户，可能在另一个系统上。在成功的破解中，你所有的“触丝线”都会失效，但通过将它们放置在所有入口处以便在系统被攻破之前获得“警告”，你仍然会收到警告，并希望在及时阻止破解者。）

原始日志消息如下所示：

```
Nov 24 13:13:18 cavu su[426]: tty2 bob-root
```

以下脚本将很好地处理此。（它可以从任何 shell 调用。）

```bash
#!/bin/csh -f

loop:

  set x="$$$"

  echo "$x" | grep -q ' : invalid password'

  if ($status == 0) then

    echo "$x"

    sed "s/\/.../...\\([^*]*\*: invalid password for /BAD PW:\" /\

    Mail 1234567@skytel.com

  endif

  echo "$x" | grep -q 'su[:].*: Authentication failed'

  if ($status == 0) then

    echo "$x"

    sed "s/\.*/.*\^([^ ]*)\*: Authentication failed for /BAD SU:\/"/\"

    Mail 1234567@skytel.com

  endif

goto loop
```

syslog_login.

```bash
#!/bin/csh -f

loop:

set x="$$$"

echo "$x" | grep -q ' : invalid password'

if ($status == 0) then

  echo "$x"

  sed "s/\/.../...\\([^*]*\*: invalid password for /BAD PW:\" /\

  Mail 1234567@skytel.com

endif
```

一旦你启用此功能，它将在你的分页器（pager）中显示以下内容。它显示了哪个系统正在使用 telnet，以便你知道需要处于什么警惕程度。

BAD PW:cavu:`bob` on `ttyp6` from `cavu`

由于你的分页器会显示时间，因此请不要在启动序列中堆砌时间戳。接下来，你需要创建一个命名管道，用于将数据从 syslog 传输到此脚本中。该管道只需要以 root 身份创建，如下所示：

```bash
mknod /usr/local/etc/syslog_auth p

chmod 600 /usr/local/etc/syslog_auth
```

接下来，你需要安排此脚本在系统启动时运行。在 Red Hat 或 Slackware 中，你可以将以下行添加到 `/etc/rc.d/rc.local` 文件中：

```bash
/usr/local/bin/syslog_login < /usr/local/etc/syslog_auth &
```
