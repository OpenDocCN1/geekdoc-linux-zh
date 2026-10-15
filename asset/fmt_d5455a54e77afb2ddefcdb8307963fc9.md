
| ns-14 | 2008-07-24 13:26:15 | Nagios | 该主机已安排在 2008-07-24 13:07:54 到 2008-07-24 14:39:23 之间开始检查。将不会发送该主机的通知。 | 否 | 计划 | 正常 |

| ns-30 | 2008-07-24 13:26:15 | Nagios | 该主机已安排在 2008-07-24 13:07:54 到 2008-07-24 14:39:23 之间开始检查。将不会发送该主机的通知。 | 否 | 计划 | 正常 |

| ns-87 | 2008-07-24 13:26:15 | Nagios | 该主机已安排在 2008-07-24 13:07:54 到 2008-07-24 14:39:23 之间开始检查。将不会发送该主机的通知。 | 否 | 计划 | 正常 |

## 1.2.3 外部命令接口：`cgi.cgi`，外部配合 `cmd.cgi`

作为一个全能型工具，`cgi.cgi` 拥有 500 个功能，涵盖了接口为外部命令提供的几乎所有可能性。`cmd_type` 参数定义了 CGI 命令应该运行哪种功能。命令为

`/http://nagiosserver/nagios/cgi-bin/cmd.cgi?cmd_type=6`

关闭特定服务的活动检查（图 16-23）。为了唯一地描述所需的服务，你必须指定主机和服务描述。如果你手动运行 CGI 命令，所示 Web 表单将查询这些值；如果 `cmd.cgi` 是由另一个 CGI 命令启动的，所需数据将通过 CGI 参数传递。可能的参数有 `host`、`service`、`hostgroup` 和 `servicegroup`，后面跟着等号（`=`），然后是相应的 Nagios 对象。

在提交命令前请输入所有必要信息。

必填字段用红色标记。

未提供所有必要值将导致错误：

图 16-23. 使用 `cmd.cgi?type=6` 禁用服务

图 16-24 列出了引用主机或服务的最重要命令，图 16-25 显示了引用全局参数控制的命令（对应于配置文件 `nagios.cfg` 中的值）。源代码文件 `include/common.h` 包含了所有可能值的完整列表，包括已计划但尚未实现的值。

图 16-24 和图 16-25 的第一列描述了命令的功能：`ADD_HOST_COMMENT` 为主机添加注释，`DISABLE_ACTIVE_SVC_CHECK` 切换服务的活动检查（缩写为 SVC）。

随后的列指定了相应函数所引的对象类型。要使用 `ADD_HOST_COMMENT` 添加注释，必须指定相关主机。因此，在 Host（主机）列中显示代码 `1`。只有在命名了匹配的服务时才能切换特定的活动服务检查，因此函数 `6` 位于 Service（服务）列中。使用 `16` 可以关闭指定主机上的所有活动服务检查；对于所有主机或服务组的活动服务检查也有相应的代码。

通过 `ACKNOWLEDGE_PROBLEM`，管理员确认其正在处理某个特定问题。`33`（Host 列）指的是主机问题，`34`（Service 列）指的是服务问题。灰色字段表示主机和服务组没有对应的函数。使用 `cmd_typ=33` 打开的 Web 表单（图 16-9，第 333 页）允许输入注释。

