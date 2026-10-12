
历史上，安装包后自动启动安装的服务是常见的。今天，确保恶意软件不会自动启动更为常见。因此，有必要手动启动 `apache2`，并将其设置为系统每次启动时自动启动。

### SUSE Linux Enterprise Server上的 Apache 服务

将 `apache2` 服务设置为每次启动时自动启动，然后使用以下命令手动启动服务：

```
chkconfig apache2
service apache2 start
```

示例 8-30 显示了启动 `apache2` 服务的预期输出。

> 示例 8-30 启动 `apache2` Web 服务

```
Insubd2:~ # chkconfig apache2
Insubd2:~ # service apache2 start
Starting httpd (forkref)
done
```

### RHEL上的 Apache 服务

RHEL 上的命令与 SUSE Linux Enterprise Server 相同，但服务名称是 `httpd` 而不是 `apache2`，如下所示：

```
chkconfig httpd
service httpd start
```

### 验证 Web 服务器正在运行

Web 服务器启动后，使用浏览器验证 Web 服务器是否按预期工作，如图 8-1 所示：启动浏览器并指向 Linux 服务器的 IP 地址。在本示例中，URL 为 `http://9.12.7.90`。

![](img/2db39dd28fa1ef80e2c2d208b955dfbd_168_0.png)

图 8-1 Apache 安装的成功测试

# 验证 PHP 是否工作

在为 PHP 构思并运行测试之前，必须确定 Apache 服务器的 DocumentRoot 目录的位置。

在 SUSE Linux Enterprise Server 中，默认位置是 `/srv/www/htdocs`。然而，可能配置了非默认位置。可以通过运行示例 8-31 所示的命令来确定文档根目录：

```
示例 8-31 在 SUSE Linux Enterprise Server 上查找 DocumentRoot
root@insud2:~# grep 'DocumentRoot' /etc/apache2/default-server.conf
DocumentRoot "/srv/www/htdocs"
```

在 RHEL 下，默认位置是 `/var/www/html`，但确定值通过示例 8-32 中的命令来显示：

```
示例 8-32 在 RHEL 上查找 DocumentRoot
[root@8z84p0-ri1 ~] grep 'DocumentRoot' '' /etc/httpd/conf/httpd.conf
DocumentRoot "/var/www/html"
```

在确认 Apache 服务器的 DocumentRoot 后，创建一个单行的 PHP 脚本，用于打印标准的 PHP 安装信息。使用 `vi` 或其他文本编辑器创建一个名为 `phpinfo.php` 的脚本文件（如示例 8-33 所示），并将脚本文件放在适当的 DocumentRoot 目录下。

示例 8-33 显示功能性的简单 PHP 脚本

```
<?php phpinfo();  ?>
```

在 DocumentRoot 目录下放置 PHP 文件后，可以使用浏览器运行 PHP 脚本。连接到您的 Web 服务器，以以下 URL 为例：

`http://92.12.7.90/phpinfo.php`

图 8-2 显示了在 SUSE Linux Enterprise Server 11 SP3 上运行的 PHP 脚本在浏览器中生成的预期 PHP 信息。

| PHP 5.3.17 | |

|---||---|

| System | Linux insud2-86.ibm.com 3.0.76-11-default #1 SMP Fri Jun 14 08:21:43 UTC 2013(02990) s390a |

| Server API | Apache 2.2 Handler |

| Virtual Directory | Disabled |

| Configuration File | /etc/php5/apache2 |

| (php.ini) Path | none |

| Loaded Configuration File | /etc/php5/apache2/php.ini |

| Scan this dir for additional files | /etc/php5/conf.d |

图 8-2 由 `phpinfo.php` 生成的 PHP 配置信息

# 在 SUSE Linux Enterprise Server 上启动 MySQL 服务

将 MySQL 数据库服务设置为每次服务器启动时自动启动，然后使用这些命令手动启动服务：

