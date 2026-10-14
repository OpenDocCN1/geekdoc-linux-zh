
# 第 5 章：设置 Gopher

这创建了 GN 源码目录结构。解压此文件生成的顶层包含四个目录：`gn`、`mkcache`、`waisgn` 和 `docs`。

下一步是编辑顶层目录中的 `config.h` 文件。你应该输入计划运行 GN 的计算机的主机名以及 Gopher 数据目录的完整路径。如果你想在 70 以外的端口运行，请编辑 `DEFAULTPORT` 条目。你应该指定系统上 `mkcache/gn_mime.types` 文件的完整路径。你可以将其放在任何方便的地方（并任意命名名称）。该文件供 `mkcache` 程序使用；请稍后关于 Content-type 的章节以了解该文件的功能。其他自定义是可能的，但通常不需要。

接下来，编辑顶层目录中的 `Makefile` 文件。这允许你指定所使用的 C 编译器，如果你想使用其他 `cc`（在 Slack Linux 的情况下，你需要指定 `gcc`）。你也可以指定两个在执行 `make install` 时存放文件的目录。其中第一个是 `SERVBINDIR`，它是你希望安装 GN 服务器可执行文件的目录路径。第二个 `BINDIR`，是 `mkcache` 程序的所在位置。

在 `gn-2.*` 目录下，执行 `make` 以生成 `gn` 服务器和 `mkcache` 工具程序。`mkcache` 工具程序会为每个服务器生成缓存文件（后文会详细描述）。二进制文件 `gn` 是服务器，可以安装在你选择的任何地方。二进制文件 `mkcache` 是一个供维护者的实用程序，应该安装在你路径中的某个位置，例如 `/usr/local/bin`。

现在你可以作为独立守护进程运行服务器（即 `sgn` 可执行文件），或者运行 `inet`（即 `gn` 可执行文件）。我们首先描述独立版本，在大多数情况下，这是你想要运行的版本。使用以下命令启动它：

```
sgn -p port [other options]/path/to/gmroot &
```

其中 `port` 是你希望服务器运行的端口号。如果这是一个非特权端口（高于 1024 的端口；如果你不清楚端口，可能需要回到第 3 章和第 4 章回顾关于端口的讨论），那么 `sgn` 可以作为普通用户运行。然而，对于 70 或 80 等特权端口，你必须以 root 身份运行上述命令。当 `sgn` 启动时，它会将用户 ID 更改为 `config.h` 中定义 `USERID` 的行所设置的值。

以 `nobody` 或其他没有访问权限的用户运行 `gn` 是重要的。永远不应该以 root 身份运行 `gn`；这样做对于维护安全性来说是一个严重的错误。我们已经尽一切努力让 `gn` 尽可能安全，即使是以 root 身份运行；但是，任何互联网上远程用户可以访问的程序都不能假设是绝对安全的。

## 设置数据目录

在你数据层级结构的每个目录中，创建一个名为 `menu` 的文件，并为你希望 `gn` 发布的每个文件或目录创建一个条目。文件中的条目格式如下：

```
# 这是一个注释

Maintainer=mailto:gnperson@host.edu

Name=这是显示在客户端上的文件描述
Path=0/path/to/dir/file
Type=0
Host=YourHost.YourU.edu
Port=70

Name=这是一个子目录
Path=1/path/to/dir/subdir
Type=1
Host=YourHost.YourU.edu
Port=70

Name=这是一个远程链接
Path=0/myfile/path
Type=0
Host=MyHost.MyUniv.edu
Port=70
```

以 `Maintainer=` 开头的行是可选的（且仅向 HTTP 客户端提供信息）。它应该包含指向该目录维护者的引用，类似于前一个（从技术上讲，任何 URL 都是允许的）。`Maintainer` 行必须是 `menu` 文件中第一个非空且非注释的行。

关于该文件中的条目项有几点需要注意。`Name` 字段必须在第一位，`Path` 字段以 `gn` 类型开头（例如，0 表示文件，1 表示目录；你将在本章稍后部分学习更多内容）。随后是相对于顶层数据目录的文件或目录路径。

`Type`、`Host` 和 `Port` 字段对于本地项目是可选的，但对于远程链接是必须的。如果不存在，`Type` 将取自 `Path` 字段的首字符，`Host` 和 `Port` 字段将是 `config.h`（或 `mkcache` 的命令行）中指定的。通常情况下，对于本地项目不包含 `Host` 和 `Port` 字段是一个好主意。如果你在将来某时刻想要将服务器移动到其他处，这样做会更方便。

在每个数据层级目录的 `menu` 文件创建后，运行 `mkcache` 即可。

## 测试设置

在编译并设置好软件后，你可以通过以下方式进行测试。为了做到这一点，首先在数据目录下创建一个符号链接：

```
ln -s /path/to/source data/link
```

然后，以 root 身份运行 `mkcache` 来生成 `.cache` 文件。运行 `mkcache` 即可。

## 故障排除

如果某些运行不符合预期，有一些技巧可以帮助你排除问题。

首先，如果 `gn` 编译并产生了如下错误：

```
ld: Undefined symbol putenv
```

这意味着库中缺少 `putenv` 函数。如果遇到这种情况，请检查 `config.h` 中的 `NEED_PUTENV` 定义，并取消其注释：

```
#define NEED_PUTENV
```

这样 `gn` 就可以正常工作了。
