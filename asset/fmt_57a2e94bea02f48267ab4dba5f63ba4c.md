
SUSE 发行版默认对系统分区使用 `Btrfs` 文件系统。`YaST` 在每次管理操作前后自动创建快照。这些快照可以使用 `YaST` 模块 `Snapper` 或此处简要介绍的 `snapper` 命令进行管理。你可以在执行的 `snapper` 命令前加上一个或多个选项：

- `--iso`

  以 ISO 格式化时间。

- `--utc`

  显示 UTC 时间（协调世界时）。

执行的操作由子命令指定：

- `cleanup number|timeline|empty-pre-post`

  根据最大快照数量、年龄或内容作为标准删除旧快照（参见 `/etc/snapper/configs/root` 配置文件）。

- `create`

  创建一个新快照。

- `delete n` 或 `n1-n2`

  删除指定的快照。使用的数字可以在 `snapper list` 中找到。

- `list`

  列出所有快照。

- `rollback [n]`

  将指定的或最近可用的快照设置为活动快照（严格来说：`Btrfs` 默认子卷）。随后的重启命令将系统恢复到创建快照时的状态。

- `undochange n1..n2 [files]`

  撤销快照 `n1` 和快照 `n2` 之间的更改——适用于所有影响的文件或仅针对参数指定的文件。

### `sort` [options] `file`

`sort` 对指定的文件进行排序并在屏幕上显示结果。排序顺序由语言设置定义，具体来说由 `LC_COLLATE` 环境变量定义。

- `-c`

  检查文件是否已排序。

- `-f`

  将小写和大写字母视为等等。

- `-k n1,n2`

  仅考虑 `n1` 和 `n2` 列之间的字符。列编号从 1 开始。通常，列由空格或字符分隔，请参见 `-tz`。如果未指定 `n2`，则将考虑从 `n1` 到行尾的所有字符。

- `-m`

  将两个或多个预先排序的文件合并成一个大的排序文件。这比先将文件放在一起再排序更快。

- `-n`

  按数字排序（即 10 在 9 之后，而不是 1 之后）。

- `-o result file`

  将结果写入指定的文件。该文件可以与排序的文件相同。

- `-r`

  反向排序。

- `-tz`

  指定两列之间的分隔符。默认设置是空白，即空格和制表符的任意组合。

- `-u`

  消除结果中的重复项。

### 示例

以下命令安装 Atom 编辑器：

```
user$ snap install --classic atom
atom 1.51.0 installed from Snapcrafters
```

```
user$ speaker-test -t wav -c2
```

### `speaker-test` [options]

来自 `alsa-utils` 的 `speaker-test` 命令帮助你跟踪音频系统的问题。为此，它产生频率。

- `-c n`

  使用 `n` 个音频通道。

- `-f n`

  以指定的赫兹频率播放正弦波。必须使用 `-t` 选项。

- `-s n`

  仅测试编号为 `n` 的音频通道。

- `-t pink|sine|wav`

  输出粉红噪声、正弦波或来自 WAV 的语音模式。

- `-w file`

  播放指定的 WAV 文件。

命令，所有命令都必须以分号结束。除了常用的 SQL 命令外，`sqlite3` 还知道一些以点（`.`）开头的特定命令，例如 `.help` 显示帮助文本或 `.tables` 列出数据库中的所有表。`.quit` 或 `Ctrl+D` 可终止 `sqlite3`。

在第二种语法变体中，`sqlite3` 直接运行指定的 SQL 命令。

### 示例

以下命令确定哪些音乐专辑存储在 ownCloud 数据库中：

```
user$ owncloud.db
sqlite> select * from oc_media_albums;
1|NightClub|1|
2|The Monroe Doctrine|2|
3|The Best Of Herbie Mann|3|
...
sqlite> .quit
```

### `ss` [options]

`ss`（套接统计）分析本地计算机的网络活动。如果执行命令时不带选项，它将返回所有具有活动连接的非监听 TCP 套接。`ss` 提供了与 `netstat` 类似的功能，但被认为是更现代的命令，在某些情况下提供更详细的信息。

