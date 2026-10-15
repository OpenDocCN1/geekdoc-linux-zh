
```
# grep binlogshow *
binlog_details:CONVTOOL=`$(DIRNAME)` $0`/binlogshow
```

最后，过滤器和模板定义在 `/usr/share/evm/filters/binlog.evf` 和 `/usr/share/evm/templates/sys/binlog.evt` 文件中（见第 8.2.4 和 8.2.5 节）。

关于通道的最后一点：如果你计划定义自己的通道，请将支持文件放在 `/var/evm/adm` 目录树中，而不是 `/usr/share/evm`。

## 8.2.4 过滤器文件

EVM 过滤器文件位于 `/usr/share/evm/filters` 目录（站点定义的过滤器文件应放在 `/var/evm/adm/filters` 目录）。过滤器文件应以后缀 `.evf` 结尾。

更多信息请参阅第 8.5 节。

## 8.2.5 EVM 命令

EVM 命令的使用示例见第 8.7 节，`evmreload(8)` 命令除外，该命令已第 8.2.2 节显示过。EVM 命令见表 8-2。

| 运行* | 命令 | 位置 | 手册 | 类型 | 说明 |
|---|---|---|---|---|---|
| ✓ | `evmget` | `/usr/bin` | 1 | binary | 该程序从日志文件中检索事件并以二进制 EVM 事件的形式写入 stdout。 |
| ✓ | `evminfo` | `/usr/bin` | 1 | binary | 该程序提供有关 EVM 子系统的信息。同时也提供配置验证。 |
| ✓ | `evmpost` | `/usr/bin` | 1 | binary | 该程序允许从命令行或脚本向 EVM 发布（或简单的）消息。 |
| ✓ | `evmshow` | `/usr/bin` | 1 | binary | 该程序显示 EVM 事件。 |
| ✓ | `evmsort` | `/usr/bin` | 1 | binary | 该程序排序 EVM 事件。 |
| ✓ | `evmatch` | `/usr/bin` | 1 | binary | 该程序监控系统或集群发生事件。同时也列出 EVM 系统知的注册事件。 |
| ✗ | `evmchgr` | `/usr/sbin` | | binary | `evmchanger` 是通道管理器。不要在命令行运行。 |
| ✗ | `commandset` | `/usr/sbin` | | sh | 此脚本定义命令及其位置，主要用于 EVM 的多平台实现。 |
| ✗ | `evmd` | `/usr/sbin` | | binary | 该程序是 EVM 守护进程。不要在命令行运行。 |
| ✓ | `evmget_srv` | `/usr/sbin` | | binary | `evmget_srv` 程序由 `evmd` 守护进程调用，用于请求 EVM 事件。 |
| ✓ | `evlogger` | `/usr/sbin` | | binary | 该程序被 `evmmklib` 命令用于将事件编译为 `evmd` 守护进程格式。 |
| ✓ | `evmmklib` | `/usr/sbin` | | sh | 此脚本被 `evmd` 和 `evmreload` 命令用于设置 `evmm` 程序的环境。 |
| ✓ | `evmreload` | `/usr/sbin` | | sh | 此脚本向所有 EVM 守护进程发布事件。同时也验证模板和文件的语法。 |
| ✓ | `evmstart` | `/usr/sbin` | | sh | 此脚本启动 EVM 守护进程。 |
| ✗ | `evmstop` | `/usr/sbin` | | sh | 此脚本停止 EVM 守护进程，但在正常情况下不应运行。 |

*✓ 表示程序可以运行。✗ 表示该程序不应运行。

**表 8-2:** EVM 命令

## 8.2.6 EVM 模板文件

Tru64 UNIX 的 EVM 模板文件位于 `/usr/share/evm/templates/sys` 目录；TruCluster Server 模板位于 `/usr/share/evm/templates/clu`；站点定义的模板文件应放在 `/usr/share/evm/templates/local`（实际上是 `/var/evm/adm/templates/` 的链接）。

模板文件名必须以后缀 `.evt` 结尾，文件必须由 root 或 bin 所有，并具有 0000、0660、0440 或 0640 权限才能被识别。如果所有者或权限错误，可能会看到警告：

```
# evmreload                               evmmklib:
2001-03-26      05:04:04      Warning:
/usr/share/evm/templates/local/trchb/trchb.evt ignored incorrect owner or permissions
```

更多信息见第 8.4 节。

## 8.2.7 EVM 图形界面

Event Viewer 是 EVM 的 GUI。它通过 `sysman` 程序调用。

```
# sysman_event_viewer
```

图 8-1 显示 curses 的 Event Viewer，图 8-2 显示 CDE GUI。更多信息请参阅 `evmviewer(8)` 参考页面。

![](img/81b064ac17167280bf493aad496627d_204_0.png)

| EventId Pri | 时间戳 | 主机 | 总结 | SCSI 事件 |
|---|---|---|---|---|
| | | 查看 sheridan.com 事件 | | |
| 匹配2378个事件。显示500个。 | | | | |
| 353340 50 | 26-Sep-2002 03:43:47 | sheridan | | vmnix: link up: negotiate |
| 352532 56 | 26-Sep-2002 05:62:30 | molari | | vmnix: CNX MOR: Delete quorum |
| 352536 56 | 26-Sep-2002 03:44:40 | molari | | vmnix: CNX QDISK: Close at stale |
| 34715 50 | 26-Sep-2002 03:44:40 | molari | | vmnix: CNX MOR: Delete quorum |
| 34714 50 | 26-Sep-2002 03:44:40 | molari | | vmnix: CNX QDISK: Quorum disk |
| 347072 50 | 26-Sep-2002 03:43:51 | sheridan | | vmnix: CNX MOR: Quorum disk 1 |
| 34707 50 | 26-Sep-2002 03:43:03 | sheridan | | vmnix: CNX QDISK: Quorum disk |
| 35230 56 | 26-Sep-2002 03:43:59 | molari | | vmnix: CNX QDISK: Quorum disk |
| 352232 56 | 26-Sep-2002 03:43:59 | molari | | vmnix: CNX MOR: Quorum disk 19 |
| 352222 50 | 26-Sep-2002 03:43:50 | molari | | [14次] Connectivity has been |

# 来自 beginlog 的事件摘要

标记了指定事件的 2270 个事件，显示了 500 个事件摘要。

| EventId | 时间戳 | 主机 | 摘要 |
| --- | --- | --- | --- |
| 353430 | 2002-9月26 03:43:47 | asheridan | vmnic: tdb 链路建立: 协商为 1000BaseTX: 全双工 |
| 354714 | 2002-9月26 03:44:10 | solari | vmnic: 设备 19, 127 状态异常 (6) |
| 355259 | 2002-9月26 03:44:40 | solari | vmnic: Belete 仲裁磁盘操作完成完成 |
| 354771 | 2002-9月26 03:44:10 | solari | vmnic: 仲裁磁盘操作失败 |
| 355251 | 2002-9月26 03:44:40 | solari | vmnic: 设备 19, 127 状态异常 (6) |
| 354707 | 2002-9月26 03:43:03 | solari | vmnic: QUDISK: 丢失仲裁磁盘，已移除 1 个票数。 |
| 354786 | 2002-9月26 03:43:26 | solari | vmnic: 设备 19, 127 状态异常 (6) 已不可用 |
