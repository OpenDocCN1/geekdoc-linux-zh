
# 还有更多……

正如名称所示，本食谱中显示的`xfs_quota`程序仅适用于XFS文件系统。如果你想在`ext4`或`btrfs`等其他文件系统上使用用户或组级别的磁盘配额，你需要安装`quota`软件包（`yum install quota`）。设置配额的方法与本食谱中所示步骤类似；请阅读手册`man quota`以开始。

# 维护文件系统

在本食谱中，我们将学习如何检查并可选地修复CentOS 7文件系统的一致性。文件系统不一致是罕见事件，文件系统检查通常在启动时自动运行。但如果系统管理员认为文件系统存在问题，他们也知道如何手动运行此类测试。

### 准备工作

完成此食谱，你需要一个具有`root`权限的、运行良好的CentOS 7操作系统安装。我们将使用虚拟设备而不是真实的磁盘设备，因为我们无法在挂载的磁盘上执行任何文件系统检查。因此，你应该已经应用了“格式化和挂载文件系统”食谱，并创建了一个1兆字节的虚拟设备，带有两个各占总大小一半的分区：一个是XFS分区，另一个是ext4文件系统。在本示例中，我们将使用名为`/dev/loop0`的虚拟设备。

如前所述，这些可以轻松替换为真实的磁盘名称。

### 如何操作？

1.  首先，以`root`身份登录并显示连接到系统的当前块设备的信息：`lsblk -io NAME,TYPE,SIZE,MOUNTPOINT,FTYPE,MODEL`
2.  在这里，你应该能看到`loop0`设备上的两个分区：`dev/loop01`和`/dev/loop02`。如果你看到它们目前已挂载到系统，请现在卸载它们：`umount /dev/loop01`、`umount /dev/loop02`
3.  现在，让我们检查XFS文件系统，在我们的示例中是`loop01`（进行相应修改）：`xfs_repair -n /dev/loop01`
4.  对于第二个分区（即`ext4`），我们将使用以下行：`fsck /dev/loop02`

# 扩展文件系统容量

CentOS 7使用逻辑卷管理器(`LVM`)来组织分区的结构和可用容量。这是一个非常动态且灵活的系统，随着时间的推移可以扩展或重新调整，这对于当今最需求且不断变化的环境至关重要。

### 准备工作

完成此食谱，你需要一个具有`root`权限的、运行良好的CentOS 7操作系统安装。我们将使用虚拟块设备而不是真实设备，向你从零开始设置`LVM`，以及如何使用它。请阅读“创建虚拟块设备”食谱，并创建带有`GPT`分区表的3兆字节虚拟块设备，它们在示例中将标记为`/dev/loop0`、`/dev/loop1`和`/dev/loop2`。

### 如何操作...

首先，我们将开始创建一个与标准CentOS 7 `LVM`结构相似的`LVM`测试环境，该结构在每个服务器系统的安装过程中都会被设置：

1.  首先，以`root`身份登录并显示虚拟块设备的信息：
    `lsblk -io NAME, SIZE`
2.  接下来，在三个虚拟块设备上的每一个创建一个跨越整个磁盘的新分区（带有文件系统标签）：
    `parted -optimal /dev/loop0 mkpart primary 2048KiB 100%`
    `parted -optimal /dev/loop1 mkpart primary 2048KiB 100%`
    `parted -optimal /dev/loop2 mkpart primary 2048KiB 100%`
3.  接下来，在每个`loop`设备上创建`LVM`物理卷（输入`yes`以移除`gpt`标签）：
    `pvcreate /dev/loop0p1`
    `pvcreate /dev/loop1p1`
    `pvcreate /dev/loop2p1`
4.  接下来，显示物理物理卷的信息：
    `pvdisplay`
5.  接下来，我们将在第一个物理卷上创建一个新的`LVM`卷组：
    `vgcreate myVG1 /dev/loop0p1`
6.  现在，显示已创建卷组的信息：
    `vgdisplay myVG1`
7.  之后，我们在第一个卷组上创建一些逻辑卷，它们在我们的`Linux`系统中被视为虚拟分区：
    `lvcreate -L 10m -n swap myVG1`
    `lvcreate -L 100m -n home myVG1`
    `lvcreate -L 400m -n root myVG1`
8.  接下来，显示逻辑卷的信息：
    `lvdisplay myVG1`
9.  现在，显示底层卷组还剩多少可用空间，如果你想扩展某些逻辑卷，这将非常重要（请查看输出中的`Free PE / Size`部分）：
    `vgdisplay myVG1`
10. 之后，在这些新的本地卷上创建文件系统：

    ```
    mkswap /dev/myVG1/swap
    mkfs.xfs /dev/myVG1/home
    mkfs.xfs /dev/myVG1/root
    ```

11. 现在，在我们已经创建了测试`LVM`系统（这与真实的CentOS `LVM`标准布局非常相似，只是尺寸较小），让我们开始使用它。

12. 首先，将当前大小为400兆字节(`M`)的根分区缩小200兆字节，之后将`home`分区增加500兆字节（确认可能的数据丢失）：

    ```
    lresize -L -200m /dev/myVG1/root
    lresize -L +500m /dev/myVG1/home
    ```

13. 使用`vgdisplay myVG`运行之前的命令来查看卷组可用空间的变化（参见`PE / Size`）。

14. 现在，让我们扩展新逻辑卷上的`XFS`文件系统：

    ```
    mkdir /media/home-test
    mount /dev/myVG1/home /media/home-test
    xfs_growfs /dev/myVG1/home
    ```

    > 不要使用`resize2fs`来扩展`XFS`文件系统，这非常重要，因为它们不兼容并且可能会损坏它们。

15. 现在，假设你的数据再次增长，你需要`home`分区达到1.5兆字节(`G`)，但底层卷组仅剩`184.00 MiB`。首先，我们需要从该卷组开始添加之前准备的两个物理卷：

    ```
    vgextend myVG1 /dev/loop1 /dev/loop2
    vgdisplay myVG1
    ```

16. 之后，我们在卷组中有了足够的可用空间（参见`PE / Size`）来扩展`home`逻辑卷（该卷必须保持挂载状态）：

    ```
    lresize -L +1500m /dev/myVG1/home
    xfs_growfs /dev/myVG1/home
    ```
