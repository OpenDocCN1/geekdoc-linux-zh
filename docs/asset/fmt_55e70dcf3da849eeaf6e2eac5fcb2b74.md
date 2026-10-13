
```
/var/saf/zmon/log
Fri Oct 20 10:02:49 2000; 393: PMTAG: zmon
Fri Oct 20 10:02:49 2000; 393: Starting state: enabled
Fri Oct 20 10:02:49 2000; 393: Get SC_ENABLE message
Fri Oct 20 10:02:49 2000; 393: max open files = 1024
Fri Oct 20 10:02:49 2000 393; max ports ttym can monitor = 1017
Fri Oct 20 10:02:49 2000 393; *ptr == 0
Fri Oct 20 10:02:49 2000 393; SUCCESS
Fri Oct 20 10:02:49 2000 393; *ptr == 0
Fri Oct 20 10:02:49 2000 393; Initialization Completed
```

# 250 理解服务访问设施 (SAF)

下面的示例显示了 `/var/saf/tcp/log` 文件末尾。`pmtag` `tcp` 是监听端口监控器的默认值。

```
tail /var/saf/tcp/log
04/06/2000 15:11:12 183; Connect: fd 7, svctag lpd, seq 117, type passfd
04/06/2000 15:12:16 183; Connect: fd 7, svctag lpd, seq 118, type passfd
04/06/2000 15:26:12 183; Connect: fd 7, svctag lpd, seq 119, type passfd
04/06/2000 15:26:13 183; Connect: fd 7, svctag lpd, seq 120, type passfd
04/06/2000 15:34:41 183; Connect: fd 7, svctag lpd, seq 121, type passfd
04/06/2000 15:53:04 399; NLFS (lp) passfd:/var/spool/lp/fifos/listenS
04/06/2000 15:50:14 183; Connect: fd 7, svctag lpd, seq 122, type passfd
04/06/2000 16:05:12 183; Connect: fd 7, svctag lpd, seq 123, type passfd
04/06/2000 16:05:12 183; Connect: fd 7, svctag lpd, seq 124, type passfd
```

> 注意。你应该定期清理或截断这些日志文件。如果你创建了 cron 任务，请参考 `crontab(1)` 手页更多信息。

# SAF 命令、任务和选项

以下章节提供了 SAF 命令中变量的快速参考；`sacadm` 和 `pmtag` 命令的任务，以及 `sacadm`、`pmtag`、`ttyadmin` 命令的选项。参考第 11 章“设置调制调器和终端”，了解如何使用 SAF 命令设置调制调器和终端的步骤。参考第 12 章“设置服务”，了解如何使用 SAF 命令设置打印机的步骤。

## SAF 变量快速参考

| 变量 | 示例 | 描述 |
| :--- | :--- | :--- |
| `dev-path` | `/dev/term/` | TTY 设备文件的完整名称。 |
| `pmtag` | `zsmon` | 特定端口监控器实例名称。 |
| `svctag` | `b` | `/dev/term/` 中的端口名称。 |
| `ttylabel` | `2400` | `/etc/ttydefs` 中的波特率和线路规范。 |
| `type` | `ventel` | `/etc/ttdevices` 中指定的调制调器类型。 |

## 服务访问控制 (sacadm) 快速参考

| 任务 | 命令语法 |
| :--- | :--- |
| 添加端口监控器 | `sacadm -a -p pmtag -t ttymon /lib/saf/listen -v ttyadm -V "comment"` |
| 禁用端口监控器 | `sacadm -d -p pmtag` |
| 启用端口监控器 | `sacadm -e -p pmtag` |
| 杀死端口监控器 | `sacadm -k -p pmtag` |
| 列出端口监控器的状态信息 | `sacadm -l -p pmtag` |
| 移除端口监控器 | `sacadm -r -p pmtag` |
| 启动端口监控器 | `sacadm -s -p pmtag` |
| 添加监听端口监控器 | `sacadm -a -p pmtag -t listen /lib/saf/listen -v ttyadm -V "comment"` |

