

系统名称类似于在 SPARC 硬件上运行 Solaris 10 的 `solaris10-spare`，或在 Intel 硬件上运行 Linux 的 `linux-i686`。

### A.4.2.1 安装 tar 文件二进制发行版

tar 文件二进制发行版的文件名类似于 *mysql-version-platform-cpu.tar.gz*。获取您所需版本和平台的发行版文件，并将其放置到您希望安装 MySQL 的目录下（例如，/usr/local）。

使用以下命令之一解包发行版文件（如果您的 tar 版本不支持 z 选项，请使用第二个命令）：

```bash
% tar zxf mysql-version-platform-cpu.tar.gz
% gunzip < mysql-version-platform-cpu.tar.gz | tar xf -
```

解包发行版文件会创建一个名为 *mysql-version-platform-cpu* 的目录，其中包含发行版的内容。为了更轻松地引用此目录，请创建一个指向该目录的名为 mysql 的符号链接：

```bash
% ln -s mysql-version-platform-cpu mysql
```

创建链接后，您可以将安装目录引用为 /usr/local/mysql（假设您将 MySQL 安装在 /usr/local 下）。

现在请前往第 A.4.3 节，“安装后步骤”。

### A.4.2.2 安装 RPM 发行版

RPM 包可用于在基于 RPM 的 Linux 系统上安装 MySQL。以下列表描述了一些更常用的软件包。在软件包文件名中，*version* 代表 MySQL 版本号，*platform* 代表目标系统类型（或者对于应该在任何支持 glibc 2.3 的 Linux 发行版上都能工作的通用软件包，则为 *glibc23*），*cpu* 指示构建该发行版的目标处理器类型。

- *MySQL-server-version-platform-cpu.rpm*
  服务器软件。
- *MySQL-client-version-platform-cpu.rpm*
  客户端程序。如果您从 RPM 包安装 MySQL，您应该始终安装客户端软件包。
- *MySQL-embedded-version-platform-cpu.rpm*
  嵌入式服务器，libmysql4。（适用于 MySQL 5.1 及更高版本）
- *MySQL-devel-version-platform-cpu.rpm*
  用于编写客户端程序的开发支持（客户端库和头文件）。如果您想编写自己的 C 程序或 Perl DBI 脚本来访问 MySQL 数据库，您将需要此 RPM。其他语言的 MySQL API 可能也依赖于这些客户端库和头文件。
- *MySQL-shared-version-platform-cpu.rpm*
  共享客户端库。
- *MySQL-bench-version-platform-cpu.rpm*
  基准测试和测试。这些需要 Perl DBI 支持。（参见第 A.4.4 节，“在 Unix 上安装 Perl DBI 支持”。）
- *MySQL-version.src.rpm*
  服务器、客户端、基准测试和测试的源代码。

安装 RPM 包时，您不需要处于任何特定的目录中，因为 RPM 包含指示其内容应放置位置的信息。对于任何 RPM 包 `rpm_file`，您都可以使用以下命令查看其内容将安装的位置：

```bash
% rpm -qpl  rpm_file
```

要安装 RPM 包，请使用此命令（您需要以 *root* 身份执行此操作）：

```bash
# rpm -i  rpm_file
```

MySQL 的各个部分被划分为不同的 RPM 包，因此您可能需要安装多个 RPM。对于典型安装，您应该同时安装服务器和客户端 RPM。如果您只安装了服务器 RPM，您将无法对其执行许多操作，因为它不包含客户端程序。

若要支持服务器，请使用此命令：

```bash
# rpm -i MySQL-version-platform-cpu.rpm
```

若要安装客户端程序，请使用此命令：

```bash
# rpm -i MySQL-client-version-platform-cpu.rpm
```

如果您计划使用客户端编程支持编写自己的程序，请确保安装开发 RPM 软件包：

```bash
# rpm -i MySQL-devel-version-platform-cpu.rpm
```

如果您想从源代码 RPM 包安装 MySQL，以下命令应该就足够了：

```bash
# rpmbuild --recompile --clean MySQL-version.src.rpm
```

现在请前往第 A.4.3 节，“安装后步骤”。

### A.4.2.3 安装源代码发行版

