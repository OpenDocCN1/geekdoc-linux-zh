
关于内核和带浮栈的 `linuxthreads` 的说明：使用 `errno`、`h_errno` 和 `_res` 的应用程序必须包含头文件（`errno.h`、`netdb.h` 和 `resolve.h`）。对于使用线程取消的多线程 C++ 程序，必须使用环境变量 `LD_ASSUME_KERNEL=2.4.1` 来使用 `linuxthreads` 库。

## 2.2 版本间的更改

- SUSE Linux 9.1 包含线程软件包 NPTL（原生 POSIX 线程库）。NPTL 与旧的 `linux-threads` 库二进制兼容。然而，`linuxthreads` 违反 POSIX 标准的地方需要 NPTL 适配。这包括：信号处理、`getpid` 返回所有线程的值，以及如果使用 `fork`，通过 `pthread_atfork` 注册的线程处理器无法工作。

- 目前系统的默认编码为 UTF-8。因此，在执行标准安装时，区域设置设置为 .UTF-8 编码（例如 `en_US.UTF-8`）。

- 在默认设置下，来自 `coreutils` 软件包的 shell 工具（`tail`、`chown`、`head`、`sort` 等）不再符合 1992 POSIX 标准，而是符合 2001 POSIX 标准（单一 Unix 规范，版本 3 == IEEE Std 1003.1-2001 == ISO/IEC 9945:2002）。可以通过环境变量强制旧行为：

```bash
_POSIX2_VERSION=199209
```

新值为 `200112`，作为 `_POSIX2-VERSION` 的默认值。可以在此处查看 SUS 标准：

表 2.1：POSIX 1992 与 2001 比较

| POSIX 1992 | POSIX 2001 |
| :--- | :--- |
| chown | chown |
| tail | tail |
| head | head |
| sort | sort |
| nice | nice |
| split | split |

## 2.3 更新系统与软件包管理

- SUSE Linux 9.1 包含线程软件包 NPTL（原生 POSIX 线程库）。NPTL 与旧的 `linux-threads` 库二进制兼容。然而，`linuxthreads` 违反 POSIX 标准的地方需要 NPTL 适配。这包括：信号处理、`getpid` 返回所有线程的值，以及如果使用 `fork`，通过 `pthread_atfork` 注册的线程处理器无法工作。

- 目前系统的默认编码为 UTF-8。因此，在执行标准安装时，区域设置设置为 .UTF-8 编码（例如 `en_US.UTF-8`）。

- 在默认设置下，来自 `coreutils` 软件包的 shell 工具（`tail`、`chown`、`head`、`sort` 等）不再符合 1992 POSIX 标准，而是符合 2001 POSIX 标准。可以通过环境变量强制旧行为：

```bash
_POSIX2_VERSION=199209
```

新值为 `200112`，作为 `_POSIX2-VERSION` 的默认值。可以在此处查看 SUS 标准：

`http://www.unix.org`

- 对于许多软件包，开发软件所需的组件（库、头文件等）已已放入独立的软件包中。如果你想自己编译软件（例如最新的 GNOME），则需要这些开发软件包。可以通过名称后缀 `-devel` 来识别，例如 `alsa-devel`、`gimp-devel` 和 `kdelibs-devel`。

可以使用 `-U` 或 `--upgrade` 以及 `-F` 或 `--freshen` 选项来更新软件包。

```
rpm -F <package>.rpm
```

此命令将删除旧版本的文件并立即安装新文件。这两个者的区别在于：`-U` 安装系统中之前不存在的包，而 `-F` 仅更新之前已安装的包。在更新时，rpm 会使用以下策略谨慎地更新配置文件：

- * 如果配置文件没有被系统管理员修改过，rpm 将安装相应文件的新版本。不需要系统管理员进行任何操作。

- * 如果配置文件在更新之前被系统管理员修改过，rpm 将修改后的文件保存为带有 `.rmporig` 或 `.rpmsave` 扩展名的文件（备份文件），并安装新包中的版本，但仅当原始安装的文件与新版本不同时才执行此操作。如果是此类情况，请比较备份文件（`.rmporig`, `.rpmsave`）与新安装的文件，并在新文件中进行所有更改。之后，请务必删除所有 `.rmporig` 和 `.rpmsave` 文件，以避免后续更新出现问题。

- * 如果配置文件已经存在，且在 .spec 文件中指定了 nore 标签，则会出现 `.rpmnew` 文件。

