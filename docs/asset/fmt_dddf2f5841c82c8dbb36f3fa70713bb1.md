
此目录中找到的每个文件名格式为 `yyymmdd_HHMMSS.zip`（其中 `yyyy` 是四位年份，`mm` 是两位月份，`dd` 是两位日期，`HH` 是两位小时，`MM` 是两位分钟，`SS` 是两位秒）。

可以通过以下步骤通过管理控制台访问备份：

- 1. 打开管理控制台并点击“配置”选项卡进入主配置页面。
- 2. 点击你想查看的配置链接。
- 3. 点击“常规”（General）选项卡。这将打开允许你执行此配置通用功能的窗口。其中一项项是查看和恢复之前部署配置的能力。
- 4. 点击“恢复”（Restore）选项卡。你会看到此配置之前的版本列表。示例见图 4.11。

| 虚拟服务器 | HTTP 监听器 | 实例 | 常规 | 性能 | 访问控制 | 证书 | Java |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 日志偏好 | MIME 类型 | 监控设置 | Web/AV | 计划事件 | 恢复 | 高级 | |

www.example.com - 配置备份
页面根据采取备份的日期列出配置。备份在部署配置时自动进行。选择备份日期并点击恢复以恢复该配置。

# 配置备份 (3)

- EST2008年1月16日 8:38:53
- EST2008年1月16日 8:41:42
- EST2008年1月15日 8:44:09

图 4.11 配置备份屏幕

除了管理控制台外，你还可以使用 CLI 中的 `list-backups` 子命令显示特定配置的备份列表，如下：

```
wadm> list-backups --config=www.example.com

20080116_203853

20080116_204142

20080116_204409

wadm>
```

然后你可以使用 `restore-config` 子命令恢复这些配置中的任何一个。以下信息提供了该子命令的概述：

```
wadm> restore-config --<TAB>

--from-backup* --echo --no-prompt --all

--verbose
```

# 第 4 章 Web 服务器 7.0 管理

```
restore-config --backup=20080116_204142 "www.example.com"

CLI201 Command 'restore-config' ran successfully
```

> 注意：回滚功能是在 Web Server 7.0 PU2 中引入的。在软件的之前的版本中无法找到此功能。

在本书编写时，您无法查看为特定配置版本定义的设置。（此功能无法通过管理控制台或 CLI 访问）。那么，你如何知道正在恢复的配置就是你需要的那一个呢？实现这一点的最佳方法是提取配置 zip 压缩包的内容，并查看包中包含的文件。虽然不建议您修改 `config store` 目录下的文件，但查看配置 zip 压缩包是您恢复适当配置的唯一方法。

## 4.7.4 删除现有配置

可以通过管理控制台或 CLI 从文件系统中删除不再使用的旧配置。要通过管理控制台删除配置，请执行以下步骤：

- 1. 打开管理控制台并点击“配置（Configurations）”选项卡进入主配置页面。
- 2. 选择您想要删除的配置旁边的复选框，并点击页面上的“删除（Delete）”按钮。将删除配置页面。该页面提供了此配置任何已部署实例的信息。
- 3. 点击 OK 按钮执行以下任务：
   - 停止部署该配置的任何节点上运行的该配置实例
   - 从部署该配置的节点上移除实例
   - 从管理服务器上的配置存储器（Configuration Store）中删除配置
- 4. 您将看到该配置从“配置”表中消失。

## 4.8 总结

CLI 中的 `delete-config` 子命令可以作为管理控制台的替代。以下信息提供了该子命令的概述：

```
wadm> delete-config --<TAB>

--echo --no-prompt --verbose config-name
```

以下演示了如何使用 `delete-config` 子命令删除配置：

```
wadm> delete-config "My Test Config"

CLI201 Command 'delete-config' ran successfully

wadm>
```

与管理控制台不同，`delete-config` 子命令不支持删除已部署的配置。如果您尝试删除已部署的配置，将收到以下错误消息：

```
wadm> delete-config "My Test Config"

ADMIN3653: Cannot delete the configuration 'My Test Config'. It has been deployed to '1' node(s).

wadm>
```

要执行此任务，您必须先从部署该配置的节点上删除任何实例。然后就可以安全地移除配置。以下命令序列演示了如何从命令行完成此操作：

```
wadm> delete-instance --config="My Test Config" www.example.com

CLI201 Command 'delete-instance' ran successfully

wadm> delete-config "My Test Config"

CLI201 Command 'delete-config' ran successfully

wadm>
```
