
此机器已连接到 Ubuntu Pro 订阅。
Main/Restricted 软件包在启用 `esm-infra` 的情况下接收 Ubuntu Pro 的安全更新，直到 2032 年。
Universe/Multiverse 软件包在启用 `esm-apps` 的情况下接收 Ubuntu Pro 的安全更新，直到 2032 年。

# ps [options]

`ps` 显示运行中进程（程序）和内核线程的列表。该命令与 `kill` 配合使用特别有用，可以强制终止已挂起的程序。`ps` 备有无数选项，这些选项在在线手册（`man ps`）中有详尽描述。在那里，您还能找到 `ps` 输出的众多信息的含义解释。`ps` 的变体是 `pstree`，它显示进程树，从而一目了然地进程的层次结构。

与其他命令相比，`ps` 具有带和不带连字符的选项。其中某些选项甚至具有不同的含义。(`ps -a` 和 `ps` 并不等效！) 两种类型的选项可以混合使用，例如 `ps -A ul`。

- `-a`
也显示其他用户的进程（而不仅仅是你自己的）。

- `-A`
显示所有进程。

- `-f`
显示进程树。

- `-f -l` 或 `l`
显示各种额外信息（内存需求、优先级等）。

- `-p n` 或 `-p n1,n2,n3`
仅显示具有指定进程号（PID）的进程。

- `--ppid n`
仅显示以 `n` 为父进程 ID 的进程，即由进程 `n` 启动的进程。

- `-u`
也显示相应进程的用户。该选项不能与 `l` 结合。

- `-x`
也显示未分配终端的进程。这些包括管理系统的 Linux 内部进程（守护进程）。

- `-Z`
也显示进程的 SELinux 上文。

## 示例

以下示例展示了 `ps` 命令的基本应用：

```
root# ps ax
```
（显示所有进程）

```
root# ps ax | grep ssh
```
（显示描述包含 ssh 的进程）

```
root# ps axu
```
（显示所有进程，包括所有者/账户）

在 Linux 上，`kthread` 内核线程守护进程号始终为 2。所有其他内核线程都由 `kthread` 启动。因此，如果您只想列出内核线程，可以使用 `ps --ppid 2`：

```
root# ps --ppid 2
```
（仅显示内核线程）

# ps2pdf [options] source.ps [target.pdf]

`ps2pdf` 从任何 PostScript 或 EPS 文件创建 PDF 文件。如果您没有指定 `target.pdf`，PDF 文件将与 PostScript 文件同名（但标识符为 `.pdf`，即 `source.pdf`）。

- `-dEncodeImages=false`
防止对图像任何压缩。生成的 PDF 文件现在非常大。通过结合 `/prepress` 设置，`ps2pdf` 现在提供具有最佳打印和曝光质量的 PDF。

- `-PDFSETTINGS=/default | /screen | /printer | /prepress`
指定 PDF 文档是针对任何用途、屏幕显示、普通打印或曝光（例如书籍打印等）进行优化。较高质量的代价是文件大小增加。这四个默认设置让您无需单独设置许多选项。

- `-rn`
指定位图字体的分辨率（单位 DPI，即每英寸点数）。

其他选项见以下地址：
`https://web.mit.edu/ghostscript/www/Ps2pdf.htm`

## 示例

以下命令从 PostScript `book.ps` 创建 PDF 文档 `book.pdf`：

```
user$ ps2pdf book.ps
```

# psql [options]

`psql` 允许执行 SQL 命令。`psql` 是 `postgresql` 的一部分。如果您只需要客户端，请使用 `postgresql-client`。

- `-c command`
运行 SQL 命令。

- `-dname`
指定建立连接的数据库。

- `-f file`
运行文件中包含的 SQL 命令。

- `-h hostname`
指定运行的主机。

- `-l`
列出所有数据库。

- `-U username`
定义用户名。

## 示例

示例展示了创建数据库、创建表、插入记录以及简单的查询：

```
user$ psql -U name -h localhost
Password for user: ********
# CREATE DATABASE test;
# \c test;
# CREATE TABLE mytable (id SERIAL PRIMARY KEY, data TEXT);
## INSERT INTO mytable (data) VALUES ('abc', 'efg');
## SELECT * FROM mytable;
id | data
-----+ 
1 | abc
2 | efg
```

# pssh 和 pscp

`pssh [options] command`
`pscp [options] local_file remote_file`

Python 脚本 `pssh` 在多个服务器上运行命令。`pscp` 从或向主机复制文件。`puke` 在所有主机上终止指定名称或模式的程序。这三个命令都需要可以使用密钥进行认证，或者由 `ssh-agent` 后台程序处理认证。

- `-h hosts.txt`
指定包含执行命令的主机主机名的文本文件的位置。

- `-o directory`
指定 `pssh` 保存命令输出以及 `pscp` 保存文件的目录。

## 示例

示例假设所有主机都是 RHEL 系统。然后，使用 `yum` 在这些计算机上执行软件更新。

```
root# pssh -h hosts.txt yum update
```

# pvcreate [options] 设备

LVM 命令 `pvcreate` 将分区或设备声明为物理卷（PV），以供以后在卷组（VG）中使用（另见 `vgcreate` 和 `vgxtend`）。

`pvcreate` 要求该分区或设备之前已标记为 LVM 分区。在 `fdisk` 中，你必须使用 `T` 快捷键命令并输入 `ae` 来此此。在 `parted` 中，需要的命令是 `set partition number lvm on`。

## 示例

以下命令将 `/dev/sdc1` 分区转换为 LVM 的物理卷：

```
root# pvcreate /dev/sdc1
Physical volume "/dev/sdc1" successfully created
```

# pvdisplay 设备

`pvdisplay` 显示指定 PV 的详细信息。

# pvremove 设备

`pvremove` 移除未使用 PV 的标签。

# pvscan

`pvscan` 列出所有的 PV。

```
pw-cat audio file
pw-cli [command]
pw-mon [options]
pw-top [options]
```

大多数现代 Linux 发行版使用 PipeWire 作为音频和视频服务器。有多种命令可以控制 PipeWire，每个命令都以 `pw-` 开头。在这里，我将关注最常用的命令：

- `pw-cat` 从音频系统传输或原始文件。该命令也可以作为 `pw-play`、`pw-record`、`pw-midiplayrecord` 或 `pw-midirecord` 运行。
- 你可以使用 `pw-cli` 修改音频设置。有无数子命令，这里只提到了最重要的：
  - `connect` 或 `disconnect` 建立或终止与外部 PipeWire 服务器的连接。
  - `create-link` 连接两个 PipeWire 节点。
  - `create-node` 和 `export-node` 管理 PipeWire 节点，即信号管理或转发的对象。
- `info id` 显示特定对象的详细信息。
- `list-objects` 列出所有的 PipeWire 对象。
- `list-remotes` 列出所有的外部 PipeWire 实例。
- `load-` 和 `unload-module` 加载或移除 PipeWire 模块。
- `send-command` 向 PipeWire 对象发送命令。
- `switch-remote` 定义激活的远程实例。

`pw-cli` 是一个底层命令。它的使用非常繁琐。由于 PipeWire 与 PulseAudio 有一个兼容层，在很多情况下，通过 `pactl` 控制设置更为方便。

- `pw-mon` 列出 PipeWire 系统已知的所有音频和视频对象，包括无数属性。
- `pw-top` 提供当前激活的 PipeWire 组件的概述，包括在音频处理过程中发生的延迟。

```
pwd
```
