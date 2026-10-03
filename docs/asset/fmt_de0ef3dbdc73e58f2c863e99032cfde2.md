
### (3) xkill

`xkill` 是在桌面中使用图形界面的工具。比如当某个图形程序假死不能退出时，运行 `xkill`，用光标标记图形界面就可以杀死，如果想终止 `xkill`，只需点击右键即可。

例如，要杀死 `firefox` 这个进程，首先在命令下运行 `xkill`，将输出“Select the window you wish to kill with...”字样，此时鼠标箭头变成一个叉图标。用此光标左点击 `firefox` 的界面，将立即杀死，同时终端将输出“xkill: killing creator of resource 0x4a008c”，表示已经将 `firefox` 杀死，清单 10-27 所示。

# 清单 10-27

```
xkill
Select the window you wish to kill with button 1...
xkill: killing creator of resource 0x4a008c
```

## 10.3.4 知识点4 Systemd

Systemd 是 system management daemon 的简写，主要用来初始化和管理系统服务。Systemd 功能强大，好用方便，在当前大多数的 Linux 发行版中（RHEL/CentOS 7+、Ubuntu 15.0+）Systemd 代替了从 UNIX 继承来的 System V 古老的 `init` 程序以及以后的 `Upstart`，成为系统管理的核心。

`systemctl` 是用于管理服务的工具，常用命令如下：

| 命令 | 说明 |
|---|---|
| `status` | 显示单元运行状态 |
| `start` | 启动单元 |
| `stop` | 停止单元 |
| `reload` | 重新加载配置 |
| `restart` | 重启单元 |
| `kill` | 向单元发送信号 |
| `is-active` | 检查单元是否激活状态 |
| `is-failed` | 检查单元是否失败状态 |
| `set-property` | 修改运行时属性 |
| `list-units` | 列出所有运行的单元 |
| `list-unit-files` | 列出所有安装的单元文件 |
| `isolate` | 切换运行级别 |
| `get-default` | 获取默认目标 |
| `set-default` | 设置默认目标 |
| `default` | 进入默认运行模式 |
| `rescue` | 进入恢复模式 |
| `halt` | 关闭系统 |
| `poweroff` | 关闭系统并断电 |
| `reboot` | 重启系统 |
| `suspend` | 挂起到内存 |
| `hibernate` | 进入混合睡眠 |
| `daemon-reload` | 重新加载守护进程配置 |

## 10.3.5 注意事项

- `list-unit-files` [单元]: 列出所有安装的单元文件及其启用状态（`status` 单元）
- 单元文件名: 启用指定的单元或单元实例（将这些单元设置为硬件自动启动）
- `is-enabled`: 检查是否有至少一个单元实例被启用（使用 `is-enabled` 命令）
- `mask` 单元文件: 屏蔽指定的单元或单元实例
- `unmask` 单元文件: 取消指定的单元或单元实例的屏蔽，这是 `mask` 命令的动作

## 10–15 systemctl list-units 命令的输出字段

| 字段 | 含义 |
| --- | --- |
| `UNIT` | 单元名称及加载状态 |
| `LOAD` | 单元激活状态 |
| `ACTIVE` | 单元子状态，与单元类型有关 |
| `DESCRIPTION` | 单元的简单说明 |

10-30 使用 `systemctl list-units` 和 `list-files` 命令都可以查看类型（`--type` 选项）或者指定状态（`--state` 选项）的 unit 或者单元文件，如清单 10-30 所示。

```bash
# 查看服务类型的单元文件
# systemctl list-files --type=service

# 查看 类型的 unit
# systemctl list-units --type=mount

# 查看状态为 enabled 的单元文件
# systemctl list-files --state=enabled

# 查看状态为 plugged 的 unit
# systemctl list-units --state=plugged
```

### (2) 查看单元/单元组件

下面以最常用的系统服务——远程连接服务 `sshd` 为例，演示如何具体查看一个 unit 的状态。

**例 3**: 查看 `sshd` 服务是否处于正在运行或者启动失败的状态，如清单 10-31 所示。

```bash
# 10-31
# 查看 sshd 服务是否正在运行，输出状态为正在运行
# systemctl is-active sshd.service
active

# 查看 sshd 服务是否启动失败
# systemctl is-failed sshd.service
active
```

**10-32 例 4**: 查看 `sshd` 服务的运行状态，及其最近的数据，如清单 10-32 所示。

```bash
# 列出运行时的状态信息及其最近的数据
# systemctl status sshd.service
● sshd.service - OpenSSH server
   Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: enabled)
   Active: active (running) since 2023-10-27 22:15:43 CST; 1h ago
   Docs: man sshd_config
   Main PID: 1300 (sshd)
   CGroup: system.slice/sshd.service
     └ 1300 /usr/bin/sshd -D
2023-10-27 22:15:43 systemd[1]: Starting OpenSSH server daemon.
2023-10-27 22:15:43 sshd[1300]: Server listening on 0.0.0.0:22.
```

