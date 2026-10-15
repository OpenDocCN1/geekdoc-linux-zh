
# UNIX 系统管理手册

## 设置磁盘配额

如果你使用磁盘配额，你应该为每个用户设置配额限制。

## 第 6 章 添加新用户

如果禁用了 shell，用户将无法登录。然而，用户仍然可以在不输入密码的情况下通过网络登录，因此这种技术已不再有效。

现如今，我们用一个程序替换用户的 shell，该程序会打印一条消息解释为什么禁用了登录，并提供纠正该情况的说明。这个伪 shell 不应该列在 `/etc/shells` 中；许多提供系统登录访问的守护进程（例如 `ftppd`）会检查用户的登录是否列在 `/etc/shells` 中，如果不在则拒绝访问（这正是你想要的行为）。

这种禁用登录的方法存在一个问题：默认情况下，`sendmail` 不会向 shell 不在 `/etc/shells` 中的用户投递邮件。即使接收者无法立即阅读邮件，干扰邮件流通常也是一个坏主意。你可以通过在 `/etc/shells` 中添加一个虚假名称 `/SENDMAIL/ANY/SHELL/` 来消除 `sendmail` 的默认行为。

## 6.9 厂商提供的账户管理工具

Solaris、HP-UX 和 Red Hat Linux 提供了一组工具，帮助自动化地创建、删除和修改用户及组。FreeBSD 也有有一组工具，我们将在下一页简要介绍。

`useradd` 命令将用户添加到 `passwd` 文件（以及 `shadow` 文件，如果适用）。它提供了一个命令行界面，易于手动运行或从自定义的 `adduser` 脚本中调用。`usermod` 命令处理现有用户的 `passwd` 条目。`userdel` 从系统中删除用户，并可选地删除用户的家目录。`groupadd`、`groupmod` 和 `groupdel` 也对 `/etc/group` 文件进行操作。

尽管这些命令非常方便，但它们很少能够实现一个站点所有的本地策略。我们建议你使用自己的 `adduser` 和 `rmuser` 脚本（这些脚本可能调用或不调用厂商工具）。`Perl` 非常适合这项任务。

例如，使用 `useradd`（使用系统默认值）创建一个新用户 "`hilbert`"，你只需要：

```bash
# useradd hilbert
```

该命令会在 `/etc/passwd` 中创建以下条目。注意 `useradd` 在密码字段中放置了一个星号 `*`，在你分配真实密码之前，该账户实际上处于禁用状态。

```text
hilbert:*105:20::/home/hilbert/bin/sh
```

`useradd` 在提供额外参数时通常更有用。在下一个示例中，我们指定 `hilbert` 的主组应为 "`faculty`"，并且他还应该被加入 "`famous`" 组。我们还覆盖了默认的家目录位置，并要求 `useradd` 在家目录不存在时创建它：

```bash
# useradd -c "David Hilbert" -d /home/math/hilbert -g faculty -G famous -m -s /bin/tcsh hilbert
```

此命令创建了以下 `passwd` 条目：

```text
hilbert:~105:30:David Hilbert:/home/math/hilbert/bin:tcsh
```

它还向 `/etc/group` 中的 "`factory`" 和 "`famous`" 组添加了用户，创建目录 `/home/math/hilbert`，并根据 `/etc/skel` 的内容填充它。在 Solaris 上（以及 Linux 上，如果使用了密码），`/etc/shadow` 中也会为 `hilbert` 创建一个条目。

你可以通过 `useradd -D` 确定默认的 `userid` 设置；在 HP-UX 和 Red Hat Linux 中，你可以在 `/etc/default/useradd` 文件中设置默认值。

`usermod` 修改已存在的账户，并带有许多与 `useradd` 相同的标志。例如，我们可以使用以下命令为 `hilbert` 的账户设置 2002 年 7 月 4 日的有效期：

```bash
# usermod -e "July 4, 2002" hilbert
```

`userdel` 删除用户账户，有效地撤销 `useradd` 所做的所有更改。要移除 `hilbert`，我们将使用以下命令：

```bash
# userdel hilbert
```

该命令删除了 `passwd`、`shadow`（如果在使用）和 `group` 文件中对 `hilbert` 的引用。默认情况下，它不会删除 `hilbert` 的家目录。（在我们的站点，我们通常会保留删除用户的家目录几周，以避免必须从备份带中恢复数据。）

FreeBSD 自带有一个 `pw` 命令，它的作用类似于 `useradd` 及其同类。如果你习惯其他系统上的 `useradd` 风格的命令，`pw` 可能会很有用。然而，与 `useradd` 不同，FreeBSD 的 `pw` 根据其第一个参数来选择行为。例如，使用 `pw` 添加用户 `hilbert`，我们将运行：

```bash
# pw useradd hilbert
```
