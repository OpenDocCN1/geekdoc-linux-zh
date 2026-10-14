
```bash
[root@nf350a ~root]$ ipssend getstatus 1
```

Found 1 IBM ServeRAID Controller(s)

Background Command Status for controller 1...

Current/Most Operation: Rebuild

Logical Drive in Progress: 2

Rebuild Rate: High

Status: Successfully Completed

Logical Drive Size (in Stripes): 128000

Number of Remaining Stripes: 0

Percentage Completes: 100.00%

图 77. 执行 `ipssend getstatus 1`

如果 ServeRAID 控制器正在重建驱动器，你将看到类似于图 78 的输出。

```bash
[root@nf350a ~root]$ ipssend getstatus 1
```

Found 1 IBM ServeRAID Controller(s)

Background Command Status for controller 1...

Current/Most Operation: Rebuild

Logical Drive in Progress: 1

Rebuild Rate: High

Status: In Progress

Logical Drive Size (in Stripes): 128000

Number of Remaining Stripes: 126473

Percentage Completes: 19%

图 78. 在重建驱动器期间执行 `ipssend getstatus 1`

## 2.5.3.3 devinfo 命令

此命令用于检索 IBM ServeRAID 控制器下设备的当前状态。`devinfo` 命令具有以下语法：

```bash
ipssend devinfo <Controller> <Channel> <SCSI ID>
```

表 2. `devinfo` 命令

| 参数 | 说明 |
| :--- | :--- |
| `Controller` | 控制器数量 (1 到 12) |
| `Channel` | 设备的通道 (1 到 3) |
| `SCSI ID` | 设备的 SCSI ID (0 到 15) |

要获取 IBM Netfinity 服务器上通道 1 上 SCSI ID 为 1 的设备的状态，请执行以下命令：

```bash
ipssend devinfo 1 1
```

你将看到类似于图 79 的输出。

```bash
@root@nf350a:/root# ipssend devinfo 1 1
```

Found 1 IBM ServeRAID Controller(s):

Device Information has been initiated for controller 1

Device is a 16 bit, Fast SCSI, tag queuing Hard Disk

Channel : 1

SCSI ID : 1

FFA (Yes/No) : No

State : Online (ONL)

Size (in MB)/(in Sectors) : 8678/1777388

Device ID : IBM-P80 ST39175L0430AL09YSS

Command Completed Successfully.

图 79. 执行 `ipssend devinfo 1 1`

如果 ServeRAID 正在重建驱动器，你将看到类似于图 80 的输出。

```bash
@root@nf350a:/root# ipssend devinfo 1 2
```

Found 1 IBM ServeRAID Controller(s):

Device Information has been initiated for controller 1

Device is a 16 bit, Fast SCSI, tag queuing Hard Disk

Channel : 1

SCSI ID : 2

FFA (Yes/No) : No

State : Rebuild (RBL)

Size (in MB)/(in Sectors) : 8678/1777388

Device ID : IBM-P80 ST39175L0430AL0A2K

Command Completed Successfully.

xSeries 和 Netfinity SuSE Linux 集成指南

```bash
[root@nf350a ~root]# ipssend devinfo 1 2
```

Found 1 IBM ServeRAID Controller(s)

Device Information has been initiated for controller 1

Device is a 16 bit, Fast SCSI, tag queuing Hard Disk

Channel : 1

SCSI ID : 2

FFA (Yes/No) : No

State : Rebuild

Size (in MB)/(in Sectors) : 8678/1777388

Device ID : IBM-P80 ST39175L0430AL02QK

Command Process Successfully.

图 80. 在重建驱动器期间执行 `devinfo 1 2`

## 2.5.3.4 hrebuild 命令

此命令用于设置热备重建（Hot Swap Rebuild）的状态。`hrebuild` 命令具有以下语法：

```bash
ipssend hrebuild <Controller> <Options>
```

表 3. `hrebuild` 命令参数

| 参数 | 说明 |
| :--- | :--- |
| `Controller` | 控制器编号 (1 到 12) |
| `Options` | ON: 启用热备重建 |
| `?` | 显示热备重建功能的状态 |

你可以通过此命令检索或设置热备重建功能。如果热备重建功能为 ON，则意味着如果 RAID 数组中的一个驱动器故障，当你用新驱动器替换故障驱动器时，该驱动器的重建会自动开始。这可以提高数据的安全性。注意 热备重建功能不应与热备驱动器（hot spare drive）混淆。热备驱动器意味着只要 RAID 数组处于正常状态，驱动器处于等待状态。一旦 RAID 数组变为关键状态，热备驱动器将启用，数据会自动重建到热备驱动器上，而无视热备重建设置。

要检索第一个 ServeRAID 控制器的热备重建状态，请执行此命令：

```bash
ipssend hrebuild 1 ?
```

你将看到类似于图 81 的输出。

```bash
[root@nf350a ~root]# ipssend hrebuild 1 ?
```

Found 1 IBM ServeRAID Controller(s)

Set Hot Swap Rebuild has been initiated for controller 1...

Hot Swap Rebuild is On for controller 1.

图 81. 执行 `ipssend hrebuild 1 ?`

要启用热备重建，请执行此命令：

```bash
ipssend hrebuild 1 on
```

你将看到类似于图 82 的输出。

```bash
[root@nf350a ~root]# ipssend hrebuild 1 on
```

Found 1 IBM ServeRAID Controller(s)

Set Hot Swap Rebuild has been initiated for controller 1...

Hot Swap Rebuild is already On for controller 1.

图 82. 执行 `ipssend hrebuild 1 on`

## 2.5.3.5 setstate 命令

通过 `setstate` 命令可以将物理设备的当前状态重新定义为指定状态。`setstate` 命令具有以下语法：

```bash
ipssend setstate <Controller> <Channel> <SCSI ID> <New State>
```

参数见表 4。

# 表 4. setstate 命令参数

| 参数 | 描述 |
| --- | --- |
| `Controller` | 控制器数量 (1 to 12) |
| `Channel` | 设备通道 (1 to 3) |
| `SCSI ID` | 设备 SCSI ID (0 to 15) |