# 10-30 管理进程和服务

```text
2023-10-27 22:15:43 sshd[1300]: Server listening on 0.0.0.0:22.
2023-10-27 22:15:43 systemd[1]: Started OpenSSH server daemon.
2023-10-27 22:32:40 sshd[1259]: Accepted password for root from 192.168.4.10 port 2255
2023-10-27 22:33:30 sshd[1265]: Accepted password for root from 192.168.1.16 port 2312
```

`status` 命令的输出内容分为两部分：第一部分是单元最近的（最多10条）日志；第二部分是运行状态的信息，可以分为6个部分，如下 10-16 所示：

| 序号 | 含义 |
| --- | --- |
| 1 | 在彩色终端上，前导点 (●) 使用不同的颜色标记状态。白色表示 inactive or deactivating；红色表示 active or failed；绿色表示 active or reloading or activating |
| 2 | “Loaded:” 开头的显示了单元的加载状态：loaded 已加载到内存中；error 表示失败；not-found 表示未找到；masked 表示单元被屏蔽。该行还包含了单元的路径、启动状态、预设启动状态。 |
| 3 | “Active:” 开头的显示了启动状态：active 表示已激活；inactive 表示未启动；activating 表示正在启动中；deactivating 表示正在停止；failed 表示启动失败（崩溃、超时等）。对于启动失败的单元，会在日志中记录失败的原因。 |
| 4 | “Doc:” 开头的显示了单元及其配置文件的帮助文档 |
| 5 | “Main PID:” 开头的显示了单元主进程的 PID |
| 6 | “CGroup:” 开头的显示了单元控制组（Control Group）中的所有进程 |

表 10-16 单元状态说明

**例 5**. 查看 ssh 服务是否被启用（用于提供服务，一般服务会自动启动），显示 `enabled` 表示启用：

```bash
# 查看 ssh 服务是否启用
# systemctl is-enabled sshd.service
enabled
```

### (3) 操作单元

操作单元的常见动作包括启动（`start`）、重启（`restart`）、停止（`stop`）、屏蔽（`mask`）、解除屏蔽（`unmask`）、启用（`enable`）和禁用（`disable`）。

**例 6**：启动、重启和停止单元（`sshd` 服务），使用清单 10-34：

- 在操作单元时，需要明确指出单元名和单元类型（type）。例如 `httpd.service` 或者 `dbus.socket`。
- 如果不指定类型，默认类型就是 `service`。

```bash
# 立即启动 sshd 服务
# systemctl start sshd

# 立即重启 sshd 服务
# systemctl restart sshd

# 立即停止 sshd 服务
# systemctl stop sshd
```

对于不同的单元，对待是不一样的。例如，对于 `service` 类型的单元，`restart` 和 `stop` 的动作也是一样的。

**例 7**：启用（`enable`）和禁用（`disable`）单元（`httpd` 服务），如清单 10-35 所示：

```bash
# 启用 httpd 服务
# systemctl enable httpd
Created symlink /etc/systemd/system/multi-user.target.wants/httpd.service -> /usr/lib/systemd/system/httpd.service
httpd 已启用
# systemctl is-enabled httpd

# 禁用 httpd 服务
# systemctl disable httpd
Removed symlink /etc/systemd/system/multi-user.target.wants/httpd.service
httpd 已禁用
# systemctl is-enabled httpd
```

启用单元来说，在大多数时候相当于将这些单元在配置时设置为“开机自动启动”或“某个目标自动启动”。事实上，启用单元是通过创建文件的符号链接实现的。

**注意**：
- 使用 `--now` 选项，屏蔽（`mask`）一个单元不会导致该单元激活（`start`），解除屏蔽（`unmask`）一个单元也不会导致该单元停止（`stop`）。
- 若使用了 `--runtime` 选项，则表示仅临时屏蔽（重启后屏蔽将失效），否则默认为永久屏蔽。

**例 8**：屏蔽（`mask`）和取消屏蔽（`unmask`）单元，如清单 10-36：

```bash
# 屏蔽 ssh 服务
# systemctl mask httpd
Created symlink /etc/systemd/system/httpd.service to /dev/null.

# 屏蔽后，httpd 服务无法启动
# systemctl start httpd
Failed to start httpd.service: Unit is masked.

# 屏蔽后，httpd 服务无法启动
# systemctl enable httpd
Failed to execute operation: Cannot send after shutdown
```

