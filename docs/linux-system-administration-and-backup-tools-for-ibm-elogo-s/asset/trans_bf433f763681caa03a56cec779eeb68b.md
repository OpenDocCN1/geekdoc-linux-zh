

3. 在“包含的文件/目录”（Files / Directories to Include）字段中，输入我们备份的文件或目录的路径。在我们的示例中，我们想要对 `usr/src` 目录进行备份。选择 OK 继续。你将看到一个类似于图 194 的窗口。

![](img/4e6a76e57a4105be55d8a1cc0750b023_207_0.png)

备份完成后，你将看到一个类似于图 195 的窗口。

196 IBM @serverSeries 和 Netinity Linux 系统管理与备份

# 终端

![](img/4e6a76e57a4105be55d8a1cc0750b023_208_0.png)

图 195. 备份完成

你还将看到一个类似于图 196 的备份报告。

# 终端

![](img/4e6a76e57a4105be55d8a1cc0750b023_208_1.png)

图 196. 备份报告

你刚刚完成了首次备份，你的文件现在安全了！

第 7 章 备份应用程序的安装与设置 197

## 7.2.4 恢复单个文件或目录

在本节中，我们将展示如何从备份中恢复文件。假设你正在备份的相同服务器上使用相同的用户 ID 恢复文件。你可以使用与备份时相同的工具进行恢复。按照以下步骤恢复文件：

- 1. 执行以下命令启动 edgemenu 备份：

```
edgemenu
```

你将看到一个类似于图 192 的窗口。选择 Restore（恢复），将出现一个类似于图 197 的窗口。

![](img/4e6a76e57a4105be55d8a1cc0750b023_209_0.png)

图 197. 正在启动恢复

- 2. 选择 Restore > Individual Files（单个文件），你将看到一个类似于图 195 的窗口。

- 3. 选择要恢复的文件或目录。选择 OK 继续，你将看到一个类似于图 198 的窗口。

198 IBM @server xSeries 和 Netinity Linux 系统管理与备份

# 终端

```
[File] [Backup] [Restore] [Verify] [Admin] [Schedule]

恢复键盘列出的文件
恢复参数
[Y] 破坏性
正在恢复文件
/usr/src/linux-2.2.10/arch/arm/mm
文件: 2114 [C  取消] es||To:

主资源: nf5500 drive DLT (/dev/std0) (DLT 磁带 35/70GB)
溢出资源: 无
库库资源: 无
主: 压缩: Hard. 磁带块: -1. 边缘块: 64. 分区: -1
溢出: N/A
上次主备份: Tue Nov 2 14 20 15 1999
本地机器: nf5500 first itso.com 管理员: nf5500 first itso.com
```

图 198. 正在恢复中

当恢复完成后，你将看到一个类似于图 199 的窗口。

# 终端

```
[File] [Backup] [Restore] [Verify] [Admin] [Schedule]

恢复键盘列出的文件
恢复参数
恢复成功
排除
排除
至:

[Ok]

主资源:
溢出资源: 无
库库资源: 无
主: 压缩: Hard. 磁带块: -1. 边缘块: 64. 分区: -1
溢出: N/A
上次主备份: Tue Nov 2 14 20 15 1999
本地机器: nf5500 first itso.com 管理员: nf5500 first itso.com
```

图 199. 恢复完成

第 7 章 备份应用程序的安装与设置 199

选择 OK 继续，你将看到类似于图 200 的恢复界面。

