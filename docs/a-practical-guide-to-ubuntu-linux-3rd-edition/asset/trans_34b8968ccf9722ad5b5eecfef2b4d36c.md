
- 定期轮询受跟踪设备以获取数据。收集此数据最常用的工具是 SNMP（简单网络管理协议；www.net-snmp.org）。
- 将数据存储在 RRD 文件中。
- 提供一个 Web 界面，允许您查看根据存储数据生成的图形。这些图形通常显示每日、每周、每月和每年的信息。

Cacti 的配置通过其 Web 界面进行，而 MRTG 和 Cricket 则通过编辑文本文件进行配置。

RRD 文件和 RRDtool 是 Cacti 许多功能的关键。Cacti 网站将 Cacti 描述为“完整的基于 RRDtool 的图形解决方案”。RRD 文件高效地存储时间序列数据，并通过使用聚合函数，使其能够轻松地为近期时间段保留大量细节，但随着文件中数据的老化，逐渐减少细节。RRDtool 可以轻松地从 RRD 文件生成简单和复杂的图形。

Cacti 有许多扩展和插件可用。一旦您熟悉了 Cacti 的基本使用和运行，请访问 cacti.net/additional_scripts.php 查看这些附加项的部分列表。还请访问文档和用户论坛，以获取更多关于 Cacti 的信息，并了解您如何为不同设备和数据源添加功能和支持。

## 配置 SNMP

如果您想监控本地系统上的数据源，请按照第 654 页“设置远程数据源”中的说明，在本地系统上安装并运行 SNMP 守护进程。

## 设置 LAMP

Cacti 是一个 LAMP（Linux, Apache, MySQL, PHP）应用程序；在配置 Cacti 之前，您必须安装和配置这些应用程序。本节介绍如何在该运行 Cacti 的系统上设置软件。关于如何设置 Cacti 将查询和报告的系统，请参阅第 654 页的“设置远程数据源”。默认情况下，Cacti 设置本地系统运行 Cacti 并作为数据源。

## 注意事项

当设置 LAMP 时，您使用名为 `mysql` 和 `cacti` 的 MySQL 数据库。Ubuntu 在安装 MySQL 时设置 `mysql` 数据库。您按照第 650 页“配置 MySQL”中的说明设置并填充 `cacti` 数据库。

您需要设置以下数据库用户。每个这些账户都应有密码：

- 一个名为 **root** 的用户，用于名为 **mysql** 的数据库。该用户必须名为 root。MySQL 安装脚本设置此用户并提示输入密码。
- 一个名为 **cactiuser** 的用户，用于名为 **mysql** 的数据库。您可以更改此用户名，但安装后，Cacti 被设置为使用 **cactiuser**。
- 一个 Cacti 管理员用户，用于名为 **cacti** 的数据库。根据安装 Cacti 时的设置，此用户名为 **admin**，密码为 **admin**。您可以设置额外的 Cacti 用户账户。

截至本文撰写时，Ubuntu 10.04 的仓库中有 Cacti 0.8.7e-2。不要被 1.0 之前的版本号误导：Cacti 是稳定的，并用于许多系统。

## 先决条件

安装以下软件包：

- cacti
- mysql-client（第 628 页）
- mysql-server（第 628 页）
- php5-cli
- apache2（Apache；第 899 页）
- rrdtool
- snmp

当安装 cacti 软件包时，APT 安装运行 Cacti 所需的所有软件包。它还运行 MySQL 安装脚本（第 629 页）并询问您是否要运行 Cacti 安装脚本。

在安装过程中，MySQL 安装脚本显示一个伪图形窗口，其中包括以下提示：

```
New password for the MySQL "root" user:
```

使用名为 **root** 的 **mysql** 数据库用户的密码响应此提示，并点击 **OK**。脚本提示您重新输入密码。

接下来 PHP 安装脚本显示一条关于 **libphp-adodb** 位置的消息（您可以忽略）。

下一个伪图形窗口询问您希望 Cacti 使用哪个 Web 服务器。选择 **Apache2**。在安装一些软件包后，Cacti 安装脚本询问您是否希望使用 **dbconfig-common** 来配置 Cacti 的数据库。回答 **No**。截至本文撰写时，该脚本不起作用；后续部分解释了如何手动配置 Cacti 数据库。

