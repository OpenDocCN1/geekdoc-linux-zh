
## 不要使用 ifdef

对于在 `OSTYPE` 文件中使用 `ifdef`，我持有一种哲学上的反对意见。我理解为什么必须这样做：这样做是为了创建一个适用于所有版本 Linux 的 `OSTYPE` 文件。然而，这只是我基本的反对意见。如果不同的 Linux 发行版需要不同的 `OSTYPE` 设置，那些发行版的开发者可以为他们自己的发行版创建一个包含正确设置的 `OSTYPE` 文件。毕竟，这正是 `OSTYPE` 文件的用途。没有理由认为不存在一个 `ostype/redhat.m4` 文件、一个 `ostype/suse.m4` 文件、一个 `ostype/slackware.m4` 文件，以及任何你可以想象的其他发行版的文件。你可能认为发行版开发者想把名字放在 `ostype` 目录中，但事实是，没有任何 Linux 发行版向 Sendmail 源码分发的 `ostype` 目录添加过 `OSTYPE`。

如列表 5.2 所示，`linux.m4` 的最后一行是一个 `FEATURE` 宏。该宏为配置添加的功能 `local_procmail`，它指定使用 `procmail` 作为本地邮件器。正如你将在第 11 章“处理垃圾邮件”中看到的，`procmail` 是一个非常强大的邮件器。Linux 使用 `procmail` 作为本地邮件器是一个加分项。`local_procmail` 特性接受最多三个可选参数：

- 邮件器的路径。分配给 `PROCMAIL_MAILER_PATH` 的路径值，在列表 5.2 中是 `/usr/bin/procmail`。通过以下 `FEATURE` 命令也可以获得相同的效果：

```
FEATURE(`local_procmail`, `/usr/bin/procmail`)
```

- 执行邮件器的命令行。默认值是 `procmail -Y -a $h -d $u`，其中如果使用 `user+address` 语法，`$h` 将被详细值替换，而 `$u` 将被收件人地址中的用户名替换。`$h` 和 `$u` 是 Sendmail 变量，用于存储标准投递三元组中的主机名和远程用户地址。在这种情况下，`procmail` 被用作本地邮件器。由于 `procmail` 被用作本地邮件器，因此没有主机名，使用 `$sh` 变量来存储详细值（参见附录 C，“Sendmail 变量、选项和标志”获取列表）。
- 邮件器的标志。默认值是 `hn`。（参见附录 C，“Sendmail 变量、选项和标志”获取列表）。

> 注意：使用 `local_procmail` 特性，`procmail` 被用作本地邮件器。命令行参数和邮件器标志是通过 `LOCALMAILER_FLAGS` 和 `LOCALMAILER_ARGS` 设置的，而不是通过 `PROCMAIL_MAILER_FLAGS` 和 `PROCMAIL_MAILER_ARGS`，后者用于 `MAILER (procmail)` 命令——尽管 `local_procmail` 使用的是 `PROCMAIL_MAILER_PATH` 而不是 `LOCALMAILER_PATH`。唉，没人说过 Sendmail 是容易的。

`linux.mx` `OSTYPE` 文件定义了程序 `procmail` 的目录路径以及一个使用 `procmail` 作为本地邮件器的特性。显然，`OSTYPE` 文件是查找文件名和邮件器选项的好地方。`linux.m4` 中的设置与我们在示例系统上尝试使用 `generic.cf` 文件时看到的问题无关，但 `linux.m4` 中的所有内容都值得理解，因为这些设置都会影响 Linux 系统的配置。

`generic-linux.mc` 加载的第二个 `m4` 源文件是来自 `domain` 目录的 `generic.m4` 文件。

`DOMAIN` 命令是可选的。它加载你创建的 `m4` 源文件以配置特定于你的域名或网络的值。你不需要创建 `DOMAIN` 源文件，但如果你有任何特定领域的处理，强烈建议你创建一个。

主机和用户名处理、域名伪装、邮件中继和反垃圾邮件功能是 `DOMAIN` 源文件中通常包含的信息类型。列表 5.3 显示了 `generic-linux.mc` 配置使用的 `generic.m4` `DOMAIN` 文件。

### 列表 5.3 `domain/generic.m4` 中的配置命令

```
[craig]$ tail -6 generic.m4

VERSIONID($id: generic.m4,v 8.15 1999/09/04 00:51:09 ca Exp '$')

define('FORWARD_PATH', '$z/.forward.w+$h:$z/.forward+$h:$z/
forward. $z/.'dn1
forward $z/.'dn1
define('conMAX_HEADERS_LENGTH', '32768')'dn1
FEATURE(`redirect`)'dn1
FEATURE(`use_cw_file`)'dn1
EXPOSED_USER(`root`)'dn1
```
