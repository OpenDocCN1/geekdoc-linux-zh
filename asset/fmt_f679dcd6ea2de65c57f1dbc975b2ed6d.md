
`/etc/rc` 使用一个名为 `rcorder` 的工具来定义资源配置脚本的执行顺序。要查看它们的执行顺序，输入 `rcorder /etc/rc.d/*`（这将列出按文件头列出的关键字和先决脚本定义的执行顺序排列的文件）。没有先决条件的脚本首先执行；随后是定义了较早脚本已运行的脚本。查看每个脚本中的 `PROVIDE`、`REQUIRE` 和 `KEYWORD` 行；参考 `man rcorder` 查看关于它们如何工作的更详细讨论，并参考 `man` 查看如何使用 `rcorder` 排序 FreeBSD 资源配置文件。

表 14.1 列出了原版 FreeBSD 6.x 系统中许多重要的资源配置文件。

| 脚本名称 | 描述 |
| :--- | :--- |
| `/etc/rc` | 主资源配置脚本，它从 `/etc/rc.conf` 读取配置设置并执行 `/etc/rc.d` 中的脚本。 |
| `/etc/rc.subr` | 一个包含的脚本，定义了位于 `/etc/rc.d` 中的许多脚本中使用的子程序。 |
| `/etc/defaults/rc.conf` | `init` 在执行早期读取此文件，以便在它的待办任务列表中查找内容。 |
| `/etc/rc.conf` | 这是全局配置文件，你通过编辑它来覆盖 `/etc/defaults/rc.conf` 中的默认值。 |

## 表 14.1 续

| 脚本名称 | 描述 |
| :--- | :--- |
| `/etc/rc.d/` | 守护进程的资源配置。此目录下的几十个脚本按 `rcorder` 定义的顺序执行。其中一些脚本的功能可以从名称 easily判断：`fsck` 磁盘检查，`named` 激活服务器，以此此类推。 |
| `/usr/local/etc/rc.d/` | 包含你编写（或添加第三方软件时安装）的新脚本的目录。 |

> 注意
>
> FreeBSD 5.0 之前的版本将配置文件放在 `/etc` 目录，并带有 rc 前缀。如果你正在使用 5.x 早期的 FreeBSD 版本，你可以选择使用旧的结构。在 `/etc/rc.conf` 中关闭 `rc_ng`（RC-Generation）选项，FreeBSD 将使用 `/etc.*` 文件而不是 `/etc/rc.d/*`。方法如下：

```
# Set rc="NO"
```

如果你不想承担新的启动结构导致不稳定的风险，这种技术可以向 FreeBSD 5.x 或 6.x 的过渡。然而，在新安装中没有理由关闭 `rc_ng` 选项，实际上在 FreeBSD 5.2 中该选项不存在。

## `/etc/defaults/rc.conf` 文件

资源配置脚本由两个位置指定的全局系统设置控制：`/etc/defaults/rc.conf` 和 `/etc/rc.conf`。前者是系统的一部分，不应修改；后者是你的全局配置文件，其设置控制了系统相对于默认配置运行的所有变体。

使用你喜喜欢的文本编辑器查看一些资源配置脚本（例如 `/etc/rc.d/named`）。你会看到每个脚本都是完全自动化的；它通过检查定义系统配置的变量或文件来工作。如果这些变量或文件存在，它就会执行一个预定义的、抽象循环，该循环从这些变量和文件中获取参数。`/etc/rc` 或任何标准脚本都不应被编辑。

## 资源配置脚本

对系统的任何修改都将在全局配置文件中进行。然而，随着可用变量列表的增长以及文件角色的扩展，这种安排很快变得难以管理。管理员在升级系统时，必须费力地将旧的 `rc.conf` 与新文件合并——这与最初直接编辑 `/etc/rc.conf` 相比，几乎没有任何改进之处。