**防火墙** 在由 Cacti 监控的系统中运行的 `snmpd` 守护进程使用 UDP 端口 161。如果受监控系统正在运行 *防火墙*，您需要打开此端口（第 876 页）。如果您希望从运行 Cacti 的系统以外的系统中的浏览器访问 Cacti，您需要打开运行 Cacti 的系统的 TCP 端口 80（参见第 901 页的“防火墙”）。要获取更通用的信息，请参阅第 25 章，其中详细介绍了 *iptables* 实用程序。

## 配置 MYSQL

为了更安全的安装，请按照第 629 页“快速入门：设置 MySQL”中的说明运行 `mysql_secure_installation`。

### 两个数据库，两个用户：mysql 数据库中的 cactiuser 和 cacti 数据库中的 admin 用户

**注意** 不要混淆数据库和用户。

**mysql** 数据库有一个名为 **cactiuser** 的用户。此用户使用 MySQL 设置和管理 **cacti** 数据库。在设置 **cacti** 数据库时，您为此用户分配密码。

**cacti** 数据库有一个名为 **admin** 的用户。当使用 `cacti.sql` 脚本填充 **cacti** 数据库时，Cacti 设置此用户。它自动将此用户的密码分配为 **admin**，但在您首次登录 Cacti 时要求更改密码。

**创建 cacti 数据库** 发出以下命令以创建名为 **cacti** 的数据库，创建名为 **cactiuser** 的 **mysql** 数据库用户，授予该用户必要的权限，并为其分配密码。将以下示例中的 `cacti_password` 替换为您选择的密码。虽然 FLUSH PRIVILEGES 语句不是必需的，但包含它是良好的实践。

```
$ sudo mysql -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5
Server version: 5.1.41-3ubuntu2.1 (Ubuntu)
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CREATE DATABASE cacti;
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL ON cacti.*
    -> TO cactiuser@localhost
    -> IDENTIFIED BY 'cacti_password';
Query OK, 0 rows affected (0.00 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)

mysql> exit
Bye
```

**设置并填充 cacti 数据库** 给出以下命令以设置并填充名为 **cacti** 的数据库。当 MySQL 提示输入密码时，提供名为 **root** 的 MySQL 用户的密码（而不是名为 **cactiuser** 的 MySQL 用户）。

```
$ zcat /usr/share/doc/cacti/cacti.sql.gz > cacti.sql
$ sudo -s mysql -p cacti < cacti.sql
Enter password:
$ rm cacti.sql
```

**编辑 debian.php**

使用 root 权限，编辑 /etc/cacti/debian.php 文件，使其看起来像以下示例。将 cactiuser 分配给 $Database_username，将前一步中 cacti_password 的值分配给 $Database_password（名为 cactiuser 的 mysql 数据库用户的密码），并将 cacti 分配给 $Database_default。不要更改其他任何值。

```
$Database_username='cactiuser';
$Database_password='cacti_password';
$basepath='';
$Database_default='cacti';
$Database_hostname='';
$Database_port='';
$dbtype='mysql';
```

## 配置 APACHE

安装 Apache 后，按照第 903 页的说明修改配置文件；如果不进行这些修改，Apache 启动时会显示错误，但仍然可以工作。使用 apache2 初始化脚本重新启动 httpd 守护进程（第 902 页）。Cacti 提供内容。

/etc/cacti/apache.conf 文件控制 Cacti 在 Apache 服务器上的位置和可访问性。您不需要修改此文件。默认情况下，Cacti 可通过 localhost/cacti 访问，或者从远程系统通过 IP/cacti 访问，其中 IP 是运行 Cacti 的系统的 IP 地址。默认的 cacti.conf 文件如下：

```
$ cat /etc/cacti/apache.conf
Alias /cacti /usr/share/cacti/site

<DirectoryMatch "/usr/share/cacti/site">
Options +FollowSymLinks
AllowOverride None
order allow,deny
allow from all

AddType application/x-httpd-php .php

php_flag magic_quotes_gpc Off
php_flag short_open_tag On
php_flag register_globals Off
php_flag register_argc_argv On
php_flag track_vars On
# this setting is necessary for some locales
php_value mbstring.func_overload 0
php_value include_path .

DirectoryIndex index.php
</DirectoryMatch>
```

有关更多详细信息，请参阅 [Alias](https://example.org/alias)（第 923 页）和 [Allow](https://example.org/allow)（第 930 页）。
