
```
$ cat /etc/hosts
# Do not remove the following line, or various programs
# that require network functionality will fail.
127.0.0.1		rose localhost.localdomain localhost
192.168.0.1		bravo example.com		bravo
192.168.0.4		mpserver
192.168.0.5		workstation
192.168.0.10		rose
...
```

如果您不使用 NIS 或 DNS 来查找主机名（称为 *hostname resolution*），您必须在`/etc/hosts`中包含您希望本地系统能够联系的所有系统。`/etc/nsswitch.conf`文件（第 455 页）中的`hosts`条目控制检查主机名解析服务的顺序。

## `/etc/inittab`

(RHEL) 初始化表

在 RHEL 下，此文件控制 System V init 进程的行为。Fedora 已用 Upstart init 守护进程取代了 System V init 守护进程；更多信息请参阅第 417 页。在 Fedora 下，此文件仅包含`initdefault`行。`inittab`中的每一行包含四个由冒号分隔的字段：

`id:runlevel:action:process`

`*id*`唯一标识`inittab`文件中的条目。`*runlevel*`是执行`*process*`的系统运行级别。`*runlevel*`由`0123456S`中的零个或多个字符组成。如果列出了多个运行级别，则相关的`*process*`将在指定的每个运行级别执行。当您未指定运行级别时，`init`将在所有运行级别执行`*process*`。当系统更改运行级别时，`inittab`中所有不包含新运行级别的条目指定的`*processes*`都会发送`SIGTERM`信号，以便它们能够优雅地终止。5 秒后，如果这些`*processes*`仍在运行，则使用`SIGKILL`强制终止它们。`*process*`可以是任何`bash`命令行。

`*action*`是以下关键字之一：`respawn`, `wait`, `once`, `boot`, `bootwait`, `ondemand`, `powerfail`, `powerwait`, `powerokwait`, `powerfailnow`, `ctlaltdel`, `kbrequest`, `off`, `ondemand`, `initdefault`, 或`sysinit`。此关键字控制在执行时如何处理`*process*`。最常用的关键字是`wait`和`respawn`。

`*wait*`关键字指示`init`启动`*process*`并等待其终止。对`inittab`的所有后续扫描都会忽略此`wait`条目。由于`*wait*`条目仅在进入`*runlevel*`时启动一次，且在系统保持在`*runlevel*`时不会再次执行，因此它常用于将`init`输出重定向到控制台。

`*respawn*`条目告诉`init`如果`*process*`不存在则启动它，但无需等待其终止。如果`*process*`存在，`init`则转到`inittab`中的下一个条目。

`init`实用工具继续重新扫描`inittab`，寻找已终止的进程。当进程终止时，`respawn`条目会导致`init`重新启动它。

`initedefault`条目告诉`init`启动时将系统置于哪个运行级别（见第 424 页的表 11-1）。如果没有此信息，`init`会在系统控制台上提示输入运行级别。`initedefault`条目的值在您配置系统或直接编辑`inittab`时设置。默认情况下，Fedora/RHEL 将`initedefault`设置为`5`，这导致系统以图形多用户模式启动。

### 编辑 `inittab` 时需小心

> 手动编辑 `inittab` 时务必小心。在编辑此文件之前，总是在同一目录下制作备份副本。如果您犯了错误，可能无法启动系统。如果无法启动系统，请参阅第 411 页的“救援模式”。

每个虚拟控制台（第 137 页）都有一个 `inittab` `mingetty` 条目，其中包含唯一的终端标识符（例如 `tty1`，即 `/dev/tty1` 的缩写）。您可以通过添加或删除 `mingetty` 行来添加或删除虚拟控制台。请记住，为您希望运行的每个 X 窗口保留一个虚拟控制台。以下是 `/dev/tty2` 的 `mingetty` 条目：

```
2:2345:respawn:/sbin/mingetty tty2
```

`mingetty` 行上的 `id` 对应 `tty` 编号。

所有操作都在 `inittab` 手册页中有文档记录。更多信息请参阅第 425 页的“启动系统”。

