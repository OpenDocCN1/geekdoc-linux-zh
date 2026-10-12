
## 第24章

### 设置 MySQL 数据库服务器

**本章内容**

-   查找 MySQL 软件包
-   配置 MySQL 服务器
-   使用 MySQL 数据库
-   显示 MySQL 数据库
-   修改表和记录
-   添加和删除用户访问权限
-   检查和修复数据库

MySQL 是一款流行的结构化查询语言（SQL）数据库服务器。与其他 SQL 服务器一样，MySQL 提供了访问和管理 SQL 数据库的手段。然而，MySQL 还提供了创建数据库结构以及向这些结构中添加、修改和删除数据的工具。因为 MySQL 是一个关系型数据库，数据可以存储和控制在小而可管理的表中。这些表可以组合使用以创建灵活而复杂的结构。

一家名为 MySQL AB 的瑞典公司负责开发 MySQL（www.mysql.com）。MySQL AB 已将 MySQL 作为开源产品发布，通过提供各种 MySQL 支持包来获得收入。该公司还支持多个应用程序编程接口（APIs），以帮助应用程序开发人员和 Web 内容创建者访问 MySQL 内容。

由于 MySQL 是开源产品，它已被移植到多个不同的操作系统（主要是 UNIX 和 Linux 系统，尽管也有 Windows 版本，现在甚至还有 Mac OS X 版本）。正如您可能猜到的那样，这些包括在 Red Hat Linux 上运行的 MySQL 二进制版本。本章包含对 Red Hat Linux 发行版中包含的 MySQL 版本的描述和操作步骤。

> **注意：**随此版本 Red Hat Linux 提供的 MySQL 版本为 3.23。如果您想探索 MySQL 的后续版本，请访问 *www.mysql.com*。截至本文撰写时，您可以下载 MySQL 4.0 的生产版本以及 MySQL 4.1 和 5.0 的开发版本。

## 查找 MySQL 软件包

您至少需要安装 mysql 和 mysql-server 软件包才能使用本章所述的步骤设置 MySQL。以下 MySQL 软件包随 Red Hat Linux 发行版提供：

-   **mysql** — 该软件包包含大量 MySQL 客户端程序（在 `/usr/bin` 中）、多个客户端共享库、默认 MySQL 配置文件（`/etc/my.cnf`）、一些示例配置文件、支持不同语言的文件以及文档。
-   **mysql-server** — 该软件包包含 MySQL 服务器守护进程（*mysqld*）和 *mysqld* 启动脚本（`/etc/init.d/mysqld`）。该软件包还创建设置 MySQL 数据库所需的各种管理文件和目录。
-   **mysql-devel** — 该软件包包含开发 MySQL 应用程序所需的库和头文件。
-   **php-mysql** — 该软件包包含一个共享库，允许 PHP 应用程序访问 MySQL 数据库。这基本上允许您在 Web 页面中添加 PHP 脚本以访问您的 MySQL 数据库。

在当前版本的 Red Hat Linux 中，所有 mysql 软件包都包含在第 3 张 CD 上。如果未安装，您可以使用 rpm 命令或 redhat-config-packages 窗口（见第 5 章所述）安装 mysql 软件包。

## 配置 MySQL 服务器

与 Red Hat Linux 中的大多数服务器软件一样，MySQL 服务器依赖于启动脚本和配置文件来提供服务。服务器活动记录到 `/var/log` 目录中的 *mysqld.log* 文件中。还有 mysql 用户和组账户用于管理 MySQL 活动。以下各节描述了这些组件如何协同工作。

> **提示：**本节所述的许多步骤中，MySQL 服务器守护进程必须正在运行。启动服务器的详细说明将在本章后面介绍。暂时，您可以通过键入以下命令（以 root 用户身份）临时启动服务器：/etc/init.d/mysqld start

### 使用 mysql 用户/组账户

安装 MySQL 软件时，它会自动创建一个 *mysql* 用户账户和一个 *mysql* 组账户。这些用户和组账户分配给 MySQL 文件和活动。这样，某人可以在没有 root 权限的情况下管理 MySQL 服务器。

