
## systemd-analyze (1)

远程执行操作。指定一个主机名，或“@”分隔的用户名和主机名以进行连接。主机名后可选地附加一个容器名，以“:”分隔，从而直接连接到指定主机上的特定容器。这将使用 SSH 与远程机器管理器实例通信。可使用 `machinectl -H HOST` 列出容器名称。

- **-M, --machine=**
  在本地容器上执行操作。指定要连接的容器名称。
- **-h, --help**
  打印简短的帮助信息并退出。
- **--version**
  打印简短的版本信息并退出。
- **--no-pager**
  不将输出通过分页器管道。

## 退出状态

成功时返回 0，否则返回非零的失败代码。

## DOT 的示例

示例 1. 绘制所有名称以“avahi-daemon”开头的单元的所有依赖项

```bash
$ systemd-analyze dot 'avahi-daemon.*' | dot -Tsvg > avahi.svg
$ eog avahi.svg
```

示例 2. 绘制所有已知目标单元之间的依赖关系

```bash
$ systemd-analyze dot --to-pattern='*.target' --from-pattern='*.target' | dot -Tsvg > targets.svg
$ eog targets.svg
```

## VERIFY 的示例

当前检测到的以下错误：

- 未知的部分和指令，
- 启动给定单元所必需的缺失依赖项，
- 在 *Documentation=* 中列出但在系统中未找到的手册页，
- 在 *ExecStart=* 及类似指令中列出但在系统中未找到或不可执行的命令。

### 示例 3. 拼写错误的指令

```bash
$ cat ./user.slice
[Unit]
WhatIsThis=11
Documentation=(1)
Requires=different.service

[Service]
Description=x

$ systemd-analyze verify ./user.slice
[.user.slice:9] Unknown lvalue 'WhatIsThis' in section 'Unit'
[.user.slice:13] Unknown section 'Service'. Ignoring.
Error: org.freedesktop.systemd1.LoadFailed: Unit different.service failed to load: No such file or directory.
Failed to create user.slice/start: Invalid argument
user.slice: man (1) command failed with code 16
```

### 示例 4. 缺失的服务单元

```bash
$ tail ./a.socket ./b.socket
==> ./a.socket <==
[Socket]
ListenStream=100

==> ./b.socket <==
[Socket]
ListenStream=100
Accept=yes

$ systemd-analyze verify ./a.socket ./b.socket
Service a.service not loaded, a.socket cannot be started.
Service b@0.service not loaded, b.socket cannot be started.
```

## 环境变量

$SYSTEMD_PAGER

在未给出 **--no-pager** 时使用分页器；覆盖 `$PAGER`。将其设置为空字符串或值“cat”等同于传递 **--no-pager**。

$SYSTEMD_LESS

覆盖传递给 `less` 的默认选项 ("FRSXMK")。

## 另见

systemd (1), systemctl (1), systemd (8), systemd.system.conf (5)

## SYSTEMD-ASK-PASSWORD

### 名称

systemd-ask-password - 向用户查询系统密码

### 概要

systemd-ask-password [OPTIONS...] [MESSAGE]

### 描述

**systemd-ask-password** 可用于使用命令行指定的问题消息向用户查询系统密码或口令。当从 TTY 运行时，它会在 TTY 上查询密码并将其打印到标准输出。当在没有 TTY 的情况下或带有 —**no-tty** 运行时，它将在全系统范围内查询密码，并允许活跃用户通过多个代理进行响应。后者仅对特权进程可用。

此工具的目的是查询全系统范围的密码——即未绑定到特定用户账户的密码。示例包括：插入时或启动时解锁加密硬盘，为 Web 和 VPN 服务器输入 SSL 证书口令。

现有的代理包括：使用 Plymouth 向用户询问密码的启动时密码代理；在控制台上直接向用户查询的启动时密码代理；通过 (1) 消息请求密码输入的代理；适用于在 GNOME 会话中运行的代理；可临时启动以处理排队密码请求的命令行代理；以及在 (1) 调用期间临时生成的 TTY 代理。

可以根据 **systemd 密码代理规范**[1] 实现额外的密码代理。

如果在 TTY 上查询密码，用户可以按 TAB 键以隐藏通常为每个输入字符显示的星号。按退格键作为第一个按键也会产生同样的效果。

### 选项

理解以下选项：

