
[337] http://localhost/nagios/docs/objectinheritance.html

## H.2 变量与宏

你可以在 `host`、`service` 和 `contact` 对象中定义变量。这些变量的名称始终以下划线开头，并像普通变量一样被使用：

```
define host {
  host_name linux0
  use      host_site0,host_generic_t
  ...
  _NRPE_PORT 5666
}
```

变量 `_NRPE_PORT` 被赋值为 `$_HOSTNRPE_$PORT$`，这意味着在下划线后添加了对象类型 `HOST`、`SERVICE` 或 `CONTACT`。这稍显遗憾，因为读起来更加困难。创建的宏可以在其他地方使用，例如在命令的定义中：

```
define command {
  command_name check_nrpe
  command_line $USER$/check_nrpe -H $HOSTADDRESS -p $HOSTNRPE_$PORT
  $ARG1$
}
```

宏允许访问配置数据、状态和检查结果。在 Nagios 3.0 中，包含针对当前状态发送的通知数量的宏 `$_NOTIFICATIONNUMBER$` 已被特定主机和服务的宏 `$_NOTIFICATIONNUMBER-BERS$` 和 `$_SERVICENOTIFICATIONNUMBER$` 取代。

可用宏的列表已大幅增加。例如，一些新宏如 `$_LONGHOSTOUTPUTS$` 和 `$_SERVICEOUTPUTS$`，它们包含了多行插件结果的扩展插件输出（详见 H.10 扩展插件输出和 B.5.1 多行插件输出，第 193 页）。

宏 `$_NOTIFICATIONID$`、`$_SERVICENOTIFICATIONID$`、`$_HOST-EVENTID$`、`$_SERVICEEVENTID$`、`$_LASTHOSTEVENTID$` 和 `$_LASTSERVICE-EVENTID$` 用于 Nagios 3.0 中分配的每个唯一标识号。

`$HOSTDISPLAYNAME$` 和 `$_SERVICEDISPLAYNAME$` 对应 Nagios 3.0 中分配的每个唯一标识号。
