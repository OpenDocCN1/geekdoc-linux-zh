
## Oracle Database 10g Linux 管理

这将调用一些检查，然后 Oracle 安装程序（Java 应用程序）将会出现。安装本身相当直接。当您调用 runInstaller 程序时，您会注意到在 Java 应用程序出现之前会进行一些检查，如图 6-1 所示。

这些检查包括以下内容：

- 确保操作系统是 Red Hat AS 2.1（Oracle 10g R1）、Red Hat AS 或 ES 3.0，或 SUSE Linux Enterprise Server 8.0（Oracle 10g R1）或 9.0。
- 确保至少有 80MB 的临时空间。
- 确保系统至少有 150MB 的交换空间。
- 确保 X Windows 环境至少支持 256 种颜色。

如果您在测试机器上运行并且未满足所有要求，您可以通过使用 IgnoreSysPreReqs 标志来绕过先决条件检查，如下所示：

```
# /oracle_stage/db_Disk1/runInstaller -ignoreSysPreReqs
```

仅应在测试系统上绕过先决条件检查，而不应在生产系统上进行。一旦完成检查或绕过检查，Java 应用程序将被调用，您应该会在屏幕上看到 Oracle 安装程序，如图 6-2 所示。

![](img/9479df2d00f5e62b87366b125224950f_185_0.png)

**图 6-1.** 启动 Oracle 安装程序

![](img/9479df2d00f5e62b87366b125224950f_186_0.png)

图 6-2. Oracle 通用安装程序

需要若干步骤才能在系统上安装 Oracle 软件。出现的屏幕将提示您做出各种决策。安装过程中您应注意以下几点：

- 操作系统组应被识别为 install。
- 在文件位置屏幕中
- 源文件位置应在您创建的暂存目录下的 stage 目录中。在我们的示例中，源路径应为 /oracle_stage/db_Disk1/stage/products.xml。
- 路径应指向 oracle_base 下的子目录。这看起来像 /opt/oracle/product/10.1.0/db_1，其中 oracle_base 为 /opt/oracle。
- 继续之前应成功完成产品先决条件检查。如果有任何错误，请更正并重试测试。
- 正确设置 Oracle 数据库名称和 SID。它应已从环境变量中获取 oracle_sid。
- 正确设置字符集。这以后很难更改。
- 设置数据库管理选项。在这里您可以选择允许使用 Grid Control 进行数据库管理的新功能。
- 设置数据库文件存储选项。在这里您可以选择使用文件系统、ASM 或原始设备来存储 Oracle 数据库文件（如果安装过程中创建数据库）。
- 设置备份和恢复选项。Oracle 10g 中的新功能是可以安排自动备份。您可以在安装过程中选择这样做，也可以稍后设置。
- 安装完成后，请注意报告的 Ultra Search、Ultra Search Administration Tool 和 iSQL*Plus 的 URL。通常包括
  - **Ultra Search** http://systemname:5620/ultrasearch
  - **The Ultra Search Administration Tool** http://systemname:5620/ultrasearch/admin
  - **iSQL*Plus** http://systemname:5560/isqlplus
  - **The Enterprise Manager database control** http://systemname:5500/em

安装完成后，需要执行一些安装后任务，如下一节所述。

## 安装后步骤

在开始使用新安装的 Oracle 10g 数据库服务器之前，必须执行一些安装后任务。这些任务包括

- 下载并安装补丁
- 配置 Oracle 产品
- 测试和验证

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

Oracle 建议运行 SQL 脚本 utlrp.sql 以重新编译可能无效的所有 PL/SQL 模块。这可以通过设置 Oracle 环境并连接到 SQL*Plus 来实现，如下所示：

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

一旦您已连接到 Oracle Database 10g 服务器，请运行 utlrp.sql 脚本（假设数据库服务器正在运行）。

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

由于客户端静态库不会作为 Oracle 安装过程的一部分创建，因此必须独立完成。要创建 libclnt10.a，请按照以下步骤操作：

```
[oracle@ptc6 oracle]$ $ORACLE_HOME/bin/genclntst
Created  /opt/oracle/product/10.1.0/db_1/lib/libclnt10.a
```

此过程假定 *oracle_home* 环境变量已设置。如果没有，您需要设置它或使用实际路径名。

## 设置 Oracle Net

另一项重要任务是设置 Oracle Net，以便 Oracle 客户端系统可以访问您的数据库服务器。可以通过编辑以下文件来配置 Oracle Net。

- 监听器文件 $ORACLE_HOME/network/admin/listener.ora
- 名称文件 $ORACLE_HOME/network/admin/tnsnames.ora

除了手动编辑网络配置文件外，还可以使用图形化 Net Configuration Assistant 或 netca 来配置网络。netca 是通过运行程序 $ORACLE_HOME/bin/netca 调用的。然后您将看到如图 6-3 所示的 Java 应用程序。

网络配置完成后，您就可以开始测试了。

![](img/9479df2d00f5e62b87366b125224950f_190_0.png)

**图 6-3.** *Oracle Net 配置助手*

