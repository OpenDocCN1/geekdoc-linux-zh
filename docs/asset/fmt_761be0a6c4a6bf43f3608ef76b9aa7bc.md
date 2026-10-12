
Select `Edit -> Add Device` from the menu. On the next screen, enter a `Hostname` or `IP Address` for each controller blade in the FASIT (Figure 5-7).

Enter a `Hostname` or `IP Address` you set on the FASTt and click `Add`. Repeat the process for the second controller blade.

![](img/69bfe4e2d59e61df50eecde9154775d5_78_0.png)

Figure 5-7 Add Device screen

Highlight `Storage Subsystem <unnamed>` and select `Tools -> Manage Device.`.

If there was no configuration previously on the storage, you should see a `Subsystem Management` screen similar to Figure 5-8.

![](img/69bfe4e4e2d59e61df50eecde9154775d5_78_1.png)

Figure 5-8 Subsystem Management window

### A.3 Updating the FASTT firmware

Obtain the latest firmware and NVRAM for the FASTT controller as described in A.2.1, “Install of the FASTT Storage client” on page 60. Unzip the file to a temporary folder:

`unzip *`

This extracts the firmware and NVRAM files for all of the current models of FASIT to the following folders:

```
../CONTROLLER CODE/FIRMWARE/<controller model>
../CONTROLLER CODE/NVRAM/<controller model>
```

Appendix A. Storage Manager and Linux 6

**Note:** You must first update the firmware and then the NVSRAM.

To update the controller firmware select `Storage Subsystem -> Download -> Firmware`. The screen shown in Figure 5-9 displays. Enter the location of the update file and click `OK` (Figure 5-9).

![](img/69bfe4e2d59e61df50eecde9154775d5_79_0.png)

Figure 5-9 Firmware Download Location screen

You now see a screen similar to Figure 5-9. This method will not find direct-attached storage controllers. Close this screen with the `Enterprise Management Window` (Figure 5-6).

![](img/69bfe4e2d59e61df50eecde9154775d5_77_0.png)

Figure 5-5 Automatic Discovery screen

![](img/69bfe4e2d59e61df50eecde9154775d5_77_1.png)

Figure 5-6 Storage Manager Enterprise Management window

现在，你必须指定逻辑驱动器参数。输入逻辑驱动器容量和名称。你还有以下选项：

- 使用推荐设置。

选择 `Customize`（自定义）并点击 `Next`（下一步）（图 5-16）。

![](img/69bfe4e2d59e61df50eecde9154775d5_83_0.png)

`图 5-16` 逻辑驱动器参数界面

你可以指定高级逻辑驱动器参数。你可以设置驱动器 I/O 特性、优先控制器所有权以及驱动器到 LUN 的映射。

根据你的环境进行任何更改。逻辑驱动器到 LUN 映射应保持为 `Map later with Storage Partitioning`（稍后通过存储分区映射）。点击 `Finish`（完成）（图 5-17）。

> **注意：** 请仔细考虑任何更改，因为它们可能会极大地影响你存储的性能。

![](img/69bfe4e2d59e61df50eecde9154775d5_84_0.png)

下一个屏幕（图 5-18）提示你 - 你是否想创建另一个逻辑驱动器 - 并为你提供以下选项：

- `Same array`（相同数组）

- `Different array`（不同数组）

在我们的情况下，我们选择 `Different array`（不同数组）来创建一个 `RAID5` 数组，然后选择 `Same array`（相同数组）在其中创建四个逻辑驱动器（图 5-19）。

![](img/69bfe4e2d59e61df50eecde9154775d5_84_1.png)

附录 A 存储管理器与 Linux 69

![](img/69bfe4e2d59e61df50eecde9154775d5_85_0.png)

参与存储分区的系统应当运行状态以便获取主机标识（`Host Identifiers`）。出于安全考虑，你不应使用 `Default`（默认），但你应该将其删除。

在子系统管理窗口中选择 `Mappings View`（映射视图）选项卡。这将显示映射启动帮助信息。阅读文本并关闭窗口（图 5-20）。

`图 5-19` 数组与逻辑驱动器

![](img/69bfe4e2d59e61df50eecde9154775d5_85_1.png)

创建存储分区共有四个主要步骤。通过高亮 `Default Group`（默认组）节点并在每个步骤中使用 `Mappings->Define`（映射->定义）菜单：

(1) 定义主机组（`Define host groups`）

仅当你有两个或多个将共享访问相同驱动器时，才定义主机组；否则，跳过并进入第 2 步。定义主机组后，高亮它，然后定义关联的主和主机端口。

(2) 定义主机（`Define hosts`）

为每个主机定义主机。

(3) 定义分区（`Define partitions`）

使用 `Storage Partitioning`（存储分区）选项定义存储分区。

更多详情请参考在线帮助中的“学习创建存储分区”（`Learn About Creating Storage Partitions`）。

`图 5-20` 映射启动帮助界面

为你的存储分区创建一个组。选择 `Mappings -> Host Group`（映射 -> 主机组）。输入名称并点击 `Add`（添加）（图 5-21）。

![](img/69bfe4e2d59e61df50eecde9154775d5_86_0.png)

高亮新的 `Host Group`（主机组）并选择 `Mappings -> Define -> Host`（映射 -> 定义 -> 主机）。输入主机名并点击 `Add`（添加）。对要组成组的每个系统重复此操作。我们正在设置一个高可用集群，其中组中有两个系统（图 5-22）。

![](img/69bfe4e2d59e61df50eecde9154775d5_86_1.png)

图 5-22 已添加主机

高亮新组中的第一个主机。`Mappings -> Define -> Host Port`（映射 -> 定义 -> 主机端口）选择 `Host Port Identifier`（主机端口标识符，早些在 `Fibre HBA BIOS` 设置中收集），它应与你系统中的字符匹配。选择 `Linux` 作为 `Host Type`（主机类型）（图 5-23）。

> **提示：** 如果 `Host Port Identifier` 下拉列表为空或缺失，请选择正确的项，否则选择 `Storage Manager` 并重启相关系统。

![](img/69bfe4e2d59e61df50eecde9154775d5_87_0.png)

图 5-23 系统中 `Fibre HBA` 的定义主机端口界面。对组中的每个系统重复此过程（图 5-24）。

![](img/69bfe4e2d59e61df50eecde9154775d5_87_1.png)

图 5-24 已添加主机端口
