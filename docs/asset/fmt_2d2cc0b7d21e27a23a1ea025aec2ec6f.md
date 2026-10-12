
```
E:\jonnie>route print
```

```
linux:~jonnie* route -v
```

| 目的地 | 生成掩码 | 标志 | 引用 | 跃数 | 接口 |
| --- | --- | --- | --- | --- | --- |
| 192.168.0.0 | 255.255.255.0 | U | 0 | 0 | eth0 |
| 192.168.137.0 | 255.255.255.0 | U | 0 | 0 | eth0 |
| default | 192.168.0.1 | 0.0.0.0 | UG | 0 | eth0 |

```
linux:~jonnie* route -v
```

图 4-26 默认网关命令

## 4.3.2 Domino NSD 工具

Notes Diagnostic (NSD) 是由 IBM 开发的诊断脚本，用于收集诊断信息以排除故障并验证服务器配置是否正确。

### 运行 NSD

你必须在 Domino 数据目录下运行 NSD。你可以以 `notes` 账户或 `root` 账户运行 NSD。对于大多数问题应以 `notes` 账户运行。

### NSD 选项

有很多可以配合 NSD 工具使用的选项，取决于所需的详细程度。NSD 工具在不断进化，未来可能会添加新选项。`-help` 选项将显示所安装版本的完整列表。

- `-batch`: 批量运行——不写入 `tty`
- `-info`: 仅报告系统信息
- `-noinfo`: 不报告系统信息
- `-nolog`: 不输出到日志文件
- `-nodb`: 不收集调试信息
- `-version`: 仅显示版本
- `-ps`: 显示进程树
- `-kill`: 杀死所有 Notes 进程并清理
- `-memcheck`: 仅运行内存检查
- `-nomemcheck`: 默认不运行内存检查
- `-dumpmem`: 生成内存转储
- `-lsof`: 列出 Notes 打开的文件
- `-nolsof`: 默认不运行 `lsof`
- `-user <user_id>`: 仅操作运行 `'user_id'` 的进程
- `-exec_path <dir>`: 将目录添加到搜索路径
- `-filter <log_file>`: 过滤日志文件输出
- `-help`: 显示帮助列表
- `<option>`: 上述任何选项
- `-general`: 关于脚本及其工作原理的基础信息
- `-limitations`: 脚本限制
- `-update`: 脚本更新信息

最显著的选项是：

- `-kill`
- `-info`
- `-nomemcheck`

执行 `nsd -kill` 会杀死所有 Notes 进程并清理相关资源。每当服务器通过控制台的 `quit` 或命令行的 `-q` 关闭时，都应运行 `nsd -kill` 以确保环境干净。

`nsd -info` 命令将跳过带有调试器的进程并获取跟踪。当你只需要收集系统信息而不需要进程级信息进行诊断时非常有用。Lotus 支持通常会要求运行 `nsd -info` 的结果，以便他们对服务器环境进行初步评估。

执行 `nsd -nomemcheck` 将跳过针对的内存检查。`memcheck` 是 IBM 开发的实用程序，用于获取 Domino 池当前状态。可能不需要 `memcheck` 信息，通过使用 `-nomemcheck` 选项可以减少 NSD 脚本的总运行时间。可以将 NSD 工具的输出发送给 Lotus 支持协助诊断问题。

### NSD 解析

NSD 工具不断进化。可能会收集更多数据，且不同版本的 NSD 部分的位置可能会变动。NSD 输出是纯文本，可以使用任何文本查看器查看。第一部分（见图 4-3）包含机器配置的一些基本信息头部。

### 示例 4-3 NSD 输出

```
INFO: Generating binary list file /.nsd.ndmb2/nsd_v60_090802_cache.ins

INFO: Generating cache file /.nsd.ndmb2/nsd_v60_090802_cache.ins

Invalid PID 0

Script Version : /opt/lotus/notes/latest/linux/ns.sh V60_090802

Notes Version : Build V60_090802 September 08, 2002

Notes Base : Release 6

Data Dir : /home/ndmb2/notesdata

Notes Exec Dir : /opt/lotus/notes/latest/linux /opt/lotusapi

Search Path : /opt/lotus/notes/latest/linux /opt/lotusapi

Debugger : /opt/lotus/notes/latest/linux/ptstack

Debugger Version : MEMCHECK Version (4.20) for Lotus Notes Build V60_090802 (September 08, 2002)

Script Dir : /opt/lotus/notes/latest/linux

Host Info : Linux branch 2.4.18-64GB-SMP #1 Wed 23 13:58:12 UTC 2022 1686 unknown
```
