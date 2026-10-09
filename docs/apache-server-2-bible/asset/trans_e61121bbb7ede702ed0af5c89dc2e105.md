

- **跨主要操作系统平台可移植** — PHP 可在所有主要平台上运行，包括 Unix、Linux、Windows、OS/2 和 Mac OS。
- **跨主要 Web 服务器平台可移植** — 在 PHP 4.0 中，Web 服务器接口（Server API，或 SAPI）已被抽象化，使其能够与包括 Apache、IIS、IPanet/Netscape Enterprise Server 和 Zeus 在内的不同 Web 服务器良好集成。
- **内置对主要数据库的支持** — PHP 为所有主要数据库实现了原生接口，包括 MySQL、Postgres、Oracle、DB2 和 MS SQL Server，这使其成为数据库驱动 Web 开发的理想选择。
- **高性能** — PHP 4 为高性能进行了重新设计；它比 PHP 3 快许多倍。Zend Technologies 提供的一个免费附加模块称为 Zend Optimizer，可以将应用程序优化到比未优化的快 40 到 100 倍。许多大型 Web 站点正在使用 PHP；你可以在 www.php.net 的 PHP 官方网站上了解它们。
- **对新开发者易于学习** — PHP 是一种类似 C 的语言，具有自动内存管理（即，无需担心指针）。PHP 还具有 Perl、Java 和 C++ 的元素。任何熟悉这些主要语言的人都可以在数小时到数天内学会 PHP。
- **支持互联网标准** — 支持互联网标准，包括 IMAP、FTP、POP、XML、W3DX、LDAP、NIS 和 SNMP。这意味着 PHP 可以轻松地与不同的标准和技术进行接口对接——全部通过一个通用的工具集完成，无需昂贵的第三方模块。
- **对企业友好** — 许多大型企业已经采用了 Java 平台，而这些公司中的许多 Java 布道者往往总是想方设法将 Java 变成即使是最小项目的“理想”平台，这通常会导致漫长的开发周期。此类公司通常倾向于对其它技术说“不”，理由是其他核心业务逻辑已经用 Java 实现，因此没有 PHP 或其同类技术的空间。现在你可以说，别着急！PHP 4 支持在任何拥有 Java 虚拟机（JVM）的系统上直接访问 Java 对象。它甚至支持 Windows 平台上的分布式 COM（DCOM）。PHP 正积极整合 Java 和其他企业技术，使得拒绝 PHP 变得越来越困难。
- **开源社区** — 开源已被证明是一种非常有效的软件开发方法。作为 Apache 软件基金会的一个开源项目，PHP 享受这一方法带来的益处。PHP 核心开发者参与了许多开源支持论坛，如 Usenet 新闻组和 IRC 频道。许多 Web 软件咨询公司也提供商业支持。

## PHP 的前置条件

大多数使用 PHP 的网站同时也使用 MySQL 作为数据库。如果你计划使用 MySQL，你应该从 www.mysql.com/downloads/index.html 下载 MySQL 的源代码或二进制发行版。阅读安装文档以了解如何在你系统上安装 MySQL。你还需要 MySQL 开发包。覆盖所有平台的 MySQL 安装超出了本书的范围。

在我运行 Apache 的 Linux 系统上，我安装了：

- i386 系统的服务器 RPM
- i386 系统的客户端程序 RPM
- i386 系统的开发用包含文件和库 RPM
- i386 系统的客户端共享库 RPM

如果你想编译支持 MySQL 的 PHP，则需要这些包含文件和库。

# 编译和安装 PHP

当前版本的 PHP 是 4.0。你可以从 `www.php.net` 下载 PHP 的源代码或二进制发行版。本节假设你已下载了最新的 PHP 源代码发行版，`php-4.1.0.tar.gz`。

> 如果你在 Windows 平台上，请阅读第 21 章“运行 PHP 脚本”以了解如何为 Apache 安装 PHP。

下载源代码发行版后，使用 `tar xvzf php-4.1.0.tar.gz` 命令在目录中提取源代码。我建议你将其安装在与安装 Apache 源代码相同的目录中。例如，如果你将 Apache 源代码安装在 `/usr/local/src/httpd-2.0.16` 目录中，那么请将 PHP 提取到 `/usr/local/src` 目录中。将会创建一个名为 `php-4.1.0` 的新子目录。

此时，你必须决定你计划如何运行 PHP。PHP 可以作为 Apache 模块运行（嵌入在服务器本身中或作为 DSO 模块），也可以作为 CGI 解决方案。CGI 解决方案意味着你在使用 PHP 脚本时不会比常规 CGI 脚本获得任何性能优势，因为每次处理 CGI 模式的 PHP 脚本时都会加载一个 PHP 解释器。

## 将 PHP 构建为 CGI 解决方案

与 Perl 类似，PHP 既可以用于独立脚本，也可以嵌入在 Web 页面中。要构建用于 CGI 模式操作的 PHP 解释器，请执行以下操作：

1. 以 root 用户身份切换到 PHP 源代码发行版目录并运行：
   `./configure --enable-docs-path`
