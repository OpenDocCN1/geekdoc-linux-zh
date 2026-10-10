
# 探索单元文件

开始探索 systemd 的最简单方法是通过 *systemd 单元*。单元定义了服务、服务组或操作。每个单元由名称、类型和配置文件组成。目前有 12 种不同的 systemd 单元类型，如下所示：

- automount（自动挂载）
- device（设备）
- mount（挂载）
- path（路径）
- scope（作用域）
- service（服务）
- slice（切片）
- snapshot（快照）
- socket（套接字）
- swap（交换）
- target（目标）
- timer（定时器）

`systemctl` 实用程序是管理 systemd 和系统服务的主要入口。其基本语法如下：

```
systemctl [OPTIONS...] COMMAND [NAME...]
```

您可以使用 `systemctl` 实用程序提供当前在您的 Linux 系统中加载的各种单元列表。Listing 6.4 展示了一个简化的示例。

**Listing 6.4** 查看 systemd 单元

```
$ systemctl list-units
UNIT                        LOAD    ACTIVE SUB     DESCRIPTION
[...]                       
smartd.service              loaded  active running Self Monitor[...]
sshd.service                loaded  active running OpenSSH serv[...]
sysstat.service             loaded  active exited  Resets Syste[...]
[...]
graphical.target            loaded  active active    Graphical I[...]
[...]
$ 
```

在 Listing 6.4 中，您可以看到各种单元以及附加信息。单元通过 *name.type*（名称.类型）格式由其名称和类型标识。系统服务（守护进程）的单元文件具有 `.service` 扩展名。因此，安全 shell (SSH) 守护进程 `sshd` 的单元文件名为 `sshd.service`。

来自 `systemctl` 实用程序的许多显示默认使用 `less` 分页器。因此，要退出显示，您必须按 `q` 键。如果您想关闭 `systemctl` 实用程序使用 `less` 分页器的功能，请在命令末尾添加 `--no-pager` 选项。

服务组通过 target 单元文件启动。在系统启动时，`default.target` 单元负责确保在系统初始化时启动所有必需和期望的服务。它被设置指向另一个 target 单元文件的符号链接，如 Ubuntu 发行版上的 Listing 6.5 所示。

**Listing 6.5** 查看 default.target 链接

```
$ find / -name default.target 2>/dev/null
/usr/lib/systemd/system/default.target
[…]
$ readlink -f /usr/lib/systemd/system/default.target
/usr/lib/systemd/system/graphical.target
$ systemctl get-default
graphical.target
$ 
```

首先，在 Listing 6.5 中，`find` 实用程序用于定位 `default.target` 单元文件的完整文件名。然后使用 `readlink` 命令找到实际的目标文件，该文件决定了系统启动时启动哪些服务。在这种情况下，目标单元文件是 `graphical.target`。

同样，请注意 Listing 6.5 中 `systemctl` 命令比另外两个命令更容易使用。它只是 `systemctl get-default`，并显示实际的目标文件。由于 `default.target` 文件位于不同发行版的不同目录中，最好始终使用 `systemctl` 实用程序。Table 6.1 展示了更常用的系统启动 target 单元文件。

**TABLE 6.1** 常用系统启动 target 单元文件

| 名称 | 描述 |
|:---|:---|
| graphical.target | 通过本地终端和/或网络为多用户提供系统访问权限。提供图形用户界面 (GUI) 访问。 |
| multi-user.target | 通过本地终端和/或网络为多用户提供系统访问权限。不提供 GUI 访问。 |
| network-online.target | 提供一个在系统建立网络连接后运行的 target。这对于启动需要网络存在的应用程序非常有用。 |
| runleveln.target | 提供对 SysV init 系统的向后兼容性，其中 n 设置为 1–6，以表示所需的 SysV 运行级别等效项。 |

在 Table 6.1 中，您会注意到 systemd 提供了对经典 SysV init 系统的向后兼容性。SysV 运行级别将在本章后面涵盖。

