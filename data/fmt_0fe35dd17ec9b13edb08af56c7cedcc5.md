
## 配置 AMaViSd-new

在 SUSE Linux Enterprise Server 10 上，你可以通过编辑以下文件之一来配置 AMaViSd-new：

- `/etc/sysconfig/amavis`
- `/etc/amavisd.conf`

### `/etc/sysconfig/amavis`

配置文件 `/etc/sysconfig/amavis` 仅在 SUSE Linux 产品上可用。

该文件中只有两个参数：

- `USE_AMAVIS`。如果设为 `yes`，Sendmail 或 Postfix 将被准备好使用 AMaViSd-new。

在 Postfix 配置文件 `/etc/postfix/main.cf` 中，你需要添加以下行：

```
content_filter = smtp-amavis:[127.0.0.1]:10024
```

通过输入 `postfix reload` 重启 Postfix。

### `/etc/amavisd.conf`

AMaViSd 通过编辑文件 `/etc/amavisd.conf` 进行配置。该配置文件的语法是纯 Perl 代码。因此，每行以分号结尾。

在 Perl 中，双引号字符串可以包含以 `"$"` 或 `"@"` 开头的变量。要在双引号字符串中包含字符 `"@"` 和 `"$"`，它们必须前面加上反斜杠。

在单引号字符串中，`"$"` 和 `"@"` 失去其特殊含义，因此通常使用单引号字符串更容易。

在这两种情况下，反斜杠都需要加倍。

在 AMaViSd-new 的文档目录 `/usr/share/doc/packages/amavisd-new/` 中，还有两种配置文件的变体可用：

- `amavisd.conf-default`。包含所有可能的参数及其默认值。
- `amavisd.conf-sample`。一个结构更清晰的文件，包含大量解释和示例。

在本节中，我们想按其在 `/etc/amavisd.conf` 文件中出现的顺序讨论一些最重要的参数。

- `@bypass_virus_checks_maps`。该数组包含病毒查找表的列表。你可以通过将该数组设为 `"1"` 来禁用病毒检查（取消注释该行）。

- `@bypass_spam_checks_maps`。该数组包含垃圾邮件查找表的列表。你可以通过将该数组设为 `"1"` 来禁用垃圾邮件检查（取消注释该行）。

除了 `@bypass_virus_checks_maps` 和 `@bypass_spam_checks_maps` 外，还有另外两个同类型的数组可用：
`@bypass_banned_checks_maps` 启用对禁止名称或文件类型的检查。
`@bypass_header_checks_maps` 启用对无效头的检查。

- `$max_servers`。预派生的子进程数量。
应与你的 MTA 管道数量匹配，例如 `/etc/postfix/master.cf` 中的 `maxproc` 字段。

```
#
=========================================================================
# service type  private unpriv  chroot  wakeup  maxproc command + args
#              (yes)    (yes)   (yes)   (never) (100)
#
=========================================================================
=
smtp     inet  n       -       n       -       2       smtpd -o
content_filter=smtp:[127.0.0.1]:10024
```