MySQL 源代码发行版的文件名类似于 *mysql-version.tar.gz*，其中 *version* 是 MySQL 版本号。（与二进制发行版不同，源代码发行版适用于所有系统，因此文件名中没有 *platform* 或 *cpu* 值。）选择您希望解包该发行版的目录并进入该目录。获取发行版文件，并使用以下命令之一进行解包（如果您的 *tar* 版本不支持 *z* 选项，请使用第二个命令）：

```bash
$ tar zxf mysql-version.tar.gz
$ gunzip < mysql-version.tar.gz | tar xf -
```

解包发行版文件会创建一个名为 mysql-version 的目录，其中包含发行版的内容。切换到该目录：

```bash
$ cd mysql-version
```

现在，在安装之前，您需要配置和编译该发行版。如果以下步骤失败，请检查 MySQL 参考手册中的安装章节，特别是其中关于您的系统类型的任何平台特定说明。

使用 configure 命令配置该发行版：

```bash
$ ./configure
```

您可能需要为 configure 指定选项。要获取可用选项的列表，请运行此命令：

```bash
$ ./configure --help
```

以下列表显示了一些常见的配置选项：

- `--with-innodb, --without-innodb`
  包括或不包括对 InnoDB 存储引擎的支持。排除 InnoDB 会使服务器更小，并使其使用更少的内存。但是，如果您计划使用 InnoDB 表，则应该包含此引擎。
- `--without-server`
  配置该发行版以仅构建客户端支持（客户端程序或客户端库）。如果您计划访问运行在另一台机器上的服务器，可能会这样做。
- `--with-embedded-server`
  构建嵌入式服务器库，libmysqlid。
- `--with-yassl, --with-openssl, --with-ssl`
  配置该发行版以包括 SSL 支持。如果您想在客户端和服务器之间使用加密的 SSL 连接，则这是必需的。在 MySQL 5.1.11 之前，使用 --with-yassl 或 --with-openssl 来选择 yaSSL 或 OpenSSL。从 5.1.11 开始，使用 --with-ssl 来选择 yaSSL，或使用 --with-ssl=path_name 来选择 OpenSSL；path_name 指示在哪里可以找到 OpenSSL 头文件和库。
- `--prefix=dir_name`
  默认情况下，安装基础目录是 /usr/local。数据目录、服务器、客户端、客户端库、头文件、手册页和语言文件安装在基础目录下的 var, libexec, bin, lib, include, man 和 share 目录中。如果您想更改安装基础目录，请使用 --prefix 选项。dir_name 应该是完整路径名。例如，要在 /usr/local/mysql 目录下安装所有内容，请使用 --prefix=/usr/local/mysql。
- `-localstatedir=dir_name`
  此选项更改数据目录的位置。如果您不想将数据库放在安装基础目录下，可以使用此选项。`dir_name` 应该是完整路径名。

运行 `configure` 后，编译该发行版并安装它：

```bash
% make
% make install
```

如果您没有使用指定具有写入权限的安装目录的 `--prefix` 选项运行 `configure`，则运行 install 命令时可能需要具有 `root` 权限。

现在请前往第 A.4.3 节，“安装后步骤”。

## A.4.3 安装后步骤

对于首次安装，在安装 MySQL 之后，您应该采取某些步骤：

1. 将您的 `PATH` 环境变量设置为包括安装 MySQL 客户端程序的目录。如果您只安装了客户端程序且没有运行服务器，那么这是此处适用的唯一步骤，您可以跳过其他步骤。
2. 初始化 MySQL 数据目录和授权表。
3. 启动 MySQL 服务器。
4. 设置时区表以启用使用命名时区。
5. 设置服务器端帮助表。

如果您正在将现有的 MySQL 安装升级到较新版本，您可能已经处理了其中许多事项，例如设置您的 `PATH` 和初始化数据目录。但是，您可能需要做其中的一项或多项事情：

- 更新您的授权表，以确保它们具有当前的结构。
- 如果您的 previous 安装来自 4.1.3 之前的版本且不支持多个时区，请设置时区表。这些表启用对命名时区的支持。
- 更新服务器端帮助表以使用当前的帮助文本。

以下各节描述了如何执行这些操作。使用适用于您情况的各节。

### A.4.3.1 设置您的 PATH 环境变量

如果您希望能够在命令行中调用 MySQL 客户端程序而无需输入其完整路径名，请将您的 `PATH` 环境变量设置为包括 `bin`

