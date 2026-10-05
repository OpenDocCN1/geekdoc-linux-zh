

# 告警动作

告警动作有很多且种类多样。有些操作非常简单，例如组、方法、任务和 SNMP 动作。我们将提供这些动作的概述。其他动作，如脚本或电子邮件动作，则更加灵活且复杂。我们将详细地介绍这些动作。

### 分组动作 (Grouping Actions) API 参考中指出，你可以拥有单个 `AlarmTriggeringAction` 而不使用 `GroupAlarmAction`。定义带有单个动作的告警是，但当你尝试从 vSphere 客户端编辑该告警的设置时，问题就出现了；“编辑设置”(Edit Settings) 选项呈灰色状态。vSphere Web Client 的问题更严重；当你尝试编辑告警时，会生成错误。因此，我们建议您即使只有一个动作，也要在 `GroupAlarmAction` 下指定您的动作，因为这些问题在当时不会发生。

> 注意：如果你想创建一个没有任何任何动作的告警，则无需指定 `AlarmTriggeringAction` 或 `GroupAlarmAction`。

### 方法动作 (Method Action) 方法动作仅适用于 HostSystem（主机系统）和 VirtualMachine（虚拟机）对象。通过使用方法动作，你可以调用任何触发告警的 HostSystem 或 VirtualMachine 对象上可用的 SDK 方法。

### 任务动作 (Task Action) 任务动作同样仅适用于 HostSystem 和 VirtualMachine 对象。你可以调用你的 vCenter Server 扩展上可用的任何任务。

### SNMP 动作 (SNMP Action) 简单网络管理协议 (SNMP) 动作是所有动作中最简单的。它们不需要任何参数。SNMP 陷阱 (trap) 将发送到你在 vCenter Server 中定义的 SNMP 团体 (communities)。

# 脚本动作 (Script Actions)

脚本动作接受一个参数——即你希望 vCenter Server 在告警触发时执行的命令。在实现这一点的过程中，可能会出现一些问题，特别是用于执行脚本的安全账户，以及 vCenter Server 内部所需的权限。我们倾向于采用以下方法：

- vCenter Server 使用域账户运行。因此，脚本通过安全支持提供程序接口 (SSPI) 执行，并使用单点登录连接到 vCenter Server。因此，你不需要指定凭据。
- 运行 vCenter Server 的域账户在 vCenter 权限模型中持有所需的权限，以执行你在脚本中想要完成的任何操作。

与你将看到的代码不同，“编辑告警”(Edit Alert) 向向中动作部分的“配置”(Configuration)字段的实际文本是单行输入的，没有回车符或行符。（我们不得不将文本分成三行；它太长了，无法适应页面。）对于像 Windows 2012 等 64 位操作系统，它看起来就像列表 17.2 所示。

## 17.2 示例脚本

```
C:\Windows\System32\cmd.exe /powershell
-PSConsoleFile C:\Scripts\MyConsole.ps1 -noninteractive
-profile file C:\Scripts\Alarm-action-script.ps1
```

监控 Windows 服务器进程的常用方法是使用 Microsoft Sysinternals 网站（http://sysinternals.com）上的 Process Explorer。当 vCenter Server 上使用 Process Explorer 时，你可以看到 vCenter Server 如何运行你的告警脚本。Process Explorer 允许你看到用于每个派生进程的参数。打开 cmd.exe 和 powershell.exe 进程的属性。Process Explorer 还允许你验证告警脚本何时完成。只需检查 cmd.exe 和 powershell.exe 进程是否在 vpxd.exe 进程下方消失即可。

在列表 17.2 中，注意命令行上使用了控制文件 (console file)。通过此文件，你可以定义加载到运行你脚本的 PowerShell 会话中的项程序 (snap-in)。

> PowerShell 控制台文件是一个基于 XML 的文件，包含 PowerShell 插件的详细信息，并以 *.pscl 扩展名保存。PowerCLI 在安装目录中带有一个名为 vim.pscl 的控制文件。你也可以使用 `Export-Console` get令创建你自己的控制文件。

![](img/62596f5acc979040608a4e5111beb7d6_630_0.png)

脚本动作可能需要一段时间才能完全执行。这取决于你的 vCenter Server 的负载，也取决于你通过控制文件加载的项程序数量。当你想要检查告警脚本的结果时，请保持耐心。在命令行上，你可以传递 vCenter Server 提供的一个或多个预定义变量。再次，你将在单行中输入信息，并带有回车或换行符（列表 17.3）。

## 17.3 带有预定义变量的示例告警脚本

```
C:\Windows\System32\cmd.exe /c powershell.exe
-ConsoleFile C:\Scripts\MyConsole.ps1 -noninteractive
-profile file C:\Scripts\Alarm-action-script.ps1 {targetName}
```

注意，这些参数是敏感的。这意味着，例如，你不能使用 `targetName`。可以在 vSphere 6.0 文档（http://docs.vmware.com）中找到完整的参数列表。脚本可以像普通的 PowerShell 参数一样访问这些参数。换句话说，你可以使用 `$alarm` 变量或在脚本中定义 `param` 语句。在告警中使用脚本之前，将其作为单独代码块进行测试是一个好主意。这样，你就可以保证它作为告警的一部分运行成功，并且不会出现本地安全策略阻止其执行或 vCenter Server 出现的问题。

如果你想捕获告警的执行情况，方法是将所有输出重定向到 `Out-File` 命令行。这样，脚本的所有输出都会被捕获在文件中。告警脚本将其接收到的参数记录到文件中可能如下所示：

```
$OutFile = C:\alarm.log
$Args | Out-File $OutFile -Append
```

访问触发你脚本的告警信息还有另一种方法。vCenter Server 启动你的告警脚本时带有多个环境变量，这些变量包含了触发脚本的告警信息。你可以在 vSphere 6.0 文档（http://docs.vmware.com）中找到这些环境变量的完整列表。这些环境变量的摘要可以在表 17.6 中找到。

## 17.6 环境变量

| 变量 | 说明 |
| --- | --- |
| ALARM_NAME | 告警名称 |
| ALARM_TARGET_NAME | 触发告警的目标名称 |
| ALARM_TARGET_ID | 触发告警的目标 ID |
| ALARM_EVENT_TYPE | 告警的事件类型 |
| ALARM_EVENT_DESC | 告警的事件描述 |
| ALARM_EVENT_VALUE | 告警的事件值 |
| ALARM_EVENT_HOST | 触发告警的主机 |
| ALARM_EVENT_VM | 触发告警的虚拟机 |
| ALARM_EVENT_DATACENTER | 触发告警的数据中心 |
| ALARM_EVENT_RESOURCE | 触发告警的资源 |
| ALARM_EVENT_DATASTORE | 触发告警的数据数据存储 |
| ALARM_EVENT_NETWORK | 触发告警的网络 |
| ALARM_EVENT_CLUSTER | 触发告警的集群 |
| ALARM_EVENT_HOST | 触发告警的主机 |
| ALARM_EVENT_TEMPLATE | 触发告警的模板 |
| ALARM_EVENT_FOLDER | 触发告警的文件夹 |
| ALARM_EVENT_VIEW | 触发告警的视图 |
| ALARM_EVENT_MESSAGE | 触发告警的消息 |
| ALARM_EVENT_TIMESTAMP | 触发告警的时间戳 |
| ALARM_EVENT_STATUS | 触发告警的状态 |
| ALARM_EVENT_SEVERITY | 告警的严重程度 |
| ALARM_EVENT_SOURCE | 触发告警的源 |
| ALARM_EVENT_USER | 触发告警的用户账户 |

