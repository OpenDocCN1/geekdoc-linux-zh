
当前正在运行的所有进程，其中应该包含`apache`或`httpd`。如果你没有看到其中一个，请检查`Apache error.log`，因为它可能会提供关于导致失败的某些见解。

## 添加模块

安装是配置某些`Apache`模块的好机会，这些模块对于构建稳健且安全的网站很有帮助。你也可以随时安装额外的模块，因为`Apache`支持动态加载模块。我们将查看的一些流行选项是`Perl`、`PHP`和`SSL`。

## 从 RPM 安装

`RPM`由`Red Hat`创建，是一个优秀的软件包系统。这种格式的包要么是预编译的二进制文件要么是源码，并将安装系统上的所有内容。它还会维护已安装软件包的数据库，并通知你依赖和冲突。虽然这无法提供太大的特殊性，但从原始编译使得任务变得极其简单。要从`RPM`安装，请执行以下命令：

```bash
rpm -ivh apache-1.3.20.rpm [使用下载的文件名]
```

这将正确安装包并显示进度条。你还应该自动启动服务器，但请检查列表以确保万无一失。更多信息和选项请访问`http://rpm.com`，你将在那里找到最新版本的`RPM`。

## 在 Debian 下安装

`Debian`是一个`Linux`发行版，包含其名为`Apt`的软件包系统。该系统提供了软件包的在线安装。与`RPM`一样，它将维护已安装软件包的数据库并自动下载依赖。另一种选项是用传统的方法（`Debian`方法）使用`dpkg`安装包，如下例：

```bash
dpkg -i apache-1.3.9.deb [使用下载的文件名]
```

`Perl`与`Apache`的集成由`mod_perl`软件包提供。这允许创建`mod_perl`。对于`Debian`用户，`apt-get install apache`通常可以找到良好的`Apache`软件包。或者，这会将`Apache`安装到默认选项`/usr/local/apache`，并带有所有标准选项。安装目录可以通过`-prefix=/var/apache/`更改。现在可以使用命令`apache start`启动`Apache`。如果你单独执行`apache`，它将为你列出其他选项，包括`stop`（停止）、`restart`（重启）和`config`（配置）。请注意，在此以及所有类型的安装过程中，你应该通过查看当前列表来验证服务器已启动。`ps apache`命令将显示

# 在 Linux 上配置 Apache Web 服务器

作者：Thomas Nooning, CCNA, CCDA

我的文章《在 Linux 上安装 Web 服务器》已经告诉了你去哪里下载`Apache`，并解释了如何在你的`Linux`上安装它。接下来我将介绍配置`Apache` Web 服务器的基础知识。我还将向你展示如何让`Apache`在系统启动时自动运行。

## 位置、位置、位置

现在我们已经了解了为什么配置文件会以目前的形式存在，让我们来看看它们位于何处。尽管`Apache`的根目录会根据安装选项而异，但这些文件通常位于`/conf`子目录下。例如，如果你按照所有默认设置安装了`Apache`，配置文件将位于`/etc/local/apache/`。

## 使用配置文件

与许多基于`Linux`的程序一样，`Apache`的配置是通过在纯文本文件中放置指令（directives）完成的。在这种情况下，文件被称为`httpd.conf`、`sd.conf`和`access.conf`。它们的位置和重要性可能因具体的安装情况而异，但格式保持不变。通过这些文件，你可以选择在何处提供 Web 文档、启动时动态加载哪些模块，以及`Apache`将监听哪个端口。

这意味着你每次都必须使用这些文件。`-command`命令行允许你在运行时从用户定义的文件加载配置。此外，来自`Red Hat`和`Debian`等发行版的预配置包可能会安装到不同的目录。在当前版本的`Debian`中，配置文件将位于`/etc/`。如果你正在使用`Red Hat`，你可能需要检查`/etc/httpd/conf`。

首先，让我们看看这三个独立配置文件文件背后的原理。这在社区中几乎带有一种类似于“三位一体”的神秘色彩。它们基本上是`NCSA 1.3` Web 服务器的遗留，并可以用不同的方式处理。

如果你运行了多个版本的`Linux`，你就知道目录结构和文件位置可能会有所不同。如果有疑问，在更新了文件数据库后，运行`locate httpd`或`locate apache`有助于确定确切位置。

一种方案是使用`httpd.conf`作为全局配置，使用`sd.conf`控制名称，使用`access.conf`设置服务器的访问控制。另一种方法是仅使用`httpd.conf`，它将支持任何可以放在另外两个文件中的指令。通过在`httpd.conf`中放置`Options AccessConf/dev/null`和`ResourceConfig/dev/null`，你可以告诉`Apache`只向该文件查找配置。

## 配置服务器

指令每行一个输入到配置文件中，并且区分大小写。命令末尾的反斜杠可以将条目扩展到多行。如果你不确定指令是否正确，`Apache`会对你的语法提供一些基础的错误检查。如果`Apache`发现某个命令存在问题，它会给你提供行号。记住，你仍然必须运行`apache start`来初始化服务器。让我们来看来自`httpd.conf`的一些标准`Apache`指令（你可以使用任的文本编辑器，如`vi`或`nano`打开它）：

