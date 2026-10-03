
## 配置 Amavis 进程

在此文件中，你还必须为 amavis 添加一个进程：

```
smtp-amavis unix - - - 2 smtp
-o smtp_data_done_timeout=1200
-o smtp_send_xforward_command=yes
-o disable_dns_lookups=yes
-o max_use=20
```

在 Postfix 配置文件 `/etc/postfix/main.cf` 中，你需要添加以下行：

```
content_filter = smtp-amavis:[127.0.0.1]:10024
```

通过输入 `postfix reload` 重启 Postfix。

## /etc/amavisd.conf

AMaSd 通过编辑文件 `/etc/amavisd.conf` 进行配置。

该配置文件的语法是纯 Perl 代码。正因如此，每行都以分号结尾。

在双引号 Perl 字符串中，可以包含以 `\$` 或 `\@` 开头的变量。要在双引号字符串中包含 `@` 和 `$` 字符，必须在它们前面加一个反斜杠。

在单引号字符串中，`\$` 和 `@` 会失去它们的特殊含义，因此通常使用单引号字符串更简单。

在这两种情况下，反斜杠都需要双写。

在 amavisd-new 的文档目录（`/usr/share/doc/packages/amavisd-new/`）中，提供了两个变文件：

- `amavisd-conf.default`：包含所有带有默认值的可能参数。
- `amavisd-conf.sample`：一个更结构化的文件，包含大量示例。

在本节中，我们按照参数在 `/etc/amavisd.conf` 文件中出现的顺序讨论一些最重要的参数：

- `@bypass_virus_maps`。此数组包含病毒查找表列表。你可以通过将数组设置为 "1"（取消注释该行）来禁用病毒检查。
- `@bypass_spam_maps`。此数组包含垃圾邮件查找表列表。你可以通过将此数组设置为 "1"（取消注释该行）来禁用垃圾邮件检查。

在 `@bypass_virus_maps` 和 `@bypass_spam_maps` 旁边还有两个相同类型的数组：

- `@bypass_banned_maps` 启用检查禁用的名称或文件类型。
- `@bypass_header_maps` 启用检查无效标头。

`$max_servers`。预叉（pre-forked）子进程的数量。应与 MTA 管道的数量一致，例如 `/etc/postfix/master.cf` 中的 `maxproc` 字段。

```
=======================================================
## service type private chroot maxproc args
## (yes) (yes) (never) (100)
=======================================================
smtp inet n n - 2 smtpd -o content_filter=smtp:[127.0.0.1]:1024
```

`$daemon_user` 和 `$daemon_group`。守护进程将切换的用户和组。

`$mydomain`。域名。

`$MYHOME`。amavisd-new 文件存储的位置。

`$TEMPBASE`。可以被 amavisd-new 使用的临时目录路径。该目录必须存在或需要手动创建。

在接下来的行中，环境变量 `$TMPDIR` 使用 `$TEMPBASE` 变量的内容进行定义。

`$QUARANTINED`。可以存放感染邮件的路径。该路径不以反斜杠结尾。

`$quarantine_subdir`。如果设置为 "1"，则会在 `$QUARANTINED` 中创建子目录以便分散。

`$daemon_chroot`。在指定的 chroot 中运行守护进程。如果你不想 chroot，请将其留空。

`$db_home`。数据库的路径。默认：`$MYHOME/db`。

`$helpers_home`。设置传递给 SpamAssassin 模块的环境变量 HOME。

`$pid_file`。PID 文件的路径。

`$lock_file`。锁文件的路径。

`@local_domains`。查找表列表，用于判断接收者是否为本地用户，即邮件是否为外发邮件。

`@mynworks`。IP 范围列表，用于确定原始 SMTP 地址是否属于内部网络。

`@mynworks`。列表，用于确定原始 SMTP 地址是否属于内部，即来自内部的。

`$log_level`。日志级别。

- 0. 启动
- 1. 错误
- 2. 详细
- 3. 调试
- 4. 警告
- 5. 关键信息

## /etc/sysconfig/amavis

- `AMAVIS_SENDMAIL_MILTER`。如果设置为 yes，则将启动 Sendmail 的 milter（邮件过滤器）接口。

使用 milter 接口，可以标准化的形式将邮件过滤器应用程序连接到 Sendmail。

更改文件 `/etc/sysconfig/amavis` 之后，你必须运行 `SuSEconfig` 命令。

将 `USE_AMAVIS` 设置为 yes 会对 `/etc/postfix/master` 进行三处更改。

### smtp 协议

| smtp | inet | n | n | 2 | smtpd -o |
| :--- | :--- | :--- | :--- | :--- | :--- |
| content_filter=smtp:[127.0.0.1]:1024 | | | | | |

### smtps 协议（仍被标记为注释）

| #smtps | inet | n | n | 2 | smtpd -o |
| :--- | :--- | :--- | :--- | :--- | :--- |
| smtpd_tls_wraermode=yes -o content_filter=smtp:[127.0.0.1]:1024 | | | | | |

### 端口 10025

| localhost:10025 inet | n | n | - | smtpd -o |
| :--- | :--- | :--- | :--- | :--- |
| content_filter= | | | | | |
