
`Apache -f "path_to_httpd.conf"`

例如，你可以创建两个主 Apache 服务，一个响应端口 `80`，另一个响应端口 `8080`，方法是创建两个 `httpd.conf` 文件。你可以使用上述命令运行这些服务中的每一个。但是，在 `Windows 2000` 或 `NT` 系统中，已经安装了一个默认的 Apache 服务，因此你只需修改 `C:\Program Files\Apache Group\Apache\conf\httpd.conf` 以反映端口更改，并将其另存为另一个文件。然后，你只需使用上述命令运行一个 Apache 实例即可。默认的 Apache 配置仍然可以在端口 `80` 上运行。

要创建一个新的 Apache 服务，请从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行以下命令：

```apache
Apache -n new_service_name -f "path_to_httpd.conf" -k install
```

运行此命令将安装一个新服务，名为 `new_service_name`，它将使用 `path_to_httpd.conf` 路径。

你也可以使用 `Apache -n existing_service_name -k uninstall` 命令移除现有的 Apache 服务。

## 配置 Windows 下的 Apache

前面章节中找到的大多数信息也适用于 Windows 上的 Apache。然而，由于 Unix 系统和 Windows 系统在底层工作方式上的差异，Windows 版 Apache 和 Unix 版 Apache 之间存在某些区别。本章将讨论这些区别。

### Windows httpd.conf 语法

Unix 系统和 Windows 系统的 `httpd.conf` 文件之所以不同，是因为 Windows 处理路径名的方式不同。
区别如下：

- 在 Windows 系统中，路径中的目录和文件名使用反斜杠分隔。例如，`c:\temp` 是一个有效的目录路径。但是，Apache 内部仍然使用前斜杠作为路径分隔符，因此你仍然必须使用前斜杠。例如，在 `httpd.conf` 文件中 `c:/temp` 是正确的，但 `c:\temp` 是错误的。

- Windows 路径通常包含空格。例如，`c:\Program Files\Apache Group\Apache\htdocs` 在 Windows 环境中是一个可接受的路径。在 `httpd.conf` 文件中使用此类路径名时，请用双引号将整个路径括起来。例如：

  ```apache
  ServerRoot "C:/Program Files/Apache Group/Apache"
  ```

  这里，`ServerRoot` 指令被设置为指向 `C:/Program Files/Apache Group/Apache` 目录。

# 第 21 章：配置 Windows 下的 Apache

- Windows 上的 `httpd.conf` 与 Unix 上的 `httpd.conf` 有何不同
- 调整 Apache 以优化性能
- 测试 Apache 配置
- 使用 Comanche 管理 Apache
- 为基于 Perl 的 CGI 脚本配置 Apache
- 如何在 Windows 上使用 `mod_perl`
- 如何在 Windows 上使用 PHP
- 如何在 Apache 中使用 ISAPI 扩展
- 如何在 Windows 上使用 `UserDir`

## 调整 Apache 性能

早在 Apache 2.0 之前，Windows 上的 Apache 就已经是多线程的。这是因为像 `Windows 2000` 和 `Windows NT` 这样的 Windows 系统在使用线程时比使用由多个子进程组成的服务表现更好。

在 Windows 系统中，Apache 仅使用两个进程运行。父进程监控子进程，后者负责使用多个线程处理所有请求。

为了控制在 Windows 下 Apache 可以同时处理多少个请求，你需要调整 `ThreadsPerChild` 指令。有关此指令的详细信息，请参见第 4 章。此指令控制负责所有请求的唯一 Apache 子进程可以创建的线程数。默认值 `50` 对于大多数网站来说应该足够了。

如果你需要更高的响应率，请确保你有适当的系统资源，例如足够的 `RAM` 和快速的 `CPU` 来支持你的速率需求。根据 `winnt_MPM` 模块的源代码，你应该可以将此值设置为最大 `4096` 个线程。对于大多数 Web 网站，低于 `256` 的数值可能更合适。

`MaxRequestsPerChild` 指令限制了子进程可以处理的请求数（有关此指令的详细信息，请参见第 4 章）。由于在 Windows 下单个子进程通过线程处理所有请求，因此此指令应设置为非常高的数值或 `0`，这意味着子进程将永不退出。

## 测试 Apache 配置

每次修改 `httpd.conf` 文件时，你都可以从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行以下命令，以确定是否创建了任何语法错误。

```apache
Apache -t
```

你也可以选择 `开始\程序\Apache httpd Server\Configure Apache Server\` 下的 `Test Configuration` 选项来执行相同操作。

如果发现错误，你可以在使用 `Apache -k restart` 命令重启服务器之前修复它。

## 使用 Comanche 管理 Apache

如果你主要是 Windows 用户，你可能会想知道 Apache 的 GUI 管理程序在哪里。抱歉，Apache 并不附带这样的程序。但有很多第三方的开发中项目甚至商业项目，你可以在 `http://gui.apache.org` 上了解更多信息。

