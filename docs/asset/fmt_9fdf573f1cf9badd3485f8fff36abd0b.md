
`sysv-rc-conf` 命令的示例输出

`sysv-rc-conf` 命令管理 Linux 系统上的 `service/runlevel` 配置。在上面的示例中，执行 `sysv-rc-conf` 会启动一个配置实用程序，允许用户选择在各个运行级别上启动哪些服务。

还可以使用 `--list` 和 `--level` 选项通过命令行显示和修改服务，如下一个示例所示。

```
# sysv-rc-conf --level 2345 apache off
# sysv-rc-conf --list apache2
apache2    2:off  3:off  4:off  5:off
# sysv-rc-conf --level 2345 apache2 on
# sysv-rc-conf --list apache2
apache2    2:on   3:on   4:on   5:on
```

使用 `sysv-rc-conf` 命令在命令行上管理服务

常用用法示例：

- `sysv-rc-conf`：显示运行级别配置实用程序
- `sysv-rc-conf --list`：列出所有服务的运行级别配置
- `sysv-rc-conf --level [LEVEL] [SERVICE] on`：在指定级别上启用服务
- `sysv-rc-conf --level [LEVEL] [SERVICE] off`：在指定级别上禁用服务

### chkconfig

用途：在基于 Red Hat Linux 的系统上显示和编辑运行级别配置。

使用语法：`chkconfig [OPTIONS] [SERVICE] [ON|OFF] [LEVEL]`

```
# chkconfig -1
```

| 服务 | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| acpi-support | off | off | on | on | on | on | off |
| acpid | off | off | on | on | on | on | off |
| alsa-utils | off | off | off | off | off | off | off |
| anacron | off | off | on | on | on | on | off |
| apache2 | off | off | off | off | off | off | off |
| apport | off | off | on | on | on | on | off |
| ... | | | | | | | |

使用 `chkconfig` 命令列出服务配置

`chkconfig` 命令管理 Red Hat Linux 系统上的服务。`-1` 参数列出当前的运行级别配置，如上面的示例所示。如果没有指定服务，将显示所有服务。指定服务名将显示该服务的运行级别配置，如下一个示例所示。

```
# chkconfig -1 apache2
```

| 服务 | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| apache2 | off | off | on | on | on | on | off |

使用 `chkconfig` 命令列出特定服务

`-s` 选项用于在指定的运行级别上启用或禁用服务，如下一个示例所示。

```
# chkconfig -s apache2 off 2345
# chkconfig -1 apache2
```

| 服务 | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| apache2 | off | off | off | off | off | off | off |

```
# chkconfig -s apache2 on 2345
# chkconfig -1 apache2
```

| 服务 | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| apache2 | off | off | on | on | on | on | off |

使用 `chkconfig` 命令管理服务

常用用法示例：

- `chkconfig -1`：列出所有服务的运行级别配置
- `chkconfig -1 [SERVICE]`：列出服务的当前配置
- `chkconfig -s [SERVICE] on [LEVEL]`：在指定级别上启用服务
- `chkconfig -s [SERVICE] off [LEVEL]`：在指定级别上禁用服务

### rc-status

用途：显示 Gentoo Linux 系统上服务的状态。

使用语法：`rc-status [OPTIONS]`

```
### rc-status
Runlevel: default
amavisd
                [ started ]
apache2
                [ started ]
clamd
                [ started ]
courier-authlib
                [ started ]
courier-imapd
                [ started ]
courier-imapd-ssl
                [ started ]
courier-pop3d
                [ started ]
hostname
                [ started ]
keymaps
                [ started ]
...
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_132_0.png)

`rc-status` 显示 Gentoo Linux 系统上服务的状态。在上面的示例中，列出了当前级别的所有服务及其当前状态。

> 注意：Gentoo Linux 使用一种非传统的 init 结构，与大多数 Linux 系统不同。您可以在 www.gentoo.org/doc/en/handbook/ 上在线阅读更多关于 Gentoo init 系统的信息。

常用用法示例：

- `rc-status`：列出当前运行级别的服务
- `rc-status -a`：列出所有服务
- `rc-status -l`：列出所有已定义的运行级别

### rc-update

用途：显示和编辑 Gentoo Linux 系统上的运行级别配置。

使用语法：`rc-update [OPTIONS] [SERVICE] [LEVEL]`

![](img/fa2f95b64a707c963dfa0445bd9281a7_133_0.png)

`rc-update` 命令管理基于 Gentoo Linux 的系统上的服务。在上面的示例中，使用 `show` 选项显示当前的运行级别配置。

`add` 和 `del` 选项用于将服务添加或删除到指定的运行级别，如下一个示例所示。

![](img/fa2f95b64a707c963dfa0445bd9281a7_133_1.png)

常用用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `rc-update show` | 列出所有服务的运行级别配置 |
| `rc-update add [SERVICE] default` | 将指定服务添加到默认运行级别 |
| `rc-update del [SERVICE] default` | 从默认运行级别中移除指定服务 |

### lssrc

用途：显示 AIX 系统上服务的状态。

使用语法：`lssrc [OPTIONS] [SERVICE/GROUP]`
