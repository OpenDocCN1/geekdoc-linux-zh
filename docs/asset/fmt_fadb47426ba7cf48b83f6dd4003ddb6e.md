
```
 /usr/lib/postgresql/man1/hba.conf sample
> /usr/share/man1/cleardb.1
> /usr/share/man1/createddb.1
> /usr/share/man1/createuser.1
> /usr/share/man1/destroydb.1
> /usr/share/man1/destroyuser.1
> /usr/share/man1/initdb.1
> /usr/share/man1/relocation.1
> /usr/share/man1/pg_dump.1
> /usr/share/man1/pg_upgrade.1
> /usr/share/man1/pg_restore.1
> /usr/share/man1/postmaster.1
> /usr/share/man1/psql.1
> /usr/share/man3/catalogs.3
> /usr/share/man3/pg_hba.conf
> /usr/share/man1/abort.1
> /usr/share/man1/alter_table.1
> /usr/share/man1/alter_user.1
> /var/lib/postgresql/template1/pg_class_index
> /var/lib/postgresql/template1/pg_class_relname_index
> /var/lib/postgresql/template1/pg_atfd
> /var/lib/postgresql/template1/pg_atfdrel_adrelid_index
> /var/lib/postgresql/template1/pg_relcheck
> /var/lib/postgresql/template1/pg_relcheck_rcreid_index
> /var/lib/postgresql/template1/pg_trigger_tgrelid_index
> /var/lib/postgresql/template1/pg_description_oboid_index
> /var/lib/postgresql/template1/PG_VERSION
> /var/lib/postgresql/template1/pg_user
> /var/lib/postgresql/template1/pg_tables
> /var/lib/postgresql/template1/pg_views
> /var/lib/postgresql/template1/pg_indexes
> /var/lib/postgresql/pg_variable
> /var/lib/postgresql/pg_database
> /var/lib/postgresql/pg_shadow
> /var/lib/postgresql/pg_group
> /var/lib/postgresql/PG_VERSION
> /var/lib/postgresql/pg_hba.conf
> /var/lib/postgresql/pg_geop.sample
> /var/lib/postgresql/pg_pwd
```

# 第18章 服务器软件（代理网络服务）

## 本章中

- Linux Squid 代理服务器
- 使用 GNU malloc 库提高 Squid 配置的缓存性能
- 加固 Squid
- 优化 Squid
- `cachemgr.cgi` 程序实用程序
- Squid 的配置

## Linux Squid 代理服务器

### 概述

代理服务器因其提供带宽、提高安全性和提升网页速度的能力而变得越来越流行。目前，市场上只有少数代理服务器。这些代理服务器有两个主要缺点：它们是商业性的，且不支持 ICP。ICP 用于交换邻近缓存中 URL 的存在提示。`Squid` 是代理服务器的最佳选择，因为它是健壮、免费且可以使用 ICP 特性的。

`Squid` 源自 ARPA 项目，由美国科学基金会资助，在国立实验室开发。它提供了高性能的网络缓存，并支持 FTP、Gopher 和 HTTP 数据。它将对象存储在内存中，在磁盘上维护健的数据库，具有复杂的访问控制机制，并支持 SSL 协议以保护连接。此外，它可以层次链接到其他基于 `Squid` 的代理服务器进行页面缓存。

在我们的编译和配置中，我们将配置 `Squid` 以加速器模式运行获得更高的性能。在加速模式下，`Squid` 服务器作为反向代理：它接受请求并从缓存中提供，或者从源服务器获取。我们还将展示如何配置代理服务器以让企业网络中的所有用户使用 `Squid`。

这些安装说明假设：

- 命令与 Unix 兼容。
- 源路径为 `/var/tmp`（可以是其他路径）。
- 在 RedHat Linux 6.1 和 6.2 上测试过。
- 所有安装步骤将在 root 用户账户下进行。
- `Squid` 版本号为 2.3STABLE

### 软件包

- `Squid` 首页：http://squid-cache.org/
- `Squid` FTP 站点：204.144.128.89
- 你必须确保下载：`squid-2.3STABLE-src.tar.gz`

### 压缩包

在安装 `Squid` 之前对系统文件创建一个列表是一个好主意，之后使用 `diff` 比较找出文件被放在了哪里。只需在安装前运行 `find > Squid1`，在安装后运行 `find > Squid2`。

### 编译

解压压缩包（tar.gz）。

```
root@~# cp squid-STABLE2-src.tar.gz /var/tmp
root@~# cd /var/tmp
root@~# tar xzf squid-src.tar.gz
```

## 配置与优化

### 步骤 1

`Squid` 代理服务器不能以超级用户 root 运行，因此我们创建一个没有 shell 的特殊用户来运行 `Squid`。

```
root@~# useradd -d /cache -s /dev/null squid
root@~# mkdir /cache/
root@~# chown -R squid /cache/
```

首先，我们将 "`squid`" 添加 `/etc/passwd` 文件。然后，如果 "`cache`" 目录不存在，则创建它。最后，我们将 "`cache`" 目录的所有者更改为 "`squid`"。

注意：通常不需要执行 `mkdir /cache/` 命令，因为我们已经在安装期间创建了该目录。如果分区不存在，你必须执行此命令。

### 步骤 2

进入新的 `Squid` 目录并在终端上输入以下命令：

编辑 `Makefile.in` 文件 (`vi icons/Makefile.in`) 并更改：

```
DEFAULT_ICON_DIR = $(sysconfdir)
DEFAULT_ICON_DIR = $(libexecdir)
```

我们将变量 `$(basedir)` 改为 `$(libexecdir)`，“icons" 目录将位于 `/usr/lib/squid` 目录下。

编辑 `Makefile.in` (`vi src/Makefile.in`) 并更改以下行：

```
DEFAULT_CACHE_LOG = $(localstateddir)/logs/cache.log
DEFAULT_CACHE_LOG = $(localstateddir)/log/squid/cache.log
```

```
DEFAULT_ACCESS_LOG = $(localstateddir)/logs/access.log
DEFAULT_ACCESS_LOG = $(localstateddir)/log/squid/access.log
```

```
DEFAULT_STORE_LOG = $(localstateddir)/logs/store.log
DEFAULT_STORE_LOG = $(localstateddir)/log/squid/store.log
```

```
DEFAULT_PID_FILE = $(localstateddir)/logs/squid.pid
DEFAULT_PID_FILE = $(localstateddir)/run/squid.pid
```

```
DEFAULT_SWAP_DIR = $(localstateddir)/cache
DEFAULT_SWAP_DIR = /cache
```

```
DEFAULT_ICON_DIR = $(sysconfdir)/icons
DEFAULT_ICON_DIR = $(libexecdir)/icons
```

## 服务器软件（代理网络服务） | 第8章
