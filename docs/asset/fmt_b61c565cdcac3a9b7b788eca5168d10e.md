
该值切换用于关闭缓存；默认值为 15。此值应取决于情况。较大的值会给 Nagios 造成巨大的压力，但存在该值可能过时且不再有效的危险。Nagios 会缓存服务检查结果。因此，当存在非常大量的服务检查时，此参数将产生影响：

```
cached_service_check=30
```

## cfg_dir

包含对象的配置文件所所在的目录。Nagios 会在该处递归搜索扩展名为 `.cfg` 的配置文件。带有名称的文件将被忽略，因此你可以在此目录中放置帮助文件，并从这些帮助文件中自动生成主机。该指令可以根据你的需要指定（参见第 35 页的 2.1 主配置文件）：

```
cfg_dir=/etc/nagios/commands
```

## cfg_file

集成一个包含对象的单个文件。此内容请参见第 55 页的 2.1 主配置文件。该指令可以根据你的需要指定。Nagios 3.0 允许设置从 Nagios.cfg 目录开始的相对路径：

```
cfg_file=/etc/nagios/commands.cfg
```

## check_external_commands

启用外部命令接口。对于通过 Web 界面执行检查或命令是必要的。此内容请参见第 292 页的 13.1 外部命令接口。默认值：

```
check_external_commands=0
```

## check_for_orphaned_services

如果在一定时间后没有收到检查结果，则将其称为孤立服务（orphaned service）。由于 Nagios 仅在存在结果时缓存检查结果，如果正在运行的检查被手动终止，可能会导致该服务永远不再被测试。如果怀疑发生了孤立服务，为了调试目的，你应该将 `check_for_orphaned_services` 设置为 `true`。Nagios 会日志文件中写入相应的错误。这是否合理可以在 Web 界面中很容易看出；所有服务都独立于其状态显示，并按最后检查时间升序排序。通常，主动检查的执行时间不应长于 `check_check_interval`。默认值：

```
check_for_orphaned_services=0
```

## check_host_freshness

如果长时间没有到达检查结果，允许对主机检查进行主动测试。Nagios 在经过 `host_freshness_interval` 步后会认为测试结果太旧了。更多关于新鲜性检查的内容（参见第 295 页的 13.4 对被动检查的过期信息做出响应）：默认值：

```
check_boost_path (Nagios 1+)
check_result_path (Nagios 3.0)
```

从 Nagios 3.0 开始，检查以文件形式缓存的路径。这并不是必需的，但其目的是让 Nagios 定期输出这些文件。每个 Nagios 实例都需要一个独立的目录。示例：

```
check_result_path=/var/nagios/checkresults
```

## check_reaper_frequency (Nagios 3.0)

清理器（Reaper）收集检查结果并为 Nagios 处理这些结果。`check_reaper_frequency` 定义了启动这些进程的间隔。短的间隔会增加系统负载；长时间的间隔可能会导致 Nagios 调度延迟。示例：

```
check_reaper_frequency=5
```

该参数取代了 Nagios 2.x 中的 `service_reaper_frequency`。

```
check_service_freshness=
```

等同 `check_host_freshness` 的服务项，Nagios 检查结果过期的时间由参数 `service_freshness_interval` 定义。默认值：

```
child_process_timeout=(Nagios 3.0)
```

Nagios 在执行检查时会启动两个子进程。这使得系统对于崩溃的插件更具健壮性。默认：

```
child_process_timeout=
```

参数 `use_large_timeout`（外部配置文件 `file.cfg`）将值设置为 0（仅一个子进程），`process_timeout` 激活此项，即 `use_large_timeout` 被设置的这一事实。

## command_interval

定义了命令测试外部命令（参见第 292 页的 13.1 外部命令接口）是否存在新条目的时间。要发生此操作，必须启用 `external_commands`。

一个简单的数字指的是时间单位，由 `interval_length` 指定的单位。要发生此操作，`external_commands` 必须启用。

一个简单的数字指的是时间单位，由 `interval_length` 指定的单位。要发生此操作，`external_commands` 必须启用。

一个简单的数字指的是时间单位，由 `interval_length` 指定的单位。要发生此操作，`external_commands` 必须启用。

## command_file

一个用于外部命令的命名管道。Nagios 使用它（参见 13.1 外部命令）。默认值：

```
command_file=/var/nagios
```

## comment_file (Nagios 2.x)

Nagios 存储注释，这可以通过 Web 界面访问。默认值：

```
comment_file=/var/nagios/comments
```

## data_format

值切换用于关闭缓存；默认值为 15。这并不是必需的，但其目的是让 Nagios 定期输出这些文件。较大的值会给 Nagios 造成巨大的压力，但存在该值可能过时且不再有效的危险。Nagios 缓存服务检查结果。因此，以文件格式缓存的的路径：

```
downtime_file=/var/nagios
```

## _file (Nagios 3.0)

从 Nagios 3.0 开始，检查以文件格式缓存的路径。默认值：

```
downtime_file=/var/nagios
```

## debug_file

为了 Nagios 调试，你可以将 `debug_file` 设置为一个路径。Nagios 会在日志文件中写入相应的错误。默认：

```
debug_file=/var/nagios/debug
```

## debug_verbosity (Nagios 3.0)

定义了调试时的详细程度：

- 0 关闭
- 1 稍微
- 2 详细
- 3 调度
- 4 主机和服务检查
- 5 事件代理

## enabled_perl (Nagios 3.0)

开启嵌入解释器。在 Nagios 2.x 中，内置的总是激活的。Nagios 3.0 允许通过参数设置此项。默认：

```
enabled_perl=1
```

## enabled_environment_macros (Nagios 3.0)

标准，如 `$ENVIRONMENT`（参见第 631 页的 D.8 使用环境变量）可以通过环境变量访问。在 Nagios 3.0 中，可用宏的数量剧增，以至于在大环境中使用它们会导致性能问题。默认：

```
enabled_environment_macro=
```

## enabled_event_handlers

全局切换主机和服务检查的（开启）或（关闭）事件处理器。更多内容请参见第 619 页的附录 C。默认：

```
enabled_event_handlers=1
```

## enabled_flag_detection

定义 Nagios 是否能够检测状态变化（标记检测，更多内容请参见第 611 页的附录 B）。默认：

```
enabled_flag_detection=0
```

## enabled_notifications

定义 Nagios 是否可以发送通知。切换此功能对于分布式安装的中心主机才有意义，它们无法生成通知，而是将其结果转发到中央 Nagios 实例（参见第 37 页的第 15 章）。默认：

```
enabled_notifications=0
```

## enabled_predictive_host_dependency_checks (Nagios 3.0)

Nagios 3.x 在给出相应的时间 `cached_host_check_horizon` 时缓存主机检查。`enabled_predictive_host_dependency_checks` 参数缓存不仅用于判断不可达主机的 `DOWN` 和 `UNREACHABLE`，还用于依赖检查，某些依赖关系已经定义（参见 12.6.2 仅在特殊情况下：主机依赖）

## enabled_predictive_service_dependencies (Nagios 3.0)

如果启用此参数（1），服务将使用缓存结果来解析依赖，而不是重新执行检查。关于服务依赖的更多内容请参见第 285 页的 12.6.1 标准情况：服务依赖。
