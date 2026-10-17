
```
# -- /etc/nagios/mysite/contactgroups.cfg
define contactgroup{
    contactgroup_name    Local
    alias               Local Site
    members             nagios
    contactgroup_members contactgroup1,contactgroup2
}
```

额外的参数 `contactgroup_members` 允许 Nagios 3.0 将其他组包含为成员。在 Nagios 2.x 中不支持此参数。

## 2.9 当 Nagios 需要执行时：命令对象

Nagios 执行的所有操作都定义在命令对象中。在示例文件 `checkcommands.cfg` 中定义了一系列仅需包含的广泛命令。要这样做，只需将文件拷贝到 `mysite` 目录：

```bash
nagios:/etc/nagios$ cp objects/checkcommands.cfg mysite/checkcommands.cfg
# /etc/nagios/mysite/checkcommands.cfg
define command {
  command_name check_ping
  command_line $USER$/check_icmp -H $HOSTADDRESS -w $ARG1 -c $ARG2 -p
}
```

`check_ping` 是定义服务时调用的命令名称。`command_line` 定义了要执行的命令。此处不仅使用了 `ping`，还使用了效率更高的 `check_icmp`。两者的差异在 6 节中有解释。

## 2.10 使用 timeperiod 定义时间段

`timeperiod` 对象描述了 Nagios 生成发送通知的时间段。包含的示例文件（Nagios 3.0: `objects/timeperiods.cfg`；Nagios 2.x: `localhost.cfg`）包含了一些可以拷贝到 `timeperiods.cfg` 文件的定义。

在此，24x7 天的定义表述为“从周日至周六，每天 24 小时”：

```
# -- /etc/nagios/mysite/timeperiods.cfg
define timeperiod{
 timeperiod_name 24x7
alias 24 Hours A Day, 7 Days A Week
 Sunday 00:00-24:00
 Monday 00:00-24:00
 Tuesday 00:00-24:00
 Wednesday 00:00-24:00
 Thursday 00:00-24:00
 Friday 00:00-24:00
 Saturday 00:00-24:00
}
```

特定工作日的每日时间也可以通过逗号“组合”：

```
define timeperiod{
 Monday 00:00-09:00,12:00-13:00,17:00-24:00
}
```

如果完全省略某项，则定义的时间段将不包含该日。

Nagios 3.0 允许定义特定日历日的周期：

```
2007-12-24 08:00-12:00
may 1 00:00-24:00
monday 2 00:00-24:00
monday 3 00:00-24:00

2007-12-24 - 2008-01-08 / 2 00:00-24:00
```

## 2.11 模板 (Templates)

Nagios 将定义分类为对象是有充分理由的：它们的特征可以被其他继承——这一特性可以节省大量的手动输入时间。你可以定义一个所谓的模板，并将其传递给其他对象作为基础，这样你只需要描述那些不同之处的细节即可。

可以通过一个示例很好地说明这一点（使用模板时所需的参数已加粗显示）：

```
# -- /etc/nagios/mysite/hosts.cfg
define host{
  name                Generic-Host
  register            0

  check_command       check-alive
  check_period        24x7
  contact_groups      localadmins
  notification_interval 120
  notification_period   24x7
  notification_options  d, u, r, f
}
```

通过 `name`，第一个对象被赋予了一个名称以便以后引用。接下来的条目 `register 0` 防止 Nagios 尝试将此模板视为真实的主机。在示例中，通用主机对象的项是不够的；因此，Nagios 在读取配置文件时会停止，并报错提示缺少此类定义所强制要求的参数，例如：

> Error: Host name is NULL

所有其他参数都涉及适用于依赖于 `Generic-Host` 的定义的设置。

在实际的主机定义中——在以下 `linux03` 和 `linux04` 的示例中——参数使用了模板并获取了预设值：

```
# -- /etc/nagios/mysite/hosts.cfg
define host{
  name                linux03
  use                 Generic-Host
  alias               Linux File Server
  address             192.168.0.1
}

define host{
  name                linux04
  use                 Generic-Host
  alias               Linux Print Server
  address             192.168.0.2
}
```

通过这种方式，你只需要完成这两个主机之间任何变化的条目。

但参数也可能出现在由模板定义的主机定义中。在这种情况下，主机处的定义具有优先级，它会覆盖模板中的值。

这种方式创建的模板通常可以用于所有对象类型。关于其使用的更多信息可以在 Nagios 3.0 在线帮助中找到：`http://localhost/nagios/docs/objectinheritance.html`³8¹。在 Nagios 2.x 中，该文件名为 `templaterecursion.html`。Nagios 3.0 的扩展功能（仅在更复杂的设置中开始发挥作用）见第 684 页的 H.1.8 继承。

> [38] 本地位于 `/usr/local/nagios/share/docs//objectinheritance.html`。

## 2.12 懒懒得输入的配置辅助

### 2.12.1 为多台计算机定义服务

通过同时为多个主机、甚至主机组定义服务，你可以极大简化服务定义：

```
# -- /etc/nagios/mysite/services.cfg
define service{
    host_name       linux01,linux02,linux04...
    service_description PING
}
```

指定多个用逗号分隔的主机可确保 Nagios 并行定义多个服务。你可以更进一步指定通配符 `*` 代替单个计算机别名。这将此服务分配给所有主机。

第三种可能性是通过通过主机组进行并行分配：

```
# -- /etc/nagios/mysite/services.cfg
define service{
    host_name       linux-servers,windows-servers
    service_description PING
}
```

在这种情况下，使用 `hostgroup_name` 参数代替 `host_name` 参数。

### 2.12.2 所有计算机的一个主机组

使用通配符 `*` 是描述包含所有定义计算机的主机组快的方法：

```
# -- /etc/nagios/mysite/hostgroups.cfg
define hostgroup{
    hostgroup_name  all-hosts
    members         *
}
```

### 2.12.3 其他配置辅助

实践中，2.11 模板中描述的覆盖多个主机的定义是最重要的。但还有其他基于升级（`escalation`）和依赖（`dependency`）对象的配置辅助，它们是在不同时间介绍给管理员的（见第 282 页的 12.5 升级管理和第 285 页的 12.6 主机间的依赖关系）。你也可以使用 `hostgroup_name` 代替 `host_name`（主机组列表），或使用 `servicegroup_name` 代替 `service_description`。此外，你可以为 `host_name` 和 `service_description` 设置值 `*`，这将涵盖所有主机或服务。
