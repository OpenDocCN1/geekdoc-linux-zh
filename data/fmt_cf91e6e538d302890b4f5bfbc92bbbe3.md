
解包 `shar` 文件。`Shar` 文件是“shell 归档”文件，用 `shar` 命令创建（见上文）。

示例：解包 `shar` 文件 `text.shar`：

`unshar-text.shar`

- `--version`: 显示版本信息并退出。
- `--help`: 显示帮助信息并退出。
- `-d DIRECTORY`, `--directory=DIRECTORY`: 在解包文件之前移动到指定的 `DIRECTORY`。
- `-c`, `--overwrite`, `-f`, `--force`: 告诉 `shar` 覆盖现有文件。
- `-e`, `--exit-0`: 当从包含多个 `shar` 归档的单个邮件文件夹解包时，在解包时将它们分开。（假设不同的 share 用 `exit 0` 分隔）。
- `-E STRING`, `--split-at=STRING`: 与 `-e` 类似，但允许指定分隔符字符串。

## `uuencode [-m] [ file ]-name`

## `uudecode [-o outfile] [ file ]...`

`uuencode`/`uudecode` 程序用于编码二进制文件以便通过仅支持传输 ASCII 数据的介质。

示例：编码二进制文件 `program` 并发送给用户 `some-guy@wherever.com`：

```
uuencode program | mail someguy@wherever.com
```

- `-m`: 使用 base64 编码格式。
- `-o`: 将输出写入指定的文件。

## `zcmp [ cmions ] file1 [ file2 ]`

## `zdiff [ diffoptions ] file1 [ file2 ]`

比较当前压缩的文件。这些命令的选项分别与 `cmp` 和 `diff` 的选项相同。

示例：比较压缩文件 `a.gz` 与压缩文件 `b.gz` 的内容：

```
zcmp a.gz b.gz
```

## `zgrep [ grepoptions ] [ -e ] pattern filename.`

此命令用于对压缩或 zip 文件执行 `grep`。该命令的选项与 `grep` 相同。

示例：在当前目录下的所有压缩文件中查找字符串“important clue”（假设具有 `.gz` 扩展名）：

```
zgrep "important clue" .gz
```

## `zmore [ name ... ]`

查看压缩文件。`zmore` 命令是交互式的，以下按键有效：

示例：显示压缩文件的内容。

## 简介

以下命令被用于启动/关机序列：

| | |
|---|-|
| `dmesg` | 显示启动信息 |
| `halt` | 停止系统 |
| `reboot` | 重启系统 |
| `poweroff` | 关闭系统电源 |
| `lilo` | 安装 LILO 引导加载程序 |
| `rdev` | 显示系统启动配置信息 |
| `runlevel` | 显示当前系统运行级别 (`runlevel`) |
| `shutdown` | 关机系统 |
| `swapon` | 启用分页硬件 |
| `swapoff` | 禁用分页硬件 |
| `sync` | 将缓冲区中的内存写入磁盘 |
| `init` | 启动系统进程 |
| `telinit` | 将系统移动到新的运行级别 |

## 相关文件

| | |
|---|-|
| `/var/log/wtmp` | 登录记录文件 |
| `/fastboot` | 此文件的存在意味着系统请求在重启时跳过 `fsck`。 |
| `/etc/inittab` | 定义在什么运行级别启动哪些进程。 |
| `/etc/shutdown.allow` | 此文件中指定的用户允许调用关机命令。 |
| `/etc/rc` | 多用户初始化文件。 |
| `/etc/fstab` | 包含系统的挂载信息 |
| `/etc/hd??` | 磁盘设备 |
| `/etc/sd??` | SCSI 磁盘设备 |
| `/etc/initscript` | 如果存在，被 `init` 用于启动新进程。 |
| `/dev/console` | 控制台设备驱动程序。 |
| `/etc/ioctl.save` | 指定控制台的 `ioctl` 状态。 |
| `/etc/lilo.conf` | 指定 LILO 配置选项。 |

## 命令

```
dmesg [-c ] [ -n level ] [ -s bufsize ]
```

