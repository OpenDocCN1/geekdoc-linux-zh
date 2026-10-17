
现在你已经准备好使用该产品了。

### 3.1.2 配置磁带设备

在开始备份之前，你需要定义你的备份设备。

要实现这一点，请按照以下步骤操作：

1. 执行命令启动 `edge.resmgr` 资源管理器：

```
/usr/lib/edge/bin/edge.resmgr
```

你将看到一个类似于图 189 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_259)

2. 点击 `New`（新建）并按资源。你将看到一个img/ 29991。

bimg/635926a3e67073343783259))图 188. 资源资源

3. 输入资源名称并选择类型。你将看到一个类似于图 191 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_259)

图 190. 定义名称

4. 输入描述、不回带节点。在我们的示例中，数据节点是 `/dev/st0`，不回带节点是 `/dev/nst1`。

5. 点击 `OK` 配置其他字段。你将看到一个类似于图 192 的窗口。

图 191. 磁带参数

6. 在这里你可以选择块因子和大小。点击 `Start` 继续。你将看到一个类似于图 193 的窗口。

图 192. 设置参数

7. 点击 `Yes`（是），这将删除磁带上的数据。你将看到一个类似于图 194 的窗口。

图 193. 性能

8. 测试完成后，你会看到阈值。点击 `OK` 继续。

图 194. 阈值

9. 通过选择 `Save`（保存）保存更改。你将看到一个类似于图 196 的窗口。

图 195. 保存定义

### 3.1.3 为备份定义设备

硬件配置好后，你需要告诉备份软件每个用户使用哪个设备。如果你以 `root` 登录，这是唯一的备份用户。按照以下步骤操作：

1. 执行命令启动 `edge.config` 菜单：

`/usr/bin/edge.config`

你将看到一个类似于图 197 的窗口。

图 197. 设备配置

2. 在这里你需要定义演示和无人备份的设备。你将看到一个类似于图 198 的窗口。

图 198. 选择备份设备

3. 输入 `A` 并按回车定义演示备份的设备。你将看到一个类似于图 199 的窗口。

```
文件分区选项

备份设备配置 (edge.config) 版本 01.01.07
Copyright 1998 - 1999 Microlite Corporation 保留所有权利
备份资源: 演示备份 无人备份
主系统: (A) Localhost (E) NONE
资源: DL
描述: DLT 磁带 35/70GB
设备节点/文件: /dev/st0
溢出系统: (B) NONE (F) NONE
资源:
描述:
设备节点/文件:
更改: (C) NONE (G) NONE
资源:
描述:
设备节点/文件:
更改 主备份资源 F 更改无人
更改 溢出备份资源 F 更改无人
更改 磁带自动库资源 I 更改无人
通过资源管理器添加/更改资源
活动系统名称为 n9f3500.first.itso.com
输入选择 (ARG,3,X7) 并按 <Enter> :
```

图 199. 定义演示设备

4. 按照步骤 1-4 处理无人设备。

你现在准备好备份你的重要文件了。

### 3.1.4 初始化磁带

在进行备份之前，你应该初始化磁带。要执行此操作，请按照以下步骤操作：

1. 执行命令启动 `edgemenu` 程序：

`/usr/bin/edgemenu`

你将看到一个类似于图 200 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_268_0.png)

图 200. ADGEMEMENU 主菜单

2. 在管理（`Admin`）菜单中选择初始化磁带（`Initialize Tapes`）。你将看到一个类似于图 201 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_268_1.png)

图 201. 初始化磁带

3. 选择初始化磁带（`Initialize Tape`）并按 `Enter`。磁带将被初始化。你将收到磁带成功初始化的消息。按 `Enter` 继续。

你可以通过选择验证（`Verify`）菜单中的显示磁带标签（`Show Tape Label`）来检查磁带属性。你将看到一个类似于图 202 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_269_0.png)

图 202. 磁带信息

### 13.1.5 你的首次备份

在本节中，我们将展示如何对所需的文件或目录进行备份。你可以在 `edgenemu` 工具中执行备份。按照以下步骤进行示例备份：

1. 通过执行命令启动 `edgenemu` 程序：

```
//usr/bin/edgenemu
```

你将看到一个类似于图 203 的窗口。

### Terminal

```
[文件] [备份] [恢复] [验证] [管理] [计划]
  [主备份]
  增量备份
  备份文件/目录
  [备份当前目录]
  单个文件或目录
```

![](img/2d69b129b41635ef36a3e6707d34b788_270_0.png)

图 203. 在备份（`Backup`）菜单中，选择备份文件/目录（`Backup Files / Dirs`），你将看到一个类似于图 204 的窗口。

