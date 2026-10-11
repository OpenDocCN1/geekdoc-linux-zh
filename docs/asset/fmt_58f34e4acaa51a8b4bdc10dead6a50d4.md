
| `file1 -nt file2` | 如果 `file1` 比 `file2` 新，则为真（新于） |

# bash 变量 `[[ ]]`

虽然 `test` 和短表示法 `[ expression ]` 在大多数 shell 中这样工作，但双括号变体 `[[` 在 `bash` 中是可选：

| 表达式 | 说明 |
| :--- | :--- |
| `[[ cs = pattern ]]` | 如果字符串匹配模式，则为真 |
| `[[ cs == pattern ]]` | 如果字符串匹配模式，则为真 |
| `[[ cs ~ regex ]]` | 如果字符串匹配正则表达式，则为真 |
| `[[ cond1 && cond2 ]]` | 如果两个条件都满足，则为真（与） |
| `[[ cond1 || cond2 ]]` | 如果至少满足一个条件，则为真（或） |

另一个区别是 `[[ ]]` 甚至不需要引号。

## 示例

以下小型脚本没有执行任何意义的任务，它仅演示了在循环中使用 `[[ ]]` 语法。

```bash
#!/bin/bash
for i in {1..10}; do
  rest=$((i%2))
  [[ $rest -eq 1 ]] && continue
  echo $i
  [[ $i -eq 6 ]] && break
done
```

## time 命令

`time` 执行指定的命令并指示花费了多少时间。输出通过标准错误进行，可以通过环境变量更改。

`time` 不仅仅替换秒表，还将执行时间分为三个部分：

- `real`: 显示实际执行时间。
- `user`: 在内核外执行程序的 CPU 时间。
- `sys`: 在内核内执行程序的 CPU 时间。

`user` 和 `sys` 的总和表示执行消耗了多少 CPU 开销。`real` 往往远大于 `user` 和 `sys` 之和。这可能有两个原因：首先，有很多进程与启动的命令并行运行，也消耗了计算时间。其次，执行命令时可能存在等待时间，例如读写文件或在网络中传输数据。

`user` 和 `sys` 分别引用 CPU 核心。如果执行的命令充分利用了多个核心，那么 `user` 和 `sys` 之和可能会大于 `real`。

### 示例

以下命令读取逻辑卷的内容并使用 `7zr` 命令压缩。在多核系统的空闲模式下，该过程需要 24 分钟。如果只有一个核心，备份创建花费更长时间（大约 40 分钟）。

```bash
root# time dd if=/dev/vg830/lv3 bs4M | 7zr a -si lv3.img.7z
real 24m53.424s
user 38m37.841s
sys 0m30.446s
```

- `settime datetime`
  - 重置日期和时间。计算机的硬件时钟也会相应更改。时间必须以 `2025-12-31 23:59:59` 的格式输入。
- `set-timezone name`
  - 设置所需的时区。
- `status`
  - 显示时间、时区和其他各种时间数据，例如夏令和冬令之间的下次切换时间。

### 示例

以下命令首先显示当前时间，然后更改时区：

```
root# timedatectl status
Local time: 2025-05-18 09:08:33 CEST
Universal time: 2025-05-18 07:08:33 UTC
RTC time: 2025-05-17 18:51:42
Time zone: Europe/Vienna (CEST, +0200)

root# timedatectl set-timezone Europe/Paris
```

```
timeout [options] time span command
```

`timeout` 执行指定的命令，如果运行时间超过指定时间，则会自动结束该命令。时间跨度指定为一个浮点数，后面带有字母 `s`、`m`、`h` 或 `t`，分别表示秒、分钟、小时或天（例如，`0.5h` 表示半小时）。

- `-k`
  - 通过 `KILL` 信号终止运行时间过长的程序。默认情况下，`timeout` 使用 `TERM` 信号，但该信号可以被忽略。

### 示例

在以下命令中，`scp` 有 30 秒的时间将文件传输到另一台计算机。之后，该进程将被取消。

```
user timeout 30 scp localfile myserver:destinationdir/
```

# tldr 命令