此命令用于显示或控制内核环形缓冲区的内容，包含启动信息。

示例：获取上次系统启动时的启动消息：`dmesg | less`

示例：设置控制台以烦人的频率显示消息：

```
# dmesg -n 3
```

- `-C` 在打印后清除环形缓冲区的内容。
- `-s bufsize` 指定用于查询内核环形缓冲区的大小。默认为 8196。
- `-n level` 指定日志消息显示到控制台的级别。注意，无论级别如何，消息都会发送到 `/proc/kmsg`。通常设置为 1，这将过滤掉除 panic 以外的所有消息。

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_350_0.png)

# `halt [-n] [-w] [-d] [-f] [-i] [-p]`

# `reboot [-n] [-w] [-d] [-f] [-i]`

# `poweroff [-n] [-w] [-d] [-f] [-i]`

`halt` 及其同义词告诉内核执行三件事之一：重启、停止或关闭电源。调用时，它们会在 `/var/log/wtmp` 文件中创建一个记录。你必须以超级用户登录才能使用此命令。

示例：强制停止系统：`halt -f`

- `-n` 不同步。
- `-w` 写入 `wtmp` 条目但实际上不重启或停止。
- `-d` 不写入 `wtmp` 条目。
- `-f` 强制停止或重启。
- `-i` 在停止/重启前关闭所有网络接口。
- `-p` 停止后执行关机。

# `lilo` 选项

此程序安装 `lilo` 引导加载程序。它高度依赖于存储在配置文件中的信息，默认是 `/etc/lilo.conf`。

示例：`Lilo` 通常在不带参数运行：`/sbin/lilo`

| | |
|---|---|
| `-v` | 运行详细模式。 |
| `-q` | 显示 `/boot/map` 中指定的映射内核文件。 |
| `-m map-file` | 使用指定的映射文件而非 `/boot/map`。 |
| `-C config-file` | 使用指定的配置文件，默认是 `/etc/lilo.conf`。 |
| `-d delay` | 指定 `lilo` 启动内核前的延迟。 |
| `-D label` | 指定内核。 |
| `-r root-directory` | 在指定的目录上强制 LILO 执行 `chroot`。用于从软盘修复。 |
| `-t` | 仅测试，不实际写入新的引导区。 |
| `-c` | 压缩。 |
| `-f disk` | 指定磁盘几何结构（默认是 `/etc/fstab`）。 |
| `-i boot-sector` | 使用指定的文件作为新的引导区。 |
| `-l` | 使用线性地址而非扇区/头部/柱面地址。 |
| `-P fixignore` | 指定是修复还是忽略表。 |
| `-s save-file` | 使用指定的文件保存覆盖引导区的数据。 |
| `-S save-file` | 允许覆盖文件。 |
| `-u device-name` | 卸载 LILO。（将指定的引导区写回 MBR。） |
| `-U device-name` | 在不检查时间戳的情况下卸载 LILO。 |
- `-R command line` 设置下次执行引导加载程序的默认命令。
- `-I label` 显示启动后运行的内核的路径。
- `-V` 显示版本号。

```
rdev [-r ] [ -o offset ] [ image { offset } ]
```

```
rdev [ -o offset ] [ image { root_device { offset } } ]
```

```
swapdev [ -o offset ] [ image { swap_device { offset } } ]
```

```
ramsize [ -o offset ] [ image { size { offset } } ]
```

```
vidmod [ -o offset ] [ image { mode { offset } } ]
```

```
rootflags [ -o offset ] [ image { flags { offset } } ]
```

如果不带参数调用，`rdev` 显示当前根系统的 `/etc/mtab`。此命令通常用于显示启动镜像中的字节对，指定根设备、视频模式、内存磁盘大小和交换设备。默认情况下，信息从偏移量 504 开始。

示例：获取根文件系统的挂载信息：`rdev`

偏移量位于：

498 根标志

500 预留

504 内存磁盘大小

506 VGA 模式

508 根设备

510 引导签名

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_352_0.png)

`image` 参数通常是之一：

`/vmlinux`

`vmlinux.test`

`/vmunix`

`vmunix.test`
