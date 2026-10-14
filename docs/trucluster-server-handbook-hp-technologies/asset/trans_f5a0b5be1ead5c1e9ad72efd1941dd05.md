

# /var/cluster/caa/script/myFirstCAA_app.scr start

如果这样可行，那么验证停止入口点是否也有效。

```
# /var/cluster/caa/script/myFirstCAA_app.scr stop
```

这是一个非常简单的示例，测试你的应用程序资源操作脚本可能需要更彻底。有关更多信息，请参阅第 23.5 节。

## 24.2.4 验证、注册并启动应用程序资源

操作脚本测试完成后，验证资源配置文件。

```
# caa_profile -validate myFirstCAA_app
```

如果配置文件验证通过，则注册资源。有关更多信息，请参阅第 23.4.7 节。

```
# caa_register myFirstCAA_app
```

资源成功注册后，启动资源。有关更多信息，请参阅第 23.4.11 节。

```
# caa_start myFirstCAA_app
Attempting to start 'myFirstCAA_app' on member 'molari'
Start of 'myFirstCAA_app' on member 'molari' succeeded.
```

启动资源后，为确保万无一失，将其迁移。

```
# caa_relocate myFirstCAA_app
Attempting to stop 'myFirstCAA_app' on member 'molari'
Stop of 'myFirstCAA_app' on member 'molari' succeeded.
Attempting to start 'myFirstCAA_app' on member 'sheridan'
Start of 'myFirstCAA_app' on member 'sheridan' succeeded.
```

## 24.3 依赖资源

创建依赖资源与我们在第 24.2 节中创建简单的高可用性资源时采用的方法类似。不同之处在于，我们还必须创建要依赖的资源（或资源）。

确定应用程序的需求（或依赖关系）。例如，如果你有一个连接到数据库的应用程序，则可以定义两个应用程序资源：

- DBuser - 为使用数据库的应用程序创建应用程序资源。将数据库应用程序资源（DB）设置为 OPTIONAL_RESOURCE 或 REQUIRED_RESOURCE 属性列表之一。
- DB - 为你的数据库创建应用程序资源。

注意，资源名称是虚构的，并非特定于任何资源类型。

另一个示例是用于通过网络备份客户端系统的应用程序资源。在这种情况下，集群充当网络上其他系统的备份服务器。可以说，备份应用程序应位于与网络以及备份介质（磁带和介质机器人）具有直接物理连接的集群成员上。在此示例中，你可以定义四个资源：

- BackupNet - 为你的网络备份程序创建应用程序资源。将网络（BackupNIC）、磁带（BackupTAPE）和更换器（BackupROBOT）资源设置为 OPTIONAL_RESOURCE 或 REQUIRED_RESOURCE 属性列表之一。
- BackupNIC - 创建网络资源。
- BackupTAPE - 创建磁带资源。
- BackupROBOT - 创建更换器资源。

注意，与前一个示例一样，资源名称是虚构的，并非特定于任何资源类型。

有关依赖资源的更多信息，请参阅第 23.6.1 节和第 23.6.2 节。

## 24.4 CFS 服务器迁移

应用程序的可用性通常取决于其成功访问应用程序数据的能力。如果应用程序数据位于文件系统上（而不是原始设备上），那么将应用程序资源和 CFS 服务器位于同一服务器上肯定会更高效。由于目前没有可用于监控文件系统 CFS 服务器位置的“CFS 服务器”资源类型，也无法作为应用程序资源的依赖项，因此以下是几种可能的解决方案：

- 创建一个监控并迁移 CFS 服务器的应用程序资源。
- 将 CFS 服务器资源和监控功能添加到现有的应用程序资源中。

### IMPORTANT：

如果你计划在多文件集域中迁移文件系统，请记住 CFS 服务器按域为 AdvFS 文件系统提供服务。

换句话说，不要创建一个将知识迁移到 member1 的资源，而另一个资源将 knowwhere 迁移到 member2。

有关更多信息，请参阅第 13 章。

## 24.4.1 CFS 服务器应用程序资源

CFS 服务器应用程序资源也可以实现为创建简单的、高可用性的应用程序资源（请参阅第 24.2 节），并考虑以下事项：

- 修改 application.tdf 类型定义文件，为文件系统和挂载点添加两个用户定义属性。这两个属性都应定义为“name_list”类型。
- 修改操作脚本中的“start”和“check”入口点以执行 CFS 服务器迁移任务。

### 24.4.1.1 添加 USR_CFS 和 USR_MNT_PT 用户定义属性

USR_CFS 属性将用于定义文件系统列表，而 USR_MNT_PT 属性将用于应与文件系统列表匹配的挂载点列表（实际上操作脚本应检查是否如此）。

```
USR_CFS   =  cluster_root#root cluster_usr#usr cluster#var
USR_MNT_PT =  / /usr /var
```

1. 保存原始 application.tdf 文件的副本。

```
# cd /var/cluster/caa/template
```

```
# cp application.tdf application.tdf.orig
```

> application.tdf 文件从 V5.1A/PK1 开始位于 /var/cluster/caa/template 目录中。

