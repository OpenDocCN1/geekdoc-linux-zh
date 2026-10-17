
Nagios 2.0 作为新接口的事件代理（`event broker`）允许以加载模块的形式为 Nagios 添加某些功能，例如将测试结果保存到数据库而不是文件。一个使用事件代理接口的应用程序是 `NDOut`（第 17 章，第 375 页）。可能的值为 `0`（关闭）和 `-1`（接受所有模块）。默认值：

```
event_broker_timeout=0
```

Nagios 检查尚未完成的处理器后的等待时间。默认值：

```
event_handler_timeout=30
```

全局启用/禁用主机检查。这在分布式环境中仅会被关闭，因为中央 Nagios 会接受来自其他 Nagios 服务器的被动结果（见第 15 章）。默认值：

```
execute_host_checks=1
```

与 `host_checks` 类似，用于服务检查。默认值：

```
execute_service_checks=1
```

指定外部命令文件接口（13.1 外部命令接口，第 292 页）可以临时存储的外部命令的最大数量。如果缓冲区不够大，可能会丢失某些结果。默认值：

```
external_command_buffer_slots=96
```

Nagios 通常为每个进程创建子进程，但设置参数 `use_large_installation_tweaks=1`（见 A.1 主配置文件）会关闭此行为。在 Nagios 中：

```
free_child_process_memory=0
```

除了通过 `event_handler` 定义的主机特定处理器外，还定义了一个全局处理器。对于两者，都必须在 Nagios 定义中启用全局参数 `enable_event_handlers` 以及参数 `event_handler_enabled`。Nagios 可以在执行主机特定处理器之前执行全局处理器（一个普通命令对象）。示例（无默认值）：

```
global_event_handler_name_of_the_command_object
```

`global_event_handler` 的服务特定等效项。除了 `enable_event_handlers` 之外，服务定义中的 `event_handler_enabled` 也必须启用。示例（无默认值）：

```
global_service_event_handler_name_of_command_object
```

主机检查检测的上限。详细信息见附录 B，第 611 页。默认值：

```
high_host_flag_threshold=30
```

服务检查检测的上限（见附录 B）。默认值：

```
high_service_flag_threshold=30
```

Nagios 触发检查后，如果该检查未返回结果的秒数。默认值：

```
check_timeout=30
```

两次检查之间的间隔时间（秒）。默认值：

```
host_freshness_check_interval=60
```

控制 Nagios 在重启后如何处理主机检查。一种复杂的程序防止 Nagios 在这种情况下同时执行所有检查，从而导致服务器过载。可能的值有：`s`（智能，自动分配主机检查），`n`（否，所有检查同时启动），`d`（笨，Nagios 以秒为间隔处理测试），以及以秒为单位指定的间隔 `x.x`。默认值：

```
host_inter_check_delay_method=s
```

```
host_perfdata_command=
```

Nagios 对象应该在每个主机检查后检查数据。这需要设置 `process_performance_data` 参数。

此参数仅在少数情况下有意义，因为 Nagios 只在需要时才执行主机检查，因此间隔非常不规则。它用于在不使用模板的情况下处理性能数据（19.1 使用 Nagios 处理插件数据，第 48 页），示例（未设置默认值）：

```
host_perdata_command=host-perdata
```

```
host_perdata_file=
```

指定一个文件或命名路径，Nagios 通过模板机制在一定程度上从中从主机获取性能数据（第 19 章）。必须设置 `process_performance_data`。示例（无默认值）：

```
host_perdata_file_mode=host-perdata
```

定义数据传递到 `host_perdata_file` 的方式。可能的值为（追加到普通文件）或（写入新文件，Nagios 3.0 允许非写入，这对于文件特别有用）。示例（无默认值）：

```
host_perdata_file_command=
```

在主机性能数据在 `host_perdata_file` 接口上处理后调用的 Nagios 命令对象。该参数仅配合模板机制且是可选的。根据 Perl（19.3 使用 Perl 性能数据）指定，它会从接口永久读取数据。示例（无默认值）：

```
host_perdata_file_processing_command=process-host-perdata-file
```

```
host_perdata_file_processing_interval=
```

如果此值（以秒为单位）大于 l，属于它的命令（`host_perdata_file_processing_command`）将按这些间隔定期运行。`0` 确保它不被使用。示例（无默认值）：

```
host_perdata_file_interval=0
```

描述输出格式。输出中的 Nagios 宏和数据格式会被 `\t`（制表符）或 `\` 替换。其中一种用法（19.1 使用 Nagios 处理插件数据，第 404 页）。示例（无默认值）：

```
host_perdata_file_template=$SERVICES$HOSTNAMES$SHOST$EXECUTION$IMES$SHOUTPUTS$SHOUTDATAS
```

```cfg
max_concurrent_nacks=0
```

```cfg
max_debug_file_size(Nagios 3.0)
```

限制调试文件的大小为指定的字节为单位的值。示例：

```cfg
max_debug_file_size=204800
```

如果大小超过了给定的值，Nagios 会为文件添加 `.old` 后缀。如果已存在同名文件，它将会被删除。因此，你必须为此处指定的大小留出空间，因为可能同时存在两个文件（带 `.old` 后缀和不带的）。

```cfg
max_host_check_spread
```

Nagios 在重启后应该在什么时间（分钟）开始主机检查？这可以防止所有测试同时执行，导致 Nagios 服务器过载。默认值：

```cfg
max_host_check_spread=30
```

```cfg
max_service_check_spread
```

类似于 `host_check_spread`，但针对服务。默认值：

```cfg
max_service_check_spread=30
```

```cfg
nagios_group
```

Nagios 守护进程运行所需的权限的用户组。默认值（编译时定义）：

```cfg
nagios_group=nagios
```

```cfg
nagios_user
```

Nagios 守护进程运行所需的权限的用户。默认值（编译时定义）：

```cfg
nagios_user=nagios
```

```cfg
nagios_timeout
```

在多少秒后，Nagios 应该放弃通知尝试（例如发送消息）。由于某些操作可能需要一定的时间，系统会首先等待接收者的确认。该值不应太低：默认值：

```cfg
nagios_timeout=30
```

```cfg
object_cache_file
```

Nagios 存储所有对象的起始文件。Web 界面使用此文件，可以在不运行 Nagios 的情况下构建普通配置文件，并加入 Web 界面的功能。默认值：

```cfg
object_cache_file=/var/nagios/objects.cache
```

```cfg
check_hosts
```

定义主机检查结果是否转发到中央 Nagios 实例。如果启用该参数，则在分布式环境中使用 `check_hosts` 中定义的命令；描述详见第 15 章第 317 页。默认值：

```cfg
check_hosts=
```

```cfg
check_services
```

定义服务检查结果是否转发到中央 Nagios 实例。如果启用该参数，则使用 `check_services` 中定义的命令。此功能用于分布式环境（见第 15 章第 317 页）。默认值：

```cfg
check_services=
```

```cfg
host_command
```

定义主机处理器，即一个 Nagios 命令对象，用于将分布式环境中的所有主机检查转发到中央实例（详见第 15 章第 317 页）。示例（无默认值）：
