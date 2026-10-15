
创建分区后，你可以对其进行格式化并创建文件系统。为此，你必须选择格式化方式。对于 Linux 分区，你可以选择将其格式化为 `ext2`、`ext3` 或 `reiserfs`。关于文件系统的更多信息请参见第 5 页的 `1.1.6` 节“Linux 中的文件系统”。在第 154 页的示例 3-10 中，你可以通过 shell 命令创建 `ext2` 文件系统。

## 3.2.2 文件系统

第 3 章 安全与管理

## 示例 3-10 格式化 Linux 分区

```
mkfs.ext2 /dev/sdb1
Filesystem label=
OS: Linux
Block size=4096
Fragment size=4096
34768 inodes, reserved for super user
First block=0
32768 blocks per group
Superblock stored on blocks: 32768,3840
Writing inode tables: done
Writing superblocks and filesystem information: done
```

在示例 3-11 中，格式化交换分区。

## 示例 3-11 格式化交换分区

```
mkswap /sdb2
Setting up swap version 1, size =
```

不要创建一个比 RAM 大两倍的交换分区。接下来创建一个目录（例如 `mkdir /data`），然后修改 `/etc/fstab` 文件，添加示例 3-12 所示的行，以便分区在启动时挂载。

## 示例 3-12 在 /etc/fstab 中添加分区

| sdb1 | /data | ext2 | defaults | 1 |
| sdb2 | swap | swap | defaults | 0 |

当重启服务器时，你的文件系统将挂载。

## 3.2.3 脚本

本节介绍如何创建 shell 脚本。shell 脚本是自定义 Linux 服务器的一种强大方法。作为一个示例，我们将创建一个简单的脚本。示例 3-13 给出了实际代码。

注意：每个 shell 都有自己的脚本语法。创建的脚本适用于 `Bash` shell。

## 示例 3-13 日志清理

```bash
#!/bin/bash

# Log eraser

LPATH=/var/log

NR_OF_DAYS=60

for i in $(find $LPATH -atime +$NR_OF_DAYS)
do
  rm -f $i
done
```

- 第一行 `#!/bin/bash` 环境脚本将运行。此行应原样处理，不要修改。
- 第六行将变量 `LPATH` 设置为 `/var/log`，第七行将变量 `NR_OF_DAYS` 设置为 `60`。我们建议使用变量，这样更容易调试你的脚本。
- `$LPATH` 和 `NR_OF_DAYS` 表示你希望使用的变量值。
- `find $LPATH -atime +$NR_OF_DAYS` 将在 `/var/log` 目录中搜索大于 60 天的文件。
- 接下来是 `for` 循环。对于每一个 `i` 值，我们将运行命令 `rm -f $i`，这将删除由 `i` 指定的文件。
- 以 `#` 开头的行是注释，但也有特殊情况，例如第一行或 `config` 命令使用的注释。

将文件保存为 `log_eraser.sh`。我们建议创建一个名为 `/scripts` 的目录，将你的脚本放在同一个位置。为了执行脚本，你必须修改文件的权限。运行命令 `chmod 700 /scripts/log_eraser.sh`。你将唯一可以读取、写入和执行该文件的人。如果你好奇，`chmod` 命令中的 `7` 来自读取(`4`)、写入(`2`) 和执行(`1`) 权限的数值相加：`4+2+1 = 7`。`chmod` 命令中的两个零表示组和其他（所有其他用户）对该文件没有权限。

参考第 135 页“文件权限”中描述的文件权限划分。

如果你将文件放在 `/scripts` 目录，运行脚本将输入 `/scripts/log_eraser.sh`。

> **注意：** 此脚本主要作为一个可以适用于其他情况的示例。尽管它可以工作，但你可能想要考虑更复杂的日志文件管理算法，或者使用内置的 `logrotate` 守护进程。

## 3.2.4 Crontab

在日常，你是 Linux 中自动运行这些脚本的调度器。`Crontab` 用于列出 crontab 中的计划程序，以 `root` 身份登录并输入 `crontab -l`。在空 Linux 安装中，你将看不到任何内容，或者会收到消息“no crontab for root”。

