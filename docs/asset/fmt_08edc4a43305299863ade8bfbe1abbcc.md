
| Client rpc | calls | badcalls | retrans | badx | timeout | wait | newcwd | timers |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 64235 | 1595 | 0 | 3 | 1592 | 0 | 0 | 886 | |

| Client nfs | calls | badcalls | nclget | nclsleep | | | lookup | root | read |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 62613 | 3 | 62643 | 0 | | | | | |
| 04% | | gettr | setattr | readlink | 21% | 30% | 0% | 2% |
| write | wrcache | create | | rename | link | symlink | | | |
| 3% | | 0% | 0% | | nfsat | | 0% | | |
| mkdir | readdir | | rmdir | | | | | | |
| 0% | | 0% | 0% | | | | | | |

此示例来自一个相对健康的 NFS 客户端。如果超过 3% 的 RPC 调用超时，可能是你的 NFS 服务器或网络存在问题。你可以通过检查 `badx` 字段轻松地发现原因。如果 `badx` 接近 0 且超时大于 3%，则发往和来自服务器的数据包在网络上丢失了。你可能可以通过增加超时时间来解决这个问题。

# 18.7 专用 NFS 服务器

快速文件服务是生产环境中的基本要素。专用 NFS 服务器已经存在多年。虽然你可以自己创建，但通常使用专用设备更好：

- 它们在大型网络中提供可靠的服务。
- 它们随着需求增长而平滑扩展。
- 它们更容易管理。
- 它们提供了集成的备份功能。

# 18.8 自动挂载

为了实现后台的挂载和卸载，自动挂载器使用虚拟文件系统。首先，在许多台机器上维护 `fstab` 是非常乏味的。其次，如果文件系统从不同的主机挂载，自动挂载器可能会挂起。第三，当服务器崩溃时，它可能会影响用户。

自动化文件系统通过一个独立的守护进程 `automountd` 进行处理。该守护进程静默工作，不需要额外的配置。

在 Linux 系统上，该守护进程称为 `automount`，设置函数由 `/etc/init.d/autofs` 脚本执行。有关 Linux 的详细信息请参阅第 717 页的“Linux”章节。在随后的讨论中，我们将设置命令称为 `automount`，将守护进程称为 `auto:intd`。

如果你更改了主映射（master map）或其引用的某个直接映射（direct map），必须重新运行 `automount` 以应用更改。使用 `-v`，`automount` 将向你显示它对配置进行的调整。

`automount` 还接受 `-t` 参数，告知自动文件系统在被移除之前可以闲置多长时间（秒）。默认值通常为 10 分钟。由于崩溃的 NFS 挂载可能会导致程序访问它，因此清理不再使用的 automount 是一种良好的习惯；不要将超时时间设置得太长。

## 直接映射 (Direct maps)

直接映射将多个文件系统挂载到一个公共目录之下。然而，目录的路径是在主文件本身中指定的。例如，挂载在 `/chimchim` 下的文件系统的间接映射可能看起来如下所示：

- users harp/harp/users
- devel -soft harp/harp/devel
- info -ro harp/harp/info

第一列列出了每个 automount 应该安装的子目录，后续项目列出了挂载选项和文件系统的 NFS 路径。此示例（可能还有存储在 `/etc/auto.harp` 中的其他）告诉 `automount` 它可以从服务器 `harp` 挂载 `/harp/users`、`/harp/devel` 和 `/harp/info` 目录，其中 `info` 以只读方式挂载，`devel` 以软（soft）方式挂载。

在此配置中，`chimchim` 和本地主机上的路径是相同的。但这种对应并非必须。

## 直接映射 (Direct maps)

直接映射列出了不共享公共前缀的文件系统，例如 `/usr/src` 和 `/tools`。一个描述这两个文件系统的直接映射（例如 `/etc/auto.direct`）向 `automount` 描述它们时可能如下所示：

```
/usr/src harp/usr/src

/cs/tools -ro monk:/cs/tools
```

> 就此的另一方面是，挂载文件系统需要一定的时间。如果文件系统不是不断重新挂载，系统响应将更快、更流畅。

## 第 18 章 网络文件系统 (The Network File System)

由于它们不共享公共父目录，每个 automount 必须通过单独的 autofs 挂载。这种配置需要更多的开销，但它的额外优点是挂载点和目录结构对于 `ls` 等命令始终是可见的。在充满间接映射的目录上使用会让用户感到困惑，因为 `automount` 在访问其内容之前不会显示子目录（它不会查看自动挂载目录的内部，因此不会导致它们被挂载）。

## 主映射 (Master maps)

主映射列出了 `automount` 应该关注的直接映射和间接映射。对于每个间接映射，它还指定了映射中定义的映射的根目录。

