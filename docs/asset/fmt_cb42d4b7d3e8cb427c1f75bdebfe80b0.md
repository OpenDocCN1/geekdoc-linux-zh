
```
umount: /mnt/smbtest: device busy
```

- 覆盖共享上的文件会报输入/输出错误，即使权限设置正确。使用 `cp` 复制文件时：

```
cp: cannot create regular file /mnt/smbtest/test.txt: Input/output error
```

如果共享上不存在该文件，则 `cp` 或 `mv` 命令可以工作。内核为 2.4x 的 Linux 不会有这种行为。在这种情况下，你可以使用 `smclient` 工具或在复制新文件之前删除共享上的旧文件。

示例 5-3 显示了用户 `ITSOUSER` 的所有任务列表。如果你处理 `QZLSFILE` 任务，可以获取如远程 SMB 客户端的 IP 地址以及其他典型的 IBM i/OS 任务信息。

## 示例 5-3 对象锁

| 对象 | 类型 | 系统 |
| :--- | :--- | :--- |
| 库 (`Library`) | `ITSOUSER` | `*USPRF` |
| | `QSQYS` | `asp device : *SYSBAS` |

输入类型选项，按回车键。4-结束任务 5-处理任务 8-处理任务锁

| 选项 | 用户 | 锁 | 状态 | 范围 | 线程 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `QZLSFILE` | `QUSER` | `*SHRRD` | `HELD` | `*JOB` | |
| | | `*SHRRD` | `HELD` | `*JOB` | |
| | | `*SHRRD` | `HELD` | `*JOB` | |
| | | `*SHRRD` | `HELD` | `*THREAD` | `00000004` |

在 iSeries Navigator 配置中也可以获得类似的信息。

打开 iSeries Navigator 并展开 iSeries → Network → Servers → TCP/IP。双击 iSeries NetServer。

在这里，你可以获取大量关于 iSeries NetServer 共享以及所有到这些共享的活动连接的信息。

## 5.4 连接到 iSeries NetServer 打印共享

Linux 通过 `lpr`、`jpd`、`cups` 等具有自己的打印缓冲支持。然而，让 Linux 使用 IBM i/OS 的打印缓冲和打印机管理功能作为打印机，将需要打印的文件发送到 IBM i/OS 打印机可能会是有益的。

### 5.4.1 如何配置打印共享

以下示例显示了如何配置打印共享，并允许 Linux 系统上的用户共享在 IBM i/OS 上配置的打印机。我们假设 IBM i/OS 上已经配置了一个打印机，并且你可以使用该打印机的输出队列 (`OUTQ`)。

> **重要：** 由于 Linux 上的打印机驱动程序支持有限，你的 IBM i/OS 打印机必须能够打印 PCL 或 postscript 数据流。如果你打算设置打印共享并配置为 IBM `'iDPTS'`、IBM 高级功能打印™ (IBM `AFP*`) `YES`，则必须使用适用于 iSeries `75221P1` 的 IBM Infoprint® Server 将 PCL 或 Postscript 数据流转换为 AFP。

更多信息请参阅标题为 IBM eServer iSeries Printing Vi: Delivering the Output of e-business 的 SG24-6250。

在本示例中，我们使用 Novel Linux 发行版连接到 iSeries NetServer 打印共享。如果你使用的是不同的 Linux 发行版，步骤和显示可能会有所不同。

最初，在 IBM i5/OS 上选择一个合适的 `OUTQ`，或使用 `CRTOUQ` 命令创建一个。要在 IBM i5/OS 上设置打印共享，你需要 iSeries Navigator。

## 使用 iSeries Navigator 创建打印共享

要共享 i5/OS 的 `OUTQ`，请在 iSeries Navigator 界面上执行以下步骤：

1. 选择 Network -> Servers -> TCP/IP 和 iSeries NetServer。
2. 展开 iSeriesNetServer 并右键点击 Shared Objects。选择 New（新建）然后选择 Printer（打印机）。
3. 在图 5-3 所示的后续屏幕中填写 Name（名称）、Output queue（输出队列）和 library（库）字段。

![](img/165c050f45ac58e1635258993855261a_89_0.png)

图 5-3 iSeries NetServer 打印共享屏幕

4. 选择 OK（确定）。
5. 选择 Shared Objects（共享对象）以检查此打印共享是否在列表中。

## 从 Linux 连接到共享打印机

