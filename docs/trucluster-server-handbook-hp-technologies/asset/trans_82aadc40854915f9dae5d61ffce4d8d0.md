

除了这些场景之外，我们还必须认识到，自 Tru64 UNIX 版本 5.0 起，已引入了一个全新的 LSM 版本，其中除了其他内容外，还更改了磁盘上的元数据以及日志记录的方式。由于这些差异，从运行 Tru64 UNIX 5.0 之前的系统导入磁盘组的方式必须与从运行 Tru64 UNIX 5.0 或更新版本系统导入磁盘组的方式不同。

导入磁盘组使用 voldg(8) 命令。这与你在独立系统上使用的命令相同。表 14-7 显示了根据我们将要导入的磁盘组的来源而基于的额外 voldg 命令选项。

除 rootdg 之外的任何磁盘组都可以被导出和导入。虽然你不能导出 rootdg，但我们将向你展示如何从另一系统导入 rootdg。

## LSM 迁移命令

| 命令 | 位置 | 手册 | 类型 | 描述 |
|---|---|---|---|---|
| volencap | /usr/sbin | 8 | binary | 对单个系统或集群上的磁盘、磁盘分区或 AdvFS 域，或一个或多个集群成员的交换设备进行封装。 |
| vollogcnvt | /usr/sbin | 8 | sh | 用于从 V5 之前的块更改日志记录 BCL 转换为脏区域日志记录 DRL 的实用程序。 |
| volmigrate | /usr/sbin | 8 | ksh | 将 AdvFS 域存储从物理存储移动到 LSM 卷（volmigrate）或从 LSM 卷移动到物理存储（volummigrate）。 |
| volreconfig | /sbin | 8 | sh | 与 volencap 命令一起使用以完成封装过程。 |
| volummigrate | /usr/sbin | 8 | symlink | 请参阅 volmigrate。 |

### 表 14-6：LSM 迁移命令

### voldg import 命令选项

| from | to | option(s) |
|---|---|---|
| Tru64 UNIX 版本 5.0 或更新 | TruCluster Server | -o shared |
| Digital UNIX 版本 3.2 - 4.0E<br>Tru64 UNIX 版本 4.0F - 4.0G | TruCluster Server | -o convert_old -o shared |
| TruCluster Server | Tru64 UNIX 版本 5.0 或更新 | -o private |
| TruCluster Server | Digital UNIX 版本 3.2 - 4.0E<br>Tru64 UNIX 版本 4.0D - 4.0G | unsupported* |

* = 有一种情况可以做到，请参阅第 14.5.2.2 节

### 表 14-7：voldg(8) 命令导入选项

## 14.6.1 从独立系统导入磁盘组到集群

### 14.6.1.1 来自 Tru64 UNIX 版本 5.0 或更新版本

要从独立系统导入磁盘组到集群，请使用以下流程：

- 1. 从独立系统上的 LSM 导出磁盘组。

```
# volume -g mydg stopall
```

```
# voldg deport mydg
```

- 2. 从独立系统断开存储连接。

- 3. 将存储连接到集群。

- 4. 扫描每个集群成员的 SCSI 总线。

```
[heridan]
# hwmgr -scan scsi -bus 3
```

```
[heridan]
# hwmgr -scan scsi -bus 3 -member molazl
```

- 5. 创建设备特殊文件（如果必要）。

```
# dsfmgr -K
```

- 6. 确定新的设备名称。

```
# hwmgr -show scsi -bus 3
```

- 7. 重建 LSM 卷设备节点。

```
# voldctl enable
```

- 8. 导入磁盘组。

- 如果磁盘组不是 rootdg（注意：如果磁盘组中并非每个磁盘都可用，则可能还需要“-f”开关）：

```
# voldg -o shared -c import mydg
```

- 如果磁盘组在原始系统上是 rootdg，则你需要重命名磁盘组，因为集群已有一个 rootdg。

在导入根磁盘组之前，你必须确定独立系统的 rootdg 的磁盘组标识符（DGID）。

```
# voldisk list dsk10 | grep group
group: name=rootdg id=999905375.1022.delemn
```

使用新的磁盘组名称导入磁盘组。我们将使用“mydg”。

```
# voldg -o shared -n mydg -c import id=999905375.1022.delemn
```

- 9. 在后台恢复磁盘组的卷。

```
# volrecover -ab -g mydg
```

### 14.6.1.2 来自 Tru64 UNIX 5.0 之前的版本

- 1. 保存 LSM 配置。

虽然保存 LSM 配置始终是一个好主意，但如果要将磁盘组从运行 Digital UNIX 版本 3.2 至 4.0E，或 Tru64 UNIX 版本 4.0F 至 4.0G 的系统移动，则尤其重要，因为你可能需要将其移回。一旦磁盘组导入到运行 Tru64 UNIX 版本 5.0 或更新版本的系统上的 LSM，元数据将被转换为新格式，不再与旧格式兼容。只要你备份了旧格式，并且没有进行后续的元数据更改（例如分离或移动数据复本），就可以将元数据恢复到旧的、V5 之前的格式。

```
# volsave -d /MyLSMbackupDirectory
```