2. 现在运行 `make && make install` 以在你的系统上编译和安装 PHP 解释器。

## 将 PHP 构建为 Apache 模块

你可以将 PHP 模块存储在 Apache 二进制文件中，或者将其作为 DSO 模块安装在 Apache 上。DSO 模块的一个优点是，只需在 `httpd.conf` 中注释掉一行配置即可将其卸载，从而节省一些内存。

### 将 PHP 构建为静态 Apache 模块

我假设你已将 Apache 源代码安装在 `/usr/local/src/httpd-version` 目录中，并将 PHP 源代码安装在 `/usr/local/src/php-version` 目录中。以下是如何编译和安装静态 Apache 模块的 PHP：

1. 如果你尚未安装 Apache，请以 root 用户身份从 Apache 源代码发行版目录运行以下命令：

   ```
   ../configure --prefix=/usr/local/web/apache
   ```
   
   如果需要，你可以添加其他选项。运行 `./configure --help` 以确定是否有其他适合你需求的选项。

2. 现在从 PHP 源代码发行版目录运行：

   ```
   ./configure --with-apache=../httpd-version \
   --with-mysql=/usr
   ```
   
   这里 `--with-mysql` 选项设置为 `/usr`，是因为 MySQL RPM 包将包含文件安装在 `/usr/include/mysql` 目录中。如果你的系统 MySQL 包含文件位于其他位置，你应该使用不同的目录名。你可以使用 `locate mysql.h` 命令来查找 MySQL 包含文件存放的位置，该命令在大多数具有 locate 数据库功能的 Unix 系统上都可用。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_455_0.png)

如果你不打算使用 MySQL 配合 PHP，或者希望使用 PHP 内置的 MySQL 支持（这仅在你不打算使用 `mod_perl` 或其他 Apache 模块配合 MySQL 时推荐），则不需要 `--with-mysql` 选项。

3. 运行 `cp php.ini-dist /usr/local/lib/php.ini` 命令，将 `php.ini-dist` 文件复制到 `/usr/local/lib` 并命名为 `php.ini`。这是稍后在“使用 php.ini 配置 PHP”部分中讨论的 PHP 配置文件。
4. 运行 `make && make install` 以编译和安装 PHP 部分的源代码。
5. 现在切换到 Apache 源代码发行版目录并运行：

   ```
   ./configure --prefix=/usr/local/apache
   --activate-module=modules/php4/libphp4.a
   ```
   
   你可以在上述命令行中添加任何其它选项。运行 `./configure --help` 命令以获取有关其他选项的信息。

6. 运行 `make && make install` 以编译和安装支持 PHP 的 Apache。
7. 运行 `/usr/local/apache/bin/apachectl restart` 命令以重新启动（或启动）Apache。

# 将 PHP 构建为动态共享对象（DSO）模块

在你将 PHP 作为 DSO 模块使用之前，必须已在 Apache 中启用 DSO 支持。要重新编译具有 DSO 支持的 Apache，请执行以下操作：

1. 以 root 用户身份从 Apache 源代码发行版目录运行以下命令：

   ```
   ./configure --prefix=/usr/local/apache --enable-so
   ```
   
   你可以根据需要添加其他选项。

2. 你可以使用 `make && make install` 命令编译和安装 Apache。

在你拥有一个启用 DSO 支持的 Apache 服务器后，你可以执行以下操作来为 PHP 创建一个 DSO 模块：

1. 以 root 用户身份从 PHP 源代码发行版目录运行以下命令：

   ```
   ./configure --with-apxs2=/usr/local/apache/bin/apxs \
       --with-mysql=/usr
   ```
   
   这里 `--with-mysql` 选项设置为 `/usr`，是因为 MySQL RPM 包将包含文件安装在 `/usr/include/mysql` 目录中。如果你的系统 MySQL 包含文件位于其他位置，你应该使用不同的目录名。你可以使用 `locate mysql.h` 命令来查找 MySQL 包含文件存放的位置，该命令在大多数具有 locate 数据库功能的 Unix 系统上都可用。

2. 现在运行 `make && make install` 以编译和安装 Apache 的 PHP DSO 版本模块。
3. 运行 `/usr/local/apache/bin/apachectl restart` 命令以重新启动（或启动）Apache。

# 配置 Apache 以支持 PHP

在你已安装 Apache 的 `mod_php` 模块并配置了前面讨论过的 `php.ini` 之后，你就可以配置 Apache 以支持 PHP 如下：

1. 如果你已将 PHP 编译并安装为 Apache 的 DSO 模块，请将以下行添加到 `httpd.conf` 文件中：

   ```
   LoadModule php4_module    modules/libphp4.so
   ```

2. 将以下行添加到 `httpd.conf` 文件中

   ```
   <Files *.php>
     SetOutputFilter  PHP
     SetInputFilter   PHP
   </Files>
   ```
   
   这告诉 Apache 任何带有 `.php` 扩展名的文件都必须被视为 PHP 脚本，并应使用 PHP 输入和输出过滤器进行处理。

