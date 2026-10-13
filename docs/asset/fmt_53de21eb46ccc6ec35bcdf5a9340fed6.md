
RPM 关注封装生成二进制包所需的所有组件，这防止了通用代码的重用。这种封装被称为源 RPM（source RPM），由源码、本地补丁和描述构建过程的 `spec` 文件组成。`spec` 文件扩展了某些配置信息，例如使用的编译器标志和构建包的架构。其他信息在准备程序包时作用不大。

接下来的示例遵循 SRPMS 的结构。它假设用户拥有用于 Apache 程序的红 Hat CD-ROM RPM：

```
# ls
COPYING README SRPMS TRANS.TBL
# cd SRPMS
# ls apache*
apache-x.x.x.src.rpm
# rpm -i apache-x.x.x.src.rpm
# cd /usr/src/redhat/SPECS
# ls
apache.spec
# ls /usr/src/redhat/SOURCES/
```

`rpm -i apache*` 命令安装了 `/usr/src/redhat/SOURCES` 目录中的补丁。`spec` 文件描述了针对特定架构的编译程序。

## 安装

在解压 tar 包之前，请检查内容。要执行此操作，请运行以下命令：

```
tar -tzvf apache_1.3.19.tar.gz
```

要解压 tar 包，首先切换到将解压的目录。然后，执行以下命令：

```
tar -xzvf apache_1.3.19.tar.gz
```

## 编译

要从源码编译程序，首先切换到解压包的目录。这被称为包的顶层目录。它的名称通常类似于 `apache_1.3.14`。

```
:/usr/src$ cd apache_1.3.19
```

解压 tar 包并进入生成的子目录后，执行一个大多数源码安装中通用的步骤：查看 `./configure --help` 的输出。

```
:/usr/src/apache_1.3.14$ --configure --help | less

--activate-module=src/modules/auth_mysql/libauth_mysql.a
  auth_mysql modules.
```

在编译服务器之前，向配置文件添加以下行：

```
AddModule modules/standard/mod_rewrite.o
--activate-module=src/modules/auth_mysql/libauth_mysql.a
# ./configure --enable-module=so --enable-rule=EAPI
```

`mod_status`, `--update`

用法: `configure` [options]

选项: [描述后的括号内为默认值]

通用选项:

- `-quiet`, `--silent`

  不打印消息

- `--verbose`, `-v`

  打印更多消息

- `--shadow=[~DIR]`

  切换到影子树（位于 DIR 下）

独立选项:

- `--help`, `-h`

  打印此消息

- `--show-layout`

  打印安装路径布局（检查和调试）

安装布局选项:

- `--layout=[F]:ID`

  使用安装路径 ID

二进制分发版通常包含所有选项的共享对象模块，可能是为了给用户提供选择。Apache 默认带的共享对象模块通常是需要的。因此，请编译这些模块，并允许根据需要加载额外的模块。默认设置是编译所有默认模块。

### --with-layout=RedHat

这将配置您的 Apache 文件以符合红帽（Red Hat）的文件布局。

以下是一行 `./configure` 命令行：

```
:/usr/src/apache_1.3.14$ ./configure \
--with-layout=RedHat --enable-module=so
```

### 动态共享对象

`--enable-module=so` 选项提供了以后或在运行时添加其他模块的能力。这些模块类似于可加载模块和 Linux 内核。例如，若要向服务器添加 php，只需添加 `mod_php` 即可，无需重新编译 Apache。

一旦 `configure` 脚本运行并确定了系统上可用的功能，就可以构建软件了。

## 安装

一旦源代码被编译成可执行文件，就可以进行安装。要安装程序，需要对文件将安装的目录具有写权限。在大多数情况下，这意味着需要以 root 账户登录。

> **注意** 只有安装阶段需要 root 权限。编译阶段不需要 root 权限，因此应该以非特权用户身份执行以防止问题。如果您没有 root 权限，可以将软件包安装到您具有写权限的目录中。这通常在配置阶段使用 `--prefix` 选项指定。