## sacadm 命令快速选项

| 选项 | 描述 |
| :--- | :--- |
| `-a` | 添加端口监控器。`-a` 选项需要 `-c` 选项。 |
| `-c` | 执行启动端口监控器的命令字符串。仅用于 `-a`。 |
| `-d` | 禁用 `pmtag` 端口监控器。 |
| `-e` | 启用 `pmtag` 端口监控器。 |
| `-f` | 指定一个或两个标志。`-f` 标志不启用指定的服务。`-f` 标志为服务创建条目。 |
| `-k` | 停止 `pmtag` 端口监控器。 |
| `-l` | 列出服务信息。 |
| `-L` | 与 `-l` 相同，但以紧凑格式输出。 |
| `-n` | 设置重启计数。如果不指定重启计数，则默认为 0。计数 0 表示如果端口监控器失败，不重启。 |
| `-p` | 为端口监控器指定标识监控标记 (`pmtag`)。 |
| `-r` | 移除 `pmtag` 端口监控器。 |
| `-s` | 启动 `pmtag` 端口监控器。 |
| `-t` | 指定端口监控器的类型——可以是 `ttymon` 或 `listen`。 |
| `-v` | 指定端口监控器的版本号。使用 `ttyadm -V` 查找版本号，或将 `ttyadm -V` 作为 `-v` 选项的参数。 |
| `-x` | 在无选项的情况下，读取 `_sactab` 数据库文件。`-x` 选项配合 `-p` 读取 `pmtag` 管理文件。 |
| `-y` | 在 `pmtag` 端口监控器的 `_sactab` 条目中包含注释。 |

## 端口监控管理 (pmadm) 快速参考

| 任务 | 命令语法 |
| :--- | :--- |
| 添加标准终端服务 | `pmadm -a -p pmtag -s svctag -i root -v ttyadm -V -m ttyadm -i 'terminal disabled.' -1 contty -ldmtty,ttcompat -d dev-path -s /usr/bin/login` |
| 禁用 ttym 端口监控器 | `pmadm -d -p pmtag -s svctag` |
| 启用 ttym 端口监控器 | `pmadm -e -p pmtag -s svctag` |
| 列出所有服务 | `pmadm -1` |
| 列出一个 ttymon 端口监控器的状态信息 | `pmadm -1 -p pmtag` |
| 列出一个 ttymon 端口监控器上运行的服务的状态信息 | `pmadm -1 -p pmtag -s svctag` |
| 添加监听服务 | `pmadm -a -p pmtag -s 1lp -i root -v nlsadmin -V -m nlsadmin -o /var/pool/1lp/fifos/listenS5` |
| 禁用监听端口监控器 | `pmadm -d -p pmtag -s 1lp` |
| 启用监听端口监控器 | `pmadm -e -p pmtag -s 1lp` |

| Option | Description |
| --- | --- |
| `-a` | 添加服务。 |
| `-d` | 在端口监控器的管理文件中 `svctag` 服务条目的标志字段中添加 `x` 以禁用该服务。此条目由 `pmtag` 端口监控器使用。 |
| `-e` | 从端口监控器的管理文件中 `svctag` 服务条目的标志字段中移除 `x` 以启用该服务。此条目由 `pmtag` 端口监控器使用。 |
| `-f xu` | 指定一个或两个标志。`x` 标志不启用指定的服务。`u` 标志为服务创建 utmpx 条目。 |
| `-i id` | 指定在启动服务时分配的标识。 |
| `-l` | 列出服务信息。 |
| `-L` | 与 `-l` 相同，但以紧凑格式列出输出。 |
| `-m` | 识别包含在 `-a` 命令行中的端口监控特定选项。 |
| `-p pmtag` | 指定端口监控标记 (`pmtag`)——例如 `zsmon`。 |
| `-r` | 从端口监控器的管理文件中移除该服务的条目。 |
| `-s svctag` | 指定与给定服务关联的服务标记 (`svctag`)——例如用于串口 A 的 `ttya`。 |
| `-t type` | 指定端口监控类型。 |
