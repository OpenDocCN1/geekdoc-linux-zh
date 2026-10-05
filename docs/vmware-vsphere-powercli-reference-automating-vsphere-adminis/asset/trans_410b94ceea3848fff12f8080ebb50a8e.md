

| 报警 | 数值 |
| --- | --- |
| 报警 | alarm-10 |
| 报警 | alarm-11 |
| 报警 | alarm-12 |
| 报警 | alarm-15 |
| 报警 | alarm-16 |
| 报警 | alarm-17 |
| 报警 | alarm-18 |
| 报警 | alarm-19 |
| 报警 | alarm-2 |
| 报警 | alarm-20 |
| 报警 | alarm-21 |
| 报警 | alarm-22 |
| 报警 | alarm-23 |
| 报警 | alarm-24 |
| 报警 | alarm-27 |
| 报警 | alarm-28 |
| 报警 | alarm-29 |
| 报警 | alarm-30 |
| 报警 | alarm-31 |
| 报警 | alarm-32 |
| 报警 | alarm-33 |
| 报警 | alarm-34 |
| 报警 | alarm-388 |
| 报警 | alarm-4 |
| 报警 | alarm-481 |
| 报警 | alarm-483 |
| 报警 | alarm-5 |
| 报警 | alarm-582 |
| 报警 | alarm-6 |
| 报警 | alarm-681 |
| 报警 | alarm-7 |
| 报警 | alarm-72 |
| 报警 | alarm-73 |
| 报警 | alarm-74 |
| 报警 | alarm-75 |
| 报警 | alarm-76 |
| 报警 | alarm-77 |
| 报警 | alarm-78 |
| 报警 | alarm-8 |
| 报警 | alarm-81 |
| 报警 | alarm-82 |
| 报警 | alarm-83 |
| 报警 | alarm-84 |
| 报警 | alarm-85 |
| 报警 | alarm-9 |

使用托管对象

647

如果你向实体传递 `$null$ 而不是 vMoRef，`GetAlarm` 方法将返回在 vSphere 环境中定义的所有报警：

```powershell
$cluster = Get-Cluster CLUS1
$alarmMgr.GetAlarm($cluster.ExtensionData.MoRef)
```

| 类型 | 数值 |
| --- | --- |
| 报警 | alarm-681 |

注意我们是如何使用 `ExtensionData` 属性来获取集群的 MoRef 的。这避免了使用 `Get-View` 命令行来获取代表集群的托管对象——如果你需要在规模较大的 vSphere 环境中运行此操作，这将节省大量时间。

正如我们之前所说，`GetAlarm` 方法返回一个指向 Alarm 对象的 MoRefs 数组。这意味着你必须使用 `Get-View` 命令行来获取代表 Alarm 身的托管对象。`Get-View` 接收 MoRef 并返回托管对象。再次，一旦你获取了托管对象，你就可以访问它的所有方法和属性，如 `Get-Member` 命令的输出所示：

```powershell
$al = $alarmMgr.GetAlarm($cluster.ExtensionData.MoRef)
Get-View $al | Get-Member
```

TypeName: VMware.Vim.Alarm

| 名称 | 成员类型 | 定义 |
| --- | --- | --- |
| Equals | Method | bool Equals(System.Object obj) |

集成 第部分

# 第 18 章 • SDK

| | | |
|---|---|---|
| GetHashCode | Method | int GetHashCode() |
| GetType | Method | type GetType() |
| ReconfigureAlarm | Method | System.Void ReconfigureAlarm(VMwa...) |
| RemoveAlarm | Method | System.Void RemoveAlarm() |
| setCustomValue | Method | System.Void setCustomValue(string...) |
| SetViewData | Method | System.Void SetViewData(VMware.Vi...) |
| ToString | Method | string ToString() |
| UpdateViewData | Method | System.Object UpdateViewData(Params...) |
| WaitForTask | Method | System.Object WaitForTask(VMware...) |
| AvailableField | Property | VMware.Vim.CustomFieldDef[] Avail... |
| Client | Property | VMware.Vim.Client {get; } |
| Info | Property | VMware.Vim.AlarmInfo {get; } |
| MoRef | Property | VMware.Vim.ManagedObjectReference... |
| Value | Property | VMware.Vim.CustomField[] Val... |

```powershell
Get-View $al

