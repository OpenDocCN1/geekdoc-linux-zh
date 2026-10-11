
每个系统都有其自身的一组关键文件和目录。你需要评估你的环境并确定其需求。我们提供了一个示例，它应能为你提供一个相当好的起点，如示例 14-4 所示。请确保根据计算环境中各个系统的需求修改此示例；不要**原样**使用它。

此外，这里有一些提示，可能有助于你为环境组织 Tripwire 配置。

-   识别关键文件。
    -   如果文件仅用于只读或主要只读，请尝试 `r` 或类似的模板。
    -   如果文件频繁被修改且总是增大，请尝试掩码 `+p!nug~sa!mc0123456789`。
    -   如果文件频繁被修改，但大小不可预测，请尝试掩码 `+p!nug~sa!mc0123456789`。
-   识别关键目录；应用上述相同的规则。
-   如果不确定如何操作，请尝试 `r` 并根据需要修改。在所有情况下，你都会发现哪里需要更改，因为你的 Tripwire 比较模式输出会变得非常庞大！

## Red Hat Linux 的示例配置文件

示例 14-4 提供了一个更实际的 Linux `tw.config` 文件。请记住，这只是一个示例！你需要根据你站点的需求修改此文件。

既然我们已经对如何设置 Tripwire 配置文件有了很好的了解，让我们看看如何使用 `tripwire` 命令。

### 示例 14-4 Linux 的 tw.config 示例文件

```
# Tripwire configuration file
# Define our own templates
# Binary files
@@define BIN E+p!nugsc17
# Read template
@@define READ E+p!nugsm17
# Log files
@@define LOGS E+p!nug
# Config files
@@define CONFIG E+p!nugC
# Directory
@@define DIR E+p!nugi
# Device files
@@define DEV E+p!nugsc1
# root directory
/                     @@DIR
```

