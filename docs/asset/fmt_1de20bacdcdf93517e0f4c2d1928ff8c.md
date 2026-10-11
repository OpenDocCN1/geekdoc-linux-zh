
# Linux 管理手册

## 邮件队列目录

- `/var/spool/mqueue` 和 `/var/spool/clientmqueue`
- `/var/spool/clientmqueue`，由管理员在安装过程中创建。
- 指向 `sendmail` 二进制文件的各种链接：`/newaliases`, `mailq`, `hoststat` 等。
- `sendmail`：更安全的本地投递代理，`smash` 和 `mail.local` 通常安装在 `/usr/lib/libexec`

你可以从 `sendmail.org` 下载最新版本的 `sendmail`。要编译并安装该包，请遵循 `setup INSTALL` 文件中的说明。首先添加 `smtp` 用户和用户组，不要给该用户提供真实的 shell。以下是一个典型的 `/etc/passwd` 条目：

这里是一个典型的 `/etc/group` 条目：

要编译软件，请进入发行版的 `sendmail` 目录，运行 `Build` 脚本，然后运行 `build`。`devtools OS/Linux` 文件包含了对 Linux 系统上 `sendmail` 的假设。Linux 发行版已经对这些文件的位置进行了标准化处理，因此 `devtools OS/Linux` 包含了示例，且可能与你的发行版并不完全对应。

在开始编译之前，你必须决定一种数据库格式以及使用 NIS 等管理数据库进行 `sendmail` 实例化的策略。对于数据库，我们建议使用 `Makefile` 中指定的 Berkeley DB 包，并通过 `DEFINE` 指定它。Linux 自带了一个旧版本的 Berkeley DB v11994。`sendmail` 可以与此版本配合，但建议你从 `sendmail.org` 获取当前版本。许可条款是通用的，因为你并不分发 DB 软件，因此不需要许可证，也不需要费用。

要自定义 `Makefile`，请不要编辑它，而是创建你自己的 `site.config.m4` 文件，并将其放在操作系统和本地环境对应的 `devtools` 目录中。例如，如果你打算使用 LDAP 和新的垃圾邮件过滤库，请在该目录下创建一个包含以下几行的 `site.config.m4` 文件：

一个 `define` 宏会替换属性的当前定义：`ADDER` 宏则在当前定义的基础上进行追加。

## 第19 章 电子邮箱

使用以下命令编译 `sendmail`：

```
% sh ./Build
```

将自动包含特定站的条目。要将 `sendmail` 安装在正确的位置，请运行

```
% sudo ./Build
```

`sendmail` 通常不设置为由 `inetd/xinetd` 控制，因此在启动时的 `rc` 文件中必须显式说明。一个典型的序列如下：

```
if [ /usr/sbin/sendmail -a -f /etc/mail/sendmail.cf ]; then
  cd /var/spool/clientmqueue; rm -f *
  cd /var/spool/mqueue; rm -f *
  /usr/sbin/sendmail -Ac -q 处理常规队列
  /usr/sbin/sendmail -Ac -q 处理客户端队列 (8.12)
  echo -n > /dev/console
```

这些行会检查 `sendmail` 二进制文件及其配置文件，然后以守护模式启动进程。当用户代理在向邮件系统提交用户消息时，它们会显式地运行 `sendmail`（有时带有 `-bm` 或 `-bs` 标志），而不是发送 SMTP 协议。在这种情况下，`sendmail` 使用配置文件 `submit.cf` 并将消息放入 `/var/spool/clientqueue` 目录。使用 `-Am` 或 `-Ac` 调用 `sendmail` 会分别将消息放入 `mqueue` 或 `clientqueue`。

Red Hat 有一个 `sendmail` 启动脚本（`/etc/init.d/sendmail`），它不会清理 `mqueue` 目录（如所示）。然而，在 `sendmail` 8.12 及更高版本中，可以使用 LDAP 用于数据库映射，并且在更改后需要重新构建映射。`/etc/sysconfig/sendmail` 中定义的参数决定了 `sendmail` 是否应该以守护模式启动，以及根据你的需求运行的频率。Red Hat 默认版本以守护模式启动 `sendmail`，并每 30 分钟运行一次队列。SUSE 的启动脚本（`/etc/init.d/sendmail`）仅检查二进制文件和配置文件，然后使用 `SENDMAIL_ARGS` 环境变量中定义的参数启动；这些参数设置在 `/rc.config` 文件中。SUSE 默认也使用守护模式并每 30 分钟运行一次队列。

上述段落（或类似的内容）如果你的 Linux 发行版不包含 `sendmail` 启动脚本，则应将其添加到 `/etc/init.d/`。一个高级的安装指南尝试清理之前中断的队列运行。可以根据需要混合使用。从历史上来看，`sendmail` 的支持文件一直在文件系统中游动，到达过如 `/usr/lib/`、`/etc/mail` 和 `/usr/share` 等目的地。`sendmail` 8.12 之后，LDAP 可以用于数据库映射，并且在更改后重新构建映射是必要的。`/etc/sysconfig/sendmail` 中定义的参数决定了 `sendmail` 是否应该以守护模式启动。`sendmail` 默认在 Debian 上安装。

`/var/spool/clientmqueue`

`sendmail` 8.12 之后，LDAP 可以用于数据库映射

`apt-get`

`sendmail` 使用配置文件 `submit.cf` 并将消息放入 `/var/spool/clientqueue` 目录