一个使用之前示例所示直接和间接映射的主映射可能如下所示：

```
# Directory Map

/harp /etc/auto.harp -proto=tcp

/etc/auto.direct
```

第一列是间接映射的本地目录名，或者是代表所有内容的特殊标记 `/-`。第二列标识存储映射的文件。你可以对每种类型拥有多个映射。当你在行尾指定挂载选项时，它们将设置该挂载内所有映射的默认值。Linux 管理员应始终为 NFS 第 4 版本服务器指定 `-fstype=nfs4` 挂载标志。

> 映射条目上的选项不会与其所指向的直接或间接映射中指定的选项混合。如果映射条目有自己的选项列表，则会忽略默认值。Linux 合并这两组设置。如果由于由于在两个地方都指定了相同的选项，则映射条目的值将覆盖默认值。

主映射通常可以通过 NIS 共享的版本进行替换或增强。详情请参阅你的文档。

## 可执行映射 (Executable maps)

如果一个映射是可执行的，则假设它是一个动态生成 automount 信息的脚本或程序。自动挂载器不会将映射作为文本文件读取，而是带有一个参数（“键”）来执行它，该参数指示了用户尝试访问哪个子目录。脚本负责打印相应的映射条目；如果指定的键无效，脚本可以简单退出而不打印任何内容。

这一强大功能弥补了自动挂载器相当奇怪的配置系统的许多缺陷。实际上，它允许你以任选格式定义全站范围的 automount 配置。你可以编写一个简单的脚本来解码每台机器上的全局配置。

## 复制文件系统自动挂载

系统带有一个实用的 `/etc/auto.net` 可执行映射，它将主机名作为键并挂载该主机上的所有文件系统。

由于 automount 脚本根据需要动态运行，因此没有在每次更改后分发配置文件或预先转换为 automount 格式；事实上，全局配置文件可以在 NFS 服务器上有一个永久的所在地。

## Automount 可见性 (Automount visibility)

当你列出自动挂载文件系统的父目录内容时，无论挂载了多少文件系统，目录看起来都是空的。你无法在 GUI 文件系统浏览器中浏览 automount。

一个示例：

```
$ /portal

$ /portal/photos

art_class_2010 florissant_1003 rmnop03

blizzard2008 frozen_dead_guy
```

当你列出自动挂载文件系统的父目录内容时，无论挂载了多少文件系统，目录看起来都是空的。你无法在 GUI 文件系统浏览器中浏览 automount。

一个示例：

```
$ /portal

$ /portal/photos

art_class_2010 florissant_1003 rmnop03

blizzard2008 frozen_dead_guy
```

自动挂载的目录是可见的。

当你列出自动挂载文件系统的父目录内容时，无论挂载了多少文件系统，目录看起来都是空的。你无法在 GUI 文件系统浏览器中浏览 automount。

一个示例：

```
$ /portal

$ /portal/photos

art_class_2010 florissant_1003 rmnop03

blizzard2008 frozen_dead_guy
```

自动挂载的目录是可见的。

## 复制文件系统自动挂载 (Replicated filesystems automount)

在某些情况下，只读文件系统如 `/usr/share` 是可见的。

## 第 18 章 网络文件系统 (The Network File System)

在 Solaris 和 HP-UX 下，`automount` 可以在服务器之间流畅切换，这也是读写挂载可能没用的另一个原因。

尽管 `automount` 可以根据效率标准在复制服务器之间进行选择，但你也可以分配式优先级。优先级是小的整数，数字越大优先级越低。默认优先级为 0，最优先。

`auto.direct` 文件定义 `/usr/man` 和 `/cs/tools` 为复制文件系统可能如下：

```
/usr/man -ro hp/share/man monk(1):usr/man

/cs/tools -ro leopard.mon/cs/tools
```

注意，如果路径相同，可以将服务器名称列在一起。第一行后的 `(1)` 设置了相对于 `/usr/man` 的优先级。`harp` 后面没有优先级表示隐式优先级 0。

## 自动挂载 (Automatic automounts (V3)): all but Linux

与其在直接或间接映射中列出所有可能的挂载，你可以告诉 `automount` 一些关于你的文件系统命名规则，让它自行判断。实现此功能的关键部分是运行远程服务器上的挂载可以查询以找到服务器导出的文件系统。在 NFS 第 4 版本中，导出总是 `/`，这消除了对这种自动化的需求。

配置“自动挂载”的方法有多种，最简单的是 `-hosts` 挂载类型。如果你在主映射文件中将 `-hosts` 作为映射名称，`automount` 将主机映射到指定的自动目录：

```
/net -hosts nosuid.soft
