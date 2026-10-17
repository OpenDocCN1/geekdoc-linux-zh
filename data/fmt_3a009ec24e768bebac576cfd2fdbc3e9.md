
你可以使用内置别名 `ALL` 使该行适用于所有命令。

在 `command_list` 中包含字符串 `sudoedit` 允许 `user_list` 中的用户权限使用 `root` 权限编辑文件。更多信息请参见第 417 页的提示。

（注：此处省略了重复的文本内容，已处理后续部分的翻译逻辑）

用户权限规范允许 Sam 在包含此规范的 sudoers 文件的所有系统（由 `ALL` 指定）上使用 sudo 挂载和卸载文件系统（以 `root` 权限运行 `mount` 和 `unmount`）：

```
ALL=(root)/bin/mount, /bin/unmount
```

`(root)` `runas_list` 是可选的。如果省略它，sudo 允许用户以 `root` 权限运行 `command_list` 中的命令。在接下来的示例中，Sam 利用了这些权限。他不能直接运行 `unmount`；相反，他必须调用 `sudo` 来运行。

```bash
$ whoami
sam
$ mount /music
unmount: only root can unmount /dev/sdb from music
$ sudo unmount /music
[sudo] password for sam:
```

如果你将上述 sudoers 中的行替换为，Sam 不允许卸载 `p03`，但他仍然可以卸载其他文件系统并挂载任何文件系统：

```
ALL=(root)/bin/mount, /bin/unmount, !bin/unmount /p03
```

sudoers 中上一行的结果显示，由于 Sam 在过去五分钟内输入过密码，sudo 不再提示密码。

## $ sudo mount /p03

Sorry, user is not allowed to execute '/bin/unmount /p03' as root.

以下行限制 Sam 挂载和卸载位于 `/p01`、`/p02`、`/p03` 和 `/p04` 的文件系统：

```
ALL=/bin/mount /p1-4, /bin/unmount /p1-4
```

以下命令显示结果：

## $ sudo mount /music

Sorry, user is not allowed to execute '/bin/unmount /music' as root on localhost.

## $ sudo mount /p03

```bash
$
```

## 422 第 11 章系统管理：核心概念

（注：此处省略了大量重复的文本描述，确保核心逻辑准确）

## 别名 (ALIASES)

别名允许你重命名用户、主机或命令。别名的格式为：

```
alias_type name = list
```

其中 `*alias_type*` 是类型（`User_Alias`, `Runas_Alias`, `Host_Alias`），`*name*` 是别名的名称，`*list*` 是逗号分隔的元素列表。在别名元素前加感叹号 `(!)` 可以否定它。

## 以 root 权限运行命令 423

`User_Alias` 用户别名列表与用户权限规范的用户列表相同（见上一节）。sudoers 中的以下行定义了三个别名：`OFFICE`、`ADMIN` 和 `ADMIN2`。

| User_Alias | OFFICE = zach, sam |

| User_Alias | ADMIN = %admin |

| User_Alias | ADMIN2 = !max |

`Runas_Alias` runas 别名列表与用户权限规范的 runas列表相同（见上一节）。以下包含了用户名 sam 和 sls：

- Runas_Alias = sam, sls

`Host_Alias` 主机别名列表与用户权限规范的主机列表相同（见上一节）。以下行定义了名为 guava 和 plum 的系统：

| Host_Alias | LCL = guava, plum |

`Cmnd_Alias` 命令别名列表与用户权限规范的命令列表相同（见上一节）。以下命令包含三个文件，并通过包含目录（用 `/` 表示），包含了该目录下的所有文件：

| Cmnd_Alias | BASIC = /bin/cat, /usr/bin/vi, /bin/df, /usr/local/safe/ |

## DEFAULTS (OPTIONS)

你可以使用 `Defaults` 关键字从默认值更改配置选项。此列表中的大多数值是隐布尔值（可以开启或关闭）或字符串。通过命名为 `Defaults` 行来开启标记，通过在它前面加 `1` 来关闭它。sudoers 中的以下行将关闭 `lecture` 和 `fqdn` 标记并开启 `tty_tickets`：