| command | host | service | hostgroup | servicegroup |
| --- | --- | --- | --- | --- |
| ADD_HOST_COMMENT | 1 | | | |
| DEL_HOST_COMMENT | 2 | | | |
| DEL_ALL_HOST_COMMENT | | 20 | | |
| ADD_SVC_COMMENT | | 3 | | |
| DEL_SVC_COMMENT | | 4 | | |
| DEL_ALL_SVC_COMMENT | | 21 | | |
| ENABLE_ACTIVE_SVC_CHECK | 15 | 5 | 67 | 113 |
| DISABLE_ACTIVE_SVC_CHECK | 16 | 6 | 68 | 114 |
| SCHEDULE_SVC_CHECK | 17 | | 7 | 115 |
| ENABLE_HOST_CHECK | 47 | | 103 | 116 |
| DISABLE_HOST_CHECK | 48 | | 104 | | |
| SCHEDULE_HOST_CHECK | 96 | | 65 | 111 |
| ENABLE_HOST_NOTIFICATIONS | 24 | | 66 | 112 |
| DISABLE_HOST_NOTIFICATIONS | 25 | | | | |
| DEL_HOST_NOTIFICATIONS | 10 | | | | |
| ENABLE_SVC_NOTIFICATIONS | 28 | 22 | 63 | 109 |
| DISABLE_SVC_NOTIFICATIONS | 29 | 23 | 64 | 110 |
| DEL_SVC_NOTIFICATIONS | 19 | 9 | | | |
| ACKNOWLEDGE_PROBLEM | 33 | 34 | | | |
| REMOVE_ACKNOWLEDGE | 51 | 52 | | | |
| ENABLE_PASSIVE_HOST_CHECKS | 92 | | 107 | 119 |
| DISABLE_PASSIVE_HOST_CHECKS | 93 | | 108 | 120 |
| ENABLE_PASSIVE_SVC_CHECKS | 39 | | 105 | 117 |
| DISABLE_PASSIVE_SVC_CHECKS | 40 | | 106 | 118 |
| SCHEDULE_HOST_DOWNTIME | 55 | | 84 | 121 |
| DISABLE_HOST_DOWNTIME | 78 | | | | |
| SCHEDULE_SVC_DOWNTIME | 56 | | 85 | 127 |
| DISABLE_SVC_DOWNTIME | 79 | | | | |
| ENABLE_EVENT_HANDLER | 43 | 45 | | | |
| DISABLE_EVENT_HANDLER | 44 | 46 | | | |
| ENABLE_FLAP_DETECTION | 57 | 59 | | | |
| DISABLE_FLAP_DETECTION | 58 | 60 | | |

图 16-24. `cmd.cgi` 最重要的主机和服务相关代码

引用全局参数（图 16-25）的函数通常可以开启或关闭。因此，`NOTIFICATIONS` 列中的值 `11` 表示开启所有通知，而 `12` 则关闭它们。如果你不确定确定函数是否符合你的预期，最好使用以下代码手动运行 `cmd.cgi`：

`http://nagiosserver/cgi-bin/cmd?typ=12`

由此生成的 Web 页面在页面右侧始终有一个小灰色框，解释对应的命令（图 16-23）。

| global parameters | START/ENABLE | STOP/DISABLE |
| --- | --- | --- |
| NOTIFICATIONS | 11 | 12 |
| SVC CHECKS | 35 | 36 |
| ACCEPTING_PASSIVE_SVC_CHECKS | 37 | 38 |
| HOST_CHECKS | 88 | 89 |
| ACCEPTING_PASSIVE_HOST_CHECKS | 90 | 91 |
| EVENT_HANDLER | 41 | 42 |
| FLAP DETECTION | 61 | 62 |
| PERFORMANCE_DATA | 82 | 83 |

图 16-23. `cmd.cgi` 全局参数代码

## 16.4 重点内容：`tac.cgi`

作为一个“战术概览”，`tac.cgi` 在单个页面提供了丰富的信息，以摘要形式显示（图 16-26）。在页面左侧，你可以按照优先级查看整个网络的故障（Network Outages），随后是摘要，底部 `tac.cgi` 列出了通知和事件处理器等监控功能是否处于激活。

最后这部分集中在显示服务上。如果一切正常（OK），CGI 仅显示问题的服务或主机，并以浅灰色突出（以及主机）。在出现问题的情况下，它区分了已查看的问题（红色高亮，Unhandled Problems）以及管理员已通过确认负责的问题（粉色背景，如 Acknowledged | Unknown）。如果主机或服务检查被禁用，它们也会以粉色背景显示，因为它们不需要管理员立即关注的问题（例如 Services Disabled）。

`tac.cgi` 用绿色标记下部分的启用功能，用红色标记禁用功能。垂直显示的 Enabled in Notifications 意味着通知已全局启用，而另一的红色背景 `Services Disabled` 则意味着它们已针对单个服务显式关闭。
