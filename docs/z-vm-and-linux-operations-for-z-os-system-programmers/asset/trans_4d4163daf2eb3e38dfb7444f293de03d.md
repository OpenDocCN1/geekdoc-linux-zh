

### 示例 4-12 Linux 客户机 LNXCER 的引导参数文件

```
ramdisk_size=65536 root=/dev/ram0 ro init=/linuxrc TERM=dumb
hostip=<9.12.5.65> hostname=<ceron>
gateway=<9.12.4.1> netmask=<255.255.254.0>
broadcast=<9.12.7.255> layer2=0
readchannel=0.0.0600 writechannel=0.0.0601 datachannel=0.0.0602
nameserver=<9.12.6.7> portname=dontcare
install=<ftp://totibim:itso@9.12.4.69/code/sles10x>
instnetdev=osa osainterface=qdio osamedium=eth Manual=0
usessh=1 sshpassword=letmein
```

请确保将 \<value\> 条目替换为根据附录 B “规划工作表”第 403 页上的规划工作表与你的资源相对应的值。另外，请不要忘记用粗体突出显示的最后一行，因为在本书中我们指导你执行 SLES10 的 SSH 安装。

## 为 Linux 虚拟机设置通用配置文件

要使所有 Linux 客户机都能看到你为 LNXMAINT 创建的 192 磁盘，其中包含引导的全部通用文件，你有两个选择：

- 费力的方法是在 MAINT 的 USER DIRECT 文件中为每个用户描述添加一个 LINK 语句。

- 更简单的方法是基于默认配置文件创建一个配置文件并添加链接语句的正确行。然后，要使用它们，在创建 Linux 客户机用户时，只需导入此新配置文件即可。

我们的示例当然基于第二种方法。

要使用更简单的方法使所有 Linux 客户机生效：

- 1. 登录到 MAINT 并编辑 USER DIRECT 文件：

    ```
    ==> x user direct c
    ```

在 USER DIRECT 文件中，你可以将对许多用户定义通用的语句分组到一个称为配置文件的结构中。然后可以通过使用 INCLUDE 语句使该配置文件成为用户定义的一部分。你在定义 LNXMAINT 用户时使用了现有的配置文件 TCPCMSU。

- 2. 创建一个名为 LNXDFLT 的新配置文件。它将包含对所有 Linux 用户 ID 通用的用户目录语句。为了减少输入，使用 “*” 前缀命令复制应在第 37-50 行的 IBMDFLT 配置文件：

    ```
    00037 **************************************************
    00038 *
    00039 PROFILE IBMDFLT
    00040  SPOOL 000C 2540 READER *
    00041  SPOOL 000D 2540 PUNCH A
    00042  SPOOL 000E 1403 A
    00043  CONSOLE 009 3215 T
    00044  LINK MAINT 0190 0190 RR
    00045  LINK MAINT 019D 019D RR
    00046  LINK MAINT 019E 019E RR
    00047  LINK MAINT 0402 0402 RR
    00048  LINK MAINT 0401 0401 RR
    00049  LINK MAINT 0405 0405 RR
    00050 *******************************
    ```

- 3. 通过删除三个 LINK MAINT 040x 行并插入示例 4-13 中用粗体文本显示的行来编辑复制的配置文件。参见示例后的说明。

### 示例 4-13 配置文件 LNXDFLT

```
PROFILE LNXDFLT
IPL CMS
MACHINE ESA 4
CPU 00 BASE
CPU 01
NICDEF 600 TYPE QDIO LAN SYSTEM VSW1
SPOOL 000C 2540 READER *
SPOOL 000D 2540 PUNCH A
SPOOL 000E 1403 A
CONSOLE 009 3215 T
LINK MAINT 0190 0190 RR
LINK MAINT 019D 019D RR
LINK MAINT 019E 019E RR
LINK LNXMAINT 192 191 RR
LINK TCPMAINT 592 592 RR
```

示例说明：

- 1 用户 ID 登录时 IPL CMS。
- 2 将机器标识为类型 ESA，最多可定义 4 个 CPU。
- 3 定义基本 CPU。
- 4 定义第二个 CPU；如果你的 LPAR 只有一个 Real IFL/CP，则不要包含此项。
- 5 定义一个连接到从虚拟地址 600 开始的 VSWITCH 的虚拟 NIC。
- 6 提供对 LNXMAINT 192 磁盘的读取访问，作为用户的 191 磁盘。
- 7 提供对 TCPMAINT 592 磁盘的读取访问，以便用户可以访问 TCPIP 服务，例如 FTP 客户端。

- 4. 保存文件：

    ```
    ====> file
    ```

## 创建第一个 Linux VM

在第 2.2.1 节“z/VM 历史”第 14 页的虚拟化讨论中，要创建 Linux 可以运行的虚拟机，你所要做的就是创建一个 z/VM 用户。首先要做的是设置用户最小磁盘。

### 设置最小磁盘

为你的 Linux 客户机创建一个新用户，并以与“为 LNXMAINT 设置最小磁盘空间”第 183 页中为 LNXMAINT 用户所做的方式完全相同的方式设置其最小磁盘。以 MAINT 身份登录并在 USER DIRECT C 文件中添加新的用户定义。这是你要包含在“为 Linux 虚拟机设置通用配置文件”第 193 页中创建的 LNXDFLT 配置文件的第一个用户。示例 4-14 显示了你可以使用的模板。

### 示例 4-14 创建 Linux 客户机用户。

```
user <lnxcer> <lnxcer> 512M 2G BDEG
include lnxdflt
option lnknopas applmon
mdisk 100 3390 0001 3338 <nwla25> mr lnx4vm lnx4vm lnx4vm
mdisk 103 3390 0001 3338 <nwla26> mr lnx4vm lnx4vm lnx4vm
mdisk 104 3390 0001 3338 <nwla27> mr lnx4vm lnx4vm lnx4vm
mdisk 105 3390 0001 3338 <nwla28> mr lnx4vm lnx4vm lnx4vm
mdisk 106 3390 0001 3338 <nwla29> mr lnx4vm lnx4vm lnx4vm
```

该示例将此 Linux 用户 ID 定义为具有以下最小磁盘和虚拟磁盘：

- 100 用于保存 /boot 分区的最小磁盘；剩余空间分配给系统 LVM，所有其他分区都将位于其中。有关 Linux LVM 的更多信息，请参阅第 307 页的“Linux 逻辑卷管理器”。
- 101-102 这些是由 SWAPGEN EXEC 在登录时创建的虚拟磁盘（VDISK）交换空间。它们未在 USER DIRECT 中定义，而是在用户登录时在用户的 PROFILE EXEC 中动态定义。
- 103-106 这些最小磁盘将由 Linux 系统 LVM 管理。