```
chkconfig mysql on
service mysql start
```

# 在 Red Hat Enterprise Linux 上启动 MySQL 服务

与 Apache 类似，MySQL 数据库服务在 RHEL 中的名称与 SUSE Linux Enterprise Server 略不同。要设置 MySQL 在每次服务器启动时启动并手动启动服务，请执行以下命令：

```
chkconfig mysql on
service mysql start
```

> 注意：SUSE Linux Enterprise 11 SP3 和 RHEL 6.4 都使用 SysVinit 命令。SUSE Linux Enterprise Server 12 和 RHEL 7 均计划使用服务管理来取代 SysVinit。

# 验证 MySQL 是否工作

在安装 MediaWiki 之前，必须正确配置并确保 MySQL 正常工作。完成以下步骤以验证 MySQL 是否工作：

- 1. 复制 MySQL 生产配置的示例配置文件 `/etc/my.cnf`。然后应用适当的所有权访问权限。阅读配置文件以了解其内容是一个好主意。示例 8-34 显示了示例命令。

  稍后，当从 x86 服务器迁移时，你可能会从 x86 服务器将 `my.cnf` 文件复制到 LinuxONE。目前，示例的 `my.cnf` 配置文件已足够在迁移前测试系统功能。

示例 8-34 配置 MySQL 配置文件

```
cp /usr/share/mysql/medium.cnf /etc/my.cnf
chown root:root /etc/my.cnf
chmod 640 /etc/my.cnf
```

> 注意：`/etc/my.cnf` 的默认权限为 644，允许任何人读取 MySQL 配置设置。安全领域的最佳实践建议系统服务不应向特权用户提供不必要的信息。将权限设置为 640 可以防止特权用户发现有关 MySQL 服务器配置的信息。

- 2. 为数据库管理用户设置临时密码。请记住此密码，因为在从 x86 服务器迁移 MediaWiki 应用之前的几个步骤中需要它。此密码可以与以后迁移的 MySQL 数据库密码相同，但不必相同。使用示例 8-35 所示的命令设置密码。

示例 8-35 为 MySQL 服务设置管理密码

```
mysqladmin -u root password 'agoodpassword'
```

为 `root` 用户设置管理密码后，未来与 MySQL 数据库的所有交互都需要提供密码。常规管理功能需要 `root` 密码，而涉及 MediaWiki 的命令将使用不同的密码。

> 注意：Linux 中的引号可能有点棘手。在设置 `root` 密码时，请记住引号并非严格必须。如果密码包含空格等特殊字符，则引号是必须的。通过运行此命令来测试 MySQL 的功能：

```
mysql -u root -p
```

# 8.6.4 使用 MySQL 和 MediaWiki 迁移 iSCSI 磁盘

外部存储的一个特别实用的方面是，磁盘可以有效地从一台机器拔下并插入另一台机器，从而加速迁移过程。这种方法并不适用于所有情况，但在 MediaWiki 示例中是行的。

在本示例中，MySQL 数据库和 Apache DocumentRoot 分别包含在独立的 ISCSI 分区上。这些分区上的文件系统将从 `zs4p01-s1` 主机（一个 x86 系统）卸载，然后挂载到运行在 LinuxONE 上的 `Insub2` 主机。

> 处理远程磁盘存储时，通过路径（by-path）引用并管理远程 LUN，而不是使用其他方法。`udev` 无法确保主机重启时使用相同的名称或 ID。唯一的持久性标识是通过路径。

# 为 LinuxONE 上的 Linux 虚拟机准备 iSCSI

在使用 iSCSI LUN 更改 x86 主机之前，请在 LinuxONE 上安装最基本的 iSCSI 软件：

- 1. 使用安全 Shell (`SSH`) 连接到名为 `insub2` 的 Linux 虚拟机。

- 2. 确保 Linux 虚拟机 `Insub2` 上安装了 `iscsi` 软件：