2. 在备份（`Backup`）菜单中，选择备份文件/目录（`Backup Files / Dirs`），你将看到一个类似于图 204 的窗口。

### Terminal

```
[文件] [备份] [恢复] [验证] [管理] [计划]
主.增量, L 或文件备份
  文件 / 目录备份
验证卷               记录锁定
[2] 验证类型（按文件）                  (X) 不锁定文件
[X] 验证期间索引                    ( ) 强制读取
  在处理归档时包含的文件
  要包含的文件/目录 [es]
  [/user/arc                          [es]
  列出包含的文件
  [
  [确定]                                     [取消]
目录文件
  资源  NONK
  计算机硬盘类型列表  文件 #asterisk
  本地备份 Bac Nov 7 10:15 am
本地机器 nr5500 first.com Administering nr5500 first itscom
```

图 204. 选择备份内容

3. 在要包含的文件/目录（`Files / Directories to Include`）字段中，输入你想要备份的文件或目录。在我们的示例中，我们想要备份目录

第 13 章 备份与恢复 253

`/usr/src/` 选择确定（`OK`）继续。你将看到一个类似于图 205 的窗口。

### Terminal

| [文件] [备份] [恢复] [验证] [管理] [计划] |
| 文件 / 目录备份 | 记录锁定 |
| [2] 验证类型（逐个文件） | (X) 不锁定文件 |
| [X] 验证期间索引 | (强制读取 |
| 备份文件 | /usr/src/linux-2.2.10/net/root |
| 文件 5122 | [C] 取消 | es |

图 205. 正在备份中

备份完成后，你将看到一个类似于图 206 的窗口。

### Terminal

| [文件] [备份] [恢复] [验证] [管理] [计划] |
|| 文件 / 目录备份 | 记录锁定 |
| [2] 验证类型（逐个文件） | (X) 不锁定文件 |
| [X] 索引 | 或强制读取 |
| 备份 / 验证 / 索引成功 | 读取 |
| Spl | [包含] |
| Make | 包含 |
| Ok | |

图 206. 备份完成

Caldera OpenLinux 和 Netfity 服务器集成指南

你还将看到一个类似于图 207 的备份报告。

```
# /tmp/lb1/http=/badv/bdt-1999-11-02/bts-19.53/bdv-st0/bbk=64/bvs=350000
a /usr/src/linux-2.10/System.map, 399 blocks
VOL=209715Mb
a /usr/src/linux-2.10/System.map-pc-97, 381 blocks
VOL=209715Mb
a /usr/src/linux-2.10/include/linux/compile h. h, 1 blocks
a /usr/src/linux-2.10/include/linux/s.out h. h, 15 blocks
a /usr/src/linux-2.10/include/linux/acct. h, 6 blocks
a /usr/src/linux-2.10/include/linux/adfs fs. h, 10 blocks
a /usr/src/linux-2.10/include/linux/adfs fs i. h, 1 blocks
a /usr/src/linux-2.10/include/linux/adfs fs-b. h, 1 blocks
a /usr/src/linux-2.10/include/linux/affs fs. h, 9 blocks
VOL=209715Mb
a /usr/src/linux-2.10/include/linux/affs fs i. h, 4 blocks
a /usr/src/linux-2.10/include/linux/affs fs sb. h, 6 blocks
a /usr/src/linux-2.10/include/linux/affs hardblocks. h, 3 blocks
```

图 207. 备份报告

你刚刚完成了备份，你的文件是安全的！

### 13.1.6 恢复文件或目录

在本节中，我们将展示如何从备份恢复文件。我们假设你使用相同的工具进行了备份。按照以下步骤进行恢复：

1. 通过执行命令启动 `edgenemu` 程序：

```
//usr/bin/edgenemu
```

你将看到一个类似于图 203 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_273_0.png)

2. 在备份（`Backup`）菜单中，选择备份文件/目录（`Backup Files / Dirs`），你将看到一个类似于图 204 的窗口。

3. 在要包含的文件/目录（`Files / Directories to Include`）字段中，输入你想要恢复的文件或目录。选择确定（`OK`）继续。你将看到一个类似于图 205 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_274_0.png)

恢复完成后，你将看到一个类似于图 210 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_277_0.png)

### 13.1.9 执行计划备份

要执行计划备份，你可以使用 `BackupEDGE` 自带的实用程序。该工具名为 `edge.nightly`。要启动该工具，请执行命令：

```
/usr/lib/edge/bin/edge.nightly
```

但在使用计划备份之前，你需要先对其进行定义。请按照以下步骤操作：

1. 启动 `edgemenu`。

