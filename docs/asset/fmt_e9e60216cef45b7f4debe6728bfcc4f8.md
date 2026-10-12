
如本节早期所述，某些应用程序和服务仅需要单向通信。正如前面提到的，记住你可能需要同时创建输入和输出规则很重要。

正如前面，输入：`sudo iptables -I INPUT 1 -s 192.168.0.100 -j ACCEPT` 插入一条规则，输入：`sudo iptables -I INPUT 1 -s 192.168.0.100 -j ACCEPT`

替换一条规则，输入：`sudo iptables -R INPUT 1 -s 192.168.0.100 -j ACCEPT`

**注意：** 在远程操作此服务时，请小心，因为你可能会在玩弄此功能时把自己锁定在远程系统之外。一旦你把自己锁在外，你需要获得对系统的某种终端访问权限来修复问题。

### Linux 存储层级

Linux 了一了一套强大的工具来管理存储设备。本节提供了这些命令的高级概述，以及存储如何被文件系统使用的摘要。

- 第 4 层：文件和目录
- 第 3 层：文件系统（例如 EXT4 等）
- 第 2 层：分区（例如 MBR 或 GPT）[可选：抽象子层，如 RAID、LUN 等]
- 第 1 层：存储（物理或虚拟）
- 第 0 层：基础设施（例如硬件、虚拟机、云、等）

第一个核心概念是“块存储”，或在内核中被称为“块设备”。块设备可以是传统的旋转硬盘（HDD），也可以是固态存储设备如 SSD 或 USB 闪存驱动。内核以固定大小的存储单元（块）在这些设备上存储和检索数据。这只是对连接到计算机的传统存储的一种另一种思考方式。当文件系统进行分区时，它会将可用存储分成较小的单元。假设你有一个 1TB 的存储设备。与其将所有内容都放在 1TB 驱动器中，不如将本地存储分成两个 512GB 分区，并让它们在文件系统中看起来像两个不同的磁盘。这允许你从逻辑上分离数据。

### 防火墙规则导出导入

导出防火墙规则，类型：`iptables-save`

导入防火墙规则，类型：`iptables-restore`

**注意：** IPv6 的等效命令是 `ip6tables-save` 和 `ip6tables-restore`。

当你完成对防火墙的操作后，使用 6 导出。**提示：** 为了清空防火墙，可以使用：`iptables -F`

某些工具可以让防火墙的管理更简单。`ufw` 允许 `22`。`ufw` 提供了防火墙的某些功能。例如，`ufw` 允许。

检查防火墙状态，类型：`ufw status`

启用/禁用防火墙，类型：`ufw enable`

包含以下标志的数据包（圣诞树攻击），类型：`sudo iptables -A INPUT -p tcp -m tcp --tcp-flags ALL,PSH,URG -j DROP`

包含以下标志的数据包（SYN 和 FIN 攻击），类型：`sudo iptables -A INPUT -p tcp -m tcp --tcp-flags SYN,FIN -j DROP`

禁用防火墙，类型：`ufw disable`

删除防火墙，类型：`ufw delete`

允许防火墙，类型：`ufw allow`

拒绝防火墙，类型：`ufw deny`

限制防火墙，类型：`ufw limit`

启用防火墙，类型：`ufw enable`

禁用防火墙，类型：`ufw disable`

重置防火墙，类型：`ufw reset`

查看防火墙状态，类型：`ufw status`

查看防火墙状态，类型：`ufw status numbered`

允许特定规则，类型：`ufw allow ...`

拒绝特定规则，类型：`ufw deny ...`

允许特定端口，类型：`ufw allow port`

允许服务，类型：`ufw allow`

删除特定规则，类型：`ufw delete ...`

删除特定端口，类型：`ufw delete port`

允许特定 IP，类型：`ufw allow from ...`
