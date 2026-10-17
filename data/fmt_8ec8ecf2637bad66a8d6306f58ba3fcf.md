
| `extract` | 从存档中提取所有标记的文件并将其写回文件系统。 |

| `help` | 列出可用命令。 |

| `ls` | 列出当前目录的内容。如果提供目录名称作为参数，则列出该目录的内容。标记为提取的文件或目录前面带有 *。 |

| `pwd` | 目录的完整路径。 |

| `quit` | 退出恢复程序。 |

作为一个示例，假设用户 `joe` 不小心删除了他主目录中的 `Mail` 子目录。`Joe` 正好是你的老板，所以你需要恢复他的文件。以下是操作方法。

将相应的磁带加载到驱动器，并以 `root` 身份登录。使用 `cd` 命令进入 `/home` 分区的顶部，然后以交互模式运行恢复程序：

```
# cd /home
# restore /dev/nrft0
```

通过输入 `ls` 命令验证你是否拥有 `/home` 分区的备份磁带。你应该看到类似的目录列表，代表在 `/home` 中有主目录的用户：

```
restore > ls
.
nbob/ jane/ joe/ lost+found/ mary/ thad/
```

是的，这就是主目录分区。现在使用 `cd` 命令切换到 `Joe` 的主目录。再次输入 `ls` 查看他主目录的内容。

```
restore > cd joe
restore > ls
./joe:
.mozilla/ Desktop/ report.html
.tcshrc Mail/ letter.txt
.xinitrc www/
```

现在使用 `add` 命令将 `Mail` 目录标记为提取：

```
restore > add Mail
```

如果你再次使用 `ls` 命令，你会发现 `Mail` 目录前面有一个星号 (*)，这意味着它已被标记为提取。

```
restore > ls
./joe:
.mozilla/ Desktop/ report.html
.tcshrc *Mail/ letter.txt
.xinitrc www/
```

# 第三部分：管理 Fedora 和 RHEL

现在使用 `extract` 命令开始提取过程。`restore` 将提示你从哪个磁带编号开始。由于这是单份磁带备份，只需输入 `y` 和 `1` 即可。当它提示你为 `.?` 设置所有者/模式时，按回车键回答 `yes`。`restore` 将恢复它正在恢复的目录的权限（如有必要）。在提取像这样的单个文件时，这并不关重要，但在执行完整恢复时，你应该对提示回答 `yes`。无论如何，你的屏幕现在应该包含以下内容：

```
restore > extract
You have not read any tapes yet.
Unless you know which volume file(s) are on you
should start with the last volume and work toward the first.
Specify next volume #: 1
set owner/mode for '.? [yn] y
restore >
```

此时，文件已经恢复，你可以通过发出 `quit` 命令退出恢复程序。就此结束。你现在已经掌握了使用 `dump` 和 `restore` 命令的基础知识。

# 配置 Amanda 进行网络备份

使用 `Amanda`（高级马里兰网络磁盘归档），你可以使用服务器上的单个大容量磁带驱动器备份多个网络的文件。`Amanda` 软件包（`amanda`、`amanda-client` 和 `amanda-server`）包含了多种命令。`Amanda` 的在线页对表 13-7 所示了了命令。

| 表 13-7：配合 Amanda 使用的备份命令 |

| Command | Description |

| `amdump` | 执行原子级 Amanda 备份。该命令通常由计算机上的 `cron` 运行，该计算机调用磁带服务器并请求对位于备份客户端上的文件系统进行备份。`amdump` 将 `disklist` 中的所有磁盘备份到磁带，如果出现问题，则备份到特殊的临时磁盘。所有备份完成后，`amdump` 会发送邮件报告失败和成功情况。 |

| `amflush` | 将备份从临时磁盘刷到磁带。在 `amdump` 报告无法将备份写入磁带后，使用 `amflush`。当发生这种情况时，备份留在临时磁盘中。在修复磁带问题后，运行 `amflush` 将备份从临时磁盘写入磁带。 |

| `amcleanup` | 清理中断的 Amanda 倾储。只有当 `amdump` 因为某些原因无法完成时才需要此命令，通常是因为磁带服务器主机在 `amdump` 运行期间崩溃了。 |

