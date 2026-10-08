

## 用户配置：.my.cnf

访问数据库服务器的用户在其主目录中会有自己的配置文件：**my.cnf**。在此，用户可以指定连接选项，例如访问数据库所使用的密码和连接超时时间。

```plaintext
[client]
password=mypassword

[mysql]
no-auto-rehash
set-variable = connect_timeout=2

[mysql-hotcopy]
interactive-timeout
```

## 启动和停止 MySQL 服务器

MySQL 服务器，**mysqld**，可以通过 `service` 命令或 `services` 工具进行管理。

```bash
service mysqld start
```

**mysqld** 脚本会调用 **safe_mysqld**，后者旨在在 Unix 系统上运行 MySQL，确保数据目录已设置且日志文件正在运行。**safe_mysqld** 脚本进而会启动 **mysqld** 守护进程。

## MySQL 工具

MySQL 提供了多种工具（如表 26-8 所示），包括服务器、客户端和管理工具。可以使用 **mysqldump** 命令处理备份。**mysqlshow** 命令可以显示数据库，效果类似于执行 SQL 命令 `SELECT *.*`，而 **mysqlimport** 可以导入文本文件，类似于 `LOAD INFILE`。

## 使用 mysql 和 mysqladmin 管理 MySQL

要管理您的 MySQL 数据库，您需要以 **root** 用户身份使用 **mysql**。**mysql** 客户端会启动 MySQL 监控器。作为 **root** 用户，您可以输入管理命令来创建数据库和数据库表，添加或删除条目，以及执行显示数据等标准客户端任务。

**表 26-8** MySQL 命令

| 命令 | 描述 |
| :--- | :--- |
| **mysqld** | MySQL 服务器 |
| **mysql** | MySQL 客户端 |
| **mysqladmin** | 创建和管理数据库 |
| **mysqldump** | 数据库备份 |
| **mysqlimport** | 导入文本文件 |
| **mysqlshow** | 显示数据库 |

以 root 用户身份登录并打开一个终端窗口。然后输入 `mysql` 命令。这将启动带有 `mysql>` 提示符的 MySQL 监控器 shell。请务必在命令末尾加上分号；否则，监控器会提供一个缩进箭头提示符，等待额外的参数。在监控器中，结束命令的是分号，而不是 ENTER 键。

```bash
# mysql -u root -p
mysql>
```

如果您已设置了 MySQL root 用户，您可以使用 `-u root` 配合 `-p` 选项。系统会提示您输入密码。

```bash
# mysql -u root -p
```

一旦 `mysql` 客户端启动，您可以使用 `status` 命令检查服务器状态，并使用 `show databases` 列出当前数据库。

```bash
mysql> status;
mysql> show databases;
```

最初会显示两个由 MySQL 为其自身管理而设置的数据库：`mysql` 和 `test`。`mysql` 数据库保存 MySQL 用户信息，而 `test` 数据库用于测试服务器。

## PostgreSQL

