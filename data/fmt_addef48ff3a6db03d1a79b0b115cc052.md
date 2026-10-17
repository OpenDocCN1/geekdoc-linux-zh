
- `/usr/sbin/squid`

- `/usr/sbin/client`

- `/var/log/squid/`

# 物理内存

Squid 最重要的资源是物理内存。你的处理器不需要极快。你的磁盘系统将是主要的瓶颈，因此快速磁盘对于高容量缓存至关重要。如果可以，请使用 IDE 磁盘。

# 安装文件

（此处列出的文件路径通常保持原样，不翻译）

- `/etc/squid`

- `/etc/squid/mib.txt`

...（此处略）

# Apache Web 服务器

Squid 是一个功能强大的 Web 服务器，支持 HTTP 1.1、身份验证等许多功能。它是最流行的 Web 服务器之一，性能等同或优于商业级服务器。由于 Apache 是复杂的，我们在后续提供了分步示例。如果它们不符合你的情况，则需要调整。

本教程是为新的 Apache 管理员编写的，描述了如何安装和运行它。

# 编译与优化

将 `mod_ssl` 应用到 Apache 源码树。

进入新的 `mod_ssl` 目录 (`mod_ssl-version`)，并在终端中执行以下命令：

```bash
CC="ecgs" \
CFLAGS="-O9 -funroll-loops -fast-math -align-math -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions" \
./configure
```

关于本页面的意见和建议请发送至 `gmourani@videotron.ca`

```bash
--apache=../apache_1.3.9 \
--with-crt=/etc/ssl/certs/server.crt \
--with-key=/etc/ssl/private/server.key
```

进入新的 Apache 目录（`cd ../apache-version`）并在终端中输入以下命令：

```bash
[root@deep]# vi +331 src/include/httpd.h 并修改：

#define HARD_SERVER_LIMIT 256
为
#define HARD_SERVER_LIMIT 1024
```

为 PHP3 的配置步骤预配置 Apache。

进入新的 apache 目录（`cd "../apache-version"`）并在终端中输入以下命令：

```bash
CC="gcc"
CFLAGS="-O9 -ffroll-loops -fast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer -fno-exceptions"
CPP="DYNAMIC_MODULE_LIMIT=0"
/config/
--prefix=/home/httpd \
--bindir=/usr/bin \
--sbinir=/usr/sbin \
--libdir=/usr/lib/apache \
--includedir=/usr/include/apache \
--sysconfdir=/etc/conf \
--locatedir=/var \
--runtimedir=/var/run \
--logfile=/var/log/httpd \
--datadir=/home/httpd \
--proxycachedir=/var/cache/httpd \
--mandir=/usr/man
```

配置 PHP3 并将其应用于 Apache 源码。

进入新的 php3 目录（`cd "../php-version"`）并在终端中输入以下命令：

编辑 php3_pgsql.h 文件（`vi +46 functions/php3_pgsql.h`）并修改以下行：

```c
#include <libpq-fe.h>
#include <libpq-fs.h>
为：
#include <usr/include/postgresql/libpq-fe.h>
#include <usr/include/postgresql/libpq-fs.h>
```

```bash
CC="gcc"
CFLAGS="-O9 -ffroll-loops -fast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -frame-pointer -fno-exceptions -usr/include/openssl"
/config/
--prefix=/usr \
--with-config-file-path=/etc/httpd \
--with-imap \
--enable-safe-mode \
--with-exec-dir=/usr/bin \
--disable-debug \
--apache=../apache_1.3.9
```

© Copyright 1999 Open Network Architecture ®

301

关于本页面的意见和建议请发送至 `gmourani@videotron.ca`

```bash
--with-postgresql (如果你需要 PostgreSQL 数据库)
--with-ldap (如果你需要 LDAP 数据库目录列表)
--enable-memory-limit=yes \
--enable-debug=no

[root@deep]# make
[root@deep]# make install
```

## 将 mod_perl 应用到 Apache 源码树并编译/安装 mod_perl 的 Perl 端。

进入新的 mod_perl 目录（`cd "../mod_perl-version"`）并在终端中输入以下命令：

```bash
perl Makefile.PL \
EVERYTHING=1 \
APACHE_SRC=../apache_1.3.9/src \
USE_APACH2 \
PREP_HTTPD=1 \
DO_HTTPD=1 \
[root@deep]# make
[root@deep]# make install
```

## 编译/安装带有 mod_ssl + mm + mod_perl 和 PHP3 的 Apache。

进入新的 Apache 目录（`cd "../apache"`）并在终端中输入以下命令：

```bash
SSL_BASE=SYSTEM\ (mod_ssl 需要),
EAPI_MM=SYSTEM\ (mm 需要)。
CC="gcc"
OPTIMA="-O3 -loops -fast-math -malign-clue -mcpu=pentiumpro -march=pentiumpro -omit-frame-pointer -no-exceptions" \
CFLAGS="-DYNAMIC_MODULE_LIMIT=0" \
--configure \
--prefix=/home/httpd \
--bindir=/usr/bin \
--sbinir=/usr/sbin \
--libexecdir=/usr/lib \
--included=/usr/include/apache \
--confdir=/etc/httpd \
--localstatedir=/var \
--rundedir=/var/run \
--logdir=/var/log \
--datadir=/home \
--proxiedir=/var/cache/httpd \
--module-dir=/var/module \
--add-module=src/modules/experimental/mod_mmap_static.c \ (如果你打算使用 mod_mmap)。
--add-module=src/modules/standard/mod_auth_db.c \ (如果你打算使用 mod_auth)。
--enable-ssl (mod_ssl 需要)。
--enable-rule=SSL_DBDM COMPAT\ (mod_ssl 需要)。
--activate-rule=src/modules/php3/libphp3.a \ (php 需要)。
--enable-php3 (php 需要)。
--activate-rule=src/modules/perl/libperl.a \ (mod_perl 需要)。
--enable-perl (mod_perl 需要)。
--disable-module=include \
--disable-module=status \
--disable-module=userdir \
--disable-module=negotiation \
--disable-module=autobindex \
--disable-module=asis \
--disable-module=imap
```

© Copyright 1999 Open Network Architecture ®

302

关于本页面的意见和建议请发送至 `gmnourani@videotron.ca`
