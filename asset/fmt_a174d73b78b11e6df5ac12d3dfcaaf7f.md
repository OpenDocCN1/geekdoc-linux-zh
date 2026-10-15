
```
restore > ls
```

`bob/` `jane/` `joe/` `lost+found/` `mary/` `thad/`

是的，这是主分区。现在使用 `cd` 命令将当前目录切换到 Joe 的主目录。再次输入 `ls` 以查看其主目录的内容。

```
restore > cd joe
```

```
restore > ls
```

`./joe:`:

`.mozilla/` `Desktop/` `report.html`

`.tcshrc` `Mail/` `letter.txt`

`.xinitrc` `News/` `www/`

现在使用 `add` 命令将 `Mail` 目录标记为提取对象：

```
restore > add Mail
```

如果你再次使用 `ls` 命令，你会看到 `Mail` 目录前面有一个星号（`*`）字符，这表示它已被标记为提取对象。

```
restore > ls
```

`./joe:`:

`.mozilla/` `Desktop/` `report.html`

`.tcshrc` `*Mail/` `letter.txt`

`.xinitrc` `News/` `www/`

现在使用 `extract` 命令开始提取过程。`restore` 会提示你输入起始磁带编号。由于这是单磁带备份，因此只需输入数字 `1`。当它提示你为 `'.,?'` 设置 `owner/mode` 时，通过输入 `y` 并回车来回答 `yes`（是）。`restore` 随后将恢复正在恢复的目标目录的文件权限（如有必要）。在像这样提取单个文件时，这一点并非关键，但执行完全恢复时，你应始终对此提示回答 `yes`。无论如何，你的屏幕上现在应显示以下内容：

```
restore > extract
```

`You have not read any tapes yet.`

`Unless you know which volume your file(s) are on`

`you should start with the last volume and work toward the first.`

`Specify next volume #: 1`

`Set owner/mode for '.,?' [yn] y`

`restore >`

此时，文件已恢复完成，你可以通过发出 `quit` 命令退出 `restore` 程序。这就是全部过程。现在你已经掌握了使用 `dump` 和 `restore` 命令的基础知识。

## 配置 Amanda 进行网络备份

使用 Amanda（Advanced Maryland Automatic Network Disk Archiver，高级马里兰自动网络磁盘归档器），你可以使用服务器上的单个大容量磁带驱动器通过网络备份多台计算机上的文件。Amanda 软件包（`amanda`、`amanda-client` 和 `amanda-server`）包含多种命令。Amanda 的在线 man 页面描述了如下表 13-7 所示的命令。

### 表 13-7：与 Amanda 一起使用的备份命令

| 命令 | 描述 |
| :--- | :--- |
| `amdump` | 执行自动 Amanda 备份。此命令通常由名为磁带服务器主机的计算机上的 `cron` 运行，并请求备份位于备份客户端上的文件系统。`amdump` 将 `disklist` 文件中的所有磁盘备份到磁带，或者如果出现问题，则备份到一个特殊的临时磁盘。所有备份完成后，`amdump` 发送邮件报告失败和成功的情况。 |
| `amflush` | 将备份从临时磁盘刷新到磁带。`amflush` 用于在 `amdump` 报告无法将备份写入磁带之后。当这种情况发生时，备份将保留在临时磁盘中。在磁带问题得到解决后，运行 `amflush` 将备份从临时磁盘写入磁带。 |
| `amcleanup` | 清理被中断的 `amdump`。仅当 `amdump` 因某些原因（通常是因为磁带服务器主机在 `amdump` 运行期间崩溃）无法完成时才需要此命令。 |
| `amrecover` | 提供交互式界面以浏览 Amanda 索引文件并选择要从哪个磁带恢复文件。`amrecover` 还可以运行 `amrestore` 和系统 `restore` 程序（例如 `lr`）。 |
| `amrestore` | 读取 Amanda 磁带，搜索请求的备份。`amrestore` 适用于从交互式恢复单个文件到恢复故障磁盘上的所有分区的各种场景。 |
| `amlabel` | 在磁带上写入 Amanda 格式标签。所有 Amanda 磁带必须使用 `amlabel` 进行标记。`amdump` 和 `amflush` 不会向未标记的磁带写入数据。 |
| `amcheck` | 验证磁带驱动器中的磁带是否正确，并且所有备份客户端系统上的所有文件系统是否已准备好进行备份。可以选择由 `cron` 在 `amdump` 之前运行，以便如果有人收到邮件警告，除非采取纠正措施，否则备份将失败。 |
| `amadmin` | 处理管理任务，例如查找恢复文件系统所需的磁带、强制主机对选定磁盘执行完全备份，以及查看计划平衡信息。 |
| `amtape` | 处理磁带更换器控制操作，例如加载特定磁带、弹出磁带以及扫描磁带架。 |
| `amverify` | 检查 Amanda 备份磁带是否存在错误（仅限 GNU tar 格式备份）。 |
| `amrmtape` | 从磁带列表和 Amanda 数据库中删除一个磁带。 |
| `amstatus` | 显示正在运行的 `amdump` 的状态。 |