- **`--icon=`**
  在密码查询旁边指定一个图标，可用于支持图形显示的所有代理。图标应遵循 **XDG 图标命名规范**[2]。
- **`--timeout=`**
  指定查询超时时间（秒）。默认为 90 秒。超时时间为 0 表示无限期等待。
- **`--echo`**
  回显用户输入而不是将其掩码。这在将 systemd-ask-password 用于查询用户名时很有用。
- **`--no-tty`**
  即使当前 TTY 可用，也绝不在当前 TTY 上询问密码。始终使用代理系统。
- **`--accept-cached`**
  如果提供，则接受缓存的密码，即之前输入的密码。
- **`--multiple`**
  与 **`--accept-cached`** 配合使用时，接受多个密码。这将每行输出一个密码。
- **`-h`, **`--help`**
  打印简短的帮助信息并退出。

### 退出状态

成功时返回 0，否则返回非零的失败代码。

### 另见

systemd (1), systemctl (1), journalctl (8), systemd (1)

### 注释

1. systemd 密码代理规范
2. XDG 图标命名规范

## SYSTEMD-BOOTCHART

### 名称

systemd-bootchart - 启动性能图形工具

### 描述

**systemd-bootchart** 是一个工具，通常在系统启动时运行，用于从运行中的系统收集 CPU 负载、磁盘负载、内存使用率以及进程信息。收集的结果以 SVG 图形的形式输出。通常，systemd-bootchart 由内核通过在内核命令行上传递 `init=/usr/lib/systemd/systemd-bootchart` 来调用。然后，systemd-bootchart 将分叉出真正的 init 以恢复正常系统启动，同时在后台监控和记录启动信息。

在收集了一定数量的数据（通常是 15–30 秒，默认为 20 秒）后，记录停止，并根据记录的信息生成一个图形。该图形包含有关资源使用顺序以及系统启动过程中存在潜在问题位置的关键线索。它本质上是 **systemd-analyze plot** 功能的更详细版本。

当然，bootchart 也可以在任意时间点使用，以收集并绘制一段时间内的此类数据。在这种情况下，建议使用 `--rel` 开关。

Bootchart 不需要 root 权限，并且可以愉快地作为普通用户运行。

Bootchart 图形默认以带时间戳的形式写入 `/run/log`，并使用 `MESSAGE_ID=9f26aa562cf440c2b16c773d0479b518` 保存到日志中。日志字段 `BOOTCHART=` 包含 SVG 格式的 bootchart。

### 调用方式

**systemd-bootchart** 可以通过几种不同的方式调用：

#### 内核调用

内核可以调用 **systemd-bootchart** 而不是 init 进程。反过来，**systemd-bootchart** 将调用 `/usr/lib/systemd/systemd`。

#### 作为独立程序启动

可以从命令行像普通应用程序一样执行 **systemd-bootchart**。在此模式下，强烈建议传递 `-r` 标志，以便不绘制自启动以来到 systemd-bootchart 启动之前经过的时间，因为这可能会导致图形极其庞大。自启动以来经过的时间也可能包括系统挂起的时间。

### 选项

这些选项也可以在 /etc/systemd/bootchart.conf 文件中设置。参见 systemd-bootchart.conf (5)。

- **-h, --help**
  打印简短的帮助信息并退出。
- **-n, --sample N**
  指定要记录的样本数量 N。样本将以 --freq 定义的间隔进行记录。
- **-f, --freq f**
  指定样本日志频率，为正的实数 f，单位为 Hz。大多数系统可以处理高达 25–50 的值而不会创建过多的开销。
- **-r, --rel**
  使用相对时间而不是绝对时间。这对于在启动后使用 bootchart 来分析已启动的系统很有用。如果没有此选项，图形将变得极其庞大。如果设置，水平轴从第一个记录的样本开始，而不是从时间 0.0 开始。
- **-F, --no-filter**
  禁用对对启动没有显著贡献的任务的过滤。寿命太短（仅在一个样本中可见）或不消耗显著 CPU 时间（少于 0.001 秒）的进程将不会在输出图形中显示。
- **-C, --cmdline**
  显示进程的完整命令行及参数，而不是仅显示进程名称。
- **-g, --control-group**
  显示进程控制组
- **-o, --output path**
  指定图形的输出目录。默认情况下，bootchart 将图形写入 /run/log。
- **-i, --init path**
