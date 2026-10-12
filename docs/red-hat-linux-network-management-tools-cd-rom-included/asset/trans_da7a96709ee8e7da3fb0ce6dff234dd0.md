
假设我们已启用系统以支持四个 *mountd* 实例：

```
`proc mountd 4 4`
```

如果代理检测到当前运行的 *mountd* 进程少于四个或多于四个，它会适当更新 MIB。

如果未指定最大值和最小值，则假定默认值为零。实际上，同时使用最大值和最小值选项提供了一种灵活的方式来满足特定的监控需求。

该命令

```
`proc ntalkd 4`
```

指示代理监控 *ntalkd* 进程，如果当前运行的进程超过四个则更新 MIB。因此，最大值选项提供了一种便捷的方式，以确保当前仅允许特定数量的进程运行。如果我们想更进一步，可以让代理在发现 *ntalkd* 进程时自动采取行动（例如终止进程）。由于未列出最小值，当未发现 *ntalkd* 进程运行时，代理将不采取任何行动。

选择使用 *proc* 关键字监控哪些 UNIX 进程，主要取决于确定哪些服务对您的环境运行至关重要。如果计算系统支持发布软件，您可能更关心打印后台处理程序和文字处理应用程序，而支持在线订单录入软件的系统可能需要监控数据库服务器进程。

另一方面，有人可能会采取这样的方法：系统上运行的一切都是关键的，都必须受到监控。乍一看，这似乎是一个合理的策略。不幸的是，这可能导致其他问题，而且在大多数情况下可能有些大材小用。如果我们想监控所有系统进程，是否也要监控网络服务等临时进程？如果是，监控哪些？此外，维护这些进程的代理配置文件充其量只是一项苦差事，因为每当系统添加或移除新应用程序和软件时，都必须更新该文件。代理的性能也会受到影响。监控大量进程可能会导致代理负载过重，这应当避免。

假设我们已配置代理监控 *mount* 进程和四个 *ntalkd* 进程。以下示例显示了当代理检测到没有 *mount* 或 *ntalkd* 进程运行时 MIB 的值：

```
enterprises.ucdavis.procTable.prEntry.prErrorFlag.1 = 1  
enterprises.ucdavis.procTable.prEntry.prErrorFlag.2 = 1  
enterprises.ucdavis.procTable.prEntry.prErrorMessage.1 = "No mount process running."  
enterprises.ucdavis.procTable.prEntry.prErrorMessage.2 = "Too few ntalkd running (# = 0)"
```

## 代理安全

UCD 代理支持 SNMPv1、SNMPv2 和 SNMPv3 安全方法，并使用表 7.2 中列出的安全关键字进行配置。代理实现的主流安全模型包括基于视图的访问控制模型 (VACM)；不过，SNMPv1 和 SNMPv2 的旧安全模型也受支持。该 VACM 模型随 SNMPv3 规范引入，简而言之，它基于不同的视图和用户级别提供安全性，这些视图和用户级别控制对单个对象、组或整个 MIB 的访问。

关键字 *com2sec* 指定源/团体名称与安全名称之间的映射，语法如下：

```
com2sec security_name source community_string
```

其中 *security_name* 可以是任意字符串，用于后续的安全策略定义。*source* 参数可以是主机名、IP 地址、网络或保留关键字 *default*。*default* 字是通配符，将匹配任何源。指定网络时，支持两种不同格式：带地址掩码的地址和带活动位数的网络地址。因此，

```
134.111.82.0/255.255.255.0
```

和

```
134.111.82.0/24
```

两者等效，可互换使用。`community_string` 代表管理实体将提供的团体密码。以下是 `com2sec` 条目的示例：

```
com2sec public-sec-name default public
```

此条目定义安全名称为 `public-sec-name`，任何使用团体字符串 `public` 的源均被允许访问。以下示例提供了额外的控制：

```
com2sec priv-sec-name 134.111.80.0/24 private-80
```

在这种情况下，定义了一个新的安全字符串 `priv-sec-name`，它将访问限制为源地址为 134.111.80.0 且团体密码为 `private-80` 的任何设备。

关键字 `group` 指令定义模型/安全名称与组之间的映射：

```
group group_name available_model security_name
```

`group_name` 是一个字符串，可以代表一组用户或任何其他组定义。`available_model` 是代理支持的已定义安全模型之一。它们包括 `any`、`v1`、`v2c` 和 `usm`。`any` 关键字是通配符，表示其他任何模型。`v1` 模型与 SNMPv1 团体字符串相关联，其中单个字符串名称用作认证令牌。`v2c` 模型采用基于公共和/或私有安全密钥的基于团体的认证。`usm` 模型，即用户安全模型 (USM)，随 SNMPv3 引入，包含规定用户必须在 SNMP 代理中定义以用于认证目的的规范。

`group` 关键字的主要目的是进一步定义对个别用户组或其他实体的控制级别。例如，请考虑以下内容：

```
group anybody any public-sec-name
```

此示例中的条目定义了一个名为 `anybody` 的组，基本上表示只要使用与 **public**-**sec-name** 关联的团体字符串，即允许使用所有安全模型进行的任何访问。因此，在示例中
`group admin usm priv-sec-name`

定义了一个称为 *admin* 的组，由于它使用 **usm** 模型和 *priv-sec-name* 安全名称，因此对访问有相当严格的限制。此时，*v2c* 和 *usm* 安全模型的确切语法和语义尚未定义。然而，为讨论起见，假设在需要的地方，相关的网络管理软件负责向代理提供适当或正确的信息。

关键字 **view** 定义了一个或多个代理 MIB 的特定视图。这是一个非常强大的功能，因为它允许以有趣且有益的方式划分网络及相关设备的网络管理功能。例如，ISP 可能会向其客户提供对其内部网络设备或特定接口的访问权限。通过仅提供对客户需要管理访问权限的那些接口和网络的访问，ISP 的网络安全和管理得以保留，但客户可以进行高级故障排除和性能监控。所有这些都可以通过网络设备中包含的代理 MIB 的不同视图来实现。

**view** 命令的语法如下：

`view name type mib_tree [mask]`

**view** 命令的下一个参数是特定视图的名称。该名称可以是任意字符串值，但应描述视图中定义的 MIB 对象或组。**name** 后跟视图类型：*included* 或 *excluded*。关键字 **included** 表示 *mib_tree* 对象包含在视图内，而 *excluded* 表示 *mib_tree* 对象不包含在视图内。*mib_tree* 表示代理内的 MIB 定义，视图将被允许或拒绝访问该定义。*mib_tree* 对象可以包含特定的 MIB 对象或组。例如，*.1.3.6.1.2.1.1* 和 *.iso.org.dod.internet.mgmt.mib-2.interfaces* 都是有效的 MIB 对象定义。以下是一个有效视图的示例：

`view system_group include system fe`