`amdump` 命令是你将最常使用的，但在开始之前，你需要在备份服务器（带有磁带驱动器的系统）和备份客户端（被备份的系统）上配置几项内容。在 amanda 客户端上，你需要安装 `amanda` 软件包。在 amanda 服务器上，你还需要安装 `amanda-server` 软件包。

### 创建 Amanda 目录

你需要创建一些目录来存放 Amanda 配置文件，并提供写入 Amanda 日志文件的位置。配置文件位于 `/etc/amanda` 目录中，日志文件位于 `/var/lib/amanda`。在这两种情况下，你应该以 `amanda` 用户身份登录，并在这些目录中创建子目录，每个子目录对应一个你打算运行的备份计划，以及一个索引文件，如下例所示。

> **注意：** 出于安全原因，你应该以 `amanda` 用户身份执行所有 amanda 管理任务。为此，root 用户可以通过输入 `passwd amanda` 并输入新密码为 `amanda` 创建密码。但是，更好的替代方案可能是锁定 `amanda` 用户账户，然后只需作为 root 用户输入 `su - amanda`（如下例所示），而无需额外密码即可执行 amanda 任务。本程序的其余部分假设你已以 `amanda` 用户身份登录。

```bash
# su - amanda
$ mkdir -p /var/lib/amanda/normal/index
$ mkdir -p /etc/amanda/normal
```

为了本示例的目的，我只创建了一个 `normal` 备份配置，用于备份几台机器上的数据驱动器。你可能还会决定创建一个升级备份配置，用于备份操作系统分区。然后，你可以在执行任何操作系统升级之前运行该备份。

你还需要指定一个临时磁盘，Amanda 可以在将备份写入磁盘之前暂时用于暂存备份。该目录应拥有大量可用空间。我的服务器上有一个大的 `/home` 分区，因此我在那里创建了一个 Amanda 目录用作临时磁盘：

```bash
# mkdir /home/amanda
# chmod 700 /home/amanda
# chown amanda /home/amanda
# chgrp disk /home/amanda
```

### 创建 amanda.conf 文件

接下来，作为 `amanda` 用户，你必须为 Amanda 创建两个配置文件，并将它们存储在 `/etc/amanda/normal` 目录中：`amanda.conf` 和 `disklist`。你可以从 `/etc/amanda/DailySet1` 目录复制这些文件的示例开始，如下所示：

```bash
$ cd /etc/amanda/DailySet1
$ cp amanda.conf disklist /etc/amanda/normal
```

`amanda.conf` 文件设置各种通用配置值，而 `disklist` 文件定义要备份的机器和分区。`amanda.conf` 文件可能相当复杂，但幸运的是，其大多数值可以保持默认值。这里是一个简化的 `amanda.conf` 文件，其中嵌入了一些注释以帮助解释内容：
