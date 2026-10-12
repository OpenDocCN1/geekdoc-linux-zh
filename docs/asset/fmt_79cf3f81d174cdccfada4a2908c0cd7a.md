
### 5. 阅读第 12 章“MySQL 通用管理”，熟悉通用的管理流程。特别是，您应该阅读关于服务器启动和关闭以及使用非特权用户账户运行服务器的章节。

### A.4.1 为 MySQL 用户创建登录账户

此步骤仅适用于首次安装，且仅当您要运行 MySQL 服务器时是必要的。如果是升级或仅安装 MySQL 客户端软件，可以跳过此步骤。

MySQL 服务器可以作为系统上的任何 Unix 用户运行，但出于安全和行政原因，您不应将服务器作为 `root` 运行。我建议您创建一个单独的账户用于 MySQL 管理，并将服务器作为该用户运行。这样，您可以登录为该用户，并拥有数据目录的完整权限以执行维护和故障排除。关于使用非 `root` 账户进行 MySQL 管理的好处，请参阅第 12.2.1.1 节“使用非特权登录账户运行服务器”。

创建用户账户的步骤因系统而异。请咨询当地文档以了解具体细节。（如果您使用 RPM 软件包，服务器 RPM 安装程序会自动为您创建一个名为 `mysql` 的用户的登录账户。）

本书在 MySQL 管理账户的 Unix 用户和组名中均使用 `mysql`。如果您计划仅为自己使用安装 MySQL，您可以从您自己的账户运行它，在这种情况下，您将在本书中看到用于用户或组名的 `mysql` 的地方使用您自己的登录名和组名。

在您创建用于运行 MySQL 的账户之前，先检查您的系统是否已经有一个账户。许多 Unix 系统在其标准账户集中包含 `mysql` 用户和组。例如，当前版本的 Mac OS X 包含 `mysql` 账户（这满足了 Mac OS X DMG 软件包假设名为 `mysql` 的登录账户已存在的假设）。

### A.4.2 在 Unix 上获取和安装 MySQL 分发版

以下各节描述了如何使用不同类型的分发版安装 MySQL。说明使用 `version` 代表 MySQL 版本号，`platform` 代表您正在安装的系统类型，`epu` 代表分发版针对其构建的处理器或类型。这些值用于分发版文件名中，以便于识别和区分不同的分发版。版本号类似于 5.0、5.6、5.1.24-rc 或 6.0.5-alpha。平台/CPU

系统名称类似于在 SPARC 硬件上运行 Solaris 10 的 `solaris10-spare`，或在 Intel 硬件上运行 Linux 的 `linux-i686`。

#### A.4.2.1 安装 tar 文件二进制发行版

`tar` 文件二进制发行版的文件名类似于 `mysql-version-platform-cpu.tar.gz`。获取您所需版本和平台的发行版文件，并将其放置到您希望安装 MySQL 的目录下（例如，`/usr/local`）。

使用以下命令之一解包发行版文件（如果您的 `tar` 版本不支持 `z` 选项，请使用第二个命令）：

```bash
% tar zxf mysql-version-platform-cpu.tar.gz
% gunzip < mysql-version-platform-cpu.tar.gz | tar xf -
```

解包发行版文件会创建一个名为 `mysql-version-platform-cpu` 的目录，其中包含发行版的内容。为了更轻松地引用此目录，请创建一个指向该目录的名为 `mysql` 的符号链接：

```bash
% ln -s mysql-version-platform-cpu mysql
```

创建链接后，您可以将安装目录引用为 `/usr/local/mysql`（假设您将 MySQL 安装在 `/usr/local` 下）。

现在请前往第 A.4.3 节，“安装后步骤”。

#### A.4.2.2 安装 RPM 发行版

RPM 包可用于在基于 RPM 的 Linux 系统上安装 MySQL。以下列表描述了一些更常用的软件包。在软件包文件名中，`version` 代表 MySQL 版本号，`platform` 代表目标系统类型（或者对于应该在任何支持 glibc 2.3 的 Linux 发行版上都能工作的通用软件包，则为 `glibc23`），`cpu` 指示构建该发行版的目标处理器类型。

- `MySQL-server-version-platform-cpu.rpm`

  服务器软件。

- `MySQL-client-version-platform-cpu.rpm`

  客户端程序。如果您从 RPM 包安装 MySQL，您应该始终安装客户端软件包。

- `MySQL-embedded-version-platform-cpu.rpm`

  嵌入式服务器，`libmysql4`。（适用于 MySQL 5.1 及更高版本）

- `MySQL-devel-version-platform-cpu.rpm`

  用于编写客户端程序的开发支持（客户端库和头文件）。如果您想编写自己的 C 程序或 Perl DBI 脚本来访问 MySQL 数据库，您将需要此 RPM。其他语言的 MySQL API 可能也依赖于这些客户端库和头文件。

- `MySQL-shared-version-platform-cpu.rpm`

  共享客户端库。

- `MySQL-bench-version-platform-cpu.rpm`

  基准测试和测试。这些需要 Perl DBI 支持。（参见第 A.4.4 节，“在 Unix 上安装 Perl DBI 支持”。）

- `MySQL-version.src.rpm`

  服务器、客户端、基准测试和测试的源代码。

安装 RPM 包时，您不需要处于任何特定的目录中，因为 RPM 包含指示其内容应放置位置的信息。对于任何 RPM 包 `rpm_file`，您都可以使用以下命令查看其内容将安装的位置：

```bash
% rpm -qpl  rpm_file
```

要安装 RPM 包，请使用此命令（您需要以 `root` 身份执行此操作）：

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

#### A.4.2.3 安装源代码发行版

MySQL 源代码发行版的文件名类似于 `mysql-version.tar.gz`，其中 `version` 是 MySQL 版本号。（与二进制发行版不同，源代码发行版适用于所有系统，因此文件名中没有 `platform` 或 `cpu` 值。）选择您希望解包该发行版的目录并进入该目录。获取发行版文件，并使用以下命令之一进行解包（如果您的 `tar` 版本不支持 `z` 选项，请使用第二个命令）：

```bash
$ tar zxf mysql-version.tar.gz
$ gunzip < mysql-version.tar.gz | tar xf -
```

解包发行版文件会创建一个名为 `mysql-version` 的目录，其中包含发行版的内容。切换到该目录：

```bash
$ cd mysql-version
```

现在，在安装之前，您需要配置和编译该发行版。如果以下步骤失败，请检查 MySQL 参考手册中的安装章节，特别是其中关于您的系统类型的任何平台特定说明。

使用 `configure` 命令配置该发行版：

```bash
$ ./configure
```

您可能需要为 `configure` 指定选项。要获取可用选项的列表，请运行此命令：

```bash
$ ./configure --help
```

以下列表显示了一些常见的配置选项：

- `--with-innodb`, `--without-innodb`

  包括或不包括对 InnoDB 存储引擎的支持。排除 InnoDB 会使服务器更小，并使其使用更少的内存。但是，如果您计划使用 InnoDB 表，则应该包含此引擎。

- `--without-server`

  配置该发行版以仅构建客户端支持（客户端程序或客户端库）。如果您计划访问运行在另一台机器上的服务器，可能会这样做。

- `--with-embedded-server`

  构建嵌入式服务器库，`libmysqlid`。