| `amrecover` | 提供交互式界面以浏览 Amanda 索引文件并选择从哪些磁带进行恢复。`amrecover` 有时也可以运行 `amrestore` 和系统恢复程序（如 `tar`）。 |

# 第 13 章：文件的备份与恢复 561

| Command | Description |

| --- | --- |

| `amrestore` | 读取 Amanda 磁带，搜索请求的备份。`amrestore` 适用于从单个文件的交互式恢复到故障磁盘上所有分区的完整恢复。 |

| `amlabel` | 在磁带上写入 Amanda 格式标签。所有 Amanda 磁带必须使用 `amlabel` 标记，`amdump` 和 `amflush` 不写入未标记的磁带。 |

| `amcheck` | 验证磁带是否在磁带器中，以及备份客户端系统上的文件系统是否准备好备份。可选在 `amdump` 之前由 `cron` 运行，这样有人就会收到邮件警告，除非采取正确的行动，否则备份将失败。 |

| `amadmin` | 处理管理任务，例如查找恢复文件系统需要哪些磁带、形成主机对所选磁盘进行备份，以及查看调度平衡信息。 |

| `amply` | 处理磁带库的控制操作，例如加载特定磁带、卸出磁带和扫描磁带架。 |

| `amverify` | 检查 Amanda 备份任务是否存在错误（仅限 GNU tar 格式备份）。 |

| `amrmtape` | 从磁带列表和 Amanda 数据库中删除磁带。 |

| `amstatus` | 提供正在运行的 `amdump` 的状态。 |

`amanda` 命令是你使用最频繁的命令，但在开始之前，你需要在备份服务器（带有磁带驱动器的系统）和备份客户端（被备份的系统）上都配置一些内容。在 Amanda 客户端上，你需要安装 `amanda` 软件包。在 Amanda 服务器上，你还需要安装 `amanda-server` 软件包。

## 创建 Amanda 目录

你需要创建一些目录来存放 Amanda 配置文件并为写入 Amanda 日志文件提供位置。配置文件位于 `/etc/amanda` 目录，日志文件位于 `/var/lib/amanda`。在两种情况下，你都应该登录这些目录，为你你打算运行的每个备份计划设置一个子目录和一个索引文件，如下例所示。

> 注意：出于安全考虑，你应该以 `amanda` 用户身份执行所有的 Amanda 管理。要做到这一点，root 用户可以使用 `passwd amanda` 为 `amanda` 创建密码并输入新密码。然而，更好的替代方案可能是锁定 `amanda` 用户账户，然后只需输入 `su amanda`（如下例所示），以便以 root 用户身份执行 am 任务而无需额外密码。其余部分假设你已以 `amanda` 用户身份登录。

```
$ su - amanda
$ mkdir -p /var/lib/amanda/normal/index
$ mkdir -p /etc/amanda/normal
```

为了本示例的目的，我只创建了一个普通备份配置，用于备份几台机器上的数据驱动器。你也可以决定创建一个升级备份配置，用于备份操作系统分区。然后你可以在执行任何操作系统升级之前运行该备份。

你还需要指定一个临时磁盘，Amanda 在写入磁带之前可以使用它缓存备份。

接下来，你必须在 `/etc/amanda` 创建两个文件：`amanda.conf` 和 `disklist`。`amanda.conf` 设置通用参数，`disklist` 定义了要备份的机器和分区。示例如下：

```
# amanda.conf - 带有注释的示例文件
# 注意，下面的关键字是 infofile，
# 是出于历史原因，现在应该是
# 一个目录（除非你选择了除了 text 以外的数据库格式）

infofile /var/lib/amanda/normal/curinfo"    # 数据库
logdir /var/lib/amanda/normal"                # 日志目录
indexdir /var/lib/amanda/normal/index"          # 索引目录
```

```
# disklist - 要备份的分区列表
# 这是一个简单的示例：

normal.root/home
normal.root/var
normal.root/etc
```

## 指定临时磁盘

在写入磁带之前建议使用。