| Defaults | !lecture,!tty_tickets,!fqdn |

`env_reset` 导致 sudo 重置环境变量，仅包含 `LOGNAME`, `SHELL`, `USER`, `USER`, `MAIL` 和 `SUDO*` 变量。默认开启。更多信息请参见 sudoers 手页。

`fqdn`（完全限定域名）对 sudoers 文件中的 FQDN（第 1165 页）执行 DNS 查询。当设置了此标记时，你可以在 sudoers 文件中使用 FQDN，但可能会降低 sudo 的性能。

## 424 426 第 11 章 系统管理：核心概念

可能会对 sudo 的性能产生负面影响，特别是 DNS 无法工作时。当设置此标志时，使用本地主机的官方 DNS 名称，而不是别名。如果 `hostname` 返回的是完全限定域名 (`FDN`)，则你不需要设置此标志。默认开启。

- `insults`: 当用户输入错误密码时，显示轻微、幽默的辱骂信息。默认关闭。另见 `passed_tries`。
- `lecture=freq`: 控制 sudo 在密码提示之前何时显示提醒消息。`freq` 的可能值为 `never`、`once` 和 `always`。指定 `lecture of freq` 等同于指定 `freq` 为 `never`。默认是 `once`。
- `mail_always`: 用户每次运行 sudo 时，都会向 mailuser 发送邮件。默认关闭。
- `mail_badpass`: 当用户在运行 sudo 时输入错误密码时，向 mailuser 发送邮件。默认关闭。
- `mail_no_host`: 当在 sudoers 文件中的用户名没有权限在本地主机上运行命令的用户运行 sudo 时，向其 发送邮件。默认关闭。
- `mail_no_perms`: 当在 sudoers 文件中的用户名没有权限运行请求的命令运行 sudo 时，向其 发送邮件。默认关闭。
- `mail_no_user`: 当不在 sudoers 文件中的用户名运行 sudo 时，向其 发送邮件。默认开启。
- `mailsub=subj`: 将警告和错误消息的默认邮件主题从默认的 `*** SECURITY information for ****` 更改为 `subj`。sudo 工具会扩展 `subj` 中的 `%h`，即本地系统的主机名。如果 `subj` 包含 shell 特殊字符，请将其放在引号之间（第 146 页）。
- `mailto=eadd`: 将警告和错误消息发送到 `eadd`（一个电子邮件地址；默认是 `root`）。如果 `eadd` 包含 shell 特殊字符，请将其放在引号之间（第 146 页）。
- `password_timeout=mins`: `mins` 是 sudo 提示超时前的分钟数。值 0（零）表示密码不超时。默认是 5。
- `password_tries=num`: `num` 是用户在 sudo 退出之前，响应 sudo 提示可以输入错误密码的次数。默认是 3。另见 `insults` 和 `lecture`。
- `rootpw`: 导致 sudo 在响应提示时仅接受 root 密码。因为 sudo 无论请求你的密码还是 root 密码都会发出相同的提示符，因此开启此标志可能会误导用户。默认关闭，导致 sudo 提示运行 sudo 的用户的密码。
- `shell_noargs`: 导致 sudo 在不带任何参数被调用时，产生一个不改变环境的 root shell。默认关闭。此选项与 `sudo -s` 选项相同。
- `timestamp_timeout=mins`: `mins` 是 sudo 时间戳（第 416 页）有效的分钟数。将 `mins` 设置为 -1 可使时间戳永久；设置为 0（零）则使 sudo 始终提示密码。默认是 5。

## 以 root 权限运行命令

`tty_tickets`: 导致 sudo 按每个 tty（终端）验证用户，而不是按每个用户验证。默认开启。

`umask=val`: `val` 是 sudo 运行用户指定的命令时使用的 umask（第 473 页）。将 `val` 设置为 0777 以保留用户的 umask 值。默认是 0022。

## 锁定 root 账户（移除 root 密码）
