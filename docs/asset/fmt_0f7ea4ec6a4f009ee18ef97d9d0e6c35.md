
| AppsUtility | | | | | | | | | | 

| Forms | All | RF | | | | | | | | 

| Shared | All | RWE CMF | | | | | | | | 

| Inventory | All | RF | | RWF | | | | | | 

| MgmtShared | | | | | RWE CMF | | | | | 

| ITWeb | All | RF | | | | | | | | 

| ITShared | All | | | | | | | RWE CMF | | 

| Engineer | All | | | | | | RF | | | 

| EngineerCAD | All | | | | | | | | | 

| EngineerRPS | All | | | | RF | | | | | 

| EngineerShared | All | | RWE CMF | | | | | | | 

| EngineerAircraft | All | RF | | | | | | | | 

| EngineerNASA | All | RF | | RWF | | | | | | 

| MigDataShared | | | | | | | | | | 

| AppsSUUsage | All | | | | | | | | | 

| | | | | | | | | | RWE CMF |

图 6-14 UAS 目录管理者工作表，第 1 页

![](img/840007e8f98ea6653e5877e945c27dc6_254_0.png)

#### UAS 目录的管理者工作表：

| 目录路径 | IRF | 管理者：AdmAsst 角色 | 管理者：ISSEng 角色 | 管理者：Rover/Eng 角色 | 管理者：Eng/Mgr 角色 | 管理者：AeroMgr 角色 | 管理者：Mig/Mgr 角色 | 管理者：PAlm 用户 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| CORP 卷 | All | | | | | | | |
| Mgmt | All | SRF | | | | | | |
| IT/Web/Engineer | All | | RWE/MF | RWE/MF | RWE/CFA | | | |
| Engineer/Aircraft | RF | | | RWE/MF | RWE/MF | RWE/MF | | |
| Engineer/WAS | All | | | | | | RWE/MF | |
| Engineer/WAS/AISS | All | | | | | | | RWE/MF |
| Engineer/WAS/Rover | All | | | | | | RWE/MF | |
| Engineer/用户名 | RF | | | | | | | |
| MigData | All | | | | | | RWE/MF | REC/MF |

**图 6-15** UAS 目录管理者工作表，第 2 页

### 属性安全

属性是你可以与文件和目录关联的标志或代码，以便网络操作系统可以确定对该文件或目录可以执行哪些类型的处理。网络管理员经常在目录和文件上设置属性，作为防止意外更改或删除的额外保护措施，或指定特殊处理，例如控制文件压缩、使文件可共享或在删除后立即清除文件。作为 CNA，你需要了解文件和目录属性、它们的用途以及如何使用 NetWare 实用工具来处理属性。

#### 文件和目录属性

设置在文件和目录上的属性会覆盖用户在该文件或目录中的有效权限。例如，如果文件被标记为只读（Read Only）属性，无论有效权限如何，你对该文件可以执行的唯一操作是读取（Read）和文件扫描（File Scan）。例如，Kari Means 对 Engineer 目录拥有所有权限，因此她将继承 Engineer 目录结构中文件和子目录的所有权限。如果 NASA 目录中名为 `Partition.dat` 的文件被标记为只读属性，即使 Kari 由于管理者分配而拥有所有有效权限，她对 `Partition.dat` 文件仍只有读取和文件扫描访问权限。然而，由于 Kari 由于对 Engineer 目录的管理者分配而继承了目录的修改（Modify）权限，她可以移除只读属性，然后更改甚至删除 `Partition.dat` 文件。

##### 文件属性

表 6-4 列出了 NetWare 文件属性及其缩写。在以下章节中，这些属性将被简要描述。

**表 6-4** 文件属性

| 属性 | 缩写 | 属性 | 缩写 |
| :--- | :--- | :--- | :--- |
| 需要存档 (Archive Needed) | A | 立即压缩 (Immediate Compress) | Ic |
| 禁止复制 (Copy Inhibit) | Ci | 已迁移 (Migrated) | M |
| 禁止删除 (Delete Inhibit) | Di | 清除 (Purge) | P |
| 不压缩 (Don't Compress) | Dc | 只读 (Read Only) | Ro |
| 不子分配 (Don't Suballocate) | Ds | 禁止重命名 (Rename Inhibit) | Ri |
| 不迁移 (Don't Migrate) | Dm | 可共享 (Shareable) | Sh |
| 仅执行 (Execute Only) | X | 系统 (System) | Sy |
| 隐藏 (Hidden) | H | 事务性 (Transactional) | T |

**需要存档 (Archive Needed (A))** 属性在文件内容被修改时自动分配给文件。复制或备份实用工具可以在将文件复制到另一个存储位置后移除此属性。此属性控制哪些文件被复制到备份磁盘，使得只备份自上次备份以来已更改的文件成为可能。

**禁止复制 (Copy Inhibit (Ci))** 属性仅用于防止 Macintosh 用户复制指定文件，例如在 Macintosh 计算机上无法运行的程序。设置此属性可防止运行 AppleTalk Filing Protocol 2.0 及更高版本的 Macintosh 计算机复制该文件。

**禁止删除 (Delete Inhibit (Di))** 属性防止文件被删除，但允许重命名或更改该文件。要删除该文件，用户必须首先被授予修改（Modify）权限以移除禁止删除属性。禁止删除属性常用于保护重要数据文件以免被意外删除，同时仍允许更改其内容。你应该考虑为组织的许多永久文件设置禁止删除属性，例如客户、工资、库存和会计数据。

用户或网络管理员可以设置**不压缩 (Don't Compress (Dc))** 属性以防止文件被自动压缩。防止文件压缩可以在访问该文件时产生微小的性能提升，因为文件不需要被解压缩。

用户或网络管理员可以设置**不子分配 (Don't Suballocate (Ds))** 属性以防止文件被子分配给其他文件。使用此属性，你可以运行某些应用程序并使用与已子分配文件不兼容的数据库系统。

**不迁移 (Don't Migrate (Dm))** 属性防止文件在卷设置了已迁移（Migrated）属性时被第三方软件移至离线。

**仅执行 (Execute Only (X))** 属性的主要用途是保护软件文件免受非法复制。只有具有管理员等价权限的用户才能在 `.exe` 和 `.com` 文件上设置仅执行属性；一旦设置，即使是网络管理员也无法移除。除非你有文件的备份副本，否则不要为文件分配仅执行属性。某些程序文件在被标记为仅执行时无法运行，因为这些程序曾用于将信息复制到计算机内存，而“仅执行”属性阻止它们应用复制功能。由于“仅执行”属性无法移除，若要摆脱该属性，您需要删除文件并从其他磁盘重新安装。

**隐藏 (H)** 属性用于隐藏文件，使其不出现在 DOS 实用程序和某些应用程序软件中。NetWare 实用程序会在启用“隐藏”属性时显示隐藏文件。一种保护软件免受非法复制的简单方法是使用“隐藏”属性将软件目录和文件从常规 DOS 实用程序中隐藏起来，然后将 `NCOPY` 和 `NDIR` 命令从 `SYS:Public` 目录移动到 `SYS:System` 目录或典型用户无法访问的其他位置。

**立即压缩 (Ic)** 属性通常分配给那些在关闭后立即压缩以节省磁盘空间的大型文件。如第 3 章所述，默认情况下，文件会在无活动七天后被压缩。

系统使用 **已迁移 (M)** 属性标记那些已被迁移至高容量存储介质（如光盘驱动器或磁带备份系统）的文件。尽管已迁移的文件对用户可访问，但在能够访问之前可能需要较长的恢复延迟时间。