在 IBM i5/OS 的 `OUTQ` 被共享后，你可以从 Linux 客户端配置 Samba 打印机。

1. 在 Novell SUSE Linux 上启动配置工具 YaST。在左侧面板选择 Hardware（硬件）部分，点击右侧面板上的打印机图标。
2. YaST 然后将初始化打印机配置工具。当打印机设置窗口打开时，选择 Add（添加）。
3. 在 Printer Type（打印机类型）窗口中选择 Network Printer（网络打印机）。
4. 在 Connection for printer（打印机连接）窗口中，选择 Print via SMB Network Server（通过 SMB 网络服务器打印）并选择 Next（下一步）。见图 5-4。

![](img/165c050f45ac58e1635258993855261a_90_0.png)

图 5-4 使用 YaST 连接到打印共享

5. 打开 Samba/Windows 打印机屏幕。按照图 5-5 所示输入以下信息并选择 Next（下一步）：
   - Host name（主机名）：输入 IBM i5/OS 的主机名或 IP 地址。
   - Remote query（远程查询）：定义打印共享名称。
   - User（用户）：输入有效的 IBM i5/OS 用户配置文件。
   - Password（密码）：输入该用户的密码。

![](img/165c050f45ac58e1635258993855261a_90_1.png)

图 5-5 YaST 中的 Samba/Windows 打印机配置窗口

6. 在 Queue Name（队列名称）窗口中，为 Linux 指定打印机名称，并勾选 `Do Local Filtering`（进行本地过滤）选项。见图 5-6。

![](img/165c050f45ac58e1635258993855261a_91_0.png)

图 5-6 指定打印机名称

7. 在 i5/OS 上选择 Linux 机机， Linux    。 IBM i iOS 打印机 支持 PCL 或 Postscript 数据流。
8. i i5- 5555555555555555555511555555555555555555555555555555555555555511111555555555555555555555555552222222525222

## 6.2 在 IBM i/OS 上设置 NFS 服务器

本节将介绍如何使用 iSeries Navigator 在 IBM i/OS 端配置和管理 NFS 服务器。执行以下步骤：

1. 在 IFS 中创建一个目录来存放 Linux 文件，例如：
   ```
   MKDIR DIR('/nfshome')
   ```
2. 在 iSeries Navigator 上选择文件系统（File System）→ 集成文件系统（Integrated File System）→ 根目录（Root）。
   选择所需的存放 NFS 目录。右键点击，选择 NFS 导出（NFS Export），然后选择属性（Properties），如图 6-1 所示。

![](img/165c050f45ac58e1635258993855261a_96_0.png)

图 6-1 使用 iSeries Navigator 创建 NFS 导出

3. 检查详情是否正确（默认用户为 `QNFSANON`），然后如图 6-2 所示选择导出（Export）。

![](img/165c050f45ac58e1635258993855261a_96_1.png)

图 6-2 使用 iSeries Navigator 配置 NFS 导出 `/nfshome`

注意：如果选择“添加到永久定义的导出列表”（Add to list of permanently defined exports），条目将被添加到 IFS `/etc/EXPORTS` 文件。

4. 现在启动 NFS 服务器。选择网络（Network）-> 服务器（Servers）-> TCP/IP。右键点击 NFS 并选择全部（All），如图 6-3 所示。

![](img/165c050f45ac58e1635258993855261a_97_0.png)

图 6-3 启动 NFS 服务器

现在，IBM i/OS 上的 NFS 已就绪。

## 6.3 挂载 IBM i/OS NFS 导出

使用 `mount` 命令对可用的 NFS 导出进行临时连接。如果你希望在 Linux 启动期间建立 NFS 连接，请修改 `/etc/fstab` 文件以在 Linux 启动时挂载文件系统。执行以下步骤：

1. 以 `root` 用户身份登录 Linux 系统。
2. 创建一个目录作为挂载点，例如 `/mnt/iseries`：
   ```
   linux:> mkdir /mnt/iseries
   ```
3. 使用以下远程文件系统挂载系统语法 `systemname:exportname /localmountpoint` 将导出挂载到目录：
   ```
   linux:> mount iseries.ito.ibm.com/nfshare /mnt/iseries
   ```
4. 不带参数的 `mount` 命令将显示所有挂载的文件系统，如示例 6-1 所示。

示例 6-1 所有挂载的文件系统