然而，Comanche（ApaCHe 的配置管理工具）是我最喜欢的，因为它支持多平台、非侵入式、可扩展且非常容易设置。你可以从 `http://www.covalent.net/projects/comanche/` 下载 Comanche。

下载 Comanche 的二进制发行版后，解压并单击可执行文件图标即可开始配置 Apache。运行 `comanche.exe` 程序时，会出现一个带有标有 Comanche 的按钮的小窗口，如 Figure 21-1 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_611_0.png)

单击标有 Comanche 的按钮以启动 Comanche。你应该看到与下面 Figure 21-2 中所示类似的屏幕。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_611_1.png)

你可以单击左侧的树元素来选择不同的配置选项。例如，单击左侧树菜单底部的 `Default Web Server` 选项会显示与 Figure 21-3 中所示类似的屏幕。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_612_0.png)

单击右侧的默认 Web 站点属性链接会调出实际的配置屏幕。

在这里，你可以使用树菜单中的 `Basic configuration`、`Module management`、`Server identification`、`Server options`、`Environment`、`Indexing`、`Proxy`、`Apache Jserv Settings`、`Alias` 或 `CGI Settings` 选项进行配置。

例如，要将 `Port` 指令更改为非默认值（即除了 `80` 之外的值），你可以展开 `Basic Configuration` 子选项树，单击 `Listening` 选项，将其设置为 `8080` 等值，如 Figure 21-4 所示。

同样，要创建一个名为 `/cgi-bin/` 的 CGI 脚本别名，指向 “`C:\Program Files\Apache Group\Apache\cgi-bin/`” 目录，我可以展开 `Alias` 选项树，单击 `CGI` 选项，并使用 `Add` 按钮添加别名，如 Figure 21-5 所示。

新创建的别名将显示在主 `Alias CGI` 屏幕上。

在配置默认 Web 服务器或新的虚拟主机时，你可以通过选中左侧的 `Default Web Server` 选项并右键单击来快速访问选项，而无需展开它，如 Figure 21-6 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_613_0.png)

![](img/e11fcbd2818a3495ac70085e5d8d1c26_613_1.png)

![](img/e11fcbd2818a3495ac70085e5d8d1c26_613_2.png)

如你所见，一旦你习惯了导航左侧的选项树，并知道哪些功能可以被创建、启用或禁用，你就可以使用此工具通过 GUI 管理 Apache。但是，请记住 Comanche 是一个正在开发中的项目。现在可以使用它，并留意可用的更新版本。

## 配置 Apache 以处理动态内容

与 Unix 版本的 Apache 类似，你可以使用 Windows 上的 Apache 通过 `CGI`、`PHP`、`SSI` 脚本生成动态内容。然而，某些动态内容生成方案的配置存在一些差异，本节将对此进行讨论。

> **注意**
> 这里讨论的大多数指令在第 4 章和第 5 章中也有讨论。你可以在这些章节中找到所有语法选项。

### 运行基于 Perl 的 CGI 脚本

要在 Windows 上的 Apache 中运行基于 Perl 的 CGI 脚本，你必须在系统上安装 Perl。你可以从 `http://www.activestate.com` 下载 Windows 版的 Perl。

正确安装 Perl 后，你可以像往常一样使用 `ScriptAlias` 指令配置 Apache 以运行 CGI 脚本。通常，脚本别名创建如下：

```apache
ScriptAlias /cgi-bin/ "C:/Program Files/Apache Group/Apache/cgi-bin/*"
```

你也可以使用 `Options ExecCGI` 指令在目录中启用 CGI 脚本。现在，为了让 Apache 调用适当的 Perl 解释器，你必须确保脚本的第一行如下：

```perl
#!d:/rive:/path_of_perl_interpreter
```

这被称为*shebang 行*。例如，如果你将 Perl 安装在 `c:\perl\bin` 目录中，你可以创建第一行设置为以下内容的 Perl 脚本：

```perl
#!c:/perl/bin
```

创建用于 CGI 的 Perl 脚本还有另一种方法。默认情况下，Perl 在 Windows 注册表中注册 `.pl` 扩展名，以便由 Perl 解释器执行。如果在 `httpd.conf` 的主服务器配置部分设置了 `ScriptInterpreterSource` 注册表指令，你就可以正确运行任何具有 `.pl` 扩展名的脚本。Apache 将从 Windows 注册表中获取解释器路径，而不是从第一行 shebang 行获取。

> **交叉引用**
> 阅读第 12 章以了解许多其他适用于 Windows 平台 Apache 的 CGI 相关问题详情。

## 运行 mod_perl 脚本

要运行 `mod_perl` 脚本，你必须安装 `mod_perl` 模块。在安装 `mod_perl` 二进制模块之前，你需要在系统中安装 Perl，因此请确保你拥有来自 `http://www.activestate.com` 的最新版本的 Windows Perl。

安装 Perl 后，你可以从命令行运行以下命令来下载并安装 `mod_perl` 模块：