> **提示**
> systemd 的主配置文件是 /etc/systemd/system.conf 文件。在这个文件中，您可以发现所有默认配置设置都通过井号 (#) 被注释掉了。查看此文件是了解当前 systemd 配置的快速方法。如果需要修改配置，只需编辑该文件即可。不过，明智的做法是先在命令行输入 `man systemd-system.conf` 查阅该文件的 man 手册页。

### 聚焦服务单元文件

服务单元文件包含信息，例如使用哪个环境文件、何时必须启动服务、哪些 target 希望启动此服务等。这些配置文件位于不同的目录中。

请记住，单元配置文件的目录位置至关重要，因为如果文件在两个不同的目录位置中找到，其中一个将优先于另一个。以下列表按优先级从低到高显示了目录位置：

1. /etc/systemd/system/
2. /run/systemd/system/
3. /usr/lib/systemd/system/

要查看可用的各种服务单元文件，您可以再次使用 `systemctl` 实用程序。然而，与查看单元时所需的命令略有不同，如 Listing 6.6 所示。

**Listing 6.6** 查看 systemd 单元文件

```
$ systemctl list-unit-files
UNIT FILE                    STATE
[...]                        
dev-hugepages.mount        static
dev-mqueue.mount           static
proc-fs-nfsd.mount         static
[...]                        
nfs.service                  disabled
nfslock.service              static
ntpd.service                 disabled
ntpdate.service              disabled
[...]                        
ctrl-alt-del.target        static
default.target               static
emergency.target             static
[...]                        
```

除了单元文件的基本名称外，您还可以在 Listing 6.6 中看到单元文件的状态。这些状态被称为启用状态（enablement states），指的是服务启动的时机。至少有 12 种不同的启用状态，但您通常会看到这三种：

- enabled：服务在系统启动时启动。
- disabled：服务不在系统启动时启动。
- static：如果另一个单元依赖于它，则服务启动。也可以手动启动。

要查看存储特定 systemd 单元文件的目录，请使用 `systemctl` 实用程序。Ubuntu 发行版上的示例如 Listing 6.7 所示。

**Listing 6.7** 查找并显示 systemd 单元文件

```
$ systemctl cat cron.service
# /lib/systemd/system/cron.service
[Unit]
Description=Regular background program processing daemon
Documentation=man:cron(8)
After=remote-fs.target nss-user-lookup.target
[Service]
EnvironmentFile=-/etc/default/cron
ExecStart=/usr/sbin/cron -f $EXTRA_OPTS
IgnoreSIGPIPE=false
KillMode=process
Restart=on-failure
[Install]
WantedBy=multi-user.target
$ 
```

请注意，在 Listing 6.7 中，第一行显示 `cron.service` 单元文件的基本名称和目录位置。接下来的几行是单元配置文件的内容。

对于服务单元文件，有三个主要的配置部分：

- [Unit]
- [Service]
- [Install]

在单元配置文件的 [Unit] 部分中，有基本的 *指令*（directives）。指令是修改配置的设置，例如 Listing 6.7 中显示的 After 设置。Table 6.2 描述了常用的 [Unit] 部分指令。

**TABLE 6.2** 常用服务单元文件 `[Unit]` 部分指令

| 指令 | 描述 |
|---|---|
| `After` | 设置此单元在指定单元之后启动。 |
| `Before` | 设置此单元在指定单元之前启动。 |
| `Description` | 描述单元。 |
| `Documentation` | 设置一个指向文档来源的统一资源标识符 (URI) 列表。URI 可以是网络位置、特定系统文件、info 页面和 man 手册页。 |
| `Conflicts` | 设置此单元不与指定单元一起启动。如果指定的任何单元启动，此单元将不会启动。（`Requires` 的反义。） |
| `Requires` | 设置此单元与指定单元一起启动。如果指定的任何单元未启动，此单元将*未启动*。（`Conflicts` 的反义。） |
| `Wants` | 设置此单元与*指定*单元一起启动。如果指定的任何单元未启动，此单元*仍然*启动。 |

![](img/c0a399aca0d18f8822d714ad0a173123_229_0.png)

> systemd 和单元配置文件的 man 手册页中包含大量有用的信息。只需输入 `man -k systemd` 即可找到若干您可以探索的项目。例如，使用 `man systemd.service` 命令探索 service 类型单元文件指令及其他内容。您可以在命令行输入 `man systemd.directives` 查找有关各种指令的信息。

单元文件中的 `[Service]` 指令设置了特定于该服务的配置项。Table 6.3 描述了常用的 `[Service]` 部分指令。

**TABLE 6.3** 常用服务单元文件 `[Service]` 部分指令

| 指令 | 描述 |
|---|---|
| `ExecReload` | 指示在单元重新加载时运行的脚本或命令（以及选项）。 |
| `ExecStart` | 指示在单元启动时运行的脚本或命令（以及选项）。 |
| `ExecStop` | 指示在单元停止时运行的脚本或命令（以及选项）。 |
| `Environment` | 设置环境变量替代项，以空格分隔。 |