## 示例 3-14 Crontab 示例

```
20 * * * /scripts/script1
20 03 08 * * /scripts/script2
0 6,12,18 * * /scripts/script3
30 2 * * 6 /scripts/script4
0 0 * * * /scripts/log_eraser.sh
*/10 * * * * /scripts/script5
```

以下是对 crontab 语法的解释。六个字段是：

分钟 | 小时 | 日期 | 月份 | 星期 | 路径

crontab 示例中的行具有以下含义：

* 每小时第 20 分运行 `/scripts/script1`。
* 在 8 月 3 日凌晨 0:20 运行 `/scripts/script2`。
* 每天凌晨 0 点、上午 6 点、中午 12 点和下午 6 点运行 `/scripts/script3`。
* 每周六凌晨 2 点 30 分运行 `/scripts/script4`。
* 每周六凌晨 0 点运行 `/scripts/log_eraser.sh`。
* 每 10 分钟运行 `/scripts/script5`。

**提示：**

- 确保服务器上的日期设置正确。
- 一周从周日开始。因此，若要在周日运行作业，请输入 `0` 而不是 `7`。

要创建一个计划：

- 以 `root` 身份登录，并在命令提示符中输入 `crontab -e`。
- 按 `i` 进入插入模式。
- 为所有六个项目输入一个值。如果某项不适用，请使用 `*`。
- 完成后，按 `Escape` 键，然后输入 `:wq`（表示写入并退出）。

**注意：**

- `crontab` 使用 `vi` 作为默认文本编辑器。此处的命令假设使用的是 `vi`。
- `cron` 有一个名为 `KCron` 的图形化前端。

## 3.2.5 网络状态

有时候，知道谁连接到了你的服务器以及正在发生什么是非常有用的。在本节中，我们将描述 `netstat` 命令和 `iptables` 实用工具的功能。

> **重要：** 本节中的信息需要一些 TCP/IP 协议知识。解释截图中的所有细节超出了本书的范围，但提供的信息已足够解释这些网络状态工具的常见用法。要学习更多关于 TCP/IP 的知识，请参见 IBM Redbook TCP/IP Tutorial and Technical Overview, GG24-3376。

## Netstat 命令

以 `root` 身份登录并输入 `netstat`，你将看到一个与第 159 页图 3-9 所示类似的屏幕。

从左到右，列的含义如下：

- `Proto`
  socket 使用的协议（TCP, UDP, raw）

- `Recv-Q`
  连接到此 socket 的用户程序尚未复制的字节数

- `Send-Q`
  远程主机尚未确认的字节数

- `Local Address`
  socket 本地端的地址和端口号

- `Foreign Address`
  socket 远端的地址和端口号

- `State`
  socket 的状态。由于 raw 模式下没有状态，且 UDP 通常不使用状态，此列可能为空，但也可以可以是以下几个值之一：

  - `ESTABLISHED`
    socket 已建立连接。

  - `SYN_SENT`
    socket 正在积极尝试建立连接。

  - `SYN_RECV`
    从网络接收到了连接请求。

  - `FIN_WAIT1`
    socket 已关闭，连接正在关闭。

  - `FIN_WAIT2`
    连接已关闭，socket 正在等待远端的关闭信号。

  - `TIME_WAIT`
    socket 在关闭后等待处理仍在网络中的数据包。

  - `CLOSED`
    socket 客户端在使用中。

  - `CLOSE_WAIT`
    远端已关闭，正在等待 socket 关闭。

  - `LAST_ACK`
    远端已关闭，socket 已关闭但仍在等待确认。

  - `LISTEN`
    socket 正在监听传入的连接。除非指定了 `--listening (-l)` 或 `--all (-a)` 选项，否则此类 socket 不包含输出中。

  - `CLOSING`
    两个 socket 都已关闭，但我们还没有设置所有数据。

  - `UNKNOWN`
    socket 的状态未知。

```
root@andrew]# # netstat

Active Internet-connections (v/o servers)

Proto Recv-Q Send-Q Local Address           Foreign Address         State
```
