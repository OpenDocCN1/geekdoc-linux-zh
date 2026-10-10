
*name* 可以是任何字符串，用于唯一标识一个库。它可以是一个词、几个字符，甚至是一个单个字母。共享数学库的名称是 `libm.so.5`，其中数学库由字母 `m` 唯一标识，主版本号为 `5`，而 `libm.a` 是静态数学库。X Window 库的名称是 `libX11.so.6`，其中 X Window 库由字母 `X11` 唯一标识，主版本号为 `6`。

大多数共享库位于 `/usr/lib` 和 `/lib` 目录中。这些目录总是首先被搜索。一些共享库位于它们自己的特殊目录中。这些目录的列表放置在 `/etc/ld.conf` 配置文件中。这些目录也会被搜索，以查找特定库。默认情况下，Linux 首先查找共享库，然后查找静态库。每当共享库更新或安装新的共享库时，你需要运行 `ldconfig` 命令来更新其在 `/etc/ld.conf` 文件中的条目以及指向它的链接（如果你从 RPM 包安装，这通常会自动完成）。

## Makefile 文件

如果不存在配置脚本，且程序不使用 `xmkmf`，你可能需要直接编辑软件的 Makefile。请务必检查此类软件的文档，查看是否需要对 Makefile 进行任何更改。可能只需要进行少数更改，但更详细的更改需要对 C 编程语言及 `make` 如何与其配合工作有深入理解。如果你成功配置了 Makefile，可能只需输入 `make` 和 `make install` 命令即可。一个可能的问题是定位 C 和 X Window 系统的开发库。X 库位于 `/usr/X11R6/lib` 目录中。标准 C 库位于 `/usr/lib` 目录中。

## 命令与程序目录：PATH

程序和命令通常安装在几个标准的系统目录中，例如 `/bin`、` /usr/bin`、`/usr/X11R6/bin` 或 `/usr/local/bin`。然而，某些软件包将其命令放在子目录中，这些子目录是您在一个标准目录内或完全独立的目录中创建的。在这种情况下，您可能无法运行这些命令，因为您的系统可能无法在新的子目录中找到它们。您的系统维护着一组目录，每次执行命令时都会在这些目录中进行搜索。这组目录存储在一个名为 `PATH` 的系统变量中，该变量在您启动系统时创建。如果某个命令位于不在此列表中的目录里，您的系统将无法定位并运行它。要使用此类命令，您需要先将新目录添加到 `PATH` 变量中的目录集合中。RPM 等安装工具会自动为您将适当目录更新到 `PATH`。

不同的服务在系统启动时会添加 `PATH` 变量。一种更安全的做法是使用 `/etc/profile` 文件中的 `pathmunge` 功能，在该文件中添加 `PATH` 定义。

### /etc/profile

为了使应用程序对所有用户可用，您可以将软件的目录添加到 `/etc/profile` 脚本中的 path 条目中。`/etc/profile` 脚本是一个系统脚本，在用户登录时为每个用户执行。请使用文本编辑器（如 KEdit、Gedit、Emacs 或 Vi）仔细编辑 `/etc/profile` 文件（您可能想先用 `cp` 命令制作一个备份副本）。您可以使用同样定义在 `/etc/profile` 中的 `pathmunge` 功能轻松将目录添加到 `PATH` 变量。例如，如果您安装了 Java 2 SDK，Java 命令将安装在 `/usr/local` 目录中一个名为 `j2sdk-1.4.2/bin` 的子目录中。该目录的完整路径名为 `/usr/local/j2sdk-1.4.2/bin`。您需要使用 `pathmunge` 将此目录添加到 `/etc/profile` 文件中分配给 `PATH` 的目录列表中。

```
pathmunge /usr/local/j2sdk-1.4.2/bin
```

您可以在 `/etc/profile` 中看到 `pathmunge` 的其他用法，例如为 root 用户添加 `/sbin`。完成更改后，您可以执行 profile 文件以使更改生效。

```
$ . /etc/profile
```

> **注意** 在较旧的系统中，您需要为 `PATH` 变量创建一个新的赋值条目。您需要添加一行，以 `PATH` 开头，后跟 `=` 符号和术语 `$PATH`，再后跟一个冒号，然后是要添加的目录。`$` 符号从 `PATH` 变量中提取路径名。如果您添加了多个目录，它们之间必须用冒号分隔。末尾也会有一个冒号。以下示例显示了包含目录列表和添加的 `/usr/local/j2sdk-1.4.2/bin` 目录的 `PATH` 变量。请注意 `=` 符号后的 `PATH` 前面的 `$`：`PATH=$PATH:/usr/local/j2sdk-1.4.2/bin`

![](img/ab68ea377332b50bf70ef1316c8175b6_694_0.png)

### .bash_profile

个别用户可以通过在其 `.bashrc` 或 `.bash_profile` 文件中放置 `PATH` 赋值来自定义其 `PATH` 变量。这样，用户可以在自己的用户目录中访问他们创建或自行安装用于自己使用的命令和程序。用户的 `.bash_profile` 文件已包含以下 `PATH` 定义。请注意 `$PATH` 的使用，它保留了之前启动脚本（如 `/etc/profile`）中已添加到 `PATH` 的所有目录。

```
PATH=$PATH:$HOME/bin
```

`.bash_profile` 文件中的以下条目将用户的 `newbin` 目录添加到 `PATH` 变量。请注意新目录前的冒号以及使用 `$HOME` 变量来指定用户主目录的路径名。

```
PATH=$PATH:$HOME/bin/;:$HOME/newbin
```

对于 `root` 用户，`PATH` 定义还包括 `sbin` 目录。`sbin` 目录包含 root 用户需要访问的系统管理程序。这里显示了 `root` 用户的 `PATH`：

```
PATH=/usr/local/sbin:/usr/sbin:/sbin:$PATH:$HOME/bin
```
