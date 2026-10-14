
这些信息显示了“反依赖”（哪些软件包需要、推荐或建议使用 `mysql-server-5.0`）、“依赖”（哪些软件包需要、推荐或建议安装 `mysql-server-5.0`）以及“提供”（此包提供了哪些功能）。“提供”列表非常强大，因为它允许多个软件包提供某种资源。例如，一个基于 MySQL 数据库的程序需要安装 MySQL，但不在乎你安装 MySQL 4.1 还是 MySQL 5.0。在这种情况下，MySQL 4.1 和 MySQL 5.0 的 Debian 包列表中都会包含 `mysql-server-4.1`，这意味着你可以安装任何一个版本来满足基于 MySQL 的应用程序。

# 从源码编译软件

编译应用程序源码并不困难。大多数源代码以压缩源码 tarball 的形式提供——即使用 gzip 或 bzip 压缩的文件。这些压缩文件通常会解压到一个包含几个文件的目录。作为普通用户编译源代码始终是一个好主意，以限制损坏或恶意代码可能造成的任何损害，因此在你的主目录下创建一个名为 `source` 的目录。

从你下载源码 tarball 的地方，使用 `tar` 的 `-C` 将其解压到 `~/source` 目录：

```bash
tar xvf packagename.tgz -C /source
```

```bash
tar xvf packagename.tar.gz -C /source
```

```bash
tar xvf packagename.bz -C /source
```

```bash
tar xvf packagename.tar.bz2 -C /source
```

如果你不确定使用了什么文件压缩方法，使用 `file` 命令来确定：

```bash
file packagename
```

现在，切换目录到 `~/source/packagename` 并寻找名为 `README`、`INSTALL` 或类似名称的文件。必要时打印该文件，因为它包含了有关如何编译和安装软件的具体说明。通常，编译源码的步骤如下：

```bash
./configure
```

这会运行一个脚本来检查是否满足所有依赖以及构建环境是否正确。如果你缺少依赖，`configure` 脚本会确切告诉你它需要哪一个。如果你在 `Synaptic` 中启用了 `Universe` 和 `Multiverse` 存储库，很有可能在那里找到缺少的软件（通常是库）。

当你的 `configure` 脚本执行成功后，运行

```bash
make
```

编译软件。最后，运行

```bash
sudo make install.
```

如果编译失败，检查错误信息的原因，并在重新之前运行

```bash
make clean
```

你也可以运行

```bash
sudo make uninstall
```
