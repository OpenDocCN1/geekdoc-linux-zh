
扩展和多行输出的格式在 8.5.1 多行插件输出（第 193 页）中描述，扩展格式的使用示例由插件 `check_multi`（8.5 使用 check_multi 汇总检查，第 191 页）提供。

## H.11 CGI

Nagios Web 界面也发生了一些有趣的变化。配置文件 `cgi.cfg`（A.2 CGI Configuration in cgi.cfg，第 306 页）中添加了一些新参数。`lock_author_names` 可防止用户名（当您对主机或服务设置确认或注释时会包含该用户名）被更改。相反，它将使用用户在向 Web 服务器身份验证时指定的用户名。因此，每个注册用户都是经过验证的用户。

`escape_html_tags` 决定是否使用插件输出中的 HTML 格式（值为 0）或是否由 Nagios 将其移除（值为 1）。为了与 `action_url`（16.4.1 Extended host information）和 `notes_url`（16.4.1 Extended host information）关联，现在有了额外的选项来指定目标窗口，即 `action_url_target` 和 `notes_uri_target`。

通过 CGI 程序 `status.cgi`（16.2.1 Variations in status display: status.cgi，第 334 页），现在可以通过 `hostprops` 和 `serviceprops` 选择硬状态（hard states）和软状态（soft states）。这在在使用 NagVis（第 18 章，第 389 页）时特别有用，因为 NagVis 默认只显示硬错误状态。

## H.12 杂项

不属于上述任何部分的改进之一是参数 `use_timezone`（第 606 页），通过它，你可以独立于 Nagios 服务器上设置的时间设置时区。只有在单台机器上运行多个 Nagios 实例时，这才是必要的。

参数 `additional_freshness_latency`（见附录 A）会延迟新鲜度检查（见 13.4 Reacting to Out-of-Date Information of Passive Checks，第 295 页），通常使用以秒为单位的时间段，以防 Nagios 等被动检查结果时等待过长。

指令 `cfg_file` 和 `cfg_dir`（A.1 The Main Configuration File nagios.cfg）现在也可以处理相对路径。基目录是包含 `nagios.cfg` 文件的目录。

参数 `temp_path` 显式指定临时目录（在 Nagios 2.x 中，临时空间仅由一个文件组成，由参数 `temp_file` 定义）。

Nagios 3.0 现在允许在所有配置文件中使用多行指令。在下一行继续的指令必须以反斜杠 `\` 结束。

## H.13 从 Nagios 2.x 升级到 3.0

如果你已经有一个运行中的 Nagios-2.x 环境，可以很轻松地切换到 Nagios 3.0。现有的配置通常会在保持不变的情况下运行。

然而，Nagios 3.0 在测试方面非常严格。很有可能一个此前未发现的错误——一个 Nagios 2.0 能够允许或忽略的错误——阻止 Nagios 3.0 启动。因此，在升级之前测试配置是一个好主意。为此，你按照第 39 页 1.2 Compiling Source Code 中的描述运行 `make all` 安装，但不运行 `make install`。你将在基础目录下获得一个可执行的 Nagios-3.0，可以使用它来从源代码测试现有配置：

```
linux:src/nagios-3.0 # ./base/nagios -v /etc/nagios/nagios.cfg
```

如果 Nagios 在此处发现错误，只要不消除该错误，它将阻止新版本 Nagios 的启动。Nagios 3.0 会对新功能给出一些警告和信息，但这些不会阻止重启。

尽管如此，在 Nagios 3.0 运行之前，你应该注意一些小细节。参数 `service_reaper_frequency` 现在更名为 `check_result_reaper_frequency`（A.1 The Main Configuration File nagios.cfg）；它在 `nagios.cfg` 中仅被重命名；`aggregate_status_updates` 被完全移除，因此在 `nagios.cfg` 中被注释掉了。

宏 `$NOTIFICATIONNUMBERS` 被明智地拆分为主机特定和特定特定宏（`$NOTIFICATIONNUMBERS $SERVICIFICATIONNUMBER`）。必须调整调整该宏的命令和脚本以确保它们能够正常工作。

为了保留 `downtime_file` 和 `comment_file` 中不再使用的文件（在本书中为 `comments.dat` 和 `downtime.dat`）的维护间隔和注释，你必须停止 Nagios，保存它们，然后移除它们开头的 Info 块，因为该块可能只出现在 `retention_file` 指定的新文件中：

```
info {
  created1144429286
  version=2.0
}
```

然后将两个文件的内容复制到保留文件的末尾，在本书中该文件为 `var/nagios/retention.dat`：

```
linux:- # /etc/init.d/nagios stop
linux:- # cd /var/nagios
linux:var/nagios # cat comments.dat downtime.dat >> retention.dat
```

现在执行剩下的三个安装步骤（见 1.2 Compiling Source Code）：

```
linux:src/nagios-3.0 # make install
...
linux:src/nagios-3.0 # make install-init
...
linux:src/nagios-3.0 # make install-commandmode
...
```
