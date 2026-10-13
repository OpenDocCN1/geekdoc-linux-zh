
The IRIXNIS rule is for people who want to use Apache on a Silicon Graphics system running IRIX and NIS. The IRIXN32 option is also meaningful for systems running an IRIX operating system. It tells Apache to use n32 libraries instead of o32 libraries.

The PARANOID rule allows you to see whether any Apache module is executing any shell scripts during configuration. Apache 1.3 allows modules to execute custom shell scripts when the configure script is run. This rule is turned off by default. If you want to enable it, set this to Yes using the --enable-rule=PARANOID option in the command line of the configure script.

The WANTHSREGEX option is automatically set to Default. This specifies that you want to use the regular expression package included with Apache. If you'd rather use your own system's regular expression package, however, you can set this option to No using the --disable-rule=WANTHSREGEX option in the command line of the configure script.

## 模块配置选项

默认模块集是通过使用 AddModule 行添加到标准 Apache 中的。模块按反向优先级顺序列出。如果您计划添加其他模块，请不要手动修改此文件。使用 configure 脚本来添加、删除、启用或禁用模块。

要启用默认未启用的模块，请使用 --enable-module=NAME 选项。要禁用模块，请使用 --disable-module=NAME 选项。例如，要禁用 CGI 模块，请使用以下命令：

```
./configure --prefix=/usr/local/apache --disable-module=cgi
```

或者，要启用用户跟踪模块，请按如下方式运行 configure：

```
./configure --prefix=/usr/local/apache --enable-module=usertrack
```

在使用前面讨论的一个或多个选项成功运行 configure 脚本后，您就可以编译和安装 Apache 了。

## 编译和安装 Apache

在运行 configure 脚本后，编译和安装 Apache 非常简单。只需从 Apache 源代码分发的顶层目录运行 make 命令即可。如果一切顺利，您将看不到任何错误消息。在这种情况下，您可以通过运行 make install 命令来安装 Apache。如果在运行 make 时出现错误，请记下错误消息并重新进行配置步骤。如果您仍有问题，请访问 Apache 网站并阅读 FAQ，以了解是否需要做其他事情才能让 Apache 运行。在我的经验中，标准 Apache 源代码分发在 Red Hat 上可以毫无问题地编译。因此，如果事情无法正常工作，请在寻求 Usenet 新闻组（如 comp.infosystems.www.servers.unix 和 linux.redhat）的帮助之前先仔细检查您的步骤。

编译并安装 Apache 后，运行 make clean 以删除编译期间创建的所有目标文件。

## 编译和安装 Apache 支持工具

当您使用 configure（或 config.status）脚本配置 Apache 时，它会自动安装一套支持工具。唯一的例外是 logresolve.pl Perl 脚本，您需要手动安装。如果您不想安装任何支持工具，可以在运行 configure（或 config.status）时提供 --without-support 选项。我强烈建议保留默认设置，因为支持工具在管理 Apache 的各个方面非常有帮助。

### apachectl

使用此脚本，您现在可以控制 Apache。要确定它接受哪些命令行选项，请不带任何命令行选项运行它，或按如下方式使用 help 选项：

/path/to/apache/bin/apachectl help

要启动服务器，请按如下方式运行脚本：

/path/to/apache/bin/apachectl start

要停止服务器，请按如下方式运行脚本：

/path/to/apache/bin/apachectl stop

要重启服务器，请按如下方式运行脚本：

/path/to/apache/bin/apachectl restart

要执行优雅重启，请按如下方式运行脚本：

/path/to/apache/bin/apachectl graceful

对于好奇的人来说，restart 参数会使 apachectl 向 Apache 发送 SIGHUP 信号，而 graceful 参数则改为发送 SIGUSR1 信号。由于后者是用户定义的（由 Apache 开发人员定义），因此对正在运行的服务器来说要友好得多。

要获取正在运行服务器的完整状态，请按如下方式运行脚本：

/path/to/apache/bin/apachectl fullstatus

您将获得一页显示各种服务器状态数据的信息。由于它很可能超过一屏的详细信息，因此建议将状态信息重定向到文件。以下是如何将数据重定向到名为 /TMP/STATUS 的文件：

/path/to/apache/bin/apachectl fullstatus >
/tmp/status

要测试服务器配置文件是否存在语法错误，请按如下方式运行 apachectl 脚本：

/path/to/apache/bin/apachectl configtest

### ab

此实用程序允许您对 Web 服务器运行基准测试。不带任何选项运行程序以了解其接受的命令行选项。

### apxs

此实用程序有助于编译用于动态加载的模块。除非在 Apache 服务器上启用了动态共享对象（DSO）支持，并且您的操作系统支持 DSO，否则它没有用。

### logresolve.pl

此 Perl 脚本不会自动安装，但您可以从 Apache 源代码分发的 src/support 目录手动将其复制到适当的位置。此脚本将 Apache 日志文件中找到的 IP 地址解析为其主机名。此脚本生成子进程并使用父进程提供缓存支持以加快 DNS 查找速度，而 DNS 查找通常非常慢。

### logresolve

此实用程序的工作方式与 logresolve.pl 脚本基本相同，只是此可执行程序默认会被安装。要了解命令行语法，请使用 -h 选项运行它。

### htpasswd

此实用程序允许您为每个目录的身份验证方案创建用户名/密码对。要查看使用语法，请不带任何参数运行程序。与前面提到的支持工具不同，此实用程序安装在 Apache 服务器安装目录的 bin 目录中。

### dbmmanage

此实用程序允许您管理 DBM 基于身份验证方案的 DBM 基于用户名/密码对。要查看使用语法，请不带任何参数运行程序。此实用程序也安装在 Apache 服务器安装目录的 bin 目录中。

### htdigest

此实用程序允许您为 MD5 摘要基于身份验证方案创建用户名/密码对。要查看使用语法，请不带任何参数运行程序。此实用程序也安装在 Apache 服务器安装目录的 bin 目录中。

## 使用可选或第三方模块自定义 Apache

在添加任何第三方模块之前，请先尝试标准 Apache，以确保在添加任何第三方代码之前一切正常。在标准 Apache 在您的系统上运行后，您可以随意自定义它。在这种情况下，您不再需要像第一次那样以相同的方式运行 configure 脚本。运行 configure 脚本时会自动创建一个名为 config.status 的脚本。config.status 脚本维护了您提供给 configure 脚本的选项的历史记录。例如，如果您按如下方式运行 configure 脚本一次：

```
./configure --prefix=/usr/local/apache --disable-module=cgi
```

config.status 脚本看起来像这样：

```
#!/bin/sh
##
##  config.status -- APACI auto-generated
##                configuration restore script
##
## Use this shell script to rerun the APACI
## configure script for restoring your configuration.
## Additional parameters can be supplied.
##
./configure \
"--prefix=/usr/local/apache" \
"--disable-module=cgi" \
"$@"
```

假设您想启用 usertrack 模块。请按如下方式再次运行 configure：

```
./configure --prefix=/usr/local/apache \
--disable-module=cgi --enable-module=usertrack
```