更新后，应在比较后删除 `.rpmsave` 和 `.rpmnew` 文件，以免它们阻塞未来的更新。如果文件之前未被 RPM 数据库识别，则分配 `.rmporig` 扩展名。

否则，使用 `.rpmsave`。换句话说，`.rmporig` 产生于从外部格式更新为 RPM。`.rpmsave` 产生于从旧 RPM 更新到新版 RPM。`.rpmnew` 不会显示系统管理员是否对配置文件进行了任何更改。可以在 `/var/adm/rpmconfigcheck` 中查看这些文件的列表。某些配置文件（如 `/etc/httpd/httpd.conf`）不会被覆盖，以允许继续运行。

`-U` 切换不仅仅是使用 `-e` 选项卸载和使用 `-i` 选项安装的等效操作。请尽可能使用 `-U`。

54 2.3. RPM — 软件包管理器

> 每次更新后，检查由 rpm 创建的带有 `.rpmorig` 或 `.rpmsave` 扩展名的备份副本。这些是您的旧配置文件。如有必要，将备份副本中的修改应用到新配置文件，并删除带有 `.rpmorig` 或 `.rpmsave` 扩展名的旧文件。

要删除软件包，输入 `rpm -e (package)`。在没有未解决依赖关系的情况下，rpm 才会删除软件包。从理论上讲，只要另一个应用程序需要它，就不删除 Tcl/Tk。即使在这种情况下，RPM 也会请求协助。如果由于某种原因或在异常情况下，在没有额外依赖项的情况下无法删除，那么使用 `--rebuilddb` 选项重新构建 RPM 数据库可能会有所帮助。

### 2.3.3 RPM 与补丁

为了确保系统的运行安全，必须定期在系统中安装更新包。以前，软件包中的错误可以通过替换整个包来消除。带有微小错误的大软件包可能会导致大量数据。然而，自 SUSE 8.1 以来，SUSE RPM 引入了一项新功能，允许在软件包中安装补丁。

以下以 pine 为例演示了最重要的考虑因素：

- 补丁 RPM 是否适用于我的系统？要检查此项，首先查询软件包的安装版本。对于 pine，可以通过以下命令完成：

```
rpm -q pine
pine-4.44-188
```

然后检查补丁 RPM 是否适用于此版本的 pine：

```
rpm -qp --basedir pine-4.44-224.i586.patch.rpm
pine = 4.44-188
pine = 4.44-195
pine = 4.44-207
```

此补丁适用于三个不同版本的 pine。示例中也列出了安装的版本，因此可以安装补丁。

- 补丁替换了哪些文件？

在补丁 RPM 中可以很容易看到受补丁影响的文件。rpm 参数 `-PPl` 允许选择特殊的补丁功能。使用以下命令显示文件列表：

```
rpm -qPPl pine-4.44-224.i586.patch.rpm
/etc/pine.conf
/etc/pine.conf.fixed
/usr/bin/pine
```

或者，如果补丁已经安装，使用以下命令：

```
rpm -qPPl pine.conf
/etc/pine.conf
/etc/pine.conf.fixed
/usr/bin/pine
```

- 如何在系统中安装补丁 RPM？

RPM 的用法与普通 RPM 相同。唯一的区别是必须已经安装了合适的 RPM。

- 系统中安装了哪些补丁，适用于哪些软件包版本？

可以使用命令 `rpm -qPa` 显示系统中所有安装的补丁列表。如果新系统中只安装了一个补丁（如示例所示），列表显示如下：

```
rpm -qPa
pine-4.44-224
```

如果在日后的某个日期，您想知道最初安装的是哪个软件包版本，可以在 RPM 数据库中找到此信息。对于 pine，可以通过以下命令显示：

```
rpm -qp --basedir pine
pine = 4.44-188
```

更多信息（包括关于补丁的信息）可以参考 `man rpm`。

56 2.3. RPM — 软件包管理器

### 2.3.4 RPM 查询

使用 `-q` 选项，rpm 执行查询以检查 RPM 数据库。可以使用多个切换来指定查询类型：

- `-i` 软件包信息

- `-l` 文件列表

- `-f` 文件（带完整路径）

- `-s` 仅显示

- `-c` 仅显示配置

- `-d` 仅显示文档

- `--dump` 详细文件

- `--provides` 软件包的功能