## `/etc/motd`

包含当日消息（message of the day），每次有人使用文本登录时都会显示此消息。此文件通常包含站点策略和法律信息。请保持此文件简短，因为用户往往会多次看到该消息。

## `/etc/mtab`

当您不带任何参数调用 `mount` 时，它会参考此文件并显示已挂载设备的列表。每次您（或 `init` 脚本）调用 `mount` 或 `umount` 时，这些实用工具会对 `mtab` 进行必要的更改。虽然这是一个 ASCII 文本文件，但您不应编辑它。另见 `/etc/fstab`。

### 修复 `mtab`

> 操作系统在 `/proc/mounts` 中维护其自身的内部挂载表。您可以使用 `cat` 显示 `/proc/mounts` 的内容，以便审查内部挂载表。有时，`/etc/mtab` 中的文件列表可能与该表中的分区不同步。为了使 `mtab` 文件与操作系统的挂载表保持一致，您可以重启系统，或者用指向 `/proc/mounts` 的符号链接替换 `/etc/mtab`（可能会丢失一些信息）。

```
# rm /etc/mtab
# ln -s /proc/mounts /etc/mtab
```

## `/etc/netgroup`

定义 `netgroup`，用于在执行远程登录和远程挂载以及启动远程 shell 时检查权限。

## `/etc/nsswitch.conf`

指定系统使用 NIS、DNS、本地文件或它们的组合作为某些信息的来源，以及查询这些服务的顺序（第 455 页）。

## `/etc/pam.d`

此目录中的文件指定 PAM（第 458 页）应用程序使用的身份验证方法。

> **注意**
>
> 除非你了解如何配置 PAM，否则请避免更改 **`/etc/pam.d`** 中的文件。PAM 配置中的错误可能导致系统无法使用。

## `/etc/passwd`

向系统描述用户。不要直接编辑此文件；相反，请使用第 556 页“配置用户和组账户”中讨论的某个实用工具。**`passwd`** 的每一行都有七个由冒号分隔的字段，用于描述一个用户：

`login-name:dummypassword:user-ID:group-ID:info:directory:program`

`*登录名*` 是用户的用户名——即你在 **`login:`** 提示符或 GUI 登录屏幕上输入的名称。`*dummypassword*` 的值是字符 `x`。加密/哈希后的密码存储在 **`/etc/shadow`** 中（第 477 页）。出于安全原因，每个账户都应设置密码。按照惯例，禁用的账户在此字段中包含一个星号 (*)。

`*用户 ID*` 是一个数字，0 表示超级用户，1–499 保留给系统账户。`*组 ID*` 标识用户为某个组的成员。它是一个数字，0–499 保留给系统账户；参见 **`/etc/group`**。你可以在 **`/etc/login.defs`** 中更改这些值并设置最大值。

`*信息*` 是各种程序（如会计程序和电子邮件）用来进一步识别用户的信息。通常它至少包含用户的名和姓。它被称为 GECOS 字段（第 1084 页）。

`*目录*` 是用户主目录的绝对路径名。`*程序*` 是用户登录后运行的程序。如果不存在 `*program*`，则假定值为 `/bin/bash`。你可以在此处输入 `/bin/tcsh` 以使用 TC Shell 登录，或输入 `/bin/zsh` 以使用 Z Shell 登录，前提是假设你指定的 Shell 已安装。**`esh`** 实用工具（第 439 页）会更改此值。

`*program*` 通常是一个 Shell，但可以是任何程序。以下 **`passwd`** 文件中的行创建一个唯一目的是执行 **`who`** 实用工具的“用户”：

```
who:x:1000:1000:execute who:/usr/bin/who
```

使用 **`who`** 作为用户名会导致系统登录你，执行 **`who`** 实用工具，然后注销你。由于新的登录提示会立即清除屏幕，**`who`** 的输出会很快闪过。由于 **`who`** 执行完毕后无法保持登录状态，因此 **`passwd`** 文件中的此条目不提供 Shell。
