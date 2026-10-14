

**图 23-1：CAA 架构**

## 23.3.2 资源管理器 (caad)

每个成员都有一个资源管理器，它与其它集群成员的资源管理器进行通信。资源管理器监控各种资源类型，并在发生某些事件或满足其它条件时管理（启动、停止、迁移）应用程序资源。事件可以是从 EVM 接收到的事件（见表 23-2）或由集群管理员直接干预（例如，运行 caa_* 命令 – 见第 23.3.6 节）。术语“其它条件”用于表示当资源配置文件中定义的某个属性值达到阈值时，导致资源管理器采取行动。我们将在以下章节中进一步讨论此问题。

资源管理器仅监控和管理 CAA 注册表 (/var/cluster/caa/registry/caa.reg*) 中的资源。换句话说，一旦你创建（或修改）一个资源，你必须将该资源注册到 CAA。

有关 CAA 资源管理器的更多信息，请参阅 caad(8) 参考页。

## 23.3.3 资源监控器

资源监控器是资源管理器用来监控和控制特定资源类型的共享库插件。由于 CAA 支持四种资源类型（截至本文撰写时），/var/cluster/caa/monitors 目录包含四个必需的资源监控器。

![](img/a0df85c2e542a8d6c913113908553aa4_666_0.png)

**表 23-2：CAA 组件 EVM 事件订阅**

请注意，自 V5.1A 起，存在一个资源监控器注册表 (caa_type.reg)，其中资源监控器向资源管理器注册。该注册表是一个文本文件，但请勿尝试编辑它。

资源监控器注册表中确实包含不可打印字符，因此要查看 caa_type.reg 文件中有哪些资源监控器，我们建议使用 strings(1) 命令。

```text
$ strings /var/cluster/caa/registry/caa_type.reg
application application.so SCRIPTPATH=/var/cluster/caa/script
network network.so NONE
tape tape.so NONE
changer changer.so NONE
```

changer、tape 和 network 资源监控器订阅 EVM 事件，以便在监控的硬件组件发生故障或变得可用时获知（见表 23-2）。

## 23.3.4 资源注册数据库

资源注册数据库位于 /var/cluster/caa/registry 目录中。文件名可能因安装的 TruCluster Server 软件版本而异，但以“caa.reg”开头。

我们将在第 23.4.4 节讨论资源属性；因此如果此时这些内容对你来说毫无意义也不必担心。我们的目的是向你展示如何获取信息，而不是如何解释它——这将在本章后面进行。

如果你是一位资深集群专家型人物（又名 TruCluster Server Snoopylogy 首席故障排除员 CT S²），并且想转储资源注册数据库的原始内容，你可以使用位于 /usr/sbin/cluster 目录中的一个相对不为人知（目前未记录因此不受支持）的工具 caa_dbConvert。

下面是一个将资源注册数据库 (caa.reg.binaryDB) 转储到 /tmp 目录的文本文件 (caa.reg.txt) 的示例。

```text
# cd /var/cluster/caa/registry
# /usr/sbin/cluster/caa_dbConvert DUMP caa.reg.binaryDB /tmp/caa.reg.txt
```

尽管我们没有展示 /tmp/caa.reg.txt 的内容，但其中确实包含大量有趣的信息。

**注意：**

如果在使用上述命令时看到以下错误，请使用完整路径名指定资源注册数据库（或像前一个示例那样更改目录位置）。

```text
mmapFile::mapFile, caa.reg.binaryDB, open error
```

例如：

```text
# caa_dbConvert DUMP /var/cluster/caa/registry/caa.reg.binaryDB /tmp/caa.reg.txt
```

### 23.3.4.1 资源注册历史数据库

资源注册历史数据库也位于 /var/cluster/caa/registry 目录中。与资源注册数据库一样，文件名可能因安装的 TruCluster Server 软件版本而异，但以 "caa.his" 开头。

**注意：**

截至本文撰写时，我们见过以下两个文件名：

- caa.his - V5.0A, V5.1, V5.1A（未修补）
- caa.his.binaryDB - V5.1A（IPK 及以上），V5.1B

