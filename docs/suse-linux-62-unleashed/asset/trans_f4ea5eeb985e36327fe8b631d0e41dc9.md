

- /usr/sbin
可执行程序放置在此目录。这包括服务器可执行文件本身。

- /var/log
服务器日志文件放置在此目录。默认情况下有两个日志文件——httpd.access_log 和 httpd.error_log，但你可以定义任意数量的自定义日志文件，包含各种信息。请参阅本章稍后关于日志的章节。

> 注意
如果你正在升级到更高版本的 Apache，RPM 将不会覆盖你的配置文件。RPM 会移动你当前的文件并在它们后面添加 .rpmnew 扩展名。例如，httpd.conf 将变为 httpd.conf.rpmnew。不要低估良好备份的重要性。在升级你关心的服务器上的任何内容之前，请务必先进行备份。

## 亲自手动编译源码

从源码安装有两种方法：旧的、熟悉的方法和新的、简单的方法。
两者的起始方式相同——你从 http://www.apache.org/ 下载源码，并在像 /tmp 这样的临时目录中解压 tar 包。这将创建一个名为 apache_version_number 的目录，其中 version_number 是你下载的版本。例如，apache_1.3.6。

## 简单方法

要用简单方法安装 Apache，只需在刚刚创建的目录中运行 ./configure。你可以提供 -prefix 参数将其安装到默认目录 /usr/local/apache/ 之外的目录。

```
./configure --prefix=/preferred/directory/
```

这将在 src/ 子目录下创建一个名为 Configuration 的文件。它还会生成用于编译服务器代码的 makefile。
完成此步骤后，输入 `make` 然后 `make install` 来编译服务器代码。
最后，输入 `/usr/local/apache/bin/apachectl start` 来启动 Web 服务器进程。

## Apache 服务器
第 11 章

如果你使用了 --prefix 参数，请将 /usr/local/apache/ 更改为你提供的任何路径。

> 注意
此处描述的 Apache Autoconf 风格接口 (APACI) 仅适用于 1.3 及更高版本。

## 旧方法

如果你想按照老办法操作，或者只是想对服务器的构建方式有更多控制权，请遵循以下步骤。

在源码目录中，将文件 Configuration.tmpl 复制为 Configuration，并使用你喜欢的编辑器打开 Configuration。仅在你确定自己在做什么时，才修改编译器标志。取消你想要包含的模块的注释，注释掉你不需要的模块，或者为你编写或获取的自定义模块添加行。

现在，运行 Configure 脚本来创建 makefile。

最后，使用 make 和 make install 编译并安装服务器。

> 提示
你可能希望将本章之前 RPM 安装部分列出的现有文件位置软链接到文件的新位置，因为默认安装位置与 RPM 包安装文件时的位置不同。不这样做可能会导致你的 Web 服务器进程在系统启动时无法启动。

我建议你一直使用 RPM 软件包，直到你真正熟悉系统启动时发生了什么为止。

## 手动安装后的文件位置

在 1.3.4 版本中，所有文件都放置在 /usr/local/apache（或你通过 --prefix 参数指定的任何目录）的各个子目录下。在 1.3.4 版本之前，文件被放置在 /usr/local/etc/httpd。请注意，编译源码产生的默认路径与软件包通常在 SuSE Linux 系统上（或者说，对于几乎任何 Linux 供应商）的安装方式大不相同。这可能会导致存在两个配置文件的副本。如果你编辑了其中一个并认为它是“真实”的，更改可能不会以你预期的方式生效。因此，建议坚持使用基于 RPM 的安装或源码 tar 包安装，而不是在两种方法之间切换。

- /usr/local/apache/conf——此目录包含所有的 Apache 配置，包括 access.conf、httpd.conf 和 smd.conf。请参阅本章稍后关于配置文件的章节。请注意，SuSE 的 RPM 安装将这些文件放在 /etc/httpd；你可能希望将它们移动到那里并相应地更改引用。
- /usr/local/apache——cgi-bin、icons 和 htdocs 子目录分别包含 CGI 程序、标准图标和默认 HTML 文档。请注意，SUSE 的 RPM 安装将这些文件放在 /usr/local/httpd；你可能希望将它们移动并相应地更改引用。
- /usr/local/apache/bin——可执行程序放置在此目录。请注意，SUSE 的 RPM 安装将 apache 二进制文件命名为 /usr/sbin/httpd。
- /usr/local/apache/logs——服务器日志放置在此目录。默认情况下有两个日志文件——access_log 和 error_log，但你可以定义任意数量的自定义日志，包含各种信息。请参阅本章稍后关于日志的章节。请注意，SuSE 的 RPM 安装将日志放在 /var/log 下并默认命名为 httpd_error_log 和 httpd_access_log。如果你托管了多个域名，通常是创建一个 /var/log/www/ 子目录，并为每个域名创建单独的访问错误日志。

到此时，你已经通过某种方式成功安装了 Apache 服务器。它会运行，但可能并不完全按照你的想法。下一节将介绍如何配置服务器，使其完全按照你的要求运行。

## 运行时配置设置

传统上，Apache 的运行时配置在三个文件中：httpd.conf、access.conf 和 smd.conf。这主要是因为配置文件是为 NCSA 编写的，而 Apache 是源自 NCSA。虽然最初将配置拆分为三个文件的决定背后有一定的逻辑，但随着时间的推移，这种做法越来越不合理。特别是你可以在任何文件中放置任何配置选项并生效。

## Apache 服务器
第 11 章

从 Apache 1.3.4 版本开始，运行时配置存储在一个文件中——httpd.conf。其他文件仍然存在，但它们只包含一条注释，告诉您这些文件纯出于历史原因，您应该将所有配置放在 httpd.conf 中。

然而，你应该注意，虽然 RPM 版本通常将配置拆分为三个文件，但本章假设你将配置文件合并为一个。

> 注意
如果你真的想这样做，仍然可以使用三文件配置方法。这对某些人来说是合理的。然而，哪些应该放在哪个文件中的区别在这些年里已经变得越来越模糊。

Apache 在进程启动（或重启）时从配置文件读取数据。你可以使用 httpd reload 命令让 Apache 进程重新加载配置信息。我们将在章稍后关于启动和停止服务器的部分讨论这一点。

你通过配置指令对服务器进行运行时配置，这些指令是你想要启用的命令，例如告诉服务器有关配置和运行的重要文件的各种选项。配置指令遵循以下语法：

```
directive option ...
```

每行指定一个指令。某些指令仅设置值（如文件名），而另一些允许你指定各种选项。特殊的指令称为节（sections），类似于 HTML。节指令被角括号包围，例如 <directive>。节通常包含一组适用于指定目录的指令：

```
<directive somdir /in/your/tree>
directive option option
directive option option
</directive>
```

所有的节都用匹配的节标签 </directive> 结束。请注意，节标签与其他任何指令一样，每行指定一个。

