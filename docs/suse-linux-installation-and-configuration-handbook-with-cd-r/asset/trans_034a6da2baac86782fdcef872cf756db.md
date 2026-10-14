

此脚本的输出应如下所示：

```
Creating Oracle Inventory pointer file (/etc/orainst.loc)
Changing groupname of /opt/oracle/orainventory to oinstall.
```

换句话说，该脚本已在 /etc 目录中创建了一个文件，其中包含 Oracle Inventory 的路径。它还授予 oinstall 组对 /opt/oracle/orainventory 目录中 Oracle Inventory 的控制权限。运行脚本后，返回 OUI 并按 Retry。

## Oracle Products

接下来出现的 Available Products 对话框询问您要安装哪个 Oracle 产品（见图 30.3）。Oracle CD 包含三种产品：

- Oracle Enterprise Edition
- Oracle Client
- Oracle Programmer

FIGURE 30.3
您可以通过单击相应的单选按钮然后单击 Next 来选择要安装的产品。

![](img/659f91d9da7b29976c0625e2e9628511_605_0.png)

本章主要讨论安装 Oracle Enterprise Edition。您仍可通过选择产品并单击 Next 来安装 CD 上的其他产品。在我们的例子中，我们选择了 Oracle Enterprise Edition 并单击了 Next。

## Installation Types

下一步是选择安装类型。您必须选择是要进行 Typical、Minimal 还是 Custom 安装。每个安装类型的简短说明显示在其下方，如图 30.4 所示。

> NOTE Oracle 建议您选择 Custom 安装，因为 Typical 和 Minimal 安装类型中存在一些错误。

### FIGURE 30.4

OUI 为 Oracle Enterprise Edition 提供三种安装类型。您必须选择希望使用哪种方法安装产品。

![](img/659f91d9da7b29976c0625e2e9628511_606_0.png)

## Creating a Database

选择 Custom 安装后，OUI 建议您创建一个新数据库。单击 Yes 以创建新数据库并填写随后的 Database Identification 对话框。您可以保留 Database Identification 的默认值，也可以根据自己的喜好更改它们（见图 30.5）。下一个问题是数据库文件的位置。您可以使用 browse 选择一个目录来存储数据库文件。Oracle 标准建议您使用其他磁盘上的目录以获得最佳性能。使用您之前在 /u02、/u03 和 /u04 上创建的挂载点作为存储数据库文件的位置。

### FIGURE 30.5

OUI 提供创建数据库的功能。您可以使用 Database Identification 对话框更改此数据库的属性。

![](img/659f91d9da7b29976c0625e2e9628511_606_1.png)

## Creating a Database During the Installation

OUI 使您能够在安装期间创建数据库。在此过程中，您将填写此数据库的标识以及数据库文件的位置。数据库文件的位置是数据库的挂载点。Oracle 建议的标准挂载点为 /u02、/u03 等。Oracle 建议您将数据库文件保存在系统硬盘以外的硬盘上。

## Network Protocols

现在，您需要选择在使用 Oracle 服务器时要使用的网络协议。您可以在 OUI 提供的列表中选择在使用 Oracle 服务器时要使用的网络接口。如果不存在任何接口，您可能需要购买完整的 Oracle 发行版或检查 Oracle 更新。

## Installation Summary

下一步是安装摘要。这是您最后一次返回并进行任何修改的机会。单击 Next 按钮并等待安装完成。安装可能需要相当长的时间，具体取决于您选择的选项以及机器的配置和负载。在 PI 300、128 RAM 上的中等安装可能需要长达 50 分钟。换句话说，除了观看进度条之外，您还可以做很多其他事情！

> NOTE Oracle 安装过程在安装期间重新链接多个二进制文件；这会导致 CPU 在相当长一段时间内使用率非常高。如果您计划在不久后进行一些实际工作，请考虑稍后再开始安装。

## Post-Installing Oracle 8.1.5 EE|STD on SuSE Linux 6.3/6.2

即使您已完成 Oracle 的安装，仍有一些其他事情需要完成。当安装过程完成后，OUI 会生成一个名为 root.sh 的文件，该文件为您安装的所有文件设置正确的权限。在开始使用 Oracle 之前应执行此文件。以 root 身份登录并执行以下命令：

