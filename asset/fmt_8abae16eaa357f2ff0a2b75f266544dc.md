
以下显示了从 `zone1` 到 `zone2` 镜像 NLD 目录的典型配置文件。

```xml
<ZLMMirConf>
<SourceServer>
<Base>https://sourceprimary.zone1.com</Base>
<Proxy />
<Type>zlm</Type>
<User>Administrator</User>
<Password>source</Password>
</SourceServer>
```

```xml
<CatalogConf>
<Name nld-9-i586/>
<LocalName nld-9-i586/>
<Folder Mirror />
<Target />
<ExcludeTarget />
<Bundle />
<ExcludeBundle />
<Package />
<ExcludePackage />
</CatalogConf>
</ZLMMirConf>
```

此配置文件会导致 `nld-9-1586` 目录在本地主服务器上进行复制和更新。本地目录名称也将是 `nld-9-586`，并存在于 ZENworks Control Center 的 `/Bundles/Mirror` 文件夹中。

### 完成配置

你应该测试您的配置文件，以查看其是否正确形成以及是否会执行预期操作。

在创建源服务器的配置文件后，运行以下命令执行镜像操作的干运行，并可选地添加 `verbose` 参数以查看详细消息：

```bash
zlmirror -c config.xml --dryrun --verbose
```

如果此操作提供了预期结果，请运行命令完成操作：

```bash
zlmirror -c config.xml
```

### 总结

需要理解的是，与关系型数据库不同，你不直接更改或修改数据库。本章讨论了 ZENWorks Management 使用的数据库。

## 第 12 章：保持 ZENWorks Linux Management 服务器同步

### 数据库存储的信息

默认情况下，ZENWorks Linux Management 使用数据库。但是，你可以使用几个命令来查看数据库中的信息：

- 库存 (Inventory)
- 日志 (Logs)
- 策略 (Policies)
- 注册 (Registration)
- 层级 (Tier)

### 访问数据库

设置 ZENWorks Management，请遵循以下步骤：

1. 在终端中，输入 `psql` 登录：

```sql
Welcome to psql 7.4.7
Type=#
```

2. 输入 `\d` 查看数据库内容。

```sql
zenworks=# \d
```

3. 输入 `\d <value>` 查看数据库中特定项目的描述。例如，如果你输入 `\d battery`，你将看到类似于图 13.1 的屏幕。

### 图 13.1

PostgreSQL 的关系列表。

| Schema | Name | Type | Owner |
| --- | --- | --- | --- |
| public | action_arg | table | postgres |
| public | batchmetry_enum | table | postgres |
| public | battery | table | postgres |
| public | bundle_deps | table | postgres |
| public | bundle_package | table | postgres |
| public | bundle_world | table | postgres |
| public | bus | table | postgres |
| public | bustype_enum | table | postgres |
| public | chassis | table | postgres |
| public | chassis_enum | table | postgres |
| public | dependency_type | table | postgres |
| public | desktop_monitor | table | postgres |
| public | driver | table | postgres |
| public | eventaram | view | postgres |
| public | file_dependency | table | postgres |
| public | floppy_disk | table | postgres |
| public | liberate_sequence | sequence | postgres |

### 图 13.2

`battery` 表描述。

| Column | Type | Modifiers |
| --- | --- | --- |
| batteryid | bigint | not null |
| name | character varying(128) |  |
| chemistry | smallint |  |
| design_capacity | smallint |  |
| design_voltage | smallint(32) |  |
| smart_bat_version | character varying(128) |  |
| manufacturer | character varying(64) |  |
| serial_number | bigint |  |
| hwid | |  |

除了列出的命令外，你还可以使用 ZENworks Control Center 或使用 `zlman` 中的命令来管理来自中的信息。

### 获取更多信息

您可以在 `www.postgresql.org` 获取 PostgreSQL 的极佳信息、文档等。

您可以在 `http://www.novell.com/documentation/edir873/index.html` 获取更多关于 ZENworks Object Store (eDirectory 8.7.3) 的信息。

### 结论

ZENworks Linux Management 为存储和管理您的 Linux 系统提供了强有功能。无论您选择 PostgreSQL 还是 Oracle，您都将获得来自 Novell 预期的企业级工具和实力。

## 故障排除

ZENworks Linux Management 是一个强大的工具，用于管理和更新您的 Linux 设备。然而，由于网络环境的复杂性，可能会出现导致 ZENworks 无法正常工作的问题。本章介绍了如何在 ZENworks Linux Management 系统中排除故障。

### 注册与取消注册设备

某些情况下，您可能需要将工作站从区域（zone）中取消注册。通过本地 `rug` 命令，您可以将设备取消注册并重新注册到目标区域。

要取消注册设备，请执行以下操作：

1. 进入设备上的命令行界面。
2. 输入 `rug sl` 命令以查看该设备注册的所有服务。注意您想要删除的服务编号（这是输出结果第一列的数字）。
3. 输入以下命令从服务中取消注册：`rug sd <服务编号>`。

这将删除该服务。如果该服务是 ZENworks Linux Management 服务且您之前已注册了它，那么取消注册的操作不会删除对象存储中的设备。如果您想删除设备对象，必须在 ZENworks 控制中心中将其删除。

## 第 14 章：故障排除

要注册一个设备，请执行以下操作：

1. 进入设备上的命令行界面。
2. 输入 `rug sl` 命令以查看该设备注册的所有服务。检查您是否已注册到目标服务器。如果已注册，您需要先取消注册。
3. 输入以下命令从服务中注册：`rug sa <ZENworks 服务器的 DNS 或地址>`。

这会将您的设备注册到该服务器的 ZENworks 区域。此操作是在系统内核注册您的设备对象。

### 创建自定义平台

有时，您的公司可能根据 ZENworks Linux Management 支持的平台之一，创建创建了某些特殊的自定义发行版。ZENworks 可以识别这些自定义发行版，随后程序包（bundles）中的 RPM 可以这些新的自定义发行版作为目标，从而允许您识别该 RPM 仅适用于此类设备类型。

要创建一个新的自定义平台，请完成以下操作：

1. 启动 ZENworks 控制中心。
2. 选择浏览器顶部的“配置”（Configuration）选项卡。
3. 从“管理区域设置”（Management Zone Settings）选择“平台”（Platforms）。
4. 滚动到屏幕底部，从“自定义平台”（Custom Platforms）快照选择“添加”（Add）。您将看到如图 14.1 所示的对话框。

图 14.1

用于创建自定义目标的“添加平台”对话框。