因此，解决方案是创建一个 `/etc/defaults` 目录，并将一个包含所有默认设置的 `rc.conf` 副本放入其中。现在，`/etc/rc.conf` 仍然存在，但它是作为一个叠加层（overlay）存在的其内容（如果存在的话）优于 `/etc/defaults/rc.conf` 中的设置。例如，如果在 `/etc/defaults/rc.conf` 中出现 `name_enable="NO"` 设置，你将通过将该设置改为 `/etc/rc.conf` 中的设置来开启服务器。后者的设置将覆盖前一个文件中的默认设置。即使没有每一个 `/etc/rc.conf` 文件，FreeBSD 也可以运行，但通常你将使用它进行网络配置（IP 地址、主机名、网关地址等）以及运行诸如 Sendmail 和 ssh 等守护进程。

查看 `/etc/defaults/rc.conf` 中的一个典型块，如列表 14.1 所示。

## 列表 14.1 `/etc/defaults/rc.conf` 节选

```
# named. 可能可以在沙箱中运行 named，详情请参 man security。
#
named_enable="NO"                  # 运行 named，即 DNS 服务器（或为 NO）。
named_program="/usr/sbin/named"    # named 的路径，如果你想使用不同的程序。
named_flags="u bind"               # named 的标志
named_pidfile="/var/run/named/pid" # 必须在此 named.conf 中也设置
named_chroot="/var/named"         # Chroot 目录（或为 "" 以不自动 chroot）
named_chroot_autoupdate="YES"      # 自动安装/更新 named 的 chroot
                                     # 组件。参阅 /etc/rc.d/named。
named_symlink_enable="YES"          # 为 chroot pid 文件创建符号链接
```

通过 `/etc/defaults/rc.conf`，你可以发现对于在 `/etc/rc.d` 中带有启动脚本的每个服务，`/etc/rc.conf` 将是默认的。在这种情况下，默认行为是完全不运行它。

通常，在 `/etc/defaults/rc.conf` 中，变量被分组为如下所示块，通过前缀保持它们的相关性，并在文件顶部使用单个 `"YES"`/`"NO"` 变量作为文件的“主开关”。如果该变量被设置为 `"NO"`，通常其余的变量都将不再重要；如果它被设置为 `"YES"`，除非被注释掉，否则所有变量都生效。被注释的行通常作为示例提供，以展示可能的替代用法，正如 `syslog` 块中的行所示：

```
syslog_flags="-s"                  # syslog 的标志（如果已启用）。
syslog_flags="-ss"               # 不绑定 inet socket 的 syslog 标志
```

![](img/77bd66253135c18493b7c99c3f112b77_436_0.png)

## `/etc/rc.conf` 文件

假设你想运行 `named`。在最简单的情况下，你只需需要编辑 `/etc/rc.conf`（“覆盖”文件）并在文件的任何位置添加以下行：

```
named_enable="YES"
```

`/etc/defaults/rc.conf` 中其余的 `named_*` 变量不需要复制到覆盖文件中。记住，“defaults”文件中的每个变量都会被 `init` 加载到内存中，只有当该块的“主开关”被设置为 `"YES"` 时，它们才会生效。在这种情况下，默认变量将在 `/etc/rc.d` 中相应脚本的执行循环中使用，以启动由你正在操作的块所控制的任何进程（在本例中为 `named`）。

## 注意事项

当你折腾 `/etc/rc.conf` 时，手头保留一个备份是一个非常好的主意，这样你就可以轻松恢复到已知的系统配置。在开始操作之前，只需复制现有文件即可创建一个备份文件（此示例文件名包含了当前日期，以便你准确追溯操作步骤）：

```
# cp /etc/rc.conf /etc/rc.conf.backup.20060127
```

要切换回备份版本，或将其移动（重命名）回原始名称：

```
# mv /etc/rc.conf.backup.20060127 /etc/rc.conf
```

或者，每当你更改 `/etc/rc.conf` 中的某行时，复制该行并注释掉未修改的旧行。这样如果你的新设置不起作用，你始终可以回到原始设置。

你可以使用这些变量进行微调，并同样轻松地覆盖它们。假设你的名称服务器是一个名为 `named` 的自定义版本。意图是让 `named` 服务器以此用户和 `bind` 组身份运行，这样它就不会受到许多权限相关漏洞的影响。为了处理这一点（假设 `named` 具有与 `named` 相同的行为和命令行选项），你只需要向 `/etc/rc.conf` 中添加以下两行：

```
named_program="named"
named_flags="-u bind"
```
