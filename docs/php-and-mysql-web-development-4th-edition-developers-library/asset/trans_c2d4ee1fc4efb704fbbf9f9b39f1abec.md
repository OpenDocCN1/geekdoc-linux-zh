
## A.5 在 Linux 上安装 PHP 和 MySQL（续）

这些选项的使用方式如下。对于每个包含路径名值的选项，如果 `configure` 能够自行确定所需信息的位置，则可以省略该选项中的路径名。

- `--with-apxs[=/path/to/apxs]`
  
  告诉 `configure` 在哪里找到 `apxs`，即 Apache 扩展工具辅助脚本，它可为其他模块提供有关 Apache 配置的信息。

- `--enable-pdo`
  
  包含对 PDO 扩展的支持。

- `--with-pdo-mysql[=/path/to/mysql]`
  
  为 PDO 包含 MySQL 支持。路径名指示 MySQL 的安装位置，以便 `configure` 能够确定 MySQL 头文件和库文件的位置。

- `--with-mysqld[=/path/to/mysql_config]`
  
  包含对 `mysqld`（“MySQL 增强版”）扩展的支持。*此选项对于 PDO 并非必需*。您可能使用此选项来启用未使用 PDO 的人员运行基于 `mysql` 扩展的脚本。`/path/to/mysql_config` 是 `mysql_config` 脚本的路径名。`configure` 调用该脚本以获取 MySQL 配置信息。

- `--with-mysql[=/path/to/mysql]`
  
  包含对 `mysql`（原始 MySQL 扩展）的支持。*此选项对于 PDO 并非必需*。您可能使用此选项来构建 `mysql`，以启用未使用 PDO 的人员运行基于原始扩展的脚本。路径名指示 MySQL 的安装位置，以便 `configure` 能够确定 MySQL 头文件和库文件的位置。

- `--with-zlib`
  
  由于 MySQL 客户端库访问压缩功能，因此需要此选项。

配置 PHP 后，按照以下方式构建并安装它（您可能需要以 *root* 身份执行安装命令）：

```bash
$ make
# make install
# cp php.ini-dist /usr/local/lib/php.ini
```

`cp` 命令将安装一个基线 PHP 初始化文件到 PHP 可以找到它的位置。如果您喜欢，可以用 `php.ini-recommended` 替换 `php.ini-dist`。请查看两者并选择您偏好的一个。

### 配置 Apache

在 PHP 和 PDO 安装完成后，编辑 Apache 配置文件 `httpd.conf`。您需要指示 Apache 在启动时加载 PHP 模块，并识别 PHP 脚本。`httpd.conf` 可能通过 Include 指令包含其他文件。如果您没有看到以下段落中描述的信息，请检查任何被包含的文件。

若要告诉 Apache 加载 PHP 模块，`httpd.conf` 需要在适当的章节中包含 LoadModule 和 AddModule 指令（查找其他类似的指令）。这些指令可能在安装步骤中已经为您添加。如果没有，您必须自行添加。它们应该类似于以下内容，尽管 LoadModule 指令中的路径名可能需要针对您的系统进行调整：

```apache
LoadModule php5_module libexec/libphp5.so
AddModule mod_php5.c
```

接下来，编辑 `httpd.conf` 以告诉 Apache 如何识别 PHP 脚本。PHP 识别基于您用于 PHP 脚本的文件名扩展名。最常见的扩展名是 `.php`，这也是本书中示例使用的扩展名。要启用 `.php` 作为 PHP 脚本扩展名，请在 `httpd.conf` 文件中包含以下行：

```apache
AddType application/x-httpd-php .php
```

您还可以告诉 Apache 在 URL 末尾未指定文件名时，识别 index.php 作为目录的允许默认文件。您可能会在 `httpd.conf` 中找到一行内容如下：

```apache
DirectoryIndex index.html
```

将其更改为：

```apache
DirectoryIndex index.php index.html
```

编辑 Apache 配置文件后，如果 `httpd` 服务器已在运行，请停止它，然后重新启动。在许多系统上，执行以下命令（以 root 身份执行）即可完成此操作：

```bash
# /usr/local/apache/bin/apachectl stop
# /usr/local/apache/bin/apachectl start
```

您还可以设置 Apache 在系统启动和关闭时自动启动和停止。请参阅 Apache 文档以获取说明。通常，这涉及在启动时运行 apachectl start，在关闭时运行 apachectl stop。

如果您在设置 PHP 时遇到问题，请检查 PHP 发行版中附带的 INSTALL 文件中的“VERBOSE INSTALL”部分。（无论如何，阅读该文件都是个好主意。它包含许多有用的信息。）

## A.5 在 Windows 上安装 MySQL

我假设您拥有相对较新的版本，如 Windows 2000、XP、2003 或 Vista。本书中涵盖的一些功能，如命名管道和 Windows 服务，在旧版本（Windows 95、98 或 Me）中不可用。

在 Windows 上可选择三种发行版类型：

