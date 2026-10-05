

## 连接到目标数据中心

一旦你成功通过数据中心 vCloud Air 系统进行身份验证，你就需要指定你想要交互的数据中心。在这里，使用了 `Get-PIDatacenter` 和 `Connect-PIDatacenter` 命令。要检索你有权访问的 vDC 列表（在网页浏览器的“订阅Subscriptions ➤”下找到），你只需运行：

```
Get-PIDatacenter
```

在例示例中，有 11 个 vDC 可连接：

```
Get-PIDatacenter
```

| Name |
| --- |
| Tech-Preview |
| PoC-Demo |
| UAT-Demo |
| Personal-Lab |
| Benchmarks |
| SDDC-Demo |
| 4-29 |
| M589572327-4001 |
| M673551135-4963 |
| M588570327-5450 |
| M662788264-4629 |

一旦列表返回，你就可以连接到该数据中心。在本例中，我们将选择 SDDC-Demo：

```
$DcConnection = Get-PIDatacenter SDDC-Demo |
Connect-PIDatacenter
```

如果你查看存储在 `$DcConnection` 变量中的内容，将得到：

```
$DcConnection
```

| Name | User | Org |
| --- | --- | --- |
| plv22-vcd.vchs.vmware.com | BrianGraf@contoso.net | SDDC-Demo |

现在你已经连接到 vDC 且连接信息存储在 `$DcConnection` 变量中，你可以在脚本中使用扩展属性中的值。如果出现任何问题，你也可以使用它们进行故障排除。关于你的连接还可以列出更多信息，例如连接状态、SessionId、连接端口，以及如果你使用了 `Format-List`  cmdlet。

## 断开目标数据中心

从目标数据中心断开连接非常简单。就像断开与 vCloud Director 或本地环境中主机的连接一样，你使用 `Disconnect` 动词——在这种情况下是 `Disconnect-PIDatacenter`。目前没有方法指定要从哪个 vDC 断开连接，因此此命令将断开你所有的 vDC 会话：

```
Disconnect-PIDatacenter -Confirm:$false
```

运行此命令会断开与 vDC(s) 的连接，但会保持对 vCloud Air 的身份验证，并允许你连接到同一 vCloud Air 账户下的其他 vDC。

## 断开 vCloud Air 连接

在完成脚本运行或当前会话后，关闭连接始终最佳实践。如果你只连接了一个服务器，可以运行 `Disconnect-PIServer -Confirm:$false`。虽然 `Disconnect-PIServer` 接受名称、通配符 (`*`) 或连接，但决定一个你和其他达成一致的方法并使用该方法以保持一致性是明智的。如果你在 CLI 会话开始时将连接保存为变量，可以引用相同的连接变量来断开连接：

```
$Connection = $global:DefaultPIServers
Disconnect-PIServer $Connection -Confirm:$false
```

## Set-PowerCLIConfiguration

并不是所有用户都需要调整 PowerCLI 配置设置。事实上，许多用户甚至忘记了 `Set-PowerCLIConfiguration` cmdlet 的存在。然而，当你利用 PowerCLI 连接到 vCloud Air 时，这里的许多设置可以对你有帮助。

## DefaultVISServerMode

当你开始在整个 vSphere 基础设施中处理多个连接时，你可能会收到警告，提示你正在同时连接到多个服务器（取决于你的 `PowerCLIConfiguration` 设置）。这在 vCloud 账户中不会发生，但有时你可能忘记正在使用哪个账户连接到 vCloud Air。你可以从 `$Global:PIServers` 变量中检索存储的内容，这将返回你当前连接的 vCloud Air 用户名：

```
$global:DefaultPIServers
```

| Name | User |
|---|---|
| vchs.vmware.com | BrianGraf@vmware.com |

## Scope

Scope 是一个在其他设置之外必须使用的参数。在使用 `Set-PowerCLIConfiguration` cmdlet 时，它可以是一个非常有用的参数。Scope 允许你定义连接的范围。

