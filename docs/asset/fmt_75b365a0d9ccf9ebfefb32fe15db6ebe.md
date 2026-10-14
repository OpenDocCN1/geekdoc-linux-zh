
SuSE Linux 的主要配置可以通过 `/etc/sysconfig` 中的配置文件以及名为 `/etc/rc.config` 的中心配置文件来完成。在后者中，会设置一些对整个系统有效的环境变量。`/etc/init.d` 中的每个脚本都会首先执行 `/etc/rc.config`，以读取适用于自身的变量值。`/etc/rc.config` 还包含用户设置的变量。`/etc/sysconfig` 中的配置文件由单独脚本来解释，例如，ISDN 配置文件仅由 `isdn` 脚本读取。

> **注意**
>
> 从 SuSE Linux 6.0 开始，具有大量调整选项的软件包会将其变量存储在 `/etc/rc.config.d` 目录中的各个文件中。例如，`sendmail` 软件包或 `i4l`（ISDN）软件包就是这种情况。
>
> 不过，为了简化起见，我们通常只提及 `/etc/rc.config`，即使该文件已被移到其他地方。

此外，大量配置文件是根据 `/etc/rc.config` 和 `/etc/sysconfig` 中的设置生成的。这是 `/sbin/SuSEConfig` 的任务。例如，如果你更改了网络配置，文件 `/etc/hosts.conf` 会重新生成，因为它取决于你所做的配置。

因此，如果你手动更改了这些文件中的任何内容，之后需要运行 `/sbin/SuSEConfig`，以确保对相应配置文件的所有更改都发生在正确的位置。如果你使用 `YaST2` 更改配置，它会自动执行 `/sbin/SuSEConfig` 并更新你的配置文件。

这种概念使你无需重启系统即可对配置进行基本更改。由于某些更改相当复杂，可能需要重新启动某些程序才能使更改生效。如果网络配置已更改，可以使用以下命令重新启动网络程序：

```
earth:    # rcnetwork stop
earth:    # rcnetwork start
```

如你所见，你可以轻松地手动启动和停止 init 脚本。通常，我们建议按以下步骤配置系统：

- 将系统切换到*单用户模式*（运行级别 1）：

```
earth:    # init 1
```

- 按需修改配置文件。这可以使用你选择的编辑器完成。
- 执行 `/sbin/SuSEconfig` 使修改生效。如果你通过 `YaST2` 修改了 `/etc/rc.config`，则这一步骤会自动完成。
- 将系统恢复到之前的运行级别。

```
root@earth:   > init 3
```

此步骤主要在你更改了系统级设置（如网络配置）时相关。对于小改动，不必进入单用户模式，但这样做可以确保所有相关程序都被正确重启。

> **提示**
>
> 要禁用 SuSEconfig 的自动配置，请在 `/etc/sysconfig/suseconfig` 中将变量 `{ENABLE_SUSECONFIG}` 设置为 `no`。如果你想使用 SuSE 安装支持，请不要禁用 SuSEConfig。也可以部分禁用自动配置。

## 系统配置：脚本和变量

在本节中，我们介绍一些系统参数及其默认设置。如果你不使用 `YaST2` 修改 `/etc/rc.config` 或 `/etc/sysconfig` 中的配置文件，务必确保将空参数设置为两个引号（例如 `KEYTABLES=""`），并将包含空格的参数用引号括起来。只由一个词组成的参数则不必加引号。

### /etc/rc.config 中的基本设置

```
PATH="/sbin:/bin:/usr/sbin:/usr/bin"
```

该变量仅供内部使用。请不要更改它。

```
CHECK_PERMISSIONS="set"
```

定义是否对照 `/etc/permissions` 文件检查文件权限。设置为 `set` 时，错误的设置会被纠正。设置为 `warn` 时，仅发出“警告”。设置为 `no` 时，此功能被禁用。

```
PERMISSION_SECURITY="easy local"
```

在 `/etc/permissions.paranoid`、`/etc/permissions.secure` 和 `/etc/permissions.easy` 中，预定义了三个安全级别。请设置为 `easy`、`secure` 或 `paranoid`。如果你选择 `paranoid`，某些系统服务可能不再可用。如有需要，请显式启用它们。