- `-4` 或 `-6`

  仅考虑 IPv4 或 IPv6 连接。

- `-a`

  显示所有套接，包括监听和非监听的。

- `-e`

  提供更多细节（扩展）。

- `-n`

  显示数值端口号，而不是服务名称。

- `-p`

  指定哪些进程使用了哪些套接。

- `-r`

  将端口号替换为服务名称。

- `-s`

  仅显示摘要信息（summary）。

- `-t` 或 `-u`

  仅考虑 TCP 或 UDP 连接。

### 示例

以下命令提供了 IPv6 连接的所有活动 TCP 套接列表：

```
users ss -6 -t -a                               Peer Address:Port
State Recv-Q Send-Q  Local Address:Port
LISTEN 0       100     ::pop3               ::*
LISTEN 0       100     ::imap2              ::*
```

| LISTEN 0 128 ::http :::** |

| LISTEN 0 100 ::smtp :::** |

| LISTEN 0 128 ::https :::** |

| LISTEN 0 100 ::pop3s :::** |

| TIME-WAIT 0 0 ffff:5.9.22.28:http ffff:188.192.181.195:50045 |

| TIME-WAIT 0 0 ffff:5.9.22.28:http ffff:188.192.181.195:50047 |

| ESTAB 0 46200 ffff:5.9.22.28:http ffff:46.10.92.30:22893 |

| FIN-WAIT-1 0 1 ffff:5.9.22.28:https ffff:203.134.55.243:51106 |

### `ssh` [options] `computer name`

### `ssh` [options] `computer name` 命令

在第一种语法变体中，`ssh` 在另一台计算机上打开 shell，从而能够在该台计算机上进行交互式工作。第二种语法变体在第二台计算机上运行单个命令。只有当第二台计算机上运行着 SSH 服务器时，`ssh` 才能工作。

- `-l login`

  在第二台计算机上使用指定的登录名而不是当前用户名。所需的登录名也可以以此格式输入：`ssh loginname@computername`。

- `-L localport:host:hostport`

  在本地计算机（`localport` 端口）和第二台计算机（`hostport` 端口）之间建立隧道。

- `-o option=value`

  启用传输额外的选项，其语法与 `/etc/ssh/ssh_config` 文件中的相同（参见 `man ssh_config`）。例如，`-o StrictHostKeyChecking=no` 会导致 SSH 停止检查已保存在 `.ssh/know_host` 中的主机数据项。这对于许多虚拟机的自动化管理非常有帮助。

- `-t`

  强制使用伪终端来执行命令，格式为 `ssh -t hostname "commands"`。这使得通过 SSH 启动 `top` 等交互式程序成为可能。连接会持续到外部命令结束（对于 `top` 来说，通过输入 Q 结束）。

- `-T`

  防止激活伪终端。你可以在以下示例中找到此选项的应用。

- `-v`

  提供全面的调试信息。如果你遇到登录问题，`ssh -v` 通常可以帮助你找到原因。该选项可以指定三次（即 `-v -v -v`）；`ssh` 然后会提供更多的调试信息。

- `-X`

  启用执行 X 程序。

### 示例

以下命令显示了你如何登录到外部计算机，且用户名保持不变。然后你可以在外部计算机（例如，你的根服务器）上运行命令。

```
kofler@uranus ssh kofler.info
kofler@kofler.info's password: ********
```

当你第一次使用 `ssh` 连接到另一台计算机时，通常会出现基于以下模式的警告：

> 无法确认 'kofler.info (1.2.3.4)' 的真实性。

> RSA 密钥指纹是 SHA256:...

> 确定要继续连接吗吗？

如果你回答 `yes`，主机密钥将被添加到 `~/.ssh/known_hosts`。

以下命令显示了如何将公钥拷贝到远程服务器：

```
ssh-copy-id user@host
```

`ssh-copy-id` 命令简化了在远程服务器上安装公钥的过程。它会自动将你的公钥添加到远程机器上的 `~/.ssh/authorized_keys` 文件中。如果不可用 `ssh-copy-id`，你可以通过以下方式手动完成：
