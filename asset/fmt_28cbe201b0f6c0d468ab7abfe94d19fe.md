
在将数据库投入生产之前，完成这些步骤非常重要。

## 下载和安装补丁

Oracle 产品的补丁可以在 Oracle MetaLink 网站 http://metalink.oracle.com 上找到。在那里，单击 Patches 并搜索您系统上已安装的 Oracle 产品或产品的补丁。每个补丁都应进行评估，如果您选择，可以在系统上安装。安装这些补丁所需的步骤随 Oracle 产品补丁集提供，并根据补丁而有所不同。

## 配置步骤

配置步骤可能取决于您的安装而不需要或需要。您可能需要执行的一些配置步骤包括以下内容：

- 备份 Oracle 数据库和二进制文件
- 配置和调优数据库
- 添加用户账户
- 生成客户端静态库

是否需要这些步骤取决于您的配置和需求。

### 记录系统

在继续之前，您应记录系统的配置方式以及如何执行 Oracle 安装。如果系统将来需要重新安装，文档可能是他人了解设置方式的唯一途径。

### 备份 Oracle 数据库和二进制文件

原始配置完成后，应备份 Oracle 二进制文件和配置文件。这使您在将来出现问题时能够将事物恢复到之前的状态。稍后，您将集中精力制定备份 Oracle 数据库本身的计划。

### Oracle 实例的初始调优

安装过程使用默认的 Oracle 参数。安装数据库并使其运行后，您需要调优 Oracle 实例以使其能够按要求执行。

### 配置数据库

希望您已创建数据库并对其外观有想法。例如，创建后，您可能需要添加更多表空间以准备导入生产数据。

160 Oracle Database 10g Linux 管理

## 重新编译无效的 PL/SQL 模块

Oracle 建议运行 SQL 脚本 `utlrp.sql` 以重新编译可能无效的所有 PL/SQL 模块。这可以通过设置 Oracle 环境并连接到 SQL*Plus 来实现，如下所示：

```
[oracle@ptc6 oracle]$ . /usr/local/bin/oraenv
ORACLE_SID = [orac]?  
[oracle@ptc6 oracle]$ sqlplus "/ as sysdba"
```

```
SQL*Plus: Release 10.1.0.2.0 - Production on Sun Apr 4 14:58:24 2004
Copyright (c) 1982, 2004, Oracle. All rights reserved.

Connected to:
Oracle Database 10g Enterprise Edition Release 10.1.0.2.0 - Production
With the Partitioning, OLAP and Data Mining options
```

一旦您已连接到 Oracle Database 10g 服务器，请运行 `utlrp.sql` 脚本（假设数据库服务器正在运行）。

```
SQL> @?/rdbms/admin/utlrp.sql
TIMESTAMP
----------------------------
COMP_TIMESTAMP UTLRP_BGN 2004-04-04 14:59:14

PL/SQL procedure successfully completed.

TIMESTAMP
----------------------------
COMP_TIMESTAMP UTLRP_END 2004-04-04 14:59:15

PL/SQL procedure successfully completed.

PL/SQL procedure successfully completed.
```

## 生成客户端静态库

由于客户端静态库不会作为 Oracle 安装过程的一部分创建，因此必须独立完成。要创建 `libclnt10.a`，请按照以下步骤操作：

```
[oracle@ptc6 oracle]$ $ORACLE_HOME/bin/genclntst
Created  /opt/oracle/product/10.1.0/db_1/lib/libclnt10.a
```

此过程假定 `oracle_home` 环境变量已设置。如果没有，您需要设置它或使用实际路径名。

## 设置 Oracle Net

另一项重要任务是设置 Oracle Net，以便 Oracle 客户端系统可以访问您的数据库服务器。可以通过编辑以下文件来配置 Oracle Net。

- 监听器文件 `$ORACLE_HOME/network/admin/listener.ora`
- 名称文件 `$ORACLE_HOME/network/admin/tnsnames.ora`

除了手动编辑网络配置文件外，还可以使用图形化 Net Configuration Assistant 或 `netca` 来配置网络。`netca` 是通过运行程序 `$ORACLE_HOME/bin/netca` 调用的。然后您将看到如图 6-3 所示的 Java 应用程序。

网络配置完成后，您就可以开始测试了。

![](img/9479df2d00f5e62b87366b125224950f_190_0.png)

图 6-3. Oracle Net 配置助手

## 测试和验证

在将任何系统或新的数据库软件投入生产之前，应对其进行彻底的测试阶段。测试数据库服务器有多种方法。这可以简单到验证您的应用程序是否返回正确的数据，也可以涉及更复杂的程序，例如使用企业级负载测试软件进行负载测试。您测试的内容和方式将取决于您的需求。

## 其他杂项配置步骤

根据您的配置和要求，您可能需要配置或安装其他组件，可能包括以下内容：

- 安装 Java 库
- 安装 Oracle Text 提供的知识库
- 配置 Oracle 消息网关
- 配置 Oracle 预编译器
- 安装随附光盘上的产品

安装和配置这些产品在 Oracle 安装文档中有详细说明。

## 摘要

本章介绍了安装和设置 Oracle Database 10g 服务器存储所需的任务。在接下来的几章中，您将学习使用 Oracle 10g RAC 集群的变体，它允许多个 Oracle 实例访问同一数据库，从而同时提供可扩展性和容错能力。

本章的开头部分重点介绍了为 Oracle Database 10g 服务器设置存储。这是一项非常重要的任务，必须在创建任何数据库之前完成。在这里您了解了 Oracle 使用的三种不同的存储方法：文件系统文件、ASM 和原始分区。您使用哪一种方法很可能取决于您的经验、技能、偏好以及个人需求。

Oracle Universal Installer 已得到改进，使用起来非常容易。安装和安装后任务完成后，您应该准备好继续设置和配置生产数据库。与任何产品一样，注重细节是成功在 Linux 上安装 Oracle 10g 的关键。

![](img/9479df2d00f5e62b87366b125224950f_192_0.png)

## PART

## III

Linux 上的 Oracle RAC

![](img/9479df2d00f5e62b87366b125224950f_194_0.png)

## 第 7 章

## Oracle Real Application Cluster 概念

## Oracle Database 10g Linux 管理

对于大多数关键任务系统而言，需要高可用性计算。如果关键任务系统数天甚至数小时不可用，您的公司可能会损失数千甚至数百万美元。许多关键任务系统无法容忍数据库不可用的哪怕少量停机时间。

今天有许多解决方案可用于提高正常运行时间并减少系统中断。其中包括：Oracle RAC、Oracle Data Guard 以及其他第三方实用程序。Oracle RAC 和 Oracle Data Guard 都是 Oracle 最大可用性架构 `MAA` 的一部分。`MAA` 将多个高可用性、容错和灾难恢复解决方案结合在一起，以提供专为最大可用性而设计的系统。

当今的关键任务系统要求高水平的可用性。任何停机时间，即使只有几分钟，也可能代价高昂。停机成本可能体现在因销售损失而减少的收入中，这可以立即衡量，或体现在客户流失中，这很难衡量。这笔费用可能高达数千甚至数百万美元。公司关键系统停机数小时或数天的情况并不罕见。

通过精心设计系统并利用 Oracle RAC 和 Data Guard 等高可用性功能，您可以提高系统的可用性。为系统设计最大可用性的概念在 Oracle 最大可用性架构 `MAA` 中有所概述。`MAA` 将多个高可用性、容错和灾难恢复解决方案结合在一起，以提供专为最大可用性而设计的系统。

> 注意
