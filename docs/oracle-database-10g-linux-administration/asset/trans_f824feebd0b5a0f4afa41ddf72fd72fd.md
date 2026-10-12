
- **512MB 物理内存** 这是 Oracle 数据库服务器正常运行所必需的；然而，这是一个最低要求。为了获得最佳运行效果，您确实应该拥有比这多得多的 RAM。

- **1GB 交换空间** 交换空间的大小通常设置为物理内存的两倍。对于 RAM 大于 2GB 的系统，交换空间的大小可在 RAM 的一到两倍范围内。您拥有的 RAM 越多，使用交换空间的可能性就越小。

- **/tmp 必须至少有 400MB 空间** 如果 /tmp 分区作为单独分区创建，则其大小必须至少为 400MB。如果 /tmp 目录是 /（根）文件系统的一部分，则除了您将用于其他用途的空间外，还必须至少有 400MB。

- **Oracle 文件空间** 您必须为最基本的 Oracle 安装分配至少 1.5GB 的空间。此数量根据您选择安装的组件而有所不同。

- **Oracle 数据文件** 为了安装基本示例数据库，您必须至少有 1.2GB 的空间。此空间可以位于文件系统、NFS 分区或 Oracle ASM（自动存储管理）磁盘组上。在 Oracle 10g RAC 环境中，此存储必须在集群中的所有节点之间共享。

这些要求应在创建 Linux 安装时予以考虑。重新构建分区以适应 Oracle 安装是相当痛苦的，并且所需的时间可能会使您的安装花费更长的时间。

## 配置文件系统

Linux 文件系统布局可以少至三个分区，也可以多到您想要的分区。Linux 配置的最低要求包括以下两个分区：

- **/, 根分区** 这是初始分区。所有其他分区都挂载在根分区的子目录上。

- **swap，交换分区** 交换分区不是作为常规文件系统挂载的，但 Linux 分区需要它才能运行。交换分区（或分区）必须根据前面列出的最低要求进行配置。

除了最小的文件系统要求外，您还可以为不同功能创建单独的分区。在安装过程中可能创建的典型分区包括以下内容：

| 分区 | 描述 |
|---|---|
| /home | /home 分区用于 Linux 用户账户的 home 目录。Oracle 用户账户在 /home 目录树中创建，但 $ORACLE_HOME 目录通常不存储在此处。 |
| /tmp | /tmp 分区用于临时文件。Oracle 在安装过程中使用此目录，操作系统在正常操作中也使用它。如果将其创建为单独分区，请确保其满足前面列出的最低要求。 |
| /usr | /usr 目录结构用于程序；然而，这不是 Oracle 程序所在的位置。Oracle 程序位于 $ORACLE_HOME 目录中，该目录通常位于 /opt 目录树中。 |
| /var | /var 目录结构用于可变长度文件，例如日志文件、打印 spool 文件等。 |
| /usr/local | /usr/local 目录树用于本地程序和配置文件。Oracle 使用此目录结构用于某些程序，但大部分 Oracle 程序位于 $ORACLE_HOME 目录树中。 |
| /opt | /opt 目录树用于可选程序。这是 $ORACLE_HOME 目录树通常所在的位置。此外，在某些系统上，Oracle 数据文件也可能存储在此目录树中。 |

配置系统时，请考虑前面列出的最低要求以及您自己的特定需求。如果您将创建 RAC 集群，请考虑 Oracle 数据文件的共享存储要求。

## 选择 Linux 组件

选择合适的 Linux 组件是规划操作系统安装的另一个重要部分。可以在初始安装后加载所需组件，但在此期间配置它们要容易得多。

自 Oracle 10g for Linux 首次发布以来，支持以下 Linux 发行版：

### Oracle 10g Release 1 (10.1.0)
- Red Hat Enterprise Linux 2.1 或 3.0
- SUSE Linux Enterprise Server 8.0 或 9.0 (SLES8 或 SLES9)

### Oracle 10g Release 2 (10.2.0)
- Red Hat Enterprise Linux EL 3 或 EL 4
- SUSE Linux Enterprise Server 9.0 (SLES9)

在这些 Linux 发行版中，首先需要安装软件开发包，以便安装 gcc 编译器和库。如果您可能需要升级 Linux 内核，还应安装内核开发包。建议将以下软件包包含在您选择安装的软件包列表中。

### Red Hat Linux 软件包

安装 Red Hat Linux 时，建议您除了默认软件包和您选择的任何其他软件包外，还安装以下软件包。这不是一个完整的列表，并不意味着不应安装其他软件包。

