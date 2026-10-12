
### How you can accommodate application interdependencies in a LinuxONE environment

### How you can redesign your application to take advantage of the strengths of the Linux platform

#### 5.3.1 Why migrate applications

Only perform application migration after thorough planning. You also need a compelling reason to act, such as the following real world situations:

- An existing application has outgrown its original platform and is close to reaching the architectural limits of the platform.
- Software license costs are rapidly increasing as servers are added to an application.
- Performance issues are arising between distributed application servers and centralized databases.
- Uncontrolled distributed server growth is leading to power and cooling issues in the data center.
- Complex distributed systems, which are costly to maintain, are suffering from increasing unreliability.
- New application development is required following a merger or acquisition.
- Regulatory requirements impose the need for a more secure environment.

Such situations present valid reasons for considering a migration to a more efficient platform like IBM LinuxONE. In cases, a migration to LinuxONE will help an organization realize significant cost savings over three to five years. Which applications can you migrate and what risks are associated with the migration?

The output of this exercise is a list of an organization's applications ordered by complexity. The list is based on factors such as the number of servers or applications that make up the "IT systems", and can be grouped as large, medium, or small applications or number of servers.

文件系统的大小取决于运行的应用程序的数量和类型，以及日志文件在服务器上保存的时间。此外，还要考虑应用程序是否被设计为在此写入文件，以及这些文件的大小和频率。

服务控制也放置在 `/var` 文件系统上，因此它永远无法扩展为共享文件系统，并且必须始终保持读/写状态。

由于它是一个动态文件系统，请将其放置在 LVM 设备上，以便根据需要进行扩展或缩小。

### /tmp 文件系统

`/tmp` 文件系统最初设计用于存储操作系统文件和临时应用程序文件。这些文件在每次系统重启时都会被删除，或者在文件不再被使用后由应用程序立即删除。一些自制应用程序使用 `/tmp` 文件系统作为转储区或交换文件资源。在少数情况下，需要增加 `/tmp` 的大小。

由于它是一个动态文件系统，请将其放置在 LVM 设备上，以便根据需要具备扩展或缩小的能力。

### /opt 文件系统

将所有第三方应用程序部署在 `/opt` 文件系统中。作为首选实践，根据开发该应用程序或软件的公司或组织对 `/opt` 目录进行进一步组织。下一级目录指定了安装的软件包。例如，在 `/opt/ibm/db2` 安装适用于 Linux 的 DB2 节点。将 WebSphere 应用程序放置在 `/opt/ibm/websphere` 目录。

文件系统的大小取决于将安装在其中的软件包的大小。估计单个软件包的需求是容易的。然而，升级、维护和额外的软件包在计划起来并不那么容易。`/opt` 文件系统也可以是一个动态文件系统，并应该配置在 LVM 设备上。

### /home 文件系统

`/home` 文件系统设计用于分配用户文件。文件系统的大小取决于服务器的功能和定义的的用户数量。例如，应用程序生产环境服务器不需要 `/home` 文件系统，因为开发人员将把文件存储在生产服务器上。然而，预计应用程序将在开发应用服务器上进行开发，因此开发人员需要足够的文件系统空间来创建和传输他们的文件。

根据情况，`/home` 文件系统可以是一个动态文件系统。如果是动态的，请将其配置在 LVM 设备上。

### 其他文件系统

在迁移过程中，可能会在特定服务器上创建的额外文件系统的示例是数据库服务器文件。基本上，你至少需要一个用于文件数据的文件系统和一个用于日志文件的文件系统。因此，除了安装应用程序二进制文件的文件系统外，必须至少创建两个文件系统。对于 IBM DB2 数据库服务器，二进制文件的默认位置是 `/opt/ibm/db2`。

其他数据库管理系统将数据存放在其他目录。例如，MySQL 数据库服务器数据文件的默认位置是 `/var/lib/mysql` 目录。如果服务器是 MySQL 数据库服务器且你正在使用 Red Hat 或 SUSE Linux 发行版，考虑在 `/var/lib/mysql` 挂载点包含一个新的文件系统。

第 5 章 迁移分析 73

对于每个目标数据库管理服务器，确保你知道二进制文件和数据文件的位置。只有通过这些信息，你就可以为目标系统规划设备和文件。

取决于你在所在地安装的 Linux 发行版，文件位置可能会差异。确保你了解这些差异（如果有），并为此制定计划。

### 附加资源

有关更多建议（例如卷组和磁盘命名规范），请参见 *Set up Linux on IBM z for Production, SG24-8137*。

### 共享文件系统

LinuxONE 环境中的数据存储可以由一个或多个 Linux 虚拟机进行物理共享。然而，由于文件系统的限制，两个 Linux 虚拟机无法同时对设备具有读/写控制。然而，这种配置在硬件层面可能是可能的。

### 5.3.2 哪些应用程序可以迁移

每个计算平台都提供特定的优势领域，迁移的目标应该是选择能够利用目标平台优势的应用程序。IBM LinuxONE 的优势包括高可用性、高 I/O 带宽能力、并发运行异构负载的灵活性，以及卓越的灾难恢复能力。

选择合适的迁移应用程序的另一个关键要素是它们是否在 LinuxONE 上支持。对于自有的应用程序，这种考虑通常不是问题，取决于它们的编写语言。此外，LinuxONE 平台上还有大量的开源应用程序可供。

### 5.3.3 选择迁移到 LinuxONE 的基本规则

本节列出并描述了选择应用程序迁移到 LinuxONE的基本规则。

以下列表包含了不能或不宜迁移到 LinuxONE 的应用程序：

- 仅在 Intel 或 UNIX 平台上提供的应用程序。
- 请求 ISV（独立软件供应商）在 LinuxONE 上支持其应用程序是一个漫长的过程。
- 已经虚拟化的服务器。

在这种情况下，虚拟化的大部分总拥有成本（TCO）效益已经实现，只能获得微小的收益。然而，如果现有的虚拟环境达到极限，或者服务器租用期在 9 到 12 个月内到，那么由于 LinuxONE 更高的虚拟化能力，将应用程序迁移到 LinuxONE 可能是一个很好的业务案例。

以下列表包含了适合迁移的应用程序及其适用性原因：