```bash
# 取消屏蔽服务
# systemctl unmask httpd
Removed symlink /etc/systemd/system/httpd.service.

# 成功启用 httpd
# systemctl enable httpd
```

**例 9**：加载（`reload`）、修改（`set-property`）和查看（`show`）单元的配置，如清单 10-37。

```bash
# 重新加载 sshd 服务的配置文件
# systemctl reload apache.service

# 重新加载 systemd 守护进程的配置
# systemctl daemon-reload

# 显示 sshd 服务所有参数
# systemctl show httpd.service
```

```bash
# 获取 httpd 服务的 CPU 分配限制额
# systemctl -p CPUShares httpd.service

# 设置 httpd 服务 CPU 分配限制额为 200
# systemctl set-property httpd.service CPUShares=500
```

`poweroff`: 退出系统并关电源。大致相当于执行 `systemctl start poweroff.target --job-mode=replace-irreversibly --no-block` 命令，并同时向用户显示一条警告信息，如清单 10-44 所示。

## 清单 10-44

```
# systemctl poweroff
```

> **注意**
>
> - 使用一次 `-force` 选项，将尝试正常停止而非直接杀死所有进程，强制卸载文件系统（或以只读模式重载），并立即关闭系统。
> - 使用两次 `-force` 选项，将跳过杀死和卸载文件系统的步骤，立即关闭系统，这会导致数据丢失、文件系统不一致等不良后果。

- `reboot`: 重启系统。大致相当于执行 `systemctl start reboot.target --replace-irreversibly --no-block` 命令，并同时向所有用户显示一条警告信息，如清单 10-45 所示。

## 清单 10-45

```
# systemctl reboot
```

- `suspend`: 休眠到内存。相当于执行 `systemctl start suspend.target` 命令，如清单 10-46 所示。

## 清单 10-46

```
# systemctl suspend
```

- `hibernate`: 休眠到硬盘。相当于执行 `systemctl start hibernate.target` 命令，如清单 10-47 所示。

## 清单 10-47

```
# systemctl hibernate
```

- `hybrid-sleep`: 进入混合休眠模式。同时休眠到内存和硬盘。执行 `systemctl start hybrid-sleep.target` 命令，如清单 10-48 所示。

## 清单 10-48

```
# systemctl hybrid-sleep
```

## 使用 at 和 crontab 计划任务

计划任务是系统自动完成的一种方式。就像闹钟一样，到了某个时间点，系统就会自动执行某些操作，实现想要的目的。在实际生活中有很多例子，例如定时发送邮件、定时备份、定时检查服务器利用率并提醒管理员。Linux 提供了 `at` 和 `crontab` 两种计划任务机制，用户能够灵活地安排计划任务以满足生产需求。

### (1) 安排计划任务

就像闹钟一样，Linux 能够在某时刻执行计划任务，`at` 就是命令。首先要确定 `at` 的守护进程是否在运行（一般情况下 `at` 是启动的），如所示：

```bash
$ systemctl status atd
● atd.service - Spooling Job
   Loaded: loaded (/lib/systemd/system/atd.service; enabled; preset: enabled)
   Active: active (running) since 2018-11-19 22:57 CST; 24min ago
   Main PID: 1246 (atd)
   Group: system.slice
```

如果 `atd` 未启动，就将其启动，如清单 10-49 所示。由于 `at` 本身是一个系统服务（守护进程），无法交互，系统提供了一个名为 `at` 的命令与其交互。

## at 命令

用法：`at [选项] [时间]`
功能：在指定的时间执行命令。`at` 命令的常用选项如下表 10-50 所示：

| 选项 | 说明 |
| :--- | :--- |
| `-file` | 从文件读取标准输出 |
| `-l` | 列出队列中等待执行的任务 |
| `-d` | 查看具体的时间 |
| `-c` | 查看任务的内容 |

使用 `at` 命令有多种方式，下面介绍几种方式的使用：

- **交互式定义任务**：在命令行输入 `at` 命令后，进入 `at` 的任务界面，在提示符下方输入任务要执行的命令，一旦定义，将输出任务号和执行时间，按 `Ctrl+D` 组合键结束。

```
at 13:00
at> echo "Hello!"
at> ^D
job 1 at Tue 20 13:00 2018
```

- **查看计划任务并尝试执行**：

```bash
$ at -l
Mon Aug 28 10:55:00 root
```

- **管道/通用定义任务**：在安排计划任务时，接收的是标准输入的内容，可以使用管道或者 here-document 重定向来执行计划任务。

```bash
echo "Hello" | at @12:00
job 2 at Wed Nov 21 12:00:00 2018
```

- **用 here-document 重定向**：

```bash
at @12:05 <<EOF
echo "Hello, Linux!"
EOF
job 3 at Wed Nov 21 12:05:00 2018
```
