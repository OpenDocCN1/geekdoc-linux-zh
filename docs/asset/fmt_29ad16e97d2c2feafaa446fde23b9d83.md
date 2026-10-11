
`perror` 显示 NetBackup 状态和故障排除信息，或来自 NetBackup 错误目录的条目。它显示与在线故障排除器（在活动监器或报告应用程序中）相同来源的信息，或来自 NetBackup 错误目录的信息。

`bpexdate` 修改镜像目录和介质目录中备份的过期日期。它还用于更改 NetBackup 介质目录的可移除介质的过期时间。

`bpimagelist` 查询 NetBackup 目录并生成 NetBackup 镜像状态的报告。它将生成一或两种类型的报告：

- 报告满足一组标准的镜像（如果不存在 `-media` 参数）
- 报告满足一组标准的可移除介质（如果不存在 `-media` 参数）

`bimmedia` 查询 NetBackup 镜像目录并报告 NetBackup 镜像的状况。它可以生成两份报告：

- 介质上的镜像报告 (Images-on-Media)
- Spangurops 报告

`bpimport` 导入已过期或来自另一个 NetBackup 或 Backup Exec 服务器的 NetBackup 和 Backup Exec 备份。

`bplabel` 在磁带介质上写入 NetBackup 标签。仅对最后一次用于 NetBackup 目录备份或由非 NetBackup 应用程序介介质标记。你也可以用它来分配特定的介质 ID。

`bplist` 根据你指定的选项列出 NetBackup 服务器上已备份和归档的文件。

`bppdelete` 从 NetBackup 数据库中删除策略。

`blist` 列出 NetBackup 数据库中的策略和策略信息。

`bpmedia` 冻结、解冻、暂停或暂停单个 NetBackup 介质 ID，允许或不允许未来的备份或归档指向该介质。注意，此命令仅适用于由 Media Manager 管理的介质。

`bpmedelist` 通过查询一个或多个 NetBackup 介质目录显示 NetBackup 状态，并生成 NetBackup 介质状态的报告。

`bpminlicense` 管理 NetBackup 许可文件。

`bpclients`, `bpclclients` 管理 NetBackup 策略中的客户端。

`bpllinfo`, `bpclinfo` 初始化、修改或显示 NetBackup 策略的属性。

`bpllinclude`, `bpclinclude` 维护 NetBackup 策略的文件列表。这是当 NetBackup 为该策略运行自动备份时被备份的文件列表。

`bppisched`, `bppclished` 向策略添加、删除或列出 NetBackup 计划。

`bppisched`, `bppclishedred` 修改 NetBackup 计划的属性。运行此命令时，由 `bppisched` 指定的计划和策略应该已经存在。

`bpolycew`, `bppiclassnew` 创建副本或重命名 NetBackup 策略。

`bcover` 启动恢复 NetBackup 内部数据库的 NetBackup 工具，并根据《NetBackup 系统管理员指南》中描述的过程恢复已备份的目录。该命令有两个模式：列出和恢复。

`bpstore` 从 NetBackup 服务器恢复文件或目录。

`bpstuard` 创建 NetBackup 存储单元组或存储单元。

`bpstudistat` 显示一个或所有 NetBackup 存储单元或存储单元组的属性。

`bpsture` 通过替换 NetBackup 目录中选定的存储单元或存储单元组属性，修改现有的 NetBackup 存储单元。

`bpverify` 验证由 NetBackup 创建的备份。

`cat_convert` 在版本 3.4 和 4.0 之间，或在 4.5 ASCII 格式和 4.5 二进制格式之间转换 NetBackup 目录 `.f` 文件。

`nbddbport` 设置 `nbddb` 数据库服务使用的 TCP/IP 端口。

`nbddbptw` 修改 `nbddb` 数据库服务使用的密码。

`vopied` 提供 VERITAS 一次密码认证的守护进程。

`vopie_util` 管理本地 `vopie` 认证文件。

## UNIX 和 Windows Media Manager 命令

大多数命令在 UNIX 和 Windows 之间是通用的。异常情况已注明。