```
#cd $ORACLE_HOME
#./root.sh
```

## Automating Database Startup and Shutdown (Version 6.2 and 6.3)

这是本章最简单的一部分。您只需按照以下步骤操作：

- 1. 编辑 /etc/rc.config。
- 2. 搜索 START_ORACLE="no" 并将其更改为 "yes"。
- 3. 搜索 ORA_HOME="" 并将其更改为 $ORACLE_HOME 的正确值。
- 4. 保存您的文件。

第二个需要编辑的文件是 /etc/oratab。编辑此文件并将 ORACLE_SID:ORACLE_HOME:N 的值更改为 ORACLE_SID:ORACLE_HOME:Y。

现在，下次启动系统时，Oracle 将在运行级别 2 - console - 和 3 - xdm 或 kdm 时自动启动。

## Configuration of SQL*Plus

数据库管理员必须掌握 SQL*Plus。SQL*Plus 提供数据定义、数据操作和数据库管理命令。虽然它可以用作基本的数据库接口，但其主要用途应该是设置数据库和数据库用户的权限。要掌握 SQL*Plus，您必须掌握 SQL 语言。

## SQL*Plus Configuration Files

SQL*Plus 的配置文件位于 $ORACLE_HOME/sqlplus/admin/glogin.sql 和用户的主目录 ($HOME/login.sql)。前者被称为全局 SQL*Plus 配置文件，是 SQL*Plus 启动时首先读取的文件，而后者其次读取。这两个文件包含 SQL*Plus 的设置。

CAUTION

用户配置文件 (login.sql) 应保存在用户的主目录中。在两种情况下会出现问题：

- 如果当前目录中存在名为 login.sql 的文件，它将被用于代替主目录中的文件。
- 如果环境变量 SQLPATH 具有一个路径，其中主目录排在最后，并且存在一个其中包含文件的目录，它将被用于代替主目录中的文件。

## Basics of Oracle on Linux

数据库管理员的负担相当重。管理员负责管理用户、数据库、安全性和系统负载。这主要通过 SQL 和一些众所周知的参数来完成。管理大型 Oracle 数据库可以被视为一门艺术和一门科学。我们不会深入讨论管理 Oracle 数据库的细节，因为这超出了本书的范围。但是，您可能希望查看随完整商业 Oracle 包提供的参考资料。本节将讨论一些新手管理员的重要注意事项。

## Who Is Who?

许多新 Oracle 管理员的一个大问题是“我们刚刚创建的那些用户是谁？”创建的 Oracle 数据库的主要用户属于 DBA 组。这些用户对数据库具有管理控制权。任何普通 Linux 用户都可以属于 DBA 组。因此，一个用户可以是普通系统用户，同时也是数据库管理员。请注意！

> CAUTION
> 您必须小心谁属于 DBA 组。用户可以是普通系统用户，但通过成为 DBA 组的成员，她也可以成为数据库管理员。

## Database Users

在大多数情况下，用户应使用您首先创建的 oracle 用户登录。通过使用应用程序或 SQL*Plus 连接到数据库，用户将识别其 Oracle 用户名和密码。

## Troubleshooting Oracle

我无法以用户 oracle 登录到 Linux（SuSE 6.3）。

在 SuSE 6.3 中，用户 oracle 已存在并属于正确的组。此用户的密码默认情况下是禁用的。您可以按照以下步骤将其更改为您想要的任何值：

- 1. 以 root 登录。
- 2. 发出命令 passwd oracle。
- 3. 将密码更改为您想要的值。在安装期间不要将其留空——这可能会在以后威胁到您的数据库安全。

我由于某种原因无法启动安装。

此问题可能由许多原因引起，例如以下：

- 您是否完全按照本章中所述的程序进行操作？
- 检查系统库的依赖关系。
- 检查系统上的 Java 安装。OUI 基于 Java，因此您可能必须卸载系统上已安装的 Java。然后，您将必须安装随附 CD 上提供的 Java 或 SuSE ftp 站点上的 Java。

