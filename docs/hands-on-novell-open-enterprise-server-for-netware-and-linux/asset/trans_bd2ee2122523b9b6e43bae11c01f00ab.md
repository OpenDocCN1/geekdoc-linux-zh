
下一步是审查目录结构，以确定其是否符合前面描述的目录指南。在 UAS 目录结构中，CAD 软件当前位于 Apps 目录的子目录中。由于 UAS 容器是拥有 [R. F.] 权限的 Apps 目录的管理者（trustee），所有用户都继承了 CAD 子目录的 [R. F.] 权限，这造成了潜在的许可问题，因为公司仅为工程部门用户购买了软件许可证。你可以通过移除 CAD 子目录 IRF 中的所有权限来阻止其他用户访问 CAD 软件，然后仅将 [R. F] 权限授予设计组，方法是使该组成为 CAD 目录的管理者。然而，这种方案并没有解决在通用目录中放置具有更高安全需求的子目录的问题。更好的解决方案是将 CAD 子目录移动到 Engineer 目录，然后进行管理者分配。为了改进文件系统的安全性，你还应该在 Web 目录中创建一个用于工程文件的子目录。这种结构将允许 Kari Means 更新基于 Web 的工程文件，而不会影响 Julie Damrau 和 Kellie Thiele 维护的其他 Web 文档。在章末项目中，你有机会更改你的 UAS 目录结构。

下一步是计划管理者分配。你应该遵循前面描述的指南，努力最小化管理者分配的数量。为了帮助完成这项任务，Eric 创建了一份目录管理者工作表（Directory Trustee Worksheet），如图 6-14 和 6-15 所示。

使用 Novell 指南，Eric 填写了该工作表，以显示每个目录的管理者分配以及对目录 IRF 的任何更改。工作表上的每一行代表第一列指定的目录路径的管理者分配。第二列指示 IRE 允许的权限。其余各列指定管理者分配。Eric 将每个需要管理者分配的对象放在“管理者”列中。在第一页上，他列出了容器对象，随后是组。在第二页上，他列出了组织角色（Organizational Role）对象和任何用户名。他通过将目录路径放在最左侧列，并在相应的容器、组或组织角色下列出访问权限，来指示每个目录的管理者分配。由于某些目录具有来自容器、组和组织角色对象的管理者分配，第二页重复了某些目录路径并添加了额外的管理者分配。请注意，Eric 使用组织角色对象来减少分配给用户的数量。

在工作表的每一页上，Eric 从最高层级的目录开始，向下工作到较低层级，对目录路径列进行了排序。首先对较高层级的目录进行管理者分配，有助于通过继承减少管理者分配的数量。Eric 将包含容器和组的列安排在左侧，随后是组织角色对象和用户分配。首先对容器和组进行分配，有助于减少管理者分配的数量，并简化文件系统安全的维护。目录的 IRE 列在第二列。然后，在相应行的剩余列中，在“管理者”标题下列出要授予每个目录的访问权限。在这个例子中，顶级容器 UAS 列在第一个管理者列中，并被授予对 Apps、Forms、Shared、Inventory 和 IT\Web 目录结构的管理者分配。接下来，Engineering OU 列在第二个管理者列中，并被授予对 Engineer\Shared、Engineer\Aircraft 和 Engineer\NASA 目录的管理者分配。

在权限已分配给容器和组之后，需要特殊权限的组织角色对象和用户将被设为必要目录的管理者。例如，作为 EngMgR 组织角色对象的所有者，Kari Means 拥有维护 Engineer 目录结构以及与 Web\Engineer 目录中的文件进行工作的权限。此外，Engineer\Users 目录的 IRE 已被修改，以仅允许 [R. F.] 权限传递到用户的家庭目录。虽然 Eric 使用了工程部门的大部分权限，但在章末项目中，你将填写目录管理者工作表，包括业务部门用户并授予其目录的访问权限。

### UAS 目录的管理者工作表：

| 目录路径 | IRF | 管理者：UAS 容器 | 管理者：Engineering 容器 | 管理者：Mig 容器 | 管理者：Mgmt 容器 | 管理者：Design 组 | 管理者：ITMigs 组 | 管理者：WebMigs 组 | 管理者：Production 组 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Apps | All | RF | None | | | | | | | 
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

### UAS 目录的管理者工作表：

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

## 属性安全

属性是你可以与文件和目录关联的标志或代码，以便网络操作系统可以确定对该文件或目录可以执行哪些类型的处理。网络管理员经常在目录和文件上设置属性，作为防止意外更改或删除的额外保护措施，或指定特殊处理，例如控制文件压缩、使文件可共享或在删除后立即清除文件。作为 CNA，你需要了解文件和目录属性、它们的用途以及如何使用 NetWare 实用工具来处理属性。

### 文件和目录属性

设置在文件和目录上的属性会覆盖用户在该文件或目录中的有效权限。例如，如果文件被标记为只读（Read Only）属性，无论有效权限如何，你对该文件可以执行的唯一操作是读取（Read）和文件扫描（File Scan）。例如，Kari Means 对 Engineer 目录拥有所有权限，因此她将继承 Engineer 目录结构中文件和子目录的所有权限。如果 NASA 目录中名为 Partition.dat 的文件被标记为只读属性，即使 Kari 由于管理者分配而拥有所有有效权限，她对 Partition.dat 文件仍只有读取和文件扫描访问权限。然而，由于 Kari 由于对 Engineer 目录的管理者分配而继承了目录的修改（Modify）权限，她可以移除只读属性，然后更改甚至删除 Partition.dat 文件。

### 文件属性

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

**仅执行 (Execute Only (X))** 属性的主要用途是保护软件文件免受非法复制。只有具有管理员等价权限的用户才能在 .exe 和 .com 文件上设置仅执行属性；一旦设置，即使是网络管理员也无法移除。除非你有文件的备份副本，否则不要为文件分配仅执行属性。某些程序文件在被标记为仅执行时无法运行，因为这些程序