另一种方法是分别使用`httpd.conf`、`sd.conf`和`access.conf`目录。服务器将自动解析位于上述配置文件中的任何文件和子目录。这将允许你以非常具体的程度将项目拆分为虚拟主机（VirtualHosts）。

```
# ServerType 既可以是 inet

## 或 standalone。

ServerType standalone

# # Port: standalone 监听的
# 端口。对于小于 1023 的端口，
# 我们最初需要让 httpd 以 root 身份运行。

Port 80

# # Document Root: 你将从中
# 提供文档的目录。
# 默认情况下，所有请求都从
## 此目录获取，符号
# 链接和别名可能被用于
## 指向其他位置。

DocumentRoot /var/www/

# # 动态共享对象 (DSO) 支持
# 为了能够使用作为 DSO 构建
# 的模块的功能，你必须在此
# 位置放置相应的
# 'LoadModule' 行。

LoadModule php4_module /usr/lib/apache/1.3/libphp4.so

# # AddType 允许你在不实际编辑
# 情况下调整 mime.types，
# 或将某些文件设置为
# 特定类型。

AddType application/x-httpd-php .php
.php3 .php
```

注意，指令之前都有注释，有助于解释语法和功能。几乎每一个配置选项都是定义某些文件本身——这是一项新功能就像我一样，只有当你无法通过其他方式解决问题时才会去阅读文档。一个值得注意的是`Load-Module`命令。在安装与`Apache`相关的程序时，你可能需要编辑配置以在启动时加载模块。如果你在`Apache`之后安装了`PHP`，你将需要上面的命令并配合`AddType`指令以确保`Apache`会处理`PHP`文件。

上面的示例是非常标准的，可能不需要编辑。然而，某些指令会随服务器的不同而改变。这些的一些示例包括：

- `ServerName`
- `ServerAdmin`
- `Bind/Address`

`ServerName`指令设置服务器的主机名，通常是一个完全限定域名。这避免了服务器尝试通过`IP`地址查找主机名，这可能不会返回你想要的结果。使用此内容的示例为：
`ServerName www.techpublic.com`

`ServerAdmin`选项仅仅是服务器的电子邮件地址。如果向多个 Web 服务器发送邮件（则使用）。

`Bind/Address`告诉`Apache`监听机器上所有的`IP`地址。如果你不想监听所有地址，这可能很重要。

# 启动 Apache

`Apache`可以手动启动，也可以在启动时自动启动。对于手动操作，你使用`apachectl`。如之前提到的，可以向此命令传递多个参数。在对配置进行更改后重启，你使用`graceful`。

要在系统启动时加载服务器，可以可以在`init.d`或`rc`中放置脚本以从`rc`调用`apachectl`。例如，列表`A`显示了你在`/etc/init/`中的脚本，或者如果上述建议在你的`Linux`系统上不起作用。

## 结论

`Apache`服务器与任何功能齐全的程序一样，有多种配置选项。主配置文件存储在纯文本文件中，可以通过你选择的文本编辑器轻松访问。除了配置文件中的注释外，`Apache`在`http://httpd.apache.org/docs`提供了关于指令和配置选项的优秀文档。

- 列表`A`：`Apache`启动脚本

```bash
## /bin/bash

#

# apache Start the apache HTTP server

#

NAME=apache

PATH=/usr/bin:/sbin:/usr/sbin/sbin

DAEMON=/usr/sbin/apache

suecex=/usr/lib/apache/sexec

PIDFILE=/var/run/$NAME.pid

CONF=/etc/apache/httpd.conf

APACHECTL=/usr/sbin/apachectl

trap "" 1

export LANG=C

test -f $DAEMON || exit 0

test -f $APACHECTL || exit 0

if egrep -i "[[:space:]]*ServerType[:space:]]+inet $CONF

then

  exit 0

fi

case "$1" in

  start)

    echo -ne "Starting web server: $NAME.\n"

    APACHECTL start

    ::

  stop)

    echo -ne "Stopping web server: $NAME.\n"

    APACHECTL stop

    ::

exit 0
```

# 安装 Apache 和 PHP

作者：Vincent Danen

在本文中，我们将介绍`Linux`下最流行的软件包之一：`Apache`服务器。`Apache`是一个开源的 Web 服务器，几乎存在于每一种`Linux`发行版中，它可能是今天互联网上最流行的 Web 服务器之一。它具有极佳的可移植性，因为它可以在`Linux`、`BSD`、`Unix`、`Windows`、`OS/2`甚至`BeOS`上运行。

由于大多数`Linux`发行版都带有一个`Apache`，因此你只需要很快就能学会从头开始构建。大多数情况下，你会使用`RPM`或`DEB`包来升级系统，但某些情况可能需要系统管理员从头构建并安装`Apache`。这在旧版系统中很常见，因为新版本的服务器可能存在依赖问题。通过`RPM`和`DEB`包安装`Apache`看起来非常简单，但我们建议查看一下那种安装方法，而我们将直接处理源码。

