
```
define command {
  command_name check_inject
  command_line $USER$ -u check_nrpe -H $HOSTADDRESS -c check_inject -a "$ARG1"
}
def service {
  host_name winsrv
  service_description Uptime
  check_command check_inject,checkUpTime ShowAll MinWarn=1d MinCr
  it=12h
  ...
}
```

存在一个安全问题，如上述所述定义了 `check_inject=$ARG1`，但你正在为可能希望 NSClient++ 检查中出现缓冲区溢出的攻击者打开一扇门。在这种情况下，客户端将只能运行在安全环境中。你应该只在安全环境中使用这种非常通用的命令，即使如此，你也应该限制

## 20.4.4 内部 NSClient++ 函数

通过 `allowed_hosts` 限制允许通过 NRPE 访问 NSC++ 的主机。另一方面，这种自由的定义在实现阶段会让工作变得容易得多，因为你可以在命令行上尝试各种组合和检查，而无需每次都为多个主机调整 `NSC.ini` 配置文件。

NSClient++ 提供了一系列内部函数，这些函数可以通过 NRPE 的 `inject` 命令通过 NRPE 调用，通常也可以通过 `check_nt` 插件调用。这些函数存储在可加载的模块中。表 20-3 概述了某个特定函数所需的模块。

表 20-3. NSClient++ 模块的内部函数

| 模块 | 函数 |
| --- | --- |
| CheckDisk | CheckFileSize, CheckDriveSize |
| CheckSystem | CheckCPU, Checkptime, CheckStartState, CheckProcState, CheckMem, CheckCounter |
| CheckEventLog | CheckEventLog |
| CheckHelpers | AlwaysOK, AlwaysCRITICAL, AlwaysWARNING, CheckMultiple |

要使用 `check_nt` 使用这些函数之一，你只需要确保在 `[modules]` 部分加载了所需的模块即可。然而，通过 NRPE 和 `inject` 调用提供了额外的配置选项。

因此，对于使用 `CheckDriveSize` 函数的 `check_nt` 强制加载检查，你可以直接使用 `check_nt` 并设置警告和临界值：

```
checkDriveSize MinWarn=1d MinCrit=12h
```（注：此处原文示例似乎断断，翻译逻辑如下）

在此示例中，`check_utime` 通过 `inject` 调用内部函数 `CheckUpTime`。如果通过 NRPE 传递参数，你可以极大地简化 `inject` 命令的定义：

```
check_inject=inject $ARG0
```

要使用 `check_nt` 与 `check_nt` 使用这些函数之一，你只需要确保所需的模块已加载在 `[modules]` 部分。然而，通过 NRPE 和 `inject` 调用提供了额外的配置选项。

因此，对于使用 `CheckDriveSize` 函数的 `check_nt` 强制加载检查，你可以直接使用 `check_nt`：

（此处由于原文后续内容存在大量重复和逻辑断裂，以下为基于指令翻译的剩余部分）

*注：由于提供的英文文本后半部分存在大量重复和乱码化描述，翻译已根据文档工程师的逻辑进行了对齐。*

具有足够大的值。默认周期为一小时。

为了一次显示多个不同时间间隔的 CPU 负载，你可以多次指定时间参数：

```
CheckCPU warn=30 crit=0 time=1m time=5m time=15m
```

`ShowAll` 影响插件输出的显示（但不影响性能数据；此处已省略这些数据）：

```
OK CPU Load ok.
OK: 1m: 2%, 5m: 25%
OK: 1m: average load 2%, 5m: average load 2%, 15m: average load 2%
```

第一行显示了 `ShowAll` 的输出，第二行显示带有该参数的输出。`CheckCPU` 分别显示每个时间间隔的值。第三行演示了参数 `ShowAll=long`。这不会为你提供更多信息，只是提供了更多的文本。

剩余的参数是 `nsclient`，它以原始 NSclient 的样式显示输出，并用 `&: 2&2&2` 分隔不同时间间隔的细节。使用此参数时不会显示性能数据。

### 使用 CheckUpTime 确定运行时间

`CheckUp` 显示自系统启动以来通过了多久。与 `CheckCPU` 一样，可以使用后缀（`s`, `m`, `h`, `d`, `w`）设置阈值：

```
CheckUp MaxWarn=time MaxCrit=time
MinWarn=time MinCrit=time ShowAll
sclient Alias=string
```

`ShowAll` 即使在没有错误状态也会显示时间。`nsclient` 将输出更改为秒的简单值，不带任何其他文本。使用 `Alias`，可以将 `Uptime` 一词替换为不同的文本：

```
OK: uptime: 1d 20:11
OK: Running_Time: 1d 20:12
```

第一行显示带有 `ShowAll` 的正常输出；第二行设置了额外的 `Alias=Running_Time`。

### 使用 CheckServiceState 检查活动

`CheckServiceState` 检查服务是否活动（启动）或否（停止）。你可以使用 `CheckAll` 开关，它可以检查所有设置了自启动标志的服务，这些服务应该在每次系统启动后运行：

```
CheckServiceState service ShowFail CheckAll
exclude=servicename
CheckServiceState serviceFail ShowAll CheckAll exclude=servicename
```

可以显式地检查单个服务的所需状态：

```
CheckServiceState MSEExchangeA=started MSSEARCH=stopped ShowFail
```

此调用检查 `MSEExchangeA` 服务是否运行以及 `MSSEARCH` 服务是否未运行。如果两个服务的状态与指定的不同，则会显示 `CRITICAL`。`ShowFail` 确保带有错误的服务会出现在输出中。

`CheckAll` 正常包含所有带有自启动标志的服务。可以通过 `exclude` 排除单个服务。

### 使用 CheckProcState 监控进程

`CheckProcState` 检查进程状态，其工作原理与 `CheckServiceState` 相同，但可用选项较少：

```
CheckProcState ShowFail
CheckProcState ShowFail process
```

对于单个进程，你可以再次指定所需状态（`process=started` 或 `process=stopped`）；否则将留由 `ShowAll` 来控制输出。`ShowFail` 是默认值，可以省略。

### 使用 CheckMem 检查内存负载

`CheckMem` 检查内存的负载水平。这里这里 参数很有很有价值：

```
CheckMem MaxWin=size MaxCrit=size
MinWin=size MinCrit=size ShowAll
```

`type=page` 和 `type=p` 显示整个内存（物理内存加交换内存），并对应 `check_nt -v MEMUX` 的值。`page` 和 `paged` 之间的区别在于使用的例程：前者使用 NSClient 的 PDH 库，源自 Windows NT 时代，而后者属于 Windows 2000 和 Windows 2003。`type=virtual` 指交换内存，`type=physical` 指所使用的内存。

`CheckMem` 的输出仅在存在错误状态时才提供可用整个内存的详情；对于 `OK` 状态，将显示指定类别中实际使用的部分。

与 `CheckFileSize` 类似，该函数的阈值后缀使用大写字母：`B`、`K`、`M` 和 `G`。允许使用后缀 `%` 指定百分比。

### 使用 CheckCounter 检查性能计数器

通过 `CheckCounter`，你可以查询 Windows 性能计数器，计数器记录了 Windows 提供的几乎所有参数：

```
CheckCounter MaxWarn=number MaxCrit=number
MinWarn=number MinCrit=number showAll
Averages=value Counter=countername
```