PostgreSQL 基于 POSTGRES 数据库管理系统，尽管它使用 SQL 作为查询语言。POSTGRES 是在加利福尼亚大学伯克利分校开发的下一代研究原型。您可以从 PostgreSQL 网站 [www.postgresql.org](http://www.postgresql.org) 获取更多信息。PostgreSQL 是一个开源项目，在 GPL 许可证下开发。

PostgreSQL 通常用于为具有高负载需求的互联网服务器（如 Web 服务器）提供数据库支持。使用几个简单的命令，您就可以创建关系数据库表。使用 `createuser` 命令创建 PostgreSQL 用户，然后您可以使用该用户登录到服务器。接下来，您可以使用 `createdb` 命令创建数据库，并使用 `create table` 指令构建关系表。通过 `insert` 命令，您可以添加记录，然后使用 `select` 命令查看它们。远程用户对服务器的访问由位于 PostgreSQL 目录（通常是 `/var/lib/pgsql`）中的 `pg_hba.conf` 文件中的条目控制。

Red Hat Linux 版本的 PostgreSQL 还包含用于轻松管理和访问 PostgreSQL 数据库的 Red Hat 数据库图形工具。使用管理员工具，您可以浏览和管理数据库；Visual Explain 工具分析查询过程；控制中心允许您管理服务器上的数据库。

## 第六部分

# 系统管理

- **第 27 章** 基本系统管理
- **第 28 章** 用户管理
- **第 29 章** 软件管理
- **第 30 章** 文件系统管理
- **第 31 章** RAID 和 LVM
- **第 32 章** 设备和模块：udev、HAL 和 MAKEDEV
- **第 33 章** 内核管理：虚拟化
- **第 34 章** 备份管理：rsync、Amanda 和 dump/restore

## 27

# 基本系统管理

Linux 旨在同时服务多个用户，在用户和系统资源、服务和设备之间提供接口。用户拥有自己的 shell，通过它与操作系统进行交互，但您可能需要以不同方式配置操作系统本身。您可能需要添加新用户、打印机和扫描仪等设备，甚至文件系统。此类操作属于系统管理范畴。执行此类操作的人被称为*系统管理员*或*超级用户*。在这个意义上，与 Linux 的交互有两种类型：普通用户的交互，以及执行系统管理任务的超级用户的交互。本书中的章节涵盖更改系统运行级别、管理用户、配置打印机、添加文件系统以及编译内核等操作。大多数任务您很少执行，例如添加新打印机或挂载文件系统。其他任务，例如添加或删除用户，您是定期执行的。基本系统管理涵盖的主题包括超级用户系统访问、选择启动的运行级别、系统配置文件以及性能监控。

使用 Linux，您可以加载不同版本的 Linux 内核以及您安装在系统上的其他操作系统。选择并启动操作系统或内核的任务由引导管理实用程序 Grand Unified Bootloader (GRUB) 管理。这是一个多功能工具，允许您加载共享相同磁盘驱动器的操作系统，并允许您选择可能安装在同一 Linux 系统上的不同 Linux 内核。

### 超级用户控制：root 用户

要执行系统管理操作，您首先必须拥有访问权限，例如允许您以 root 用户身份登录的正确密码，从而使您成为超级用户。由于超级用户有权更改系统中的几乎任何内容，因此此类密码通常是一个被严密保护的秘密，经常更改，并且只提供给那些职责是管理系统的人员。使用正确的密码，您可以作为系统管理员登录到系统，并以不同方式配置系统。您可以启动和关闭系统，以及切换到不同的操作模式，例如单用户模式。您还可以添加或删除用户，添加或删除整个文件系统，备份和恢复文件，甚至指定系统的名称和地址。

*注意* 如果启用了 SELinux，超级用户访问将受 SELinux 规则控制。参见第 17 章。

要成为超级用户，您需要登录到 *root 用户账户*。这是一个用于系统管理操作的特殊账户，对 Linux 操作系统的所有组件拥有不受限制访问权限。您可以从 GUI（图形用户界面）登录屏幕或命令行登录提示符登录为 root 用户。然后，您可以访问所有管理工具。使用像 GNOME 这样的 GUI 接口，root 用户可以访问许多 Red Hat 和 Fedora GUI 管理工具，例如用于管理用户的 system-config-users。如果您从命令行界面登录，您可以运行相应的管理命令，如 `rpm` 来安装包或 `useradd` 来添加新用户。从您的 GUI 桌面，您也可以通过终端窗口运行命令行管理工具。root 用户的命令行接口使用特殊的提示符，即井号 #。在下一个示例中，用户以 root 用户身份登录到系统并接收到 # 提示符。

```text
login: root
password:
#
```

### root 用户密码

作为 root 用户，您可以使用 `passwd` 命令更改 root 登录密码，也可以更改系统上任何其他用户的密码。`passwd` 命令会利用可插拔认证模块 (PAM) 检查您的密码，如第 28 章所述，以查看您是否选择了容易被破解的密码。要从 GUI 界面更轻松地更改 root 密码，您可以使用 system-config-rootpassword 工具。

```bash
# passwd root
New password:
Re-enter new password:
#
```

您必须采取措施保护您的 root 密码。任何以 root 用户身份获得访问权限的人都将完全控制您的系统。`passwd` 命令的在线手册提供了有关处理和选择密码的详细建议。例如，切勿将密码存储在系统的文件中，也切勿选择基于任何可访问信息（如您的电话号码或出生日期）的密码。基本准则是尽可能使您的密码复杂，使用包含数字和大小写字母的多个单词短语，但又要确保您仍能轻松记住，这样您就永远不需要写下来。您可以使用以下命令访问 `passwd` 在线手册页

```bash
# man passwd
```

### root 用户访问：su

当您登录到普通用户账户时，可能需要您登录为 root 并成为超级用户。通常，您必须先注销您的用户账户，然后登录到 root。相反，您可以使用 `su` 命令（切换用户）在保持登录您的用户账户的同时直接登录到 root。如果您使用的是像 GNOME 这样的 GUI 桌面，您可以从终端窗口输入 `su` 命令，或者使用