# /proc 变化很多，所以我们尽可能捕获它
/proc                 @@DIR
# 捕获这些目录
/tmp                  @@DIR
/mnt                  @@DIR
/mnt/cdrom            @@DIR
/mnt/floppy           @@DIR
/mnt/disk             @@DIR
/net                  @@DIR
/misc                 @@DIR
# root 的主目录 - 不会像 /home 那样经常变化
/root                 @@READ
# 关键启动资源，包括内核 (/boot/vmlinu)
/boot                 @@READ
# 关键配置目录和文件
# 我们使用 CONFIG 捕获大多数内容 & 修改
# 其余内容。
/etc                  @@CONFIG
/etc/inetd.conf       @@READ
/etc/rc.d             @@READ
/etc/exports          @@READ
/etc/mtab             @@LOGS
/etc/motd             @@LOGS
/etc/group            @@READ
/etc/passwd           @@LOGS
/etc/shadow           @@LOGS
/etc/security         @@READ
/etc/pam.d            @@READ
/etc/fstab            @@READ
/etc/cron.d           @@READ
/etc/cron.daily       @@READ
/etc/cron.hourly      @@READ
/etc/cron.monthly     @@READ
/etc/cron.weekly      @@READ
/etc/ftppers         @@READ
/etc/hosts            @@READ
/etc/hosts.allow      @@READ
/etc/hosts.deny       @@READ
/etc/login.defs       @@READ
/etc/logrotate.conf   @@READ
/etc/logrotate.d      @@READ
/etc/netconfig         @@READ
/etc/sendmail.cf       @@READ
/etc/shells           @@READ
/etc/sysconfig         @@READ
# 截断 home - 该目录有很多变化
/home                 @@READ
# var 树
/var/spool            @@LOGS
/var/log              @@LOGS
/var/spool/cron       @@LOGS
/var/spool/mqueue     @@LOGS
/var/spool/mail       @@LOGS
# 关键二进制文件和 /usr
/sbin                 @@READ
/bin                  @@READ
/lib                  @@READ
/usr                  @@READ
# 设备文件
/dev                  @@DEV
```

## Tripwire 命令

`tripwire` 命令可以接受许多选项。这些选项在表 14.4 中列出。通常，*tripwire* 以比较模式运行。当使用 `-initialize`、`-update`、`-E`（或 `-preprocess`）、`-help` 或 `-version` 选项时，情况则不然。当使用 `-interactive` 选项时，tripwire 首先以比较模式运行，然后以交互式更新模式运行。

接下来，我们将查看以三种运行模式运行 *tripwire*——即初始化、比较和更新。

**表 14.4 tripwire 命令的标志**

| 标志 | 描述 |
| :--- | :--- |
| `-initialize` | 生成数据库。这是初始化模式。 |
| `-update` *pathname* 或 *entry* | 这是更新模式。它更新数据库中指定的路径名或条目。如果使用 *pathname* 且它是文件，则只更新该文件。如果使用 *pathname* 且它是目录，则递归更新该目录及其 *pathname* 下的所有文件和目录。如果参数是配置文件中的一项 *entry*，则更新整个条目。 |
| `-interactive` | 此模式提供交互更新数据库的机会。它首先以比较模式运行，然后针对发现的每个差异询问用户是否应更新数据库。 |
| `-loosedir` | 此选项通过忽略大小、链接数、修改时间和 inode 改变时间来减少目录检查。这提高了性能，但有丢失重要信息的风险。 |
| `-d` *database* | 读取指定的数据库，而不是在默认位置查找（Red Hat 5.2/6.0 上的 */var/spool/tripwire*）。你可以使用 `-d -` 指定标准输入。 |
| `-c` *config* | 从 *config* 读取配置信息，而不是默认位置（Red Hat 5.2/6.0 上的 */etc/tw.conf*）。可以使用 `-c -` 指定标准输入。 |
| `-dfd` *openfd* | 从打开的文件描述符 *openfd* 读取数据库。这对压缩和加密非常有用。 |
| `-cfd` *openfd* | 从打开的文件描述符 *openfd* 读取配置信息。这对压缩和加密非常有用。 |
| `-D`*var*=*string* | 将变量 *var* 定义为 *string*。其作用等同于在配置文件中使用了 `@@define`。 |
| `-U`*var* | 取消定义变量 *var*。其作用等同于在配置文件中使用了 `@@undef`。 |
| `-i` # 或 all | 指示 *Tripwire* 忽略列出的签名编号（将 # 替换为签名编号）。必须提供逗号分隔的列表中的多个签名编号。使用 all 代替数字列表会抑制所有签名编号。此标志的目的是提高性能，但可能会丢失安全信息。 |
| `-E` 或 `-preprocess` | 仅预处理文件。输出到标准输出。 |
| `-q` | 抑制比较模式中的输出细节。每识别到一个异常只打印一行。特别是，不打印比较消息。 |
| `-v` | 详细模式。打印正在扫描的文件名。 |
| `-help` | 打印无编码解释帮助消息，然后退出。 |
| `-version` | 打印版本信息，然后退出。 |

## Tripwire 初始化模式

如第 382 页的 *Tripwire 概述* 中所述，初始化模式的目的是构建数据库。虽然这种模式使用频率不高，但正确地设置它很重要，因为现在生成的数据库随后将用于与系统中实际存在的内容进行比较。生成的数据库是 ASCII 格式。因此，可以手动读取。可能有这样或那样的场合这会非常有用，因为你随时可以进行手动检查。

示例 14-5 显示了 *Tripwire* 数据库初始化示例。请注意，在初始化的末尾，*Tripwire* 告诉你它将数据库放置在

### 示例 14-5 初始化 *Tripwire* 数据库

```
tripwire -v -initialize
### Phase 1: Reading configuration file
### Phase 2: Generating file list
### Phase 3: Creating file information database
scanning: /usr/local/bin
scanning: /usr/local/bin/opiekey
scanning: /usr/local/bin/otp-md4
...
<lots of output snipped>
...
###
### Warning: Database file placed in ./databases/tw.db_topcat.
###           Make sure to move this file and the configuration
###           to secure media!
###

(Tripwire expects to find it in '/var/spool/tripwire/.' )
```