`tldr` 是 "too long, didn't read" 太长没读）的缩写，是对通常极其庞大的手册页的一种批评。`tldr` 尝试做得更好，提供了一些常用命令的指示性示例。因此，该命令是此书的一个很好的补充。输出在终端中以颜色高亮。

```
user tldr rsync
向或从远程主机传输文件（但不在两个远程主机之间传输），默认使用 SSH。要指定远程路径，请使用 userhost:path/to/file_or_directory。更多信息：
https://download.samba.org/pub/rsync/rsync.1.
- 传输文件：
```

`rsync path/to/source path/to/destination`

```
- - 使用归档模式（递归复制目录，在不解析的情况下复制符号链接，并保留权限、所有者和修改时间）：
rsync --archive path/to/source path/to/destination

- - 在发送到目标时压缩数据，显示详细且人类可读的进度，并在中断时保留部分传输的文件：
rsync --compress --verbose --human-readable --partial --progress \path/to/source path/to/destination

- - （另外五个使用示例）
```

## top [q]

`top` 每五秒显示一次所有运行进程的列表，进程根据其计算时间的份额进行排序。如果在调用时指定了可选 `q` 参数，`top` 将不断更新列表并占用所有的空闲计算时间。按 `q` 终止程序。

### 方案

比 `top` 更方便且视觉效果更好的替代方案是 `btop` 和 `htop` 命令，大多数发行版必须单独安装。这些命令提供了各种附加功能，为输出着色，并允许水平和垂直滚动查看运行中的进程。

如果你感兴趣的内存消耗和 CPU 使用率，而是运行进程的 I/O 活动或能效，那么你应该查看 `iotop` 或 `powertop` 的描述。

## touch [options] files

`touch` 更改文件保存的最后修改时间。如果在不带选项运行命令，则会将当前时间保存为修改时间。如果文件不存在，将创建一个长度为 0 字节的新文件。

- `-r file`
  - 使用文件的保存修改时间。
- `-t time`
  - 指定时间。必须使用 `[[CC]YY]MMDD[.ss]` 格式，例如 `202512311730` 表示 `2025/12/31` 下午5:30。或者，你也可以通过 `-d` 选项指定更可读的格式。

### 示例

在此示例中，`touch` 用于比较目录中的所有文件与目标目录文件的修改时间。如果你忘记了哪些文件是现在复制的，这很有。

```
user$ cd target

user$ find -type f -exec touch -r /source {}
```

# tr

`tr` 将字符串1的所有字符替换为字符串2对应的字符。两个字符串长度应该相同。未出现在字符串1中的字符保持不变。无法用多个字符替换单个字符（例如用"o"）——这必须使用 `sed` 等命令。

- `-d`
  - 删除字符串1指定的字符。字符串2不需要指定。

### 示例

在以下示例中，`tr` 将所有小写字母替换为大写字母并在终端显示结果（标准输出）：

```
user$ tr a-z A-Z < file
```

## traceroute

`traceroute` 提供本地计算机到目标地址 TCP/IP 数据包路径上的所有站点列表。为每个站点指定运行时间（默认尝试三次）。只有在目标地址端口未被防火墙拦截，`traceroute` 才能工作。在这种情况下，`traceroute` 只返回星号。

- `-4` 或 `-6`
  - 使用 IPv4 或 IPv6 协议。默认情况下，`traceroute` 使用相应的协议。如果主机关联了 IPv4 和 IPv6 地址，`traceroute` 优先使用 IPv4。对于 `traceroute`，`-6` 应用。
- `-m n`
  - 确定中间站点的最大数量（默认 30）。
- `-n`
  - 仅显示中间站点的 IP（不显示主机名）。
- `-q`
  - 使用指定的 UDP 端口（默认）。
- `-q n`
  - 发送 `n` 个数据包并测量数据包的响应时间（默认）。

### 示例

以下命令显示我的本地计算机和 Web 服务器之间的站点。在某些站点，IP 数据包通过不同的路由器路由，这表示冗余连接。

```
root traceroute kofler.info (213.239.211), 30 hops max, 60 byte packets

1 device.lan (10.0.0.138) 14.116 ms 13.376 ms 13.112 ms

2 62.47.95.239 (62.47.95.239) 25.650 ms 27.489 ms 29.245 ms
```
