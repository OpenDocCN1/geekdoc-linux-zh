
# ps -aux

# ps -aux | grep 'httpd'

在 Mandrake、SuSE、Caldera 和 Red Hat Linux 系统上，你使用特殊的脚本手动启动和停止服务器。这些脚本位于 `/etc/rc.d/init.d` 目录（SuSE 为 `/etc/rc.d`），并且名称与服务器程序相同。例如，带有 `start` 选项的 `/etc/rc.d/init.d/httpd` 脚本会启动 Web 服务器（SuSE 为 `/etc/rc.d/httpd`）。使用带有 `stop` 选项的该脚本则会停止它。在 Red Hat 和 Mandrake 上，无需使用脚本的完整路径，可以使用 `service` 命令和脚本名称。以下命令是等效的。

```bash
/etc/rc.d/init.d/httpd stop
service httpd stop
```

与其每次启动系统时都手动执行所有服务器程序，不如让系统自动为你启动服务器。你可以通过两种方式实现此，取决于你想如何使用服务器。你可以让服务器从启动系统到关机一直持续运行。

自动启动并持续运行的服务器被称为独立服务器（standalone server）。Mandrake、Caldera、SuSE 和 Red Hat 使用 System Init 过程在系统启动时启动服务器。该过程使用位于 `/etc/rc.d/init.d`（SuSE 为 `/etc/rc.d`）的启动脚本。大多数 Linux 系统默认配置 Web 服务器自动启动并持续运行。此对应的脚本称为 `httpd`，位于 `/etc/rc.d/init.d`。

要仅在接收到服务请求时启动服务器，你需要使用 `xinetd` 或 `inetd` 守护进程进行配置。`xinetd` 守护进程是 `inetd` 的更新版本，用于 Mandrake 和 Red Hat。如果你在 `xinetd.d` 文件中添加、更改或删除服务器条目，你必须重启 `xinetd` 守护进程使更改生效。你可以使用 `/etc/rc.d/init.d/xinetd` 脚本配合 `restart` 命令来重启 `xinetd` 守护进程，如下所示：

```bash
# service xinetd restart
```

你也可以使用 `xinetd` 脚本启动和停止 `xinetd` 守护进程。这将有效关闭 `xinetd` 守护进程管理的所有服务器（在 `/etc/xinetd.conf` 文件或 `inetd.d` 目录列出的服务器）。

```bash
# service xinetd stop
# service xinetd start
```

你还可以通过向进程发送 `SIGHUP` 信号直接重启 `inetd`，强制其重启。你需要使用 `kill` 命令配合 `-HUP` 选项和 `inetd` 守护进程的 PID。你可以使用 `ps -aux` 命令列出所有进程，然后使用 `grep` 定位 `inetd` 条目，如下所示。此处 PID 将存储在 `/var/run/inetd.pid` 文件中。

```bash
# ps -aux | grep inetd
# kill -HUP inetd-process-id
```

> 注意早期版本的 Linux 系统使用 `inetd` 守护进程（术语代表互联网服务守护进程）而不是 `xinetd`。`xinetd` 旨在作为 `inetd` 的增强版。如果你正在升级到 `xinetd`，可以使用 `inetdconvert` 命令将 `inetd` 条目转换为 `xinetd` 配置。

## 服务管理工具：chkconfig 和 System V Init

在大多数发行版中，KDE System V Init 编辑器和 `chkconfig` 命令提供了简单的接口，供你选择启动哪些服务器以及希望它们在何时启动。此外，大多数发行版还提供了自己的工具，例如 Red Hat 上的 `serviceconfig`、Mandrake 控制中心上的服务面板，或 YaST 控制中心。你也可以使用 Linux 和 Webmin 来进行这些更改。你使用这些工具来控制启动的任何守护进程，包括系统服务如 `cron`、打印服务器、用于 Samba 和 NFS 的远程文件服务、Kerberos 的身份验证服务，当然还有 FTP 或 HTTP 的 Internet 客户端。这些守护进程被称为服务，你应该将它们视为管理这些服务的工具。其中任何一个服务都可以设置为在不同级别下启动或在特定级别启动。

这些工具管理由 `/etc/rc.d/init.d` 目录下的脚本启动的服务。如果你添加了一个新服务，`chkconfig` 和 System V Init 编辑器可以管理其在各种运行级别（runlevels）下的启动。这些链接指向 `init.d` 目录中的启动脚本。运行级别目录从 0 到 6，其中 `/etc/rc.d/rc3` 对应级别 3，`/etc/rc.d/rc5` 对应级别 5。从运行级别中删除服务仅会在相应的 `rc.d` 目录中重建 S85 链接。它不会触动 `init.d` 目录中的启动脚本。在指定的运行级别启动服务器会将链接放回运行级别目录。例如，如果你指定 `httpd` 不再运行级别 3 启动，则 `rc3.d` 目录中的 `S85httpd` 链接将被删除。让 `httpd` 在运行级别 5 启动会在 `rc5.d` 目录中重建 `S85httpd` 链接。更多细节请参阅后续关于 SysV Init 脚本章节，有关运行级别的更多信息请参考第 25 章。

## chkconfig

通过 `chkconfig` 命令，你可以指定想要启动的服务器以及启动它的级别。与其他服务管理工具不同，`chkconfig` 在独立模式和 `xinetd` 下工作效果同样良好。虽然独立服务可以在任何运行级别运行，你也可以在 `xinetd` 运行的运行级别上开启或关闭 `xinetd` 服务。表 1-19 列出了不同的 `chkconfig` 选项。