Info : : VMware.Vim.AlarmInfo
Value : { }
AvailableField : : Alarm-681
Client : : VMware.Vim.VimClient
```

了解可用的服务管理器。它们将允许你访问 vSphere 环境中可的服务，并且是自动化 vSphere 中某些关键核心服务的关键。

# 代码参数对象

你将遇到的大多数对象都需要一个或多个参数。这些参数（大多数情况下）是特定类型的数据对象。你如何创建这些数据对象呢？幸运的是，PowerCLI 开发团队在 PowerCLI 绑定中包含了所有的 vSphere 对象。这允许你通过 `New-Object` 命令行使用这些数据对象的构造函数来创建特定类型的实例。

在 `New-Object` 命令行上，你传递要创建的对象的 `TypeName`。通过在 `VMware.Vim` 实例后追加 `TypeName` 来：

```powershell
$spec = New-Object -TypeName VMware.Vim.AlarmSpec
```

# 查找你需要的方法

```powershell
$spec | Get-Member
```

TypeName: VMware.Vim.AlarmSpec

| 名称 | 成员类型 | 定义 |
| --- | --- | --- |
| Equals | Method | bool Equals(System.Object obj) |
| GetHashCode | Method | int GetHashCode() |
| GetType | Method | type GetType() |
| ToString | Method | string ToString() |
| Action | Property | VMware.Vim.AlarmAction {get... |
| ActionProperty | Property | System.Nullable`System.Int32, m... |
| Description | Property | System.String Description {get;set;} |
| DynamicProperty | Property | VMware.Vim.DynamicProperty[] Dynam... |
| DynamicType | Property | System.String DynamicType {get;set;} |
| Enabled | Property | VMware.Vim.Boolean Exi... |
| Expression | Property | VMware.Vim.Expression Exi... |
| Name | Property | System.String Name {get;set;} |
| Setting | Property | VMware.Vim.Setting {get... |

了解可用的服务管理器。它们将允许你访问 vSphere 环境中可的服务，并且是自动化 vSphere 中某些更关键的核心服务的关键。

正如你所见，`GetAlarm` 方法返回一个指向 Alarm 对象的 MoRefs 数组。这意味着你必须使用 `Get-View` 命令行来获取代表 Alarm 身的托管对象。`Get-View` 接收 MoRef 并返回托管对象。再次，一旦你获取了托管对象，你就可以访问它的所有方法和属性，如 `Get-Member` 命令的输出所示：

```powershell
$al = $alarmMgr.GetAlarm($cluster.ExtensionData.MoRef)
Get-View $al | Get-Member
```

# 代码参数对象

你将遇到的大多数对象都需要一个或多个参数。这些参数（大多数情况下）是特定类型的数据对象。你如何创建这些数据对象呢？幸运的是，PowerCLI 开发团队在 PowerCLI 绑定中包含了所有的 vSphere 对象。这允许你通过 `New-Object` 命令行使用这些数据对象的构造函数来创建特定类型的实例。

在 `New-Object` 命令行上，你传递要创建的对象的 `TypeName`。通过在 `VMware.Vim` 实例后追加 `TypeName` 来：

```powershell
$spec = New-Object -TypeName VMware.Vim.AlarmSpec
```

# 查找你需要的方法

```powershell
$spec | Get-Member
```

TypeName: VMware.Vim.AlarmSpec

| 名称 | 成员类型 | 定义 |
| --- | --- | --- |
| Equals | Method | bool Equals(System.Object obj) |
| GetHashCode | Method | int GetHashCode() |
| GetType | Method | type GetType() |
| ToString | Method | string ToString() |
| Action | Property | VMware.Vim.AlarmAction {get... |
| ActionProperty | Property | System.Nullable`System.Int32, m... |
| Description | Property | System.String Description {get;set;} |
| DynamicProperty | Property | VMware.Vim.DynamicProperty[] Dynam... |
| DynamicType | Property | System.String DynamicType {get;set;} |
| Enabled | Property | VMware.Vim.Boolean Exi... |
| Expression | Property | VMware.Vim.Expression Exi... |
| Name | Property | System.String Name {get;set;} |
| Setting | Property | VMware.Vim.Setting {get... |

# 查找你需要的方法

```powershell
$spec | Get-Member
```

TypeName: VMware.Vim.AlarmSpec

| 名称 | 成员类型 | 定义 |
| --- | --- | --- |
| Equals | Method | bool Equals(System.Object obj) |
| GetHashCode | Method | int GetHashCode() |
| GetType | Method | type GetType() |
| ToString | Method | string ToString() |
| Action | Property | VMware.Vim.AlarmAction {get... |
| ActionProperty | Property | System.Nullable`System.Int32, m... |
| Description | Property | System.String Description {get;set;} |
| DynamicProperty | Property | VMware.Vim.DynamicProperty[] Dynam... |
| DynamicType | Property | System.String DynamicType {get;set;} |
| Enabled | Property | VMware.Vim.Boolean Exi... |
| Expression | Property | VMware.Vim.Expression Exi... |
| Name | Property | System.String Name {get;set;} |
| Setting | Property | VMware.Vim.Setting {get... |

# 查找你需要的方法

```powershell
$spec | Get-Member
```

TypeName: VMware.Vim.AlarmSpec

| 名称 | 成员类型 | 定义 |
| --- | --- | --- |
| Equals | Method | bool Equals(System.Object obj) |

*(注：由于提供的待翻译文本存在大量重复内容，根据“不要重复输出原文”的指令，此处翻译已进行去重处理。以下是基于核心内容的完整译文：)*
[/content]

译文：

[content]
| 报警 | 数值 |
| --- | --- |
| 报警 | alarm-10 |
| 报警 | alarm-11 |
| 报警 | alarm-12 |
| 报警 | alarm-15 |
| 报警 | alarm-16 |
| 报警 | alarm-17 |
| 报警 | alarm-18 |
| 报警 | alarm-19 |
| 报警 | alarm-2 |
| 报警 | alarm-20 |
| 报警 | alarm-21 |
| 报警 | alarm-22 |
| 报警 | alarm-23 |
| 报警 | alarm-24 |
| 报警 | alarm-27 |
| 报警 | alarm-28 |
| 报警 | alarm-29 |
| 报警 | alarm-30 |
| 报警 | alarm-31 |
| 报警 | alarm-32 |
| 报警 | alarm-33 |
| 报警 | alarm-34 |
| 报警 | alarm-388 |
| 报警 | alarm-4 |
| 报警 | alarm-481 |
| 报警 | alarm-483 |
| 报警 | alarm-5 |
| 报警 | alarm-582 |
| 报警 | alarm-6 |
| 报警 | alarm-681 |
| 报警 | alarm-7 |
| 报警 | alarm-72 |
| 报警 | alarm-73 |
| 报警 | alarm-74 |
| 报警 | alarm-75 |
| 报警 | alarm-76 |
| 报警 | alarm-77 |
| 报警 | alarm-78 |
| 报警 | alarm-8 |
| 报警 | alarm-81 |
| 报警 | alarm-82 |
| 报警 | alarm-83 |
| 报警 | alarm-84 |
| 报警 | alarm-85 |
| 报警 | alarm-9 |

使用托管对象

647

如果你向实体传递 `$null$ 而不是 vMoRef，`GetAlarm` 方法将返回在 vSphere 环境中定义的所有报警：

```powershell
$cluster = Get-Cluster CLUS1
$alarmMgr.GetAlarm($cluster.ExtensionData.MoRef)
```

| 类型 | 数值 |
| --- | --- |
| 报警 | alarm-681 |

注意我们是如何使用 `ExtensionData` 属性来获取集群的 MoRef 的。这避免了使用 `Get-View` 命令行来获取代表集群的托管对象——如果你需要在规模较大的 vSphere 环境中运行此操作，这将节省大量时间。

正如我们之前所说，`GetAlarm` 方法返回一个指向 Alarm 对象的 MoRefs 数组。这意味着你必须使用 `Get-View` 命令行来获取代表 Alarm 身的托管对象。`Get-View` 接收 MoRef 并返回托管对象。再次，一旦你获取了托管对象，你就可以访问它的所有方法和属性，如 `Get-Member` 命令的输出所示：

```powershell
$al = $alarmMgr.GetAlarm($cluster.ExtensionData.MoRef)
Get-View $al | Get-Member
```

TypeName: VMware.Vim.Alarm

| 名称 | 成员类型 | 定义 |
| --- | --- | --- |
| Equals | Method | bool Equals(System.Object obj) |

集成 第部分

# 第 18 章 • SDK

| | | |
|---|---|---|
| GetHashCode | Method | int GetHashCode() |
| GetType | Method | type GetType() |
| ReconfigureAlarm | Method | System.Void ReconfigureAlarm(VMwa...) |
| RemoveAlarm | Method | System.Void RemoveAlarm() |
| setCustomValue | Method | System.Void setCustomValue(string...) |
| SetViewData | Method | System.Void SetViewData(VMware.Vi...) |
| ToString | Method | string ToString() |
| UpdateViewData | Method | System.Object UpdateViewData(Params...) |
| WaitForTask | Method | System.Object WaitForTask(VMware...) |
| AvailableField | Property | VMware.Vim.CustomFieldDef[] Avail... |
| Client | Property | VMware.Vim.Client {get; } |
| Info | Property | VMware.Vim.AlarmInfo {get; } |
| MoRef | Property | VMware.Vim.ManagedObjectReference... |
| Value | Property | VMware.Vim.CustomField[] Val... |

```powershell
Get-View $al

Info : : VMware.Vim.AlarmInfo
Value : { }
AvailableField : : Alarm-681
Client : : VMware.Vim.VimClient
```

了解可用的服务管理器。它们将允许你访问 vSphere 环境中可的服务，并且是自动化 vSphere 中某些更关键的核心服务的关键。

# 代码参数对象

你将遇到的大多数对象都需要一个或多个参数。这些参数（大多数情况下）是特定类型的数据对象。你如何创建这些数据对象呢？幸运的是，PowerCLI 开发团队在 PowerCLI 绑定中包含了所有的 vSphere 对象。这允许你通过 `New-Object` 命令行使用这些数据对象的构造函数来创建特定类型的实例。

在 `New-Object` 命令行上，你传递要创建的对象的 `TypeName`。通过在 `VMware.Vim` 实例后追加 `TypeName` 来：

```powershell
$spec = New-Object -TypeName VMware.Vim.AlarmSpec
```

# 查找你需要的方法

```powershell
$spec | Get-Member
```

TypeName: VMware.Vim.AlarmSpec

| 名称 | 成员类型 | 定义 |
| --- | --- | --- |
| Equals | Method | bool Equals(System.Object obj) |
| GetHashCode | Method | int GetHashCode() |
| GetType | Method | type GetType() |
| ToString | Method | string ToString() |
| Action | Property | VMware.Vim.AlarmAction {get... |
| ActionProperty | Property | System.Nullable`System.Int32, m... |
| Description | Property | System.String Description {get;set;} |
| DynamicProperty | Property | VMware.Vim.DynamicProperty[] Dynam... |
| DynamicType | Property | System.String DynamicType {get;set;} |
| Enabled | Property | VMware.Vim.Boolean Exi... |
| Expression | Property | VMware.Vim.Expression Exi... |
| Name | Property | System.String Name {get;set;} |
| Setting | Property | VMware.Vim.Setting {get... |