```
终端
权限  Uid Gid 字节  最后修改 文件名
-xr-xr-x   0/0    203807 Aug 10 20:41 1999 /usr/src/linux-2 2.10/System
-xr-xr-x   0/0    199497 Aug 10 21:06 1999 /usr/src/linux-2 2.10/vmem
-rw-r---- 0/0    31363 Sep 30 23:59 1999 /usr/src/linux-2 2.10/include
-rw-r---- 0/0     7295 Jan 26 18:19 1999 /usr/src/linux-2 2.10/include
-rw-r---- 0/0    52058 Feb 05 12:13 1999 /usr/src/linux-2 2.10/include
-rw-r---- 0/0     4620 Apr 24 00:20 1999 /usr/src/linux-2 2.10/include
-xr-xr-x   0/0     2760 Mar 11 14:33 1999 /usr/src/linux-2 2.10/include
-xr-xr-x   0/0    10324 Apr 24 00:26 1999 /usr/src/linux-2 2.10/include
-xr-xr-x   0/0     4472 Jan 26 18:19 1999 /usr/src/linux-2 2.10/include
-rw-r---- 0/0    28710 Feb 24 01:01 1998 /usr/src/linux-2 2.10/include
-rw-r---- 0/0    13648 Dec 12 13:58 1998 /usr/src/linux-2 2.10/include
-rw-r---- 0/0     2674 Jul 30 14:17 1998 /usr/src/linux-2 2.10/include
```

图 200. 恢复报告

你的文件已成功恢复！

## 7.2.5 主备份与增量备份

通常，系统管理员会执行主备份和增量备份。主备份是对系统中所有文件的备份。增量备份仅是对上次主备份以来发生更改文件的备份。当你需要恢复数据时，请恢复主备份和最后一个增量备份。BackupEDGE 可以执行不同类型的增量备份。关于从 edgemenu 工具执行增量备份的说明，请参考 BackupEDGE 手册。

要执行主备份，请遵循以下步骤：

- 1. 执行以下命令启动 edgemenu 程序：

```
edgemenu
```
你将看到一个类似于图 192 的窗口。
2. 选择 Backup（备份） > Master Backup（主备份），你将看到一个类似于图 201 的窗口。

200 IBM @xSeries 和 Netfinity Linux 系统管理与备份

# 终端

![](img/4e6a76e57a4105be55d8a1cc0750b023_212_0.png)

图 201. 正在备份

3. 选择你需要的选项并选择 **Execute Backup**（执行备份）开始备份。你将看到一个类似于图 202 的窗口。

# 终端

![](img/4e6a76e57a4105be55d8a1cc0750b023_212_1.png)

图 202. 正在进行主备份

当备份完成后，你将看到一个类似于图 203 的窗口。

第 7 章 备份应用程序的安装与设置 201

![](img/4e6a76e57a4105be55d8a1cc0750b023_213_0.png)

```
[File] [Backup] [Restore] [Verify] [admin] [schedule]
验证卷                主备份               记录锁定
[2] 验证类型 (逐个文件)  () 不锁定文件
[2] 索引                                    读取
                             备份 / 验证 / 索引成功
[ ] 拆分                                     排除
[ ] 制作                                     相对

主资源 : 无
溢出资源 : 无
库库主 : 压缩 : Hard, 磁带块 -1, 边缘块 64. 分区 -1
溢出 M/V
上次主备份 : Tue Nov 24 20:15 1999
本地机器 : nf5500 first itso.com 管理员: nf5500 first itso.com
```

图 203. 主备份完成

选择 OK 完成操作，你将看到一个类似于图 204 的备份报告。

![](img/4e6a76e57a4105be55d8a1cc0750b023_213_1.png)

```
主备份               Tue Nov 2 20:17:54 1999
使用未使用的文件锁定
tag=/dev/sdb1vm/Master-part-1999-11-02/btwm=20:17/bdv=st0/bbk=64/bvs=350000
a /lost+found 0 blocks
a /boot+found 0 blocks
a /boot/stage1.py 28 blocks
a /boot/boot_b 0 blocks
a /boot/boot_b.orig 2 blocks
a /boot/chain.b 2 blocks
VG-209715DB
a /boot/message. 0 blocks
符号链接到 ===: message col22
a /boot/message col22 57 blocks
a /boot/message col22 ttt. 4 blocks
VG-209715DB
a /boot/c02 d.b 2 blocks
```