你使用该选项让服务在某些运行级别下启动，或不启动。你可以通过 `--level` 选项指定要影响的运行级别。如果没有指定级别，`chkconfig` 将使用服务 `init.d` 启动脚本中的任何 `chkconfig` 默认信息。Mandrake 和 Red Hat 会安装这些缺失的信息（如果缺失，`chkconfig` 将使用运行级别 3、4 和 5）。下面的示例将使 Web 服务器 (httpd) 在运行级别 5 启动。

- `chkconfig --level 5 httpd on`

### 表 19-1 chkconfig 选项

| 选项 | 说明 |
|---|---|
| `--level runlevel` | 指定一个运行级别，以开启、关闭或重置服务。 |
| `--list service` | 列出不同运行级别下服务的启动信息。xinetd 服务仅为开启或关闭。不带参数时，将列出所有服务，包括 xinetd。 |
| `--add service` | 添加服务，在指定的默认运行级别（或在未指定时）中创建链接。 |
| `--del service` | 删除所有运行级别目录中该服务的所有链接（启动和关闭）。 |
| `service on` | 开启服务，在指定的或默认运行级别目录中创建启动链接。 |
| `service off` | 关闭服务，在指定的或默认运行级别目录中创建关闭链接。 |
| `service reset` | 重置服务启动信息，根据服务 `init.d` 启动脚本中 `chkconfig` 条目中的指定创建默认链接。 |

`off` 选项实际上会配置服务在进入指定的运行级别时关闭。接下来的示例将在进入运行级别 3 时关闭 Web 服务器。如果它未在运行，则将保持关闭状态。

```bash
chkconfig --level 3 httpd off
```

`reset` 选项将把服务恢复到其服务 `init.d` 启动脚本中指定的 `chkconfig` 默认选项。

```bash
chkconfig wu-ftpd reset
```

若只想查看某个服务的启动信息，你只需配合 `--list` 选项使用服务名。

```bash
chkconfig --list httpd
httpd 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

## 第 19 章：服务器管理

与 System V Init 编辑器不同，`chkconfig` 也具有启用或禁用 `xinetd` 服务的能力。只需带有 `on` 或 `off` 选项输入 `xinetd` 服务。该服务将被启动或关闭，其位于 `/etc/xinetd.d/` 目录下的 `xinetd` 配置脚本将相应编辑禁用行。例如，要启动运行在 `xinetd` 上的 Samba 配置服务器 `swat`，只需输入：

```bash
chkconfig swat
chkconfig --list swat
swat on
```

`xinetd` 的 `swat` 配置文件 `/etc/xinetd.d/swat` 的禁用行将被编辑为 `no`，如下所示。

```
disable=no
```

如果你想关闭 `swat` 服务器，可以使用 `off` 选项。

```bash
chkconfig off
```

当用户在没有指定级别选项的情况下启动 `httpd` 服务时，`chkconfig` 将在运行级别（runlevels）3、4 和 5 上启动 `httpd`。

- `chkconfig httpd on`

还应该添加一个描述行，`chkconfig` 可以使用该行来描述该服务。在描述中，你输入对服务的简短描述，并在换行前使用 `\` 符号来使用多行内容。

```bash
# description: Apache 是一个万网 Web 服务器。它用于提供 \
# HTML文件 CGI.
```

## System V 初始化编辑器

KDE 系统初始化编辑器（System Init Editor）提供了一个 GUI 界面，允许你管理系统上的任何守护进程——作为系统守护进程的 Internet 服务器，例如打印服务器。初始化编辑器分为三个主要窗格。左侧是一个标记为“available”（可用）的滚动窗口，列出了系统上所有可用的守护进程。这些包括 Internet 服务器的守护进程，例如 `httpd`。右侧占据了窗口的大部分，分为上半部分和下半部分。上半部分有滚动窗口，每个对应一个运行级别。这些是当前配置在各自运行级别运行的守护进程。下半部分也包含滚动窗口，每个对应一个运行级别。这些是在切换到该运行级别时将关闭的进程。系统管理员可以在一个运行级别切换到另一个运行级别。在正常处理下启动的所有服务器都列在启动运行级别 5（图形登录）和运行级别 3（命令行）滚动窗口中。图 19-1 显示了 System V 初始化编辑器。

一个名为 System V Runlevel Editor 的旧程序仍在某些发行版中使用。它的运行方式与 System V 初始化编辑器相似，但有几处不同。

你可以配置服务器在进入特定运行级别时自动启动。你的系统运行在某些运行级别，每个级别由指定的数字指定，例如多用户级（运行级别 3）、图形登录级（运行级别 5）和管理级（运行级别 1）。有关运行级别的讨论，请参见第 25 章。要让服务器在指定的运行级别运行，请将其拖入你希望其启动的运行级别的可用滚动窗口中。例如，如果你使用图形登录，启动时的运行级别是 5。要让 Web 服务器 `httpd` 在每次启动系统时都自动启动，请检查它是否在运行级别 5 启动滚动窗口中。如果没有，将 `httpd` 条目拖入运行级别 5 启动滚动窗口的可用窗口中。在该窗口中选择一个有可用数字的位置，例如 15 或 17 之间，或者滚动窗口的末尾。滚动窗口中会出现一个 `httpd` 条目。如果你不希望

Linux: The Complete Reference（Linux 完全参考）

```bash
/etc/rc.d/init.d/httpd start
Starting httpd
[OK]
```