- **开发工具** 该软件包集包括 gcc 编译器、PERL、python 和调试器。
- **内核开发** 这对于安装 Oracle 并不是特别必需，但如果您将来需要更新 Linux 内核，则是必需的。

Oracle 10g 安装所需的最小组件集如下列出：

### Oracle 10g R1 的系统组件

| 系统 | 组件 |
|---|---|
| Red Hat 2.1 和 3.0 | make-3.79 |
| | binutils-2.11.90.0.8-12 |
| Red Hat Enterprise Linux 2.1 (x86) | gcc-2.96.108.1 |
| | openmotif-2.1.30-11 |
| Red Hat Enterprise Linux 3 | gcc-3.2.3-2 |
| | compat-db-4.0.14-5 |
| | compat-gcc-7.3-2.96.122 |
| | compat-gcc-c++-7.3-2.96.122 |
| | compat-libstdc++-7.3-2.96.122 |
| | compat-libstdc++-devel-7.3-2.96.122 |
| | openmotif-2.2.2-16 |
| | setarch-1.3-1 |

### Oracle 10g R2 的系统组件
- **系统**
  - Red Hat 2.1 和 3.0
  - Red Hat Enterprise Linux 2.1 (x86)
  - Red Hat Enterprise Linux 3
- **组件**
  - make-3.79
  - binutils-2.11.90.0.8-12
  - gcc-2.96.108.1
  - openmotif-2.1.30-11
  - make-3.79.1
  - gcc-3.2.3-34
  - glibc-2.3.2-95.20
  - compat-db-4.0.14-5
  - compat-gcc-7.3.2-96.128
  - compat-gcc-c++-7.3.2-96.128
  - compat-libstdc++-7.3.2-96.128
  - compat-libstdc++-devel-7.3.2-96.128
  - openmotif21-2.1.30-8
  - setarch-1.3-1

### SUSE Linux 软件包

安装 SUSE Linux 时，建议您除了默认软件包和您选择的任何其他软件包外，还安装以下软件包。这不是一个完整的列表，并不意味着不应安装其他软件包。

- **开发工具** 该软件包集包括 gcc 编译器、PERL、python 和调试器。
- **内核开发** 这对于安装 Oracle 并不是特别必需，但如果您将来需要更新 Linux 内核，则是必需的。

由于默认情况下安装了更多必需组件，SUSE Linux 的要求略低于 Red Hat Linux。以下组件是 Oracle 安装所必需的。Oracle 10g 安装所需的最小组件集是

### Oracle 10g R1
- gcc-3.2.2-38
- openmotif-2.2.2-124

### Oracle 10g R2
- gcc-3.3.3-43
- gcc-c++-3.3.3-43
- glibc-2.3.3-98
- libaio-0.3.98-18
- libaio-devel-0.3.98-18
- make-3.80
- openmotif-libs-2.2.2-519.1

## 摘要

只要您满足最低要求，Oracle 安装就会正确完成。如果未在系统上安装最低要求的软件包，安装过程中二进制文件重新链接的部分将失败。

## Linux 安装后程序

一旦您成功安装了 Linux 操作系统，就必须采取一系列步骤来为 Oracle 10g 安装做好准备。这些步骤包括添加 Oracle 用户和组账户、为 Oracle 程序和数据库文件创建目录、配置 Linux 内核参数以及设置环境变量。这些步骤对于正确安装 Oracle Database 10g 服务器是必要的。在接下来的几节中，您将看到如何执行这些任务。

## 配置内核参数

为了使 Oracle 数据库服务器正常运行，必须配置某些操作系统资源。这些资源默认设置为过低的水平，无法让 Oracle Database 10g 服务器启动并正常运行。幸运的是，Linux 操作系统允许动态更改这些参数，因此修改内核参数时无需重新启动。

有几种方法可以修改内核参数。可以通过修改 /proc 伪文件系统中的值来动态修改内核参数。回顾一下，/proc 文件系统包含内核系统性能和配置信息，以及更改内核参数的方法。

需要为 Linux 配置的参数涉及信号量、共享内存、最大打开文件数以及 IP 的端口范围。所有信号量参数都存在于 /proc/sys/kernel/sem 文件中，分别是 semmsl、semmns、semopm 和 semmni。必须满足以下最低值：

| 参数 | 值 | 描述 |
| :--- | :--- | :--- |
| semmsl | 250 | 每个 ID 的信号量最大数 |
| semmns | 32000 | 系统中的信号量最大数（必须大于或等于 semmni * semmsl） |
| semopm | 100 | 每次信号量调用的最大操作数 |
| semmni | 128 | 信号量标识符的最大数 |