## 编译 Apache

`Apache`的配置是通过`configure`脚本完成的。这并不是你在实际配置文件中看到的配置。在在这里，你配置的是`Apache`的一些默认值，例如文件的安装位置、对额外功能和模块的支持等。

假设你已经安装了`Apache`，只是想在将整个系统迁移之前，测试运行新版本的`Apache`。这有助于确保在切换之前在使用新`Apache`时没有遇到困难，并且如果遇到问题可以最大限度地减少停机时间。

为了实现这一点，我们将把`Apache`安装在`/usr/local`而不是`/usr`目录树。这意味着 Web 服务器将安装到`/usr/local/apache`而不是`/usr/bin`。这样做，我们将如下配置：

```bash
./configure --prefix=/usr/local/apache
```

但我们并不是为了安装`Apache`（因为因为它提供了我们可能需要的某些）。相反，我们将运行列表`A`中的配置。

这比上一个例子多做了几件事，这些可能对你的网站至关重要。告诉`configure`我们希望最终安装位置在`/usr/local/apache`，并告诉它启用所有模块。默认情况下，`Apache`会启用模块，但不是所有模块，有些非常有用的模块，比如`mod_rewrite`。我们要启用的下一步是对最大数量模块的动态共享对象 (DSO) 支持，在我们的情况下是所有模块。启用 DSO 支持很重要，因为它允许你通过简单的重新配置并重启`Apache`来加载和卸载模块，而如果你想移除对特定模块的支持或添加对另一个模块的支持，则无需重新编译。

## 获取 Apache 源码

你首先需要获取源代码。你可以选择`Apache`的最新版本，也可以选择最近的开发版本（截至本文为`2.016 (beta)`版）。从`http://apache.org/dist/file/apache_1.3.20.tar.gz`下载最新版本。将此文件保存到`/usr/local/src`目录。

下一步是解压存档。通过`root`身份完成：

```bash
cd /usr/local/src
tar xzvf apache_1.3.20.tar.gz
```

你现在会在`/usr/local/src`树下有一个`apache_1.3.20/`子目录。现在进入该目录。是时候运行`configure`脚本了，它将设置我们的`Apache`选项。

![Image](img/18a4efcf5db19984d10d986ab04de74b_106_0.png)

服务器与服务 91

## 列表 A：使用 configure 安装 Apache

```bash
./configure --prefix=/usr/local/apache \
    --enable-module=all --enable-shared=max \
    --disable-module=auth_db --disable-module=auth_digest \
    --with-perl=/usr/bin/perl --enable-suxec --suxec-caller=nobody \
    --suxec-safepath=/bin:/usr/bin:/local/bin
```

我们接做的工作是启用两个模块：`auth_db`和`auth_digest`。`auth_db`模块用于`HTTP`基础认证，用户名和密码存储在`DBMS`数据库中而不是明文密码文件中。`.htpasswd`文件要简单一些，这就是为什么我选择禁用这个模块。`auth_digest`模块是`mod_digest`模块的更新版本，允许使用`MD5`摘要进行用户验证。该模块被团队标记为实验性模块，所以如果你想使用`MD5`认证，可以使用`mod_digest`模块；然而，`auth_digest`在当前服务器上可能运行良好。如果你坚持要用`MD5`认证，请先尝试`mod_digest`，如果无效，再构建`auth_db`并使用它。请注意，你可以二选一，不能兼用。

执行`make install`然后坐下，喝杯咖啡，让编译器工作。这可能需要一些时间，取决于你机器的速度。不过，你可能会在构建过程中遇到一些困难。我在尝试编译`mod_rewrite`模块时遇到了一个问题，它在构建中找不到`gdbm.h`文件。由于`Apache`只在`src/include`中查找，而不在系统包含或子目录中查找，我创建了一个指向`/usr/include/gdbm/gdbm.h`的软链接（你必须安装`gdbm`开发库；所有使用`RPM`或`DEB`的发行版都是如此）。

```bash
ln -s /usr/include/gdbm/gdbm.h /usr/local/src/apache_1.3.20/src/include/gdbm.h
```

最常用的。例如，如果你希望`PHP`与你的`MySQL`数据库交互，你就需要启用`MySQL`支持。

`8080`。这将告诉`Apache`绑定到`8080`端口，这适用于测试。

最后，你需要编译`PHP`。实现方法与编译`Apache`相同，只需运行两个魔术命令：

```bash
make
make install
```

你还需要取消`PHP`支持的注释。在同一个文件中，转到第 843 行并取消以下两行的注释：

```
AddType application/x-httpd-php .php
AddType application/x-httpd-php-source .php
```

大功告成！你现在安装了`Apache`服务器及其`PHP`支持。

# 测试 Apache 和 PHP

保存你的更改。现在我们想要启动`Apache`，为了这样做，我们将使用以下命令：

```bash
/usr/local/apache/bin/apache start
```
