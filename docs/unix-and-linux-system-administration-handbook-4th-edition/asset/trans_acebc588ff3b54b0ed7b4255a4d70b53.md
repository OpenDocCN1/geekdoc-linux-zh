

## 池资源

池资源将备份介质，通常是磁带，归组为集合，供特定的备份作业使用。将用于异地归档存储的磁带与用于夜间增量的磁带分开可能很有用。每块介质都被分配给单个池，因此可以轻松地自动回收某些磁带并归档其他磁带。

```
Pool {
    Name = Full_Pool
    Pool Type = Backup
    Recycle = yes
    AutoPrune = yes
    Storage = T1 4000
    Volume Retention = 365 days
}
```

## 调度资源

调度资源定义备份作业的时间表。名称、日期和时间规范是唯一必需的参数，但正如下面示例所示，你可以偷偷加入额外的参数值。这些值随后会覆盖作业规范中设置的默认参数。

下面，完整备份在每月第一个星期二晚上 8:10 运行。增量备份使用不同的磁带池，并在每周三至周一晚上 8:10 运行。

```
Schedule {
    Name = "Nightly"
    Run = Level=Full Pool=Full_Pool 1st tue at 20:10
    Run = Level=Incremental Pool=Incremental_Pool wed-mon at 20:10
}
```

## 客户端资源

客户端资源标识要备份的计算机。每个资源都有唯一的名称、IP地址和密码；每个客户端都需要一个。用于存储备份元数据的目录也指定了。File Retention 和 Job Retention 参数指定在此客户端的文件和作业记录应在目录中保留多长时间。如果设置了 AutoPrune 参数，已过期的數據将从目录中删除。修剪仅影响目录记录，而不影响存储在备份磁带上的实际文件；磁带的回收在池资源中配置。

```
Client {
    Name = harp
    Address = 192.168.1.28
    FDPort = 9102
    Catalog = MYSQL
    Password = "TbEpJqrcy"
}
```

## 文件集资源

FileSet 资源定义要包含在备份作业中或从备份作业中排除的文件和目录。除非你的系统具有相同的分区方案，否则你可能需要为每个客户端准备不同的文件集。FileSet 资源可以定义多个 Include 和 Exclude 参数，以及诸如正则表达式之类的单个选项。默认情况下，Bacula 会递归备份目录但不会跨分区，因此请注意在单独的 File 参数中列出你想要备份的所有分区。

在下面的示例中，我们启用了软件压缩以及签名选项，该选项为每个备份的文件计算哈希值。这些选项会增加备份的 CPU 开销，但可以节省磁带容量或帮助识别在疑似安全事件期间被修改的文件。

```
FileSet {
  Name = "harp"
  Include {
    Options {
      signature=SHA1
      compression=GZIP
    }
    File = "/"
    File = "/boot"
    File = "/var"
  }
  Exclude = { /proc /tmp /journal /fsck }
}
```

## 作业资源

作业资源通过将客户端、文件集、存储、池和调度资源联系起来，定义特定备份作业的整体特征。通常，每个客户端有一个作业定义，尽管如果你想以不同的频率备份不同的文件集，可以轻松设置多个作业。

你可以提供一个可选的 JobDefs 资源来为所有备份作业设置默认值。使用此资源可以简化每个作业的配置数据。

```
Job {
  Name = "Harp"
  JobDefs = DefaultJob
  Level = Full
  Write Bootstrap = "/bacula/bootstraps/harp.bsr"
  Client = harp
  FileSet = harp
  Pool = Full_Pool
  Incremental Backup Pool = Incremental_Pool
  Schedule = "Nightly"
  Prefer Mounted Volumes = no
  Max Run Time = 36000
}
```

“引导”文件是由 Bacula 创建的特殊文本文件，其中包含有关要恢复的文件的信息。引导文件列出了恢复作业所需的文件和卷，对于裸机恢复非常有帮助。它们不是强制性的，但强烈推荐。

引导文件是在恢复期间创建的，或在备份期间创建，如果你为作业定义了 Write Bootstrap 参数。Write Bootstrap 告诉 Bacula 将引导信息保存到何处。引导文件在完整备份期间被覆盖，并在增量备份期间追加。

## bacula-sd.conf：存储守护进程配置

存储守护进程从文件守护进程接收数据并将其传输到实际的存储介质，或反之亦然，在恢复的情况下。资源 Storage、Device 和 Autochanger 在 bacula-sd.conf 文件中定义，以及通用的 Messages 和 Director 资源。

### Director 资源

Director 资源控制哪些调度器被允许联系存储守护进程。bacula-dir.conf 的 Storage 资源中的密码必须与 bacula-sd.conf 的 Director 资源中的密码匹配。

```
Director {
  Name = bull-dir
  Password = "jIKkrZuE00"
}
```

### Storage 资源

Storage 资源相对简单。它定义了一些基本的工作参数，例如守护进程的网络端口和工作目录。

```
Storage {
  Name = bull-sd
  SDPort = 9103
  WorkingDirectory = "/var/bacula/working"
  Pid Directory = "/var/run"
  Maximum Concurrent Jobs = 2
}
```

### 设备资源

每个存储设备都有自己的设备资源定义。此资源指定有关物理备份硬件的详细信息，无论是磁带、光学介质还是在线存储。详细信息包括介质类型、功能以及由磁带更换机或媒体机器人管理的设备的自动更换机信息。

下面的示例定义了一个带自动磁带更换机的 LTO-3 驱动器。请注意 /dev/nst0 是一个非倒带设备，这几乎总是你想要的。Name 参数定义了一个符号名称，用于关联该

