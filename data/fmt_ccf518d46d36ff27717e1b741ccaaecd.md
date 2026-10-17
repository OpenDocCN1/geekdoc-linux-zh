
```
Director {
Name = bull-dir
DIRport = 9101
Query File = "/etc/bacula/query.sql"
Working Directory = "/var/Bacula/working"
Pid Directory = "/var/run"
Maximum Concurrent Jobs = 1
Password = "B@cu1Lik3s,fru17"
Messages = Standard
}
```

`Director` 资源某种程度上是 Bacula 之海的母舰。它的参数定义了调度器的名称和基本行为。选项设置了其他进程与调度器通信的通信端口、调度器存储临时文件的位置，以及调度器可以同时处理的并发作业数。

`Password` 参数定义了控制台程序用于验证调度器身份的密码。在控制台配置文件 `bconsole.conf` 的 `Director` 资源中，必须设置相同的密码。虽然密码以明文形式出现在配置文件中，但它绝不会通过网络传输。

在我们的配置示例中，调度器和控制台都托管在同一台机器上。然而，尽管如此，两个配置文件中都需要密码。

### 通用目录服务

```
Catalog {
Name = ATE
DBName = bacula;
user = bacula;
password = "fru17,B0Wl"
}
```

`Catalog` 资源部分标识了 Bacula 存储其运行记录的数据库。为了简单起见，我们为所有作业定义了一个目录。然而，Bacula 支持多个目录，如果你倾向于为每个客户端组维护一个独立的数据库，这个功能就会非常有用。目前，所有的目录数据库都必须位于同一个物理数据库服务器上。

`DBName` 参数是目录数据库的名称。该数据库在安装期间根据 `configure` 命令的数据库选项进行设置。Bacula 的预构建数据库创建脚本可以在 Bacula 源码发行版的 `src/cats` 目录下找到。

```
# Job definitions
Job {
    Name = "harp"
    Level = Full
    Write Bootstrap = "/atrust/admin/backups/bootstraps/harp.bsr"
    Client = harp
    File Set = harp
    Storage = SureStore
    Pool = SSFullPool
    Incremental Backup Pool = SSIIncrementalPool
    Schedule = Nightly
}
```

`Job` 资源定义了特定备份作业的参数。通常，每个客户端有一个 `Job` 定义。大部分参数都是自明的，但几个需要额外的讨论。

`Write Bootstrap` 告诉 Bacula 如何写入关于备份的启动信息，以便在恢复期间使用。启动文件列出了恢复作业所需的文件和卷。它们不是强制性的，但强烈建议使用。启动文件在全量备份期间会被覆盖，在增量备份期间会被追加。

`Client`、`File Set`、`Storage`、`Pool` 和 `Schedule` 参数都是对 `bacula-dir.conf` 文件中定义资源的向前引用。

```
# FileSet
FileSet {
    Name = "harp"
Include {
    Options {
        signature=MD5
        compression=GZIP
    }
    File = "/"
    File = "/boot"
    File = "/usr"
    File = "/usr/local"
    File = "/var"
}
Exclude { /proc /tmp /journal .fksck }
}
```

## 9.8 Bacula

`FileSet` 资源定义了备份作业中要包含或排除的文件和目录。每个文件集可以定义多个 `Include` 和 `Exclude` 参数以及单独的 `Options`。默认情况下，Bacula 会递归备份目录，但不跨越分区。请注意在单独的 `File` 参数中列出你想要备份的所有分区。

支持许多额外的 `Options`，包括正则表达式和通配符。两个值得注意的选项是 `signature`（设置为 `SHA1` 或 `MD5`），它为每个被备份的文件计算哈希值，以及 `compression`，它在写入磁带之前对数据进行压缩。`signature` 选项会增加备份的 CPU 开销，但在怀疑发生事件时可能证明很有价值。

```
Schedule {
 Name = "Nightly"
 Run =Full=SSFullPool 1st-sue at 20:10
 Run =Incremental=SSIncrementalPool-mon at 20:10
}
```

`Schedule` 定义了备份作业的运行时间。自动备份作业需要 `Name` 参数和至少一个 `Run` 参数，但单个 `Schedule` 中可以包含多个参数。在这里，全量备份在每月第一个和第五个周二晚上 8:10 运行，增量备份在每周周三到周一晚上 8:10 运行。

日期和时间规范是 `Run` 参数的唯一强制部分，但正如此示例所示，你可以插入额外的参数值。这些值将覆盖 `Job` 规范中的默认参数集。在这里，我们设置了每个备份所使用的 `Level` 和介质池。

请参阅在线 Bacula 文档获取完整的日期/时间规范和关键字列表。

### Pool 定义 -- 第一个池是默认池

```
Pool {
 Name = SSFullPool
 Pool Type = Backup
 Recycle = yes
 Accept Any Volume = yes
}
```

```
Pool {
 Name = SSIncrementalPool
 Pool Type = Backup
 Recycle = yes
 Accept Any Volume = yes
}
```

`Pool` 资源将备份介质通常是磁带分组用于特定备份作业的集合。在本例中我们运行全量备份和每日增量，因此创建了两个 `Pool` 资源。两个非常有用的参数是 `Recycle` 和 `Accept Any Volume`。如果 `Recycle` 参数设置为 `yes`，Bacula 会自动清除标记的卷。`Accept Any Volume` 参数指定 Bacula 是否可以写入池中的任何卷。

```
Client {
  Name = harp
Address = 192.168.1
DIRport = 9101
Catalog = bull-dir
File Retention = 3 months
Job Retention = 6 months
AutoPrune = yes
}
```
`Client` 标识要备份的计算机。每个计算机都需要一个。`File Retention` 和 `Job Retention` 指定了文件和记录保留的时间。如果设置了 `AutoPrune`，过期数据将从目录中删除。

`Storage` 资源描述了如何与存储进程通信，它控制备份设备。在我们的示例中，我们有 LTO1。

```
Storage {
  Name = SureStore
Address = bull-dir
SDPort = 9101
Password = "Fru1tV3ggles"
Device = StorageDevice
Autochanger = yes
Media Type = LTO1
}
```
`Storage` 资源描述了如何与存储进程通信，它控制备份设备。在我们的示例中，我们有 LTO1。存储进程连接到调度器服务器。

## 9.8 Bacula

`Messages` 资源告诉 Bacula 如何处理每个进程生成的特定类型的消息。可以定义多个 `Messages` 资源并分配给特定的作业。

这种类型非常可配置；变量和命令列表可以在文档中找到。该配置将进程和作业的状态信息发送到控制台和标准文件，并通过电子邮件分发。

```
Messages {
Name = Standard
mailcommand = /etc/bacula/mail.sh -s "%t %c %k"
operatorcommand = /etc/bacula/operator.sh -h localhost -f "Bacula: Intervention needed for %j"
mail = bacula-pager@bacula.com = mount
console = all
operator = skipped
append = "/var/log/bacula.log" = all
}
```

存储进程配置文件必须包含一个 `Storage` 资源。这些资源相对简单。它们定义了一些基本参数，例如进程的网络端口和工作目录，并标识存储进程应该向哪个调度进程发送消息。

# 第 9 章 – 备份