- **Noinstall**（无安装）包是一个包含 MySQL 安装所需所有组件的 Zip 归档文件。Noinstall 包的文件名以 `mysql-noinstall` 开头。您只需解压归档文件以生成一个文件夹，然后将该文件夹移动到您希望安装 MySQL 的位置。例如，解压名为 `mysql-noinstall-5.0.51-win32` 的发行版会产生一个名为 `mysql-noinstall-5.0.51-win32` 的文件夹。如果您希望将 MySQL 安装在 `c:\mysql`，请将文件夹重命名为 `mysql` 并将其移动到 `c:` 驱动器的根目录。

- **Complete**（完整）包包含配置向导以及 MySQL 安装所需的所有组件。Complete 包的文件名形式为 `mysql-version-win32.zip`。要安装 Complete 包，请下载它，启动其中包含的 `Setup.exe` 程序，然后按照其对话框中的说明操作。

- **Essentials**（基础）包与 Complete 包类似，但仅包含 MySQL 安装所需的最小文件集。例如，它省略了 MySQL 服务器的调试版本。Essentials 包是一个自包含的安装程序，文件名以 `mysql-essential` 开头，后缀为 `.msi`。要安装 Essentials 包，请下载它，启动它，然后按照其对话框中的说明操作。

Complete 和 Essentials 包安装程序倾向于将 MySQL 放置在 `c:\Program Files\MySQL` 下，而不是 `c:\mysql`。它们还会创建一个开始菜单项和一个 Windows 注册表项，而 Noinstall 包不会这样做。

有关在 Windows 上安装 MySQL 的更多信息，请参阅《MySQL 参考手册》中的安装章节。

为了能够在命令行上调用 MySQL 程序而无需键入其完整路径名，请将您的 `PATH` 环境变量设置为包含 MySQL 安装位置下的 bin 目录。例如，如果您在 `c:\mysql` 安装 MySQL，请将 `c:\mysql\bin` 添加到您的路径中。您可以通过使用控制面板中的系统项来设置路径。您可能需要重启 Windows 才能使更改生效。

以下说明假设您已设置好 `PATH` 变量，因此它们省略了命令名称前的路径（除了使用 `mysqld` 完整路径名的 `mysqld --install` 命令外）。

在 Windows 上安装 MySQL 后，由于发行版中已预初始化了数据目录和授权表，因此无需初始化数据目录或授权表。但是，如果您将 MySQL 安装在安装程序选择的默认位置以外的任何位置，您*必须*在一个选项文件中放置一个 `[mysql]` 选项组，该文件是服务器启动时读取的文件，以便服务器可以确定安装基础目录和数据目录的位置。典型的选项文件是 MySQL 安装目录中的 `my.ini` 文件或 `c:\my.ini`。例如，如果您在 `c:\mysql` 安装 MySQL，选项组应该看起来像这样（注意路径名中使用正斜杠而不是反斜杠）：

```ini
[mysql]
basedir=C:/mysql
datadir=C:/mysql/data
```

如果您选择了不同的安装目录，您需要更改选项文件中的路径名。

Windows 的 MySQL 发行版包含几个服务器，每个服务器都使用不同的选项构建：

- 在 MySQL 5.1.21 之前，*mysql* 和 *mysql*-nt 分别是没有和具有命名管道支持的独立服务器。
- 从 MySQL 5.1.21 开始，*mysql* 包含命名管道支持，并且不再有单独的 *mysql*-nt 服务器。
- 所有版本的 *mysql*-debug 都支持命名管道、调试和自动内存分配检查。

一般来说，除非您需要 *mysql*-debug 服务器提供的调试支持，否则选择其他服务器会更好。*mysql*-debug 比其他 Windows 服务器使用更多的内存，运行速度也更慢。

对于支持使用命名管道进行连接的服务器，此连接类型默认是禁用的。所有服务器都支持共享内存连接，但这些连接默认也是禁用的。要启用这些功能，您必须在选项文件的 [mysql] 组中添加适当的行：

```ini
[mysql]
enable-named-pipe
shared-memory
```

在 Windows 上，任何 MySQL 服务器都可以安装为在 Windows 启动时自动启动的服务。例如，要将 *mysql* 服务器安装为 Windows 服务，请使用以下命令：

```bash
C:\> C:/mysql/bin/mysql --install
```

install 命令使用服务器的完整路径名。如果服务器安装在不同的位置，请相应地修改路径名。

如果您使用 `--install-manual` 而不是 `--install`，服务器将安装为 Windows 服务，但不会在 Windows 启动时自动运行。您必须使用 Windows 服务管理器或 `net start` 命令。

如果您将 MySQL 服务器安装为 Windows 服务，您可以通过将它们放入选项文件的 [mysql] 组中指定其他选项。

对于安装为服务的服务器，您可以使用 Windows 服务管理器手动启动它。您应该能够在 Windows 控制面板中的“服务”项或“管理工具”项中找到它。该服务也可以使用以下命令启动：

```bash
C:\> net start MySQL
```

