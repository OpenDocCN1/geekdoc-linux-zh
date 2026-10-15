

## 安装

本章指导您在 Linux 系统上安装 DB2 的过程。它涵盖单分区和多分区环境，并提供三种安装方法的说明：DB2 Setup、db2_install 和响应文件安装。

以下主题将被讨论：

- 基本要求
- 安装注意事项和规划
- 多分区安装注意事项
- 用户和组设置
- 安装 DB2

## 2.1 基本要求

在安装 DB2 之前，确保您拥有所需硬件和软件非常重要。您可能需要配置通信并安装额外的软件包，以便 DB2 能够成功运行。

在本节中，我们将介绍以下安装先决条件：

- DB2 支持的 Linux 发行版
- 所需磁盘空间
- 内存要求
- 通信要求
- 所需内核级别和库
- 额外软件要求

### 2.1.1 DB2 支持的 Linux 发行版

确保您的 Linux 发行版级别得到 DB2 支持。有关当前支持的 Linux 发行版、内核和库的最新信息，请参阅 DB2 for Linux 验证网站：

http://www-3.ibm.com/software/data/db2/linux/validate

在撰写本书时，以下 Linux 发行版已成功通过与 DB2 配合使用的验证（表 2-1）：

表 2-1 当前支持的 Linux 发行版、内核和库

| Platform | Distribution | Kernel | Libraries | Comments |
|---|---|---|---|---|
| IA 32 | Red Hat 7.2 | 2.4.9-34 | glibc 2.2.4 | |
|  | Red Hat 7.3 | 2.4.18 | glibc 2.2.5 | |
|  | Red Hat AS 2.1 | 2.4.9 | glibc 2.2.4 | |
|  | Red Hat 8.0 | 2.4.18-14 | glibc 2.2.93-5 | |
|  | SCO Linux 4.0 | 2.4.19 | glibc 2.2.5 | |
|  | SuSE 7.3 | 2.4.10 | glibc 2.2.4 | |
|  | SuSE Pro 6.0 | 2.4.18 | glibc 2.2.5 | |
|  | SuSE Pro 8.1 | 2.4.19 | glibc 2.2.5 | |
|  | SuSE SLES-7 | 2.4.7 | glibc 2.2.2 | |
|  | SuSE SLES-8 | 2.4.19 | glibc 2.2.5 | |
|  | TurboLinux Server 7 | 2.4.9 | glibc 2.2.4 | |
|  | TurboLinux Server 8 | 2.4.18-5 | glibc 2.2.5 | |
|  | United Linux 1.0 | 2.4.19 | glibc 2.2.5 | |
| IA 64 | SuSE SLES 8 | 2.4.19 | glibc 2.2.5 | |
|  | United Linux 1.0 | 2.4.19 | glibc 2.2.5 | |
| zSeries (32 bit) | Red Hat 7.2 | 2.4.9-38 | 2.2.4 | Run up2date to get the required kernel fixes from Red Hat |
|  | SuSE SLES 7 | 2.4.7-58 | 2.2.4 | SuSE refresh is required: SLES-7-PatchCD-1-s390-20020522.iso -- compat.rpm contains libstdc++ 6.1 |
|  | SuSE SLES 8 | 2.4.19 | 2.2.5 | |

## 2.1.2 所需磁盘空间

在配置分区时，您必须考虑以下磁盘要求（表 2-2）：

表 2-2 所需磁盘空间

| Install Type | Description | Required disk space |
|---|---|---|
| Typical | DB2 is installed with most features and functionality, including graphical tools such as the Control Center and Configuration Assistant. | 450 to 500 MB |
| Compact | Installs only basic DB2 features and functions and does not include graphical tools. | 350 to 400 MB |
| Custom | This option allows you to select the features you want to install. | 350 to 700 MB |

您还应为所需软件、通信产品、DB2 文档和数据库分配磁盘空间。在 DB2 Version 8 中，HTML 和 PDF 文档现在提供在单独的 CD-ROM 上。仅安装英文版核心 DB2 HTML 文档需要 25 MB 磁盘空间；仅安装英文版所有 HTML 文档需要 82 MB 磁盘空间。额外语言需要额外空间。

## 2.1.3 内存要求

我们建议您为 DB2 ESE 分配至少 256 MB 的 RAM，但应为其他软件和通信产品分配额外内存。在确定内存要求时，请注意以下事项：

- 我们建议您的 SWAP 空间至少是 RAM 的两倍。
- 应为可能在系统上运行的非 DB2 软件分配额外内存。
- 需要额外内存来支持数据库客户端和数据库活动。
- 内存要求将受数据库系统大小和复杂性以及特定性能要求的影响。

