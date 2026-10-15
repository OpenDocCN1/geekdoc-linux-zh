
`-xzf mysql-versionnumber.tar.gz`

`cd mysql-versionnumber`

`./configure --prefix=/usr/local/mysql-versionnumber`

`make`

`make install`

接下来，你将设置配置文件以指定某些管理和安全选项。你可能修改某些预制的配置文件以适应你的需求。对于 MySQL，有 `my-huge.cnf`、`my-large.cnf`、`my-medium.cnf` 或 `my-small.cnf`。这些配置文件是为不同类型的服务器设计的。例如，对于服务器，你可以选择修改 `my-small.cnf` 文件。你可以将选定的预制配置复制到配置文件目录并重命名为 `/etc/my.cnf`。将所有者分配为 `root` 并为 `root` 用户分配读写权限。通过 `vi` 编辑器，你可以在文件中添加新用户账户或启用 `innodb` 选项，该选项为 MySQL 提供了一个符合 ACID 的存储引擎，提供了提交、回滚和崩溃恢复能力。

# 在线课程数据库开发

在配置 `my.cnf` 文件后，你应该使用命令 `mysql install ab` 创建 mysql 数据库，使用命令 `mysqld_safe` MySQL 数据库服务器，并使用 `root` 账户连接新创建的 MySQL 服务器。在首次启动 MySQL 服务器后，你可以为 `root` 账户设置密码。设置新密码后重启服务器，MySQL 服务器即可可以使用。

对于 RPM 类型的安装，有两种类型的包：服务器安装包和客户端安装包。服务器安装包包含所有内容，而客户端安装包仅用于访问安装在另一台计算机上的 MySQL 服务器。如果你已经下载了 RPM 安装包，可以使用该命令对服务器和客户端 RPM 进行标准安装。

```bash
rpm -i MySQL-server-VERSION.glibc23.i386.rpm

rpm -i MySQL-client-VERSION.glibc23.i386.rpm
```

在安装文件之前，RPM 将验证软件包的完整性和真实性。服务器 RPM 包的数据将被放置在 `/var/lib/mysql` 目录下。在安装过程中，RPM 安装包将创建 `mysql` 登录用户账户。RPM 安装包还会配置 `/etc/init.d/` 文件，指定服务器将在启动时启动。如果安装成功，在安装完成后，你的 MySQL 数据库服务器应该处于运行状态。此时，你应该为 `mysql` 登录账户分配密码以确保 MySQL 服务器的安全。一旦 MySQL 数据库服务器运行，数据库设计人员和开发者就可以继续为在线教学/学习系统设计和开发数据库。

## 示例2：设置 PHP 和 MySQL 开发环境

PHP 和 MySQL 的集成为开发 Web 应用程序提供了开发环境。PHP 是一种脚本语言，用于开发动态 Web 页面。MySQL 为动态 Web 页面提供支持。要开发 PHP 和 MySQL 开发环境，你需要三个应用程序软件包：Apache Web 服务器、MySQL 和 PHP。Apache Web 服务器和 MySQL 的安装在之前已经介绍过。以下简要描述了 PHP 的安装。

第一个任务是从网站下载 PHP：

`http://www.php.net/downloads.php`

由于安装文件格式为 `.gz` 文件，你可以使用 `tar -xzf` 命令解压 PHP 安装文件。下一步是使用命令 `./configure` 对文件进行编译。使用 `make` 命令创建用于安装的可执行文件，并执行命令 `make install` 来安装 PHP 包。在初始安装之后，PHP 模块将添加到 Apache Web 服务器中。然后再次运行 `make` 和所有命令完成安装。

安装 PHP 后，允许 PHP 访问 MySQL，应使用 `ln` 命令从 `/chroot/httpd/tmp/` 创建一个指向 `/chroot/mysql/tmp/mysql.sock` 的链接。这两个文件将物理地被放置在同一个文件系统中。要测试 PHP 的安装，你可以创建一个包含以下内容的 `.php` 文件。

```php
<?php phpinfo();
?>
```
