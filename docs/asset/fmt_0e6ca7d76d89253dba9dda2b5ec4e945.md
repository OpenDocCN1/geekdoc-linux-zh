
# 使用此 shell 脚本重新运行 APACI

## 配置此脚本以恢复你的配置

## 可以提供额外的参数

```bash
.configure \n--prefix=/usr/local/apache \n--disable-module-cgi \n"$@"
```

假设现在你想启用 usertrack 模块。你可以按照如下方式再次运行 `configure`：

```bash
.configure --prefix=/usr/local/apache \n--disable-module-cgi --enable-module=usertrack
```

或者，你可以运行：

```bash
.config.status --enable-module=usertrack
```

如你所见，`config.status` 让使用 `configure` 的工作变得更加简单。我建议你在今后所有的编译中都使用它。另外注意，如果你决定从头开始，只需删除 `config.status` 并运行 `configure` 来创建一个全新的 `config.status`。

# 添加 FastCGI 支持

在为你的 Apache 添加 FastCGI 支持之前，你必须从 FastCGI 网站（http://www.fastcgi.com/）下载最新的 FastCGI 模块（`mod_fastcgi.c`）。

- 第一步是提取 FastCGI 模块分包。然后，将分包拷贝或移动到 Apache 源码分发的 `SRC/MODULES/FASTCGI` 目录。接着，切换到 Apache 源码分发的顶级目录并按如下方式运行配置脚本：

```bash
.configure \n--activate-module=src/modules/fastcgi/libfastcgi
```

如果你之前使用 APACI 编译过 Apache，并希望保留现有配置以及新的 `mod_fastcgi.c` 模块更新，请运行以下命令：

```bash
.config.status \
-activate-module=src/modules/fastcgi/libfastcgi.a
```

# 第四部分：设置内网/互联网服务

现在，运行 `make` 命令重新构建 Apache 服务器可执行文件（`httpd`）。如果没有 `get` 错误信息，请再次带上 `install` 运行 `make` 命令以重新安装 Apache 可执行文件。

一旦构建了新的 Apache 可执行文件，你应该检查并验证 `mod_fastcgi.c` 模块是否包含在可执行文件中。验证此最简单的方法是运行以下命令：

```bash
/path/to/your/apache/httpd -l
```

确保你使用的是适当的路径，而不是前面所示 `/path/to/your/apache`。你应该在 `-l` 选项产生的输出中看到 `mod_fastcgi.c`。如果你没有看到它，说明你漏掉了编译 Apache 的一个或多个步骤，请返回并检查你的步骤。

# 在 Apache 中嵌入 Perl 解释器

确保你的系统上安装了最新版本的 Perl。使用 `perl -v` 命令检查已安装的 Perl 版本号，并与 http://www.perl.com/ 上的最新版本进行比对。如果你没有最新版本，我建议你下载并安装它。我在本书中使用的是 5.005-002 版本。

一旦你在目标系统上安装了 Perl，你需要从 http://perl.apache.org 下载最新版本。

此外，许多用于验证 `mod_perl` 安装的测试可能需要安装 LWP Perl 模块以及 LWP 的先决模块，这可能是个好主意。如果你已经正确安装了 Perl，可以使用 CPAN 模块轻松地安装 LWP 模块。按如下方式运行 CPAN：

```bash
perl -MCPAN -install LWP
```

完成这些先决工作任务后，你可以安装 `mod_perl` 模块。

向你的 Apache 服务器安装 `mod_perl` 支持分为两个部分。首先，你必须用 `mod_perl` 更新 Perl 分发，然后用 `mod_perl` 更新 Apache 分发。为了简化起，我假设你已经从 http://perl.apache.org 下载并解压了 `mod_perl` 源码分包，该目录使得 Apache 源码和 `mod_perl` 源码共享同一个父目录作为顶级目录，换句话说，Apache 源码和 `mod_perl` 源码分发都是同一个父目录的子目录。这里讨论的安装示例假设 Apache 服务器位于 `/usr/local/build/example/apache-1.3.6`，而 `mod_perl` 源码分包位于 `/usr/local/build/usr/local/build/mod-perl-1.16`。（注意，你的 Apache 和 `mod_perl` 版本号可能会不同。）

# 第 12 章：Web 服务

切换到源码分发目录（`/usr/local/build/usr/local/build/mod-perl-1.16`），并运行以下命令：

```bash
perl Makefile.PL APACHE_SRC=../apache-1.3.6/src \
DO_HTTPD=1 \
USE_APACHE=1 \
PREP_HTTPD=1 \
EVERYTHING=1
```

这将构建 `mod_perl` 的 Perl 端，并准备 `mod_perl` 的 Apache 端。一旦你运行了上述命令，只要没有错误信息中断操作，就可以运行以下命令：

```bash
make
make test
make install
```

你现在必须完成 `mod_perl` 安装的 Apache 端。如果是第一次编译 Apache，你可以从 Apache 源码分发中运行以下命令：

```bash
.configure -prefix=/path/to/where/you/want/to/install/apache \
-activate-module=src/modules/fastcgi/libfastcgi.a
```

然而，如果你已经编译过 Apache，请使用以下命令：

```bash
.config.status
```

这将构建 `mod_perl` 的 Perl 端，并准备 `mod_perl` 的 Apache 端。一旦你运行了上述命令，只要没有错误信息中断操作，就可以运行以下命令：

```bash
make
make test
make install
```

你现在必须完成 `mod_perl` 安装的 Apache 端。如果是第一次编译 Apache，可以从 Apache 源码分发中运行以下命令：

```bash
.configure -prefix=/path/to/where/you/want/to/install/apache \
-activate-module=src/modules/fastcgi/libfastcgi.a
```

然而，如果你已经编译过 Apache，请使用以下命令：

```bash
.config.status
```

# 添加 PHP 支持

在安装 PHP 之前，请确保从 http://www.php.net/ 下载了最新分包。一旦解压了分包，切换到你的 Apache 源码分发目录并按如下运行配置脚本：

```bash
.configure \
--prefix=/path/to/your/apache
```

# 第四部分：设置内网/外网服务

```
KeepAliveTimeout 15
MinSpareServers 5
MaxSpareServers 10
StartServers 5
MaxClients 150
MaxRequestsPerChild 30
```

现在，让我们仔细查看这些每一个指令。

# 作为独立或 inetd 服务器运行 APACHE

默认 `httpd.conf` 配置文件的第一个指令是 `ServerType`。该指令指定了 Web 服务器的运行方式。服务器可以使用两种方法之一运行：独立运行（stand-alone）或 `inetd`。独立模式和 `inetd` 方法在功能上似乎相同，但它们存在巨大差异。区别在于服务器的性能。由 `inetd` 运行的进程在完成请求服务后就会退出。而在独立模式下，Web 服务器进程在消失之前会持续运行一段时间。这使得它们有机会被未来的请求重用。由于独立模式消除了为每个请求启动一个新进程的开销，因此这种模式效率更高。默认值（stand-alone）适用于大多数网站。如果你决定坚持使用此默认值，可以跳过本节的剩余内容。然而，如果你倾向于将 Apache 作为 `inetd` 服务器运行，请将此指令设置为 `inetd` 值。

然后，你需要编辑 `/etc/inetd.conf` 文件，为 Apache 添加一条新记录。该文本文件具有特定的记录格式，你应该通过查看文件中的现有条目来确定该格式。对于 Red Hat Linux 系统，`inetd.conf` 的语法如下：

```
service_name sock_type proto flags user server_path args
```
