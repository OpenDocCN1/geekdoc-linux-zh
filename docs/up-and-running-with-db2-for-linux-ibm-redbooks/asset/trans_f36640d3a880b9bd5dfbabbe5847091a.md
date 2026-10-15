

Edition media packs. Run db2setup to install this product using the installation wizard.

- 2. 安装 Perl 5。Perl 通常由 Linux 发行版提供，但你也可以从以下位置下载：
  http://www.cpan.org/

- 3. 构建、测试并安装 DBI 模块。DBI 是一个开放标准 API，可为用 Perl 编写的客户端应用程序提供数据库访问。通用的 Perl DBI 模块可以从 CPAN 网站下载：
  http://www.cpan.org/modules/by-category/07_Database_interfaces/DBI/
  请参考该网站上的 Readme 文件获取安装说明。

- 4. 构建、测试并安装 DBD::DB2 驱动程序。
  DBD::DB2 驱动程序与 DBI 和 DB2 客户端配合使用以访问数据库。
  最新版的 DB2 Perl DBI 驱动程序可以从以下位置下载：
  http://www.ibm.com/software/data/db2/perl/
  在撰写本文时，最新可用的驱动程序为 DBD-DB2-0.76。

  - 在安装 DBD::DB2 驱动程序之前，将 DB2_HOME 环境变量设置为安装目录：
    export DB2_HOME=/opt/IBM/db2/V8.1

  - 通过输入以下命令解压 DBD-DB2-0.76。在此示例中，我们将解压到 /db2home/db2inst1/perl 目录。
    tar xzf DBD-DB2-0.76.tar.gz -C /db2home/db2inst1/perl
    设置此文件的权限以允许 DB2 用户访问。

  - 在 DBD-DB2-0.76 目录中，以 DB2 用户身份登录并运行以下命令以构建和安装 DBD::DB2 驱动程序：
    perl Makefile.PL
    make
    make test
    - make 命令构建软件
    - make test 命令执行自检

  - 现在以 root 用户身份登录并运行以下命令：
    make install
    - make install 命令安装 DBI 然后删除工作目录

## 5. 启用 DBI 模块

要使 Perl 能够加载 DBI 模块，必须在你的 DB2 应用程序中包含以下行：

```
use DBI;
```

当你使用以下语法通过 DBI->connect 语句创建数据库句柄时，DBI 模块会自动加载 DBD::DB2 驱动程序：

```
my $dbhandle = DBI->connect('dbi:DB2:dbalias', $userID, $password);
```

其中：

- $dbhandle 表示 connect 语句返回的数据库句柄
- dbalias 表示在你的 DB2 数据库目录中编目的 DB2 别名
- $userID 表示用于连接数据库的用户 ID
- $password 表示用于连接数据库的用户 ID 的密码

> 注：Red Hat 8.0 和 SuSE 8.1 包含 Perl 和 Perl DBI RPM 包（Red Hat：perl-5.8.0-55.i386.rpm 和 perl-DBI-1.30-1.i386.rpm；SuSE：perl-5.8.0-57.i586.rpm 和 perl-DBI-1.28-30.i586.rpm）。要使用 Perl 创建 DB2 应用程序，Red Hat 8.0 和 SuSE 8.1 用户只需安装并编译 DBD::DB2 包即可。

剩下的就看你了。以下是 DB2 上 Perl 应用程序开发的一些良好参考资料：

http://perl.apache.org/docs/1.0/guide/
你需要了解的关于 mod_perl 技术的一切。

http://dbi.perl.org/
关于 DBI 的有用信息。

http://www.ibm.com/software/data/db2/perl/
IBM DB2 Perl 数据库接口网站。

http://www2.boulder.ibm.com/dmd/library/tutorials/db2linux/db2linux.html
在此网站底部有一个有用的教程，名为“使用 Perl 访问 DB2 for Linux”。

### 8.3.2 PHP

如果你想创建 Web 启用的数据库应用程序，你应该考虑使用 DB2 for Linux 与 PHP（超文本预处理器语言）。PHP 是一种服务器端、跨平台脚本语言，允许你将应用程序逻辑直接嵌入到 HTML 文件中。它可用于从基于 Web 的应用程序访问 DB2 以生成定制的动态内容或从 Web 浏览器捕获数据库事务。它支持使用 Unified-ODBC 访问方法访问 DB2，其中用户级 PHP 通过 DB2 CLI 层使用 ODBC 调用与 DB2 通信。PHP 最常用的是与 Apache Web 服务器一起使用，但也适用于其他 Web 服务器，如 WebSphere、thttpd 和 AOLServer。PHP Apache 模块作为 Apache（httpd）进程的一部分运行。

下面我们提供了一些有用的网站参考，可帮助你使用 Apache 服务器设置 PHP 和 DB2。

- 要下载和安装 Apache Web 服务器，请参考：

  http://httpd.apache.org

  该网站告诉你有关在 Linux 上安装和配置 Apache 的所有需要了解的信息。它针对 Red Hat，但也应适用于其他发行版。

- 要在 Linux 上为 Apache 1.x.x 下载和安装 PHP 4.x，请访问：

  http://php.apache.org

  这是一个很棒的网站，提供有关如何获取、安装、编译和设置 Linux 上 Apache 的 PHP 的详细、易于遵循的说明。

- 有许多配置步骤是必需的才能使其正常工作。这些步骤在互联网上的“使用 IBM DB2 for Linux 的 Apache Web 开发”教程中有所介绍。访问以下网站下载此教程：

  http://www7.boulder.ibm.com/dmdd/library/tutorials/db2linux/db2linux.html

### 8.3.3 C++

C++ 是一种非常流行且功能强大的编程语言。目前，DB2 for Linux 支持以下 C/C++ 编程语言和编译器：

- 对于 Intel x86 上的 Linux：GNU/Linux gcc 和 g++ 版本 2.95.3 和 2.96

- 对于 Linux/390：GNU/Linux gcc 和 g++ 版本 2.95.3

访问 DB2 应用程序开发网站，了解有关 Linux 上 Intel 的 gcc 和 g++ 版本 3.0 支持以及 Linux/390 未来版本支持的信息：

http://www.ibm.com/software/data/db2/udb/ad

有关 DB2 上 C/C++ 编程的更多信息，请参阅 IBM DB2 UDB 应用程序开发指南：构建和运行应用程序 V8，SC09-4825。

