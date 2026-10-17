
现在，进入新的 PHP4 目录（`cd ./php-4.0`）并在终端中输入以下命令：

1) 编辑 `php_postgresql.h` 文件（`vi +46 postgresql/php_postgresql.h`）并修改以下行：

```c
#include <libpq-fe.h>
#include <libpq-fs.h>
```
阅读：
```c
#include <usr/include/postgresql/libpq-fe.h>
#include <usr/include/postgresql/libpq-fs.h>
```

在 `php_postgresql.h` 文件中进行这些修改是为了指示 PHP4 配置期间 PostgreSQL 数据库的 `libpq-fe.h` 和 `libpq-fs.h` 头文件的位置。在 Red Hat 中，库位于 `(/usr/include/postgresql)`。

2) 现在，我们必须在 Linux 服务器上配置并安装 PHP4：

```bash
CC="egcs \"
CFLAGS="-O9 -funroll-loops -fast-math -malign-double -mcpu=pentiumpro -march=pentiumpro -fomit-frame-pointer=-no-exceptions \"
```
此处省略了重复的配置块，翻译翻译保持了与原文一致的逻辑结构

# 服务器软件（Web 网络服务）

## 第9 章

这些最不使用的模块可以减少加载操作，并限制 Apache Web 服务器的安全风险。关于每个模块的信息，请参阅您的 Apache 文档。

### 第 7 步

现在，我们必须在 Linux 服务器上安装 Apache：

```
[root@apache_1.3.12]# make
[root@apache_1.3.12]# make install
[root@apache_1.3.12]# rm -rf /usr/sbin/apachectl
[root@apache_1.3.12]# rm -rf /usr/local/man/apache.8
[root@apache_1.3.12]# rm -rf /home/httpd/icons/
[root@apache_1.3.12]# rm -rf /home/httpd/https
[root@apache_1.3.12]# cd /var/www/php-4.0/
[root@php-4.0]# make install -m 644 php.ini /usr/lib/php.ini
[root@php-4.0]# rm -rf /etc/httpd/conf/ssl/
[root@php-4.0]# rm -rf /etc/httpd/conf/ssl.crt
[root@php-4.0]# rm -rf /etc/httpd/conf/ssl.key
[root@php-4.0]# rm -rf /etc/httpd/conf/ssl.prm
[root@php-4.0]# rm -rf /home/httpd/conf/httpd.conf.default access.conf.default
```

`make` 命令将源文件编译成可执行文件，而 `make install` 将将二进制文件和任何支持文件安装到适当的位置。`rm` 命令将删除负责启动和停止 Apache 守护进程的小脚本 `apachectl`，因为在我们利用 Linux 系统 V 时，使用了 Apache 位于 `/etc/rc.init.d/` 目录下的更好的脚本 `httpd`。当我们使用 Apache 的自动索引功能时，还会删除 Apache 下的 `home/httpd/icons` 目录。此功能可能会带来安全风险，因此我们在配置文件中禁用了它。因此，我们安全地删除了该目录以为 Linux 服务器腾出空间。`home/httpd/https` 目录处理与 Apache 相关的所有功能，因此在我们阅读完文档后可以将其删除以释放空间。`install-m` 命令将 `php.ini` 安装到适当的目录下以替换现有文件。此文件控制 `/etc/httpd/conf/` 下的 `ssl.crt`、`ssl.key` 和 `ssl.prm` 目录，所有与 SSL 相关的目录并处理公私钥。由于我们使用了另一个位置（`/etc/ssl/`），我们可以安全地删除它们。最后，删除未使用的 `httpd.conf`、`httpd.conf.default`、`access.conf` 和 `access.conf.default` 文件，它们的用途现在由 `httpd` Apache 文件处理。

### 工作后的清理

```
[root@#]# cd /var/tmp
[root@#]# rm -rf apache-version.tar.gz mod_ssl-version/mod_ssl-version.tar.gz php-version/php-version.tar.gz mod-perl/mod-perl.tar.gz
```

`rm` 命令将删除我们用于编译和安装 Apache、mod_ssl、mod_perl 和 php 的所有源文件。它还将删除 `/var/tmp/` 目录下的 Apache、mod_ssl、mod_perl 和 php 压缩包。

### 配置

不同服务的配置文件根据您的需求和网络架构具有非常特定的性。有些人可能安装 Apache 服务器来提供网页服务；另一些人可能安装带有数据库连接和 SSL 支持的电子商务系统等。在本书中，我们为您提供了一个带有 PHP、Perl、SSL、LDAP 和密码身份验证设置的 `httpd.conf` 文件，用以向您展示不同的可能性。

我们将专注于这些文件的优化和安全性，并将所有调整留给您的喜好。您将需要阅读这些程序附带的文档，并希望理解它们。

我们在书中描述的所有软件在名为 `floppy.tgz` 的 tar 压缩包中都有一个特定的目录和子目录，其中包含特定程序的程序配置。如果您获得了此存档文件，您就不需要手动重制下面不同的配置文件，或通过剪切和粘贴它们来创建您的配置文件。无论您决定手动复制它们，还是编辑为您的需求制作的文件并将文件放在适当的 Apache 服务器存档中，它们都将位于您服务器上的适当位置，如下所示。要下载的服务器配置文件存档位于以下 Internet 地址：http://open.com/books/floppy.tgz

- 运行 Apache 服务器需要以下文件，并且必须在服务器的适当目录中创建或复制它们。
- 将 `httpd.conf` 文件复制到 `/etc/httpd/` 目录。
- 将 `apacherotate` 文件复制到 `/etc/logrotate.d/` 目录。
- 将 `httpd` 脚本文件复制到 `/etc/rc.d/init.d/` 目录。

您可以在我们的 `floppy.tgz` 存档中获取下面列出的配置文件。请从压缩的 `floppy.tgz` 存档中将以下文件复制到适当的位置，或直接从这里剪切粘贴到相关文件中。

### /etc/httpd/conf/httpd.conf 配置

`httpd.conf` 文件是 Apache 服务器的主配置文件。存在许多选项，阅读 Apache 附带的文档是非常重要的。通过 Apache 附带的文档获取更多关于选项的说明。以下配置是支持 SSL 的最小化配置。请注意注释掉与安全相关的参数，并根据需要修改 `httpd.conf`。

### 部分 1：全局配置

```
DefaultType text/plain
```

### 部分 2：主服务器

```
Port 80
```

### 部分 3：虚拟主机