要定义自己的设置，例如创建一个文件 `/etc/permissions.local`，然后将变量设置为 `local`。

> **注意**
>
> 如果你定义自己的 `/etc/permissions.local`，请确保你的设置与轮转机制（`logrotate` 软件包）不冲突。`logrotate` 会覆盖 `/etc/permissions.local` 中的设置。参见第 273 页的 *日志文件 — logrotate 软件包* 一节。

```
HALT_SOUND="no"
```

设置为 `yes` 或 `quint`，可在系统关机或重启时播放五度音音序；设置为 `octave`，则播放八度音。

```
CHECK_INITTAB="yes"
```

`SuSEconfig` 可以对 `/etc/inittab` 做一些修改。如果你不希望这样，请将此变量设置为 `no`。

```
CONSOLE_SHUTDOWN="reboot"
```

此变量决定 `init` 进程如何处理 [Ctrl] + [Alt] + [Del]。必须将 `CHECK_INITTAB` 设为 `yes` 才能激活此功能。可能的设置为 `ignore`、`reboot` 或 `halt`。默认值为 `reboot`。

```
DVB_SOUND_CHIP="ti"
```

选择 DVB 卡上的声音芯片 — `ti` 或 `crystal`。

```
START_FRONTBASE="no"
```

启动 FrontBase 和 FrontBase Web 服务吗？

```
IRCSERVER="sun.cosmos.com"
```

指定一个以空格分隔的 IRC 服务器列表（*互联网中继聊天*）。

```
SECCHK_USER="root"
```

此变量决定安全检查脚本的报告发送到哪个电子邮件地址。默认为 `root`。

```
START_SECCHK="yes"
```

此变量控制安全检查脚本是否应自动在每晚、每周或每月运行。设置为 `no` 可禁用。

```
KERNEL_LOGLEVEL="1"
```

`klogd` 的默认日志级别。

```
SYSLOGD_PARAMS=""
```

`syslogd` 的参数，例如 `"-r = my.dom.ain"`。

```
LOAD_MEMSTAT_MODULE="no"
```

启用此选项可在启动时自动为 `xosview` 加载 `memstat` 内核模块。

### /etc/sysconfig 中文件的设置

**suseconfig** – SuSEconfig 的设置。

```
ENABLE_SUSECONFIG="yes"
```

决定 SuSEconfig 是否负责更新配置。如果你想咨询我们的安装支持，请不要禁用 SuSEconfig。

```
MAIL_REPORTS_TO="root"
```

选择要将 SuSEconfig 在自动系统管理期间创建的电子邮件报告发送给哪个用户。

```
MAIL_LEVEL="warn"
```

如果只想发送重要消息，请将变量设置为 `warn`。如果日志文件也要通过邮件发送，请将其设置为 `all`。

```
CREATE_INFO_DIR="yes"
```

如果应使用 perl 脚本自动生成文件 `/usr/share/info/dir`，请将此变量设置为 `yes`。该文件是所有 info 页面的索引。

```
CREATE_JAVALINK="yes"
```

如果你将此变量设置为 `yes`，SuSEconfig 可以自动创建链接 `/usr/lib/java` 和 `/usr/lib/jre`，它们分别指向合适的 JDK 或 JRE。

```
CREATE_PERLLOCAL_POD="yes"
```

SuSEconfig 可以修改你的 `perllocal.pod` 吗？

```
UPDATE_GROFF_CONF="yes"
```

更新 DESC 以获得正确的页面尺寸吗？

```
GROFF_PAGESIZE=""
```

如果在你的 `printcap` 中找不到正确的页面尺寸，可以将此变量设置为 `groff` 和 `ghostscript` 均支持的以下值：`letter`、`legal`、`a4` 或 `b5`。

**`CHECK_ETC_HOSTS="yes"`**  

定义 SuSEconfig 是否应检查并修改 `/etc/hosts`。

**`BEAUTIFY_ETC_HOSTS="no"`**  

`/etc/hosts` 是否应由 SuSEconfig 排序？

**`SORT_PASSWD_BY_UID="no"`**  

如果此变量设置为 `yes`，SuSEConfig 会按“uid”和“gid”对 `/etc/passwd` 和 `/etc/group` 进行排序。

**`CWD_IN_ROOT_PATH="no"`**