2. 选择 `Schedule`（计划）-> `Nightly Scheduling`（每日调度）。你将看到一个与图 218 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_279_0.png)

图 218. 计划设置

3. 在这里你可以定义备份计划。你需要定义备份的类型和时间。要定义备份类型，选择 `A` 并按回车，你将看到一个与图 219 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_280_0.png)

图 219. 定义备份类型

4. 指定你想执行的备份类型。在我们的示例中，我们选择了 `M` 代表主备份（master backup）。返回返回主窗口。

> 注意

> 你不能混合使用主备份和增量备份。如果你的主备份可以放入一个磁带盒，我们建议每天执行一次主备份。如果你的主备份无法放入一个磁带盒，请每周执行一次手动主备份，每天执行增量备份。

5. 接下来，你需要通过选择 `B` 并按回车来指定每日备份的时间。你将看到一个与图 220 类似的窗口。

```
Currently 1999-11-04 12:09:22
At what hour do you want your Master Backups to start? (0-23)
Press [ENTER] for 23 (11 PM) :
```

图 220. 设置时间

6. 定义你备份的时间。你将看到一个与图 221 类似的窗口。

```
Terminal <2>
BackupEDGE Nightly Archive Setup Menu (edge_cronset) Version 01.07
Copyright 1988 - 1999 by Microsoft Corporation All Rights Reserved
Choice Settings Type Current Last
A BackupEDGE Backup Type Master Master
B Backup Time (24 hour format) 12:30 12:30
C Mail Notification To root root
D (t) Backup on Sundays YES root
E (t) Backup on Tuesdays YES YES
F (t) Backup on Wednesdays YES YES
H (t) Backup on Thursdays YES YES
I (t) Backup on Fridays YES YES
J (t) Backup on Saturdays YES YES
K Verify After Backup BIT BIT
L Index After Backup YES YES
M Send Diagnotstics Output To /dev/null
N Print Backup Results To DISABLED
S Save Settings - Create New Cron
X Exit - Abandon Changes Use Last Entries 1999-11-04 12:37:39
(t) Toggles Entry (YES or No)
please Type Letter of Your Selection and Press [ENTER] 
```

图 221. 计划定义后

7. 选择 `S` 并按回车设置设置。配置程序将在 `cron` 数据库中创建一个用于执行 `edge.nightly` 工具的条目。从现在起，`cron` 将按照你之前步骤中的定义执行备份工具。

# 注意

在开始使用计划备份之前，你需要将文件 `/usr/lib/edge/bin/S88egde` 复制到 `/etc/rc.d` 目录。此脚本将在系统重启时清除 `edge.nightly`。

你也可以从自己的脚本启动 `edge.nightly`。当你从命令行或脚本以 `root` 身份启动 `edge.nightly` 后，它将执行备份。

## 13.2 轻量级 RecoverEDGE

使用 `RecoverEDGE` 工具可以创建恢复磁盘，以便在灾难时重建系统。`RecoverEDGE` 处理重建 `FDisk`、分区表、重建文件系统以及恢复数据的细节，即使硬盘的大小或几何结构发生了变化。`RecoverEDGE` 使用实时系统备份，因此不需要关闭系统。你甚至可以通过网络恢复系统。

使用 `RecoverEDGE` 恢复系统非常简单。要恢复系统应遵循以下任务：

1. 识别并修复故障原因。

2. 从 `RecoverEDGE` 磁盘启动。

3. 重配置你的文件系统。

4. 恢复你的备份。

5. 重启。

6. 系统就绪。

# 注意

`RecoverEDGE` 使用主备份和增量备份进行恢复，因此数据的准确性取决于这些备份。

### 13.2.1 创建 RecoverEDGE 启动磁盘

在使用 `RecoverEDGE` 进行灾难恢复之前，你需要构建启动磁盘。创建启动磁盘请遵循以下步骤：

1. 启动创建 `RecoverEDGE` 启动磁盘的工具：

```
/usr/bin/re
```

你将看到一个与图 222 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_283_0.png)

图 222. `RecoverEDGE` 工具

2. 选择 `Configure`（配置）并按回车，你将看到一个与图 223 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_284_0.png)

图 223. 配置菜单

3. 选择 `Disk Layout`（磁盘布局）选项并按回车，你将看到一个与图 224 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_284_1.png)

图 224. 磁盘布局菜单

4. 在这里你可以为 `RecoverEDGE` 磁盘配置内核模块、网络和文件系统。选择 `Kernel`（内核）选项，你将看到一个与图 225 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_285_0.png)

图 225. 内核选项

在这里定义用于磁盘的内核。

5. 返回上一个阶段并选择 `Modules`（模块）并按回车，你将看到一个与图 226 类似的窗口。