- `acsd` 自动磁带系统 (ACS) 守护进程，与 Media Manager 接口，在自动磁带系统 (ACS) 控制下自动装载和卸载磁带。
- `lmfd`, `ifcd` 库管理设施 (LMF) 守护进程和控制进程与 Media Manager 接口，在 LMF 机器人中装载和卸载卷。
- `ltid` 启动 Media Manager 设备守护进程。`ltid` 命令启动 Media Manager 设备 (`ltid`) 和自动卷识别守护进程 (`avrd`)。这些守护进程管理 Media Manager 设备。如果 Media Manager 中定义了机器人设备，`ltid` 命令还会启动相应的机器人守护进程，以及 Media Manager 卷 `vmd`。
- `odl` 光盘库 (ODL) 守护进程与 Media Manager 接口，在光盘库中装载和卸载光盘刻片。
- `rsmd` 可移除介质管理器 (RSM) 进程与 Media Manager 接口，自动装载和卸载受 Windows 2000 可移除介质管理器 (RSM) 控制的磁带。
- `stopt` 停止 Media Manager 设备守护进程、`avrd`。
- `tld4` 介质库 4MM 守护进程与 Media Manager 接口，在 4MM 机器人中卸载卷。
- `tld8`, `tldcd` 介质库 8MM 守护进程和控制进程与 Media Manager 接口，在 8MM 机器人中卸载卷。
- `ttld`, `tldcd` DLT 守护进程和控制进程与 Media Manager 接口，在 DLT 机器人中卸载卷。
- `thnd`, `thoc` TLH 守护进程和控制进程与 Media Manager 接口，在 TLH 机器人中卸载卷。
- `tmld` TLM 守护进程与 Media Manager 接口，在 TLM 机器人中卸载磁带。
- `ptautocont` 通常由设备配置向导用于全局数据库以自动发现和配置设备。
- `tpclean` 管理磁带驱动器清洁，允许 Media Manager 自动清洁（ACS、LMF、ODL 或 TLH 机器人）。
- `tpconfig` 磁带配置工具。`tpconfig` 可以作为命令行界面或菜单界面（仅限 UNIX），用于配置用于 的机器人和驱动器。
- `tpformat` 为 Media Manager 格式化光盘。
- `tpreq` 请求磁质卷并将文件名与分配的驱动器关联。
- `tpmount` 从驱动器移除磁质卷并从目录移除关联的磁带。
- `ts8d` 磁带堆栈 8MM 守护进程与 Media Manager 接口，在 8MM 机器人中卸载磁带。
- `tssd` 磁带堆栈 DLT 守护进程与 Media Manager 接口，在 DLT 机器人中卸载磁带。
- `tshd` 磁带堆栈 TLH 守护进程与 Media Manager 接口，在 TLH 机器人中卸载磁带。
- `vmadd` 向卷数据库添加卷。
- `vmcmd` 基于字符的媒体管理实用，用于管理卷和卷池、管理条码规则以及由 Media Manager 卷守护进程 (`vmd`) 控制的机器人。
- `vmchange` 修改 Media Manager 卷数据库中的信息。
- `vmcheckckxx` 报告机器人库的媒体内容并将其与卷卷对比。
- `vmd` Media Manager 卷守护进程，管理卷数据库，响应添加、更改、列出或删除卷的请求。
- `vmdelete` 从卷数据库中删除卷。
- `vmopromcd` 对驱动器执行操作功能。
- `vmpool` 管理卷池，允许添加、更改、删除或列出卷池。
- `vmquery` 查询卷数据库，或分配或取消分配卷。
- `vmrule` 管理条码规则。
- `vmupdate` 清点机器人库的媒体内容并更新卷数据库。

## 录 B：术语表

### A

**活动作业 (active job)**

NetBackup 当前正在处理备份或恢复数据的作业。

**活动日志 (activity logs)**

可以针对特定的 NetBackup 程序和进程可选开启的日志，用于进一步调查问题。

**活动监器 (Activity Monitor)**

一种 NetBackup 管理工具，用于显示 NetBackup 作业、服务和进程的信息，并对它们进行有限的控制。

### B

**备份标识符 (backupid)**

分配给每个备份映像的唯一标识符。该标识符存储在 NetBackup 映像目录的备份信息中，并用于跟踪所有的备份映像。

**备份窗口 (backup window)**
