
| Delete | 从待提取列表中移除文件或目录。如果指定了目录，该目录下的所有文件、子目录以及子目录中的文件也将从列表中移除。注意，这不会影响 dump 归包中的存储内容，而是影响恢复期间提取哪些文件。 |

| Extract | 提取当前待提取列表中的所有文件和目录，并在文件系统中恢复它们。 |

| help | 列出可用命令。 |

# 第四部分 红帽 Linux 系统维护

## 表 22-4 restore 命令（续）

| 命令 | 含义 |
| :--- | :--- |
| ls | 列出 dump 归包中当前查看目录的内容。如果指定了目录，则列出该指定目录的内容而非当前目录的内容。文件列表中标记为 * 的文件和目录当前被标记为待提取。 |
| pwd | 打印 dump 归包中当前查看目录的路径。 |
| quit | 退出恢复程序。restore 不执行其他操作。 |
| setmodes | 不是提取文件，而是设置系统上文件的权限，使其与 dump 归包中标记为待提取的文件权限匹配。 |
| verbose | 切换详细模式的开启或关闭。 |

## 使用 TAR

Red Linux 包含了 GNU 版本的 tar。它包含了对旧版标准版本的某些扩展。它包含了一些用于多卷备份的扩展。使用 AMANDA，你可以配置红 Linux 机器作为备份服务器。当归包空间不足时，tar 会提示插入新的介质。AMANDA 是一套用于备份的工具，需要指定命令。表 22-5 列出了这些选项。

### 表 22-5 TAR 选项

| 命令 | 含义 |
| :--- | :--- |
| A | 在 dump 归包中的文件。 |
| D | 要进行比较的文件系统。 |
| R | 从特定磁带开始恢复。 |
| T | 列出 dump 归包的内容。 |
| U | 早于 dump 归包中的文件。 |
| X | 从 dump 归包中提取文件。 |

# 第 22 章：文件系统的备份与恢复

| 命令 | 含义 |
| :--- | :--- |
| A | 在 dump 归包中的文件。 |
| D | 创建新的归归包。 |
| R | 在此指定命令外，你还需要指定设备或文件。 |

# 高级工具

本节讨论了 AMANDA、`pax` 和 `taper` 等高级工具。

## 使用 AMANDA

AMANDA（高级网络存档）软件包是一套用于机器备份的工具。要使用 Amanda，你需要安装以下软件包：

- Amanda
- Amanda-client
- Amanda-server
- Gnuplot

你需要在作为备份服务器的机器上安装 `Amanda-server` 和 `gnuplot`。然而，在任何需要备份的机器上必须安装 `Amanda-client`。Amanda 包含了多个命令，见表 22-6。

### 表 22-6 AMANDA 命令

| 命令 | 用途 |
| :--- | :--- |
| Amdump 通常由 cron 作执行，在 Amanda 服务器上运行。它请求客户端进行备份。 |
| Amflush 如果 amdump 写入磁带时遇到困难，备份将保存在磁盘的临时空间中。问题解决后，运行此命令将临时空间中的数据写入磁带。 |
| Amcleanan 如果 Amanda 服务器在运行 amdump 时崩溃，应运行此工具清理中断的 amdump。 |
| Amrecover 提供了一种选择使用哪些磁带恢复文件的方法。 |
| Amrestore 用于从 Amanda 备份中恢复单个文件或目录或整个分区。 |
| Alabel 向磁带写入 Amanda 标签。在使用 amdump 写入之前，必须使用此命令对磁带进行标记。 |
| Amcheck 在运行 amdump 之前应运行此工具，以验证磁带是否正确。 |
| Amadmin 执行各种管理任务。 |
| Amtape 用于底层磁带控制，如加载和卸载磁盘。 |
| Amverify 检查 Amanda 磁带是否有错误。 |
| Amrmtape 从 Amanda 数据库中删除特定标签的磁带。 |
| Amstatus 报告运行中的 amdump 程序的当前状态。 |