```
ppm install http://theoryx5.uwinnipeg.ca/ppmpackages/mod_perl-version.ppd
```

例如，要安装 `mod_perl` 的 1.25 版本，请运行：

```
ppm install http://theoryx5.uwinnipeg.ca/ppmpackages/mod_perl-1.25_1.3.19.ppd
```

在安装过程中，系统会提示你输入 Apache modules 目录的完全限定路径名。安装过程中显示的提示如下所示：

```
Which directory should mod_perl.so be placed in?
(enter q to quit) [C:/Apache/Modules]
```

如果你将 Apache 安装在默认目录 `C:\Program Files\Apache Group\Apache` 中，请输入 `C:\Program Files\Apache Group\Apache\Modules`。`mod_perl.so` 模块应安装在此目录中。

现在，你需要在 `httpd.conf` 中添加以下指令以加载 `mod_perl.so` 模块。

```
LoadModule perl_module modules/mod_perl.so
```

你还应按以下方式在 `httpd.conf` 中设置 `PATH` 变量：

```
PerlSetEnv PATH "C:\WINNT\system32;C:\WINNT;C:\perl;C:\perl\bin"
```

我假设你在 `C:\WINNT` 中安装了 Windows，在 `C:\WINNT\system32` 中有 `system32` 目录，并且你在 `C:\perl` 目录中安装了 Perl，Perl 解释器存储在 `C:\perl\bin` 目录中。如果这些假设中的任何一项（它们是 `Windows 2000` 或 `NT` 系统的默认值）不正确，请相应地进行更改。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_615_0.png)

默认情况下，`Windows` 目录要么是 `C:\WINDOWS`（对于 Windows 9x），要么是 `C:\WINNT`（对于 `Windows 2000` 和 `Windows NT` 系统）。如果你不确定，请打开一个控制台窗口（通常称为 DOS 窗口），输入 `echo %windir%` 命令来显示 `windir` 环境变量的值，该值指向 Windows 操作系统目录。你还可以在提示符下运行 `set` 命令来显示其他所有环境变量，例如 `path`，其中通常既包含 `OS` 目录，也包含 `system32` 目录。

要在启动时加载一组 mod_perl 模块，请使用名为 `startup.pl` 的启动脚本（你可以使用其他任何名称），并使用以下指令：

```
PerlRequire "Drive:/your_path/startup.pl"
```

别忘了将 `Drive:/your_path/startup.pl` 更改为 `startup.pl` 的实际路径。在 `startup.pl` 中，使用 `use module_name ();` Perl 语句加载你的模块。例如，以下 `startup.pl` 脚本加载了 `CGI` 模块、`DBI`（数据库独立接口）模块以及允许缓存数据库连接的 `Apache::DBI` 模块：

```
#!/c:/perl/bin/perl

use CGI ();

use DBI ();

use Apache::DBI ();
```

![](img/e11fcbd2818a3495ac70085e5d8d1c26_616_0.png)

关于许多仍然适用于 Windows 平台上的 Apache 的其他 mod_perl 相关事项，请参阅第 16 章以获取详细信息。请记住，要从 `CPAN` 下载模块，你必须使用 `ppm` 命令，而不是第 16 章中使用的 `perl -MCPAN -e` shell 命令。例如，要安装 `Apache::DBI` 模块，你必须运行：

```
ppm install http://theoryx5.uwinnipeg.ca/ppmpackages/Apache-DBI.ppd
```

同样，要安装 `Apache::ASP`，你必须运行：

```
ppm install http://theoryx5.uwinnipeg.ca/ppmpackages/Apache-ASP.ppd
```

## 运行 PHP 脚本

要在 Windows 上的 Apache 中运行 PHP 脚本，请遵循以下步骤：

- 1. 从 `http://www.php.net/distributions/` 下载最新的 PHP 二进制分发包
- 2. 在 `c:\php` 目录中解压分发包。将 `c:\php\php4ts.dll` 复制到 Windows `system32` 目录。对于 `Windows 2000` 和 `NT` 系统，默认目录为 `C:\WINNT\system32`。另外，将 `c:\php.ini-dist` 复制到 Windows 目录，在 `Windows 2000` 或 `NT` 中默认为 `C:\WINNT`。
- 3. 默认的 `php.ini` 对大多数站点有效，但如果你愿意，可以对其进行编辑。默认情况下，Windows 平台上的 PHP 内置了 `MySQL` 和 `ODBC` 支持，因此你不需要为其启用任何扩展。但是，你应该查看 `extension=module_name.dll` 行，以确定是否需要启用其中的任何行。例如，如果你计划使用 GD 库（用于生成 PNG 图像）配合 PHP，那么你需要通过删除行首的分号字符来取消注释 `extension=php_gd.dll` 行。
- 4. 将以下行添加到 `httpd.conf` 中：

```
LoadModule php4_module c:/php/sapi/php4apache.dll

AddType application/x-httpd-php .php

AddType application/x-httpd-php .php4
```
