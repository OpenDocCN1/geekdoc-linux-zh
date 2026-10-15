

| 查看器 | 描述 |
|--------|-------------|
| Gnome Ghostview (GV) | 用于显示 PostScript 和 PDF 文件的 Gnome 界面 |
| KGhostView | 用于显示 PostScript 和 PDF 文件的 KDE 界面 |
| xpdf | 仅用于显示 PDF 文件的 X Window System 工具 |
| KDVI | 用于显示 TeX DVI 文件的 KDE 工具（KViewShell 的插件） |
| Acrobat Reader | Adobe PDF 和 PostScript 显示应用程序 |

Linux 还提供了一款专业级的排版工具，名为 TeX，常用于排版复杂的数学公式。TeX 生成的 DVI 文档随后可由 DVI 查看器查看，Linux 上有多个此类查看器。由 TeX 文档应用程序生成的 DVI 文件可由 KDVI 查看。KDVI 是 KViewShell 工具的插件，该工具可显示和打印任何具有插件的文档类型。您可以在图形菜单中将 KDVI 作为 DVI 查看器访问。

这些应用程序可在图形子菜单下获得。xpdf 的名称为 PDF 查看器，GV 使用的名称为 Postscript 查看器，KGhostView 命名为 PS/PDF 查看器（更多图形应用程序），KDVI 称为 DVI 查看器。

## 数据库管理系统

数据库软件通常可分为三类：SQL、Xbase 和数据库数据库。基于 SQL 的数据库是专业级的关联数据库，其文件由中央数据库服务器管理。使用数据库的应用程序不直接访问文件。相反，它们向数据库服务器发送请求，然后由服务器执行实际访问。SQL 是这些工业级数据库上使用的查询语言。Red Hat Linux 包含 MySQL 和 PostgreSQL 数据库。两者都是可免费用于 Linux 的开源项目。表 11-6 列出了当前可用于 Linux 的 DBMS。

Xbase 语言是 dBase 数据库语言的增强版本，用于访问最初为 PC 上的 dBase 开发的数据库文件格式。与 Xbase 一起，数据库管理系统可以直接访问数据库文件。Xbase 主要用于较小的个人数据库，数据库文件通常位于用户自己的系统上。

### SQL 数据库（RDMSs）

SQL 数据库是关系数据库管理系统（RDMSS），专为广泛的数据库管理任务而设计。许多主要的 SQL 数据库现在都有 Linux 版本，包括 Oracle、Informix、Sybase 和 IBM（当然不包括 Microsoft）。这些是最顶级的商业和专业数据库管理系统。Linux 已证明其能够支持复杂且要求苛刻的数据库管理任务。此外，还有许多可免费用于 Linux 的 SQL 数据库，提供几乎相同的功能。大多数商业数据库还提供免费的个人版本，例如 Oracle、Adabas D 和 MySQL。

### TABLE 11-6
Linux 的数据库管理系统

| 系统 | 站点 |
|---|---|
| PostgreSQL | PostgreSQL 数据库：www.postgresql.org |
| MySQL | MySQL 数据库：www.mysql.com |
| Oracle | Oracle 数据库：www.oracle.com |
| Sybase | Sybase 数据库：www.sybase.com |
| DB2 | IBM 数据库：www.software.ibm.com/data/db2/linux |
| Informix | Informix 数据库：www.informix.com/linux |
| Adabas D | Adabas D 数据库：www.softwareag.com/adabasd |
| GNU SQL | GNU SQL 数据库：www.ispras.ru/~kml/gss |
| Flagship | Xbase 数据库文件的接口：www.fship.com/free.html |

### PostgreSQL

PostgreSQL，随 Red Hat 提供，是基于 POSTGRES 数据库管理系统，但使用 SQL 作为其查询语言。POSTGRES 是加州大学伯克利分校开发的下一代研究原型。PostgreSQL 的 Linux 版本包含在大多数发行版中，包括 Red Hat、Debian 和 Mandrake 发行版。您可以在 www.postgresql.org 的 PostgreSQL 网站上获取更多信息。PostgreSQL 是一个开源项目，在 GPL 许可证下开发。

> 注意 Red Hat 现在提供一个名为 Red Hat Database 的 Linux 版本，其中包含 PostgreSQL，针对数据库操作进行了优化。

PostgreSQL 通常用于为需求繁重的互联网服务器提供数据库支持，例如 Web 服务器。通过几个简单的命令，您可以创建关系数据库表。使用 createuser 命令创建 PostgreSQL 用户，然后您可以用该用户登录服务器。然后您可以使用 createdb 命令创建数据库，并使用 create table 指令构建关系表。使用 insert 命令，您可以添加记录，然后使用 select 命令查看它们。对服务器的远程用户访问由位于 PostgreSQL 目录中的 pg_hba.conf 文件中的条目控制，通常为 /var/lib/pgsql。

### MySQL

MySQL，随 Red Hat 提供，是一款真正的多用户、多线程 SQL 数据库服务器，由 MySQL AB 支持。MySQL 是一款开源产品，可根据 GPL 许可证免费使用。您可以在其网站 www.mysql.com 上获取最新信息。该网站包含详细的文档，包括手册和常见问题解答。

MySQL 采用客户端/服务器模型构建，服务器守护进程 mysqld 响应客户端程序的请求。MySQL 设计用于速度、可靠性和易用性。它旨在成为大型数据库的快速数据库管理系统，同时在密集使用下保持可靠。MySQL 维护用于全局的 /etc/my.cnf 配置文件
