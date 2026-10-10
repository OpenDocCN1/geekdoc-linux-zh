

`ServerRoot` 指令标识服务器本身的根位置。其他配置文件和日志文件均相对于此目录进行标识。

多个 Apache 配置选项与日志记录相关。特别是，`ErrorLog` 设置错误日志文件的文件名，`CustomLog` 设置访问日志文件，`LogLevel` 设置系统记录器级别，而 `LogFormat` 控制存储在访问日志文件中的数据格式。（第 4 章介绍了系统记录器。）

用户或网站维护人员可以使用 Apache 服务目录中的 `.htaccess` 文件覆盖某些 Apache 配置选项。`.htaccess` 文件的格式与主 Apache 配置文件完全相同，但在此文件中设置的选项仅影响 `.htaccess` 文件所在的目录树。通常，此文件仅由通过全局 `UserDir` 指令共享个人网页的用户，或那些可以编辑服务器主 Web 空间目录的一个或多个子目录但没有完整管理权限来编辑主 Apache 配置文件的网站维护人员使用。

## 使用 Apache 模块

许多 Apache 功能是通过可选代码实现的。这些代码有时直接编译到主 Apache 二进制文件中，但其他时候则存储在单独的模块中。这些模块类似于 Linux 内核模块：它们是独立的文件，可以根据系统的整体需求和配置被加载到内存中或被忽略。要加载模块，你需在 `httpd.conf` 配置文件中使用 `LoadModule` 指令：

```
LoadModule module_name module_filename
```

`module_name` 通常与 `module_filename` 相关，只是后者包含了相对于服务器根目录（通过 `ServerRoot` 设置）的路径，并且通常以 `.so` 结尾。两者的形式也可能略有不同。例如，你的配置文件中可能有一行如下所示：

```
LoadModule auth_basic_module modules/mod_auth_basic.so
```

这一行加载了一个提供某些身份验证功能的模块。你的发行版默认的 Apache 配置很可能包含许多 `LoadModule` 指令。你可以在 http://httpd.apache.org/docs/2.2/mod/ 了解它们的作用。（如果你的 Apache 版本不是 2.2.x 版本，请将 2.2 更改为你的 Apache 版本。）

某些模块可能直接编译进你的 Apache 版本中。要查看系统上哪些模块是以此方式编译的，请根据你的 Apache 二进制文件的名称输入 `httpd -l` 或 `apache -l`。

## 配置脚本

许多站点运行 Web 服务器仅仅是为了提供静态内容——即内容不会改变的页面。然而，Web 服务器也可以运行动态内容，例如通用网关接口（CGI）脚本、超文本预处理器（PHP，一个递归缩写，以前展开为 *Personal Home Page*）脚本或 Java Servlet。这些脚本可以扩展 Web 服务器的功能，使其能够为用户提供动态内容或代表客户端执行计算功能。每种技术都非常复杂，本节仅提供了足够在你所在的 Apache 中启用对这些技术支持的信息。如果你需要维护依赖脚本技术的站点，你应该查阅该主题的其他文档。

> **警告**
>
> 在 Web 服务器上启用脚本功能存在风险，因为带有错误脚本的错误配置可能给攻击者一种破坏计算机整体安全性的方式。因此，我强烈建议你除非比本文对这个主题的简短介绍学到更多关于 Web 服务器及其脚本功能的知识，否则不要尝试这样做。

CGI 脚本是在客户端请求下在 Web 服务器上运行的脚本或程序。CGI 脚本可以用任何语言编写——C、C++、Perl、Bash、Python 或其他语言。CGI 脚本可以是实际的脚本或编译后的程序，但由于它们通常是真正的脚本，因此 *CGI 脚本* 这一术语适用于任何形式的 CGI 程序，即使它是编译过的。脚本必须以能生成有效 Web 页面的方式编写，但该主题过于复杂，无法在此详述。

要在 Apache 中激活 CGI 脚本支持，通常使用 `ScriptAlias` 指令指向一个特殊的 CGI 目录：

```
ScriptAlias /cgi-bin /usr/www/cgi-bin
```