### 安装前测试

在许多软件包中，有一个命令可以测试程序并确保其编译正确。该命令有两种形式之一：

```
:/usr/src/apache_1.3.14$ make check
:/usr/src/apache_1.3.14$ make test
```

如果可用其中一个命令，它将运行一系列测试并报告程序是否能正常运行。可能可以在安装之前运行程序。请务必指定程序从当前目录运行：

```
:/usr/src/apache_1.3.14$/program
```

许多程序在安装之前无法运行。假设没有错误，请继续安装：

```
:/usr/src/apache_1.3.14$ make
:/usr/src/apache_1.3.14$ make install
```

这将所有程序和所有相关文件复制到适当的位置。一旦安装过程完成，退出 root 账户并尝试运行程序。

此过程通常需要一段时间，取决于软件包的大小以及计算机的内存和速度。进程完成后，用户应返回到命令行提示符且不显示任何错误消息。如果有错误，必须确定原因。最常见的原因是缺少软件包。

## 系统工具

系统工具简化了 Apache 的安装和维护。它们还缩短了更新时间并缩小了安装错误的范围。工具通常用于普通的 Web 服务器安装，从而消除了源码下载和源码编译。

### httpd 守护进程

Web 服务器使用 `httpd` 进程与客户端（如 Netscape）通信。`httpd` 守护进程通常运行在 80 端口。它为用户提供了许多 Apache 配置和自定义选项。

### 默认值

如果运行单个守护进程，请使用默认值，无需提供特殊内容。在编译之前不进行任何更改将产生一个在编译后即可立即使用的基础 Web 服务器。本节涵盖了某些默认值。

对于红帽，Apache 的主目录将是 `/usr/local/apache`（Debian 默认为 `/etc/apache`，Slackware 默认为 `/var/lib/apache`）。所有支持文件和目录将基于此位置生成。

服务器将监听主机上存在的所有网络接口。这可能是需要的，也可能不需要，但对于默认安装，它确保了 Apache 将监听在活动接口上并可用于测试。

系统提供了所有路径、启动配置和测试页面。

使用默认值配置只需在源码目录中调用以下命令：

```
$ ./configure
```

这非常简单。为了提供这种简洁易的安装过程，人们付出了大量工作，它自 Apache 1.3 发布以来一直可用。

### 定制化

如之前所述，Apache 使用类似于 GNU `configure` 脚本来为编译做一切准备。Apache 脚本的一个方面是 `configure` 可以作为参数接受的各种选项。对于通用安装，没有必要学习所有选项。

另一个重要的配置选项涉及修改步骤，我们将简要讨论这些步骤，为后面的章节做准备，在那些它们将用于 CGI 脚本等工作。

Web 服务器具有额外功能通常是必要的，例如脚本或数据库集成。此外，管理员可能不希望 Apache 位于默认目录 `/usr/local/apache` 中。若要指定对默认值的更改，可以在命令行中作为 `configure` 的选项添加它们。带有命令行选项调用 `configure` 通常具有以下形式：

```
$ ./configure --some_option=argument_forthatoption
```

因此，一个真实世界的选项类似于：

```
$ ./configure --prefix=/www
```

`--prefix` 选项告诉 `configure` 脚本服务器将安装在系统的哪个位置。查看前面的示例，可以看到 Apache 的所有文件将位于 `/www` 目录内。`--prefix` 的参数是自由形式的，因此要使用 `--prefix=/missouri`，安装脚本将使用 missouri 作为 Apache 的主目录。另一个选项是 `--with-layout=GNU`。

## 模块和 SSL

Apache 使用类似于 GNU `configure` 脚本来为编译做一切准备。Apache 脚本的一个方面是 `configure` 可以作为参数接受的各种选项。对于通用安装，没有必要学习所有选项。

另一个重要的配置选项涉及修改步骤，我们将简要讨论这些步骤，为后面的章节做准备，在那些它们将将用于 CGI 脚本等工作。
