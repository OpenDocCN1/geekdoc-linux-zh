
- 企业卷管理系统 (`EVMS`) — 逻辑卷管理器的增强版本，支持 Novell NSS 卷。另见逻辑卷管理器。

- `info` 页面 — 使用 `info` 命令查看的命令行文档页面。Info 页面比 man 页面更新，并且通常包含更多信息。

- `inode` — 包含有关 Linux 文件信息的索引项。

- 日志文件系统 — 一种记录应用于磁盘分区的数据事务日志的文件系统。

- 本地组 — 由 Linux 管理员创建并用于分配用户权限和特权的组账户。

- 逻辑卷管理器 (`LVM`) — 一种将物理硬盘分区分组为卷组以创建逻辑卷的卷管理系统。

- `man` 页面 — 使用 `man` 命令查看的命令行文档页面。

- 网络文件系统 (`NFS`) — 一个允许将文件和目录导出到网络以供远程访问的 Linux 文件系统服务器。

- RedHat 软件包管理器 (`RPM`) — 一种由 `rpm` 命令用于安装和管理软件的软件安装文件格式。

- `shell` — 一种用于输入命令和启动程序的 Linux 命令行环境。

- 系统组 — Linux 操作系统创建的用于授予访问特定系统资源权限的组账户。

- 虚拟文件系统切换 (`VFS`) — 一种操作系统接口系统，它将来自进程的用户请求发送到实际的磁盘文件系统。

- X-Window — 用于提供图形支持的接口，其他软件包（如 KDE 和 Gnome 桌面）基于此进行绘制。

### 复习题

1. 以下哪个系统组可用于创建备份系统管理员？

   a. admin

   b. root

   c. domain admin

   d. manager

2. root 用户被分配的用户 ID 为 ____________。

   a. 0

   b. 1

   c. 100

   d. 10

3. SUSE Linux 中的默认 Shell 是以下哪一个？

   a. Bourne

   b. Bourne Again (`Bash`)

   c. Korn

   d. C

4. SUSE Linux 使用以下哪个文件来存储加密密码？

   a. `passwd`

   b. `system`

   c. `shadow`

   d. `password`

5. 哪个命令可以列出所有已登录系统的用户？

   a. `who`

   b. `users`

   c. `stat`

   d. `su`

6. 下列哪一项通常提供更新的命令文档版本？

   a. `man` 手册页

   b. `info` 信息页

   c. root 页面

   d. system 系统页面

7. 运行级别 ____________ 包含 X-Window 图形界面以及对网络环境的支持。

   a. 3

   b. 1

   c. 10

   d. 5

8. 下列哪个 `RPM` 选项表示该软件包不包含二进制代码？

   a. i586

   b. noarch

   c. src

   d. bin

   e. nosrc

9. 下列哪一个是日志型文件系统？（选择所有适用项。）

   a. FAT32

   b. NTFS

   c. ext2

   d. ext3

   e. ReiserFS

10. 下列哪个文件系统通过网络使数据可用？

    a. ext2

    b. ReiserFS

    c. `NFS`

    d. `LVM`

11. 第二个 SCSI 驱动器上的第一个分区将被命名为 ________。

    a. `sda2`

    b. `sdb1`

    c. `db21`

    d. `db12`

12. 支持 Novell 存储服务需要以下哪项？

    a. `LVM`

    b. `EVMS`

    c. ReiserFS

    d. ext2

13. 哪个文件包含驱动器挂载信息？

    a. `fileconfig`

    b. `mount`

    c. `system`

    d. `fstab`

14. 你需要在调整分区大小之前卸载该分区。此说法正确还是错误？

15. 使用哪个命令切换到 root 用户？

    a. admin

    b. root

    c. `su`

    d. `grep`

16. 下列哪一项与 ReiserFS 文件系统配合使用？

    a. `LVM`

    b. `EVMS`

    c. NSS

    d. `LVM2`

17. 下列哪个命令为 EngData 目录的所有者授予所有权限，为指定组授予读写权限，并为所有其他用户授予读取权限？

    a. `chmod 764 EngData`

    b. `chmod 755 EngData`

    c. `chmod 975 EngData`

    d. `chmod 531 EngData`

18. 下列哪一项用于与其他 Linux 系统共享目录？

    a. Samba

    b. `NFS`

    c. NIS

    d. Share

19. Linux 命令行界面也被称为下列哪一项？

    a. system 接口

    b. `shell`（壳）

    c. GUI

    d. terminal

20. 下列哪一项用于从压缩文件安装和管理 Linux 应用程序？

    a. `YaST`

    b. Samba

    c. `RPM`

    d. `EVMS`

### 案例项目

#### 案例项目 13-1：比较卷管理器

Eric 希望你能比较 `LVM` 系统和 Novell 存储服务（NSS），并解释它们的相似之处和不同之处。请写一篇短文，比较 `LVM` 和 NSS 的组件。

#### 案例项目 13-2：比较文件系统权限

Eric 希望你能比较 Linux 和 NetWare 中的文件系统权限。请给 Eric 写一份简短的备忘录，概述它们的相似之处和不同之处。

#### 案例项目 13-3：比较 Linux 和 NetWare 权限

表 13-13 列出了执行某些文件系统任务所需的 NetWare 权限。在接下来的两列中，填写执行该操作所需的 Linux 权限以及用于分配权限的八进制值。

**表 13-13 常见功能所需的权限**

| 任务 | 所需的 NetWare 权限 | Linux 权限 | 八进制值 |
| :--- | :--- | :--- | :--- |
| 读取文件 | 读取（Read） | | |
| 查看目录列表 | 文件扫描（File Scan） | | |
| 更改文件中的数据内容 | 写入（Write） | | |
| 使用创建备份文件的文本编辑器向已关闭的文件写入 | 写入（Write）；创建（Create）；擦除（Erase）；修改（Modify，并非总是需要） | | |
| 运行程序文件 | 读取（Read） | | |
| 创建新文件并写入 | 创建（Create） | | |
| 从目录中复制文件 | 读取（Read）、文件扫描（File Scan） | | |
| 将文件复制到目录中 | 创建（Create） | | |
| 将多个文件复制到已有文件的目录中 | 创建（Create）；文件扫描（File Scan） | | |
| 创建子目录 | 创建（Create） | | |
| 删除文件 | 擦除（Erase） | | |

### 动手项目

#### 动手项目 13-1：创建本地 Linux 用户和组

你需要将 Universal AeroSpace 的商业部门添加到你的 SUSE Linux 服务器中。使用本章学到的技术，设置以下本地组和用户账户：

- 经理组（Managers group）：Lynn Dai, David Heise

- 会计师组（Accountants group）：Terry Blackwell, George Perez, Amy Pan

- 桌面出版组（Desktop Publishers group）：Diana Brady, Julie Damrau

#### 动手项目 13-2：创建和挂载 LVM 目录结构

使用 `YaST` 中的 `LVM` 选项创建一个名为 `userdata` 的逻辑卷，并将其挂载在 `/usr` 结构中。让你的讲师检查结果。

# 第 14 章

## 在 Linux 上规划和实施 NOVELL OES

- 识别 SUSE Linux 中包含的 Novell 服务

- 创建 eDirectory 对象并允许 eDirectory 用户访问 Linux 服务

- 使用 NetWare 核心协议（NCP）启用从 Windows 系统访问 Linux 目录

- 在 Linux 服务器上创建 NSS 卷，并通过 Samba 允许 Windows 客户端访问

- 描述在 Linux 服务器上设置 iPrint 的步骤