`mysql` 用户条目在 `/etc/passwd` 文件中如下所示：

```
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
```

所示的 `mysql` 条目表明 `mysql` 用户的 UID 和 GID 为 27。标识此用户账户的文本字符串为“MySQL Server”。主目录为 `/var/lib/mysql`，默认 shell 为 `/bin/bash`。标识的主目录将包含目录，用于存放您为 MySQL 服务器定义的数据表的每个表。

`mysql` 的组条目更简单。`/etc/group` 文件中的以下条目表明 `mysql` 组具有组 ID（GID）27。

```
mysql:x:27:
```

如果您想检查与 MySQL 关联的文件的所有权，您会看到大多数这些文件都将 `mysql` 指定为拥有每个文件用户账户和组账户。这允许由 `mysql` 用户运行的守护进程访问数据库文件。

## 添加管理用户

要管理 MySQL，您需要创建至少一个管理账户。您可以使用 `mysqladmin` 命令执行此操作。要将 root 用户添加为 MySQL 管理员，请以 root 用户身份登录并从终端窗口键入以下内容（将 `my47gmc` 替换为您自己的密码）：

```
# mysqladmin -u root password my47gmc
```

运行此命令后，root 用户可以使用该密码运行任何 MySQL 管理命令。

如果您在登录为其他用户时想要使用管理权限运行 MySQL 命令，可以在不重新登录的情况下执行。只需在您运行的 MySQL 命令命令行中添加 `-u root` 参数。换句话说，一旦 MySQL 账户创建，Linux root 用户账户与 MySQL root 用户账户没有任何关联。您通常会为这两个账户使用不同的密码。

> **提示**：为避免每次运行 MySQL 客户端命令时都输入密码，您可以在选项文件中的 [client] 组下添加密码选项。最安全的方法是在 root 用户的主目录中创建一个 `.my.cnf` 文件，其中包含以下行（将最后显示的参数替换为您自己的密码）。

```
[client]
password=my47gmc
```

## 设置 MySQL 选项

您可以通过使用选项文件或命令行参数来设置影响 MySQL 应用程序行为的选项。MySQL 服务器（以及其他管理工具）在启动时（如果存在）会读取以下选项文件：

-   `/etc/my.cnf` — 包含由 mysqld（服务器守护进程）和 mysql.server（用于启动服务器守护进程的脚本）读取的全局选项。
-   `/var/lib/mysql/my.cnf` — 主要包含 mysqld 守护进程的选项。
-   `-defaults-extra-file` — 您可以在命令行中指定一个包含服务器要使用的选项的文件。例如，以下命令将导致在全局选项之后、用户特定选项之前读取文件 `/home/jim/my.cnf` 中的选项：

```
# mysqld --defaults-extra-file=/home/jim/my.cnf
```

-   `$HOME/.my.cnf` — 包含用户特定选项。（`$HOME` 指用户的主目录，例如 `/home/susyg`。）

表 24-1 显示了读取选项文件（按上一项目符号列表中所示顺序）并在处理中使用这些选项的 MySQL 命令。选项包含在由方括号内单个单词标识的组中。每个命令读取的组名也在表中显示。

**表 24-1：与 MySQL 命令关联的选项组**

| 命令 | 描述 | 组名 |
| :--- | :--- | :--- |
| `mysqld` (in `/usr/libexec`) | MySQL 服务器守护进程。 | `[mysqld]` `[server]` |
| `safe_mysqld` | 由 `mysql` 启动脚本运行以启动 MySQL 服务器。 | `[mysql]` `[server]` `[mysql.server]` |
| `mysql` | 提供基于文本的界面用于显示和操作 MySQL 数据库。 | `[mysql]` `[client]` |
| `mysqladmin` | 用于创建和维护 MySQL 数据库。 | `[mysqladmin]` `[client]` |
| `isamchk` | 用于检查、修复和优化 ISAM 数据库（.ism 后缀）。 | `[isamchk]` |
| `myisamchk` | 用于检查、修复和优化 MyISAM 数据库（.myi 后缀）。 | `[myisamchk]` |
