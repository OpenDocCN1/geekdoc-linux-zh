

# DB2 Tools Catalog 创建

本附录提供了手动创建 DB2 Tools Catalog 的示例以及与 Tool Catalog 创建相关的信息。此外，此处还简要介绍了通知设置。

如果您在安装 DB2 时未创建工具目录，可以使用 DB2 Control Center 或命令行处理器创建。如果使用 DB2 Control Center，则在调用 DB2 Control Center 后，可以选择 Tools --> Tools Settings --> Scheduler Settings，并创建一个新的 Tools Catalog。

这里我们提供了使用 DB2 CLP 手动创建 Tools Catalog 的示例，同时还包括在创建 Tools Catalog 之前和之后检查 DAS 配置变化的步骤，以及 CREATE TOOLS CATALOG 命令自动创建的新表空间和缓冲池。

在创建 Tools Catalog 之前，我们使用 GET ADMIN CFG 获取 DAS 的当前配置，如示例 B-1 所示。您可以看到，与 Tools Catalog 相关的一些参数目前为空，包括 TOOLSCAT_DB、TOOLSCAT_INST TOOLSCAT_SCHEMA。我们将使用此信息在稍后比较 CREATE TOOLS CATALOG 命令所做的 DAS 配置更改。

## 示例：B-1 检查当前 DAS 配置

```
db2inst1@UDBLNX08:~> db2 get admin cfg

Admin Server Configuration

Authentication Type DAS                 (AUTHENTICATION) = SERVER_ENCRYPT

DAS Administration Authority Group Name (DASADM_GROUP) = dasadm1

DAS Discovery Mode                      (DISCOVER) = SEARCH
Name of the DB2 Server System           (DB2SYSTEM) = UDBLNX08

Java Development Kit Installation Path DAS (JDK_PATH) = /opt/IBMJava2-131

DAS Code Page                           (DAS_CODEPAGE) = 0
DAS Territory                           (DAS_TERRITORY) = 0

Location of Contact List                (CONTACT_HOST) =
Execute Expired Tasks                   (EXEC_EXP_TASK) = NO
Scheduler Mode                          (SCHED_ENABLE) = OFF
SMTP Server                             (SMTP_SERVER) =
Tools Catalog Database                  (TOOLSCAT_DB) =
Tools Catalog Database Instance         (TOOLSCAT_INST) =
Tools Catalog Database Schema           (TOOLSCAT_SCHEMA) =
Scheduler User ID                       =
```

然后我们按示例 B-2 使用 CLP 创建 Tools Catalog。

## 示例：B-2 使用 CLP 创建 Tools Catalog

```
db2inst1@UDBLNX08:~> db2 "create database toolscat"
DB20000I  The CREATE DATABASE command completed successfully.
db2inst1@UDBLNX08:~> db2 "create tools catalog esecat0 use existing database toolscat"
DB20000I  The CREATE TOOLS CATALOG command completed successfully.
```

在前面的示例中，如果您愿意，可以直接通过 CREATE TOOLS CATALOG 命令使用 CREATE NEW DATABASE 参数创建新数据库（此处为 TOOLSCAT）；有关 CREATE TOOLS CATALOG 命令语法的详细信息，请参阅 IBM DB2 UDB Command Reference V8，SC09-4828。

然后您可以再次检查 DAS 配置参数，您可能会发现与 Tools Catalog 相关的参数已自动更改。

## 示例：B-3 DAS Tools Catalog 参数自动更改

```
db2inst1@UDBLNX08:~> db2 get admin cfg

    Admin Server Configuration

Authentication Type DAS                 (AUTHENTICATION) = SERVER_ENCRYPT

DAS Administration Authority Group Name (DASADM_GROUP) = dasadm1

DAS Discovery Mode                      (DISCOVER) = SEARCH
Name of the DB2 Server System           (DB2SYSTEM) = UDBLNX08

Java Development Kit Installation Path DAS (JDK_PATH) = /opt/IBMJava2-131

DAS Code Page                           (DAS_CODEPAGE) = 0
DAS Territory                           (DAS_TERRITORY) = 0

Location of Contact List                (CONTACT_HOST) =
Execute Expired Tasks                   (EXEC_EXP_TASK) = NO
Scheduler Mode                          (SCHED_ENABLE) = ON
SMTP Server                             (SMTP_SERVER) =
Tools Catalog Database                  (TOOLSCAT_DB) = TOOLSCAT
Tools Catalog Database Instance         (TOOLSCAT_INST) = db2inst1
Tools Catalog Database Schema           (TOOLSCAT_SCHEMA) = ESECAT0
Scheduler User ID                       =
```

除了自动的 DAS 参数更改外，在 Tools Catalog 数据库中，还创建了一系列新表，其模式名称由 TOOLSCAT_SCHEMA 指定，此处为 ESECAT0。并且创建了两个新的表空间，其中一个