这一行告诉 Apache 在 `/usr/www/cgi-bin` 中查找脚本。此目录可以是 `DocumentRoot` 目录的父目录的一个子目录，但如果你愿意，它们的位置可以大不相同。

相比之下，PHP 是一种专门用于构建 Web 页面的脚本语言。与 CGI 脚本一样，编写 PHP 脚本是一个复杂的话题，在 Linux+ 考试中不予涵盖。然而，你应该知道如何在 Apache 中激活 PHP 支持。要开始这项任务，请确保已安装必要的 PHP 软件包。你可能需要一个名为 `php` 的软件包，也许还需要各种支持或附属软件包。

安装 PHP 后，你可以配置 Apache 以支持它。这是通过如下的 Apache 配置行完成的：

```
# Use for PHP 5.x:
LoadModule php5_module     modules/libphp5.so
AddHandler php5-script php

# Add index.php to your DirectoryIndex line:
DirectoryIndex index.html index.php
AddType text/html       php
```

> **注意**
>
> 上述配置适用于 PHP 5 版本。如果你使用其他 PHP 版本，可能需要更改文件名。

此配置中的前两行只是加载 PHP 模块和处理器。`DirectoryIndex` 和 `AddType` 行帮助 Apache 管理 PHP 文件。`DirectoryIndex` 行将替换你配置中的现有行——或者更准确地说，你应该确保 `index.php` 与用于索引文件的其他任何文件名一起出现在 `DirectoryIndex` 行上。

除了这些全局选项之外，保存 PHP 脚本的目录可能包含名为 `php.ini` 的文件，这些文件设置各种 PHP 解释器选项。有很多选项，例如 `user_dir`、`include_path` 和 `extensions`。如果你需要调整 PHP 设置，我建议从示例文件开始，例如 `/etc` 中的全局 `php.ini` 文件。

最终的 Web 服务器脚本解决方案是 Tomcat（http://tomcat.apache.org），它使 Apache 能够在服务器计算机上运行 Java Servlet。Tomcat 在概念上类似于 PHP。与 PHP 一样，你必须首先在系统上安装合适的 Tomcat 软件包。主要的 Tomcat 软件包可能名为 `tomcat5`、`tomcat6` 或类似名称。（在我写作时，第 6 版是 Tomcat 的最新版本，但第 5 版在许多发行版中仍然可用。）高级软件包工具，如 Yum 或 APT，将帮助你找到合适的软件包。

安装 Tomcat 后，你必须告诉 Apache 如何使用它。通常，Tomcat 软件包会安装自己的配置文件，其中包含在 Apache 中启用支持的选项。要使用它们，你只需在 Apache 配置文件中添加一行，例如：

```
include /tomcat/conf/mod_jk.conf-auto
```

你引用的具体文件可能因发行版而异，因此你应该检查自己的 Tomcat 软件包，看看它安装了什么配置文件。

无论使用哪种脚本工具，你都可以通过其 SysV 启动脚本重启 Apache，以启用脚本支持。然后，由你或你的 Web 开发人员创建适当的脚本来管理网站上的动态内容。这是一个非常复杂的主题，不在 Linux+ 考试的范围内。

## 配置虚拟主机

另一个在大型系统中很有用的 Web 服务器功能是虚拟主机——一台服务器托管多个网站。假设两个拥有两个域名的组织，比如 example.com 和 pangaee.edu 都想托管网站，但为了降低成本，他们决定共享一台计算机来完成这项工作。两个组织都将其域名中的主机名指向该计算机的 IP 地址。虚拟主机使拥有此 IP 地址的计算机能够根据用户在远程 Web 浏览器中输入的主机名做出不同的响应。Web 托管 ISP 大量使用此功能，在一台计算机上支持许多域名。如果你更改了公司名称，这也可能很方便——你可以运行一台服务器，响应旧域名的同时响应新域名，并在旧名称上显示关于更改的通知。

实现虚拟主机有几种方法。一种方法是使用 `VirtualHost` 指令创建一个块：

```
<VirtualHost *>  
ServerName www.example.com
```