安装 AMANDA 在安装必要的 RPM 后，还需要额外的安装才能让 Amanda 运行。你必须为运行的每个备份计划在 `/etc/Amanda` 和 `/usr/admn/Amanda` 目录中创建子目录。例如，如果你计划运行名为 test 的备份计划，你必须执行以下命令：

# 第 22 章：文件系统的备份与恢复

你还需要为 Amanda 创建一些临时空间，用于存放它正在进行备份的文件。例如，如果你想在根分区上创建一个目录来此此空间，可以使用以下命令创建一个 Amanda 目录：

```
mkdir /Amanda
```

### 配置 AMANDA

要配置 Amanda，你必须创建一个 `Amanda.conf` 文件，并将其放在你创建的 `/etc/amanda` 子目录下。例如，在示例中，它的路径将是 `/etc/amanda/Amanda.conf`。`Amanda.conf` 文件有许多选项，如表 22-7 所示，但大多数选项都有默认值。

#### 表 22-7 AMANDA.CONF 选项

| 选项 | 示例 | 含义 |
| --- | --- | --- |
| org "name" | org "Tristero" | 此选项指定 Amanda 生成的报告中使用的名称。 |
| mailto "accounts" | mailto "root@example" | 此选项指定了 Amanda 应该负责备份过程的账户名。 |
| dumpuser "account" | dumpuser "Amanda" | 此选项指定了 Amanda dump 进程运行时使用的用户账户。 |
| inparallel number | inparallel 5 | 此项指定了可以同时运行的 dump 进程数量。 |
| netusage num unit | netusage 1000 Kbps | 此项指示了 Amanda 在备份时允许消耗的带宽。其设置应确保即使消耗了所有分配的带宽，仍足够的带宽供与 Amanda 备份进程同时运行的其他任务使用。 |

#### 表 22-7 AMANDA.CONF 选项（续）

| 选项 | 示例 | 含义 |
| --- | --- | --- |
| dumpcycle num unit | dumpcycle 1 week | 此选项指定了备份周期的长度。 |
| runcycle num | runcycle 7 | 此选项指定了在一个备份周期内应该执行的备份次数。因此，备份周期为 1 周且运行 7 次意味着每周进行一次完整备份，Amanda 每周会进行 6 次增量备份。 |
| tapespercycle num unit | tapespercycle 7 tapes | 此选项指定了在一个备份周期内可用的磁带数量。 |
| runtapes num | runtapes 1 | 此选项指定了每次备份中可用的磁带数量。 |
| tapedev "device" | tapedev /dev/rft0 | 此选项指定了磁带设备的设备名称。 |

`Amanda.conf` 文件还包含一些复杂的选项，它们由包含多个子字段的块组成。`holdingdisk` 块定义了存放正在备份数据的临时存储空间。你可以在一个文件中定义多个 `holdingdisk` 块。定义格式如下：

```
holdingdisk name
{
  directory "name"
  use num unit
}
```

示例 `holdingdisk` 块：

```
{
  directory "/example"
  use 4 Gb
}
```

`tapetype` 块定义了备份中可能使用的特定类型的磁带。它定义了磁带的属性，如长度和速度。`tapetype` 定义格式如下：

```
Define tapetype name
{
  comment "freeform string"
  length num unit
  filemark num unit
  speed num unit
}
```

示例 `tapetype` 定义：

```
Define tapetype EXAMPLE
{
  comment "These are fictional numbers."
  length 5000 mbytes
  filemark 100 kbytes
  speed 500 kbytes
}
```

`interface` 块定义了可用于 Amanda 服务器与客户端之间通信的特定网络接口。`interface` 定义指定了在该网络接口上可以使用多少带宽。该定义的语法如下：

```
Define interface name
{
  comment "Freeform string"
  use num unit
}
```

示例 `interface eth0`：
