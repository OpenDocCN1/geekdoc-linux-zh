

不幸的是，rpm 使用百分号来同时表示节标识符和指令，例如在 %Prep 和 %Files 部分中，这可能会让人困惑。一些打包者会将节标识符的首字母大写，而将指令名称保持全小写，以便在 spec 文件中区分两者，但这并非通用做法。

spec 文件中的大多数节包含 shell 脚本，这些脚本执行构建过程该阶段所需的操作。如果你不熟悉 shell 脚本编写，可以参考第 14 章“自定义 Shell 环境”中的“Shell 编程”一节。

## 构建过程中使用的节

以下节在构建过程中使用：

- **%Prep** — 此节包含一个 shell 脚本，用于解压源文件并应用补丁。它在准备（prep）阶段使用。
- **%Build** — 此节包含一个 shell 脚本，用于构建（编译）软件。它在构建（build）阶段使用。
- **%Install** — 此节包含一个 shell 脚本，用于安装软件。它在安装（Install）阶段使用。（你可能已经看出其中的规律了！）
- **%Files** — 此节包含软件包中文件和目录的清单。
- **%Clean** — 这个可选节包含一个 shell 脚本，用于在软件包构建后进行清理。
- **%Changelog** — 此节包含关于 SPEC 文件本身的变更日志信息。

## 用于软件包脚本的节

以下脚本不在构建时使用；它们会被插入到软件包中，并在最终用户系统上由软件包管理器在安装、移除或验证软件包时使用。

- **%Pre/%Post** — 在最终用户系统上安装软件包文件之前和之后运行的脚本。
- **%Preun/%Postun** — 在最终用户系统上移除软件包文件之前和之后运行的脚本。
- **%Triggerin/%Triggerun** — 在特定软件包安装和卸载时运行的脚本。例如，邮件客户端可以使用这些脚本在安装 sendmail 时添加 sendmail 支持。
- **%Triggerpostun** — 在特定软件包卸载之后运行的脚本（而 %Triggerun 是在软件包卸载之前运行的）。
- **%Verify** — 包含一个在最终用户系统上运行以验证软件包文件的脚本。如果为空，则使用 RPM 的默认验证机制。

## 辅助软件包

在 spec 文件中定义辅助软件包是很常见的。例如，如果一个软件包 mypackage 还附带一个 mypackage-devel 软件包，那么两者会在同一个 spec 文件中描述。

通常，辅助软件包中唯一不同的是文件列表和信息字段。为了定义辅助软件包的信息字段，spec 文件使用 `%package` 指令，后跟字段。之后，各个节使用软件包的名称来区分——例如：

```spec
%package devel
Summary: Development files for applications which will manipulate RPM packages.
Group: Development/Libraries
%ifos linux
Requires: python >= 1.5.1
%endif
%description devel
This package contains the RPM C library and header files. These development files
will simplify the process of writing programs which manipulate RPM packages and
databases and are intended to make it easier to create graphical package managers
or any other tools that need an intimate knowledge of RPM packages in order to
function.
```

## 构建软件包

使用 rpm 的 -b 选项来构建软件包。你可以将此命令与其他选项结合使用，仅执行构建过程的某些阶段。这对于调试软件包的构建过程非常有用。表 17.2 列出了构建选项及其对应的阶段。

**表 17.2  RPM 构建选项**

| Option | 阶段或动作 |
|---|---|
| `p` | 准备（Prep） |
| `c` | 构建（编译） |
| `i` | 安装 |
| `b` | 打包（创建二进制软件包） |
| `a` | 全部（构建二进制和源码软件包） |
| `l` | 检查文件列表 |
| `--short-circuit` | 仅执行此阶段（不执行前面的阶段） |

## 准备阶段

在软件包构建的准备阶段，会运行 spec 文件中 %prep 节中的脚本。该脚本将从 TAR 文件中解压源文件并应用补丁，为软件的实际编译做准备。

在此阶段，会在 /usr/src/distribution/BUILD 下创建一个目录。文件将放置于此，其他阶段也将在此目录中操作。

你可以使用任何需要的命令在 BUILD 目录中准备源文件。不过，有两个特殊指令可以处理大多数需要执行的操作。`%setup` 指令用于解压 Source 行中列出的源文件。`%patch` 指令用于应用 Patch 行中列出的补丁。

## 构建阶段

构建阶段是 rpm 使用 %Build 节中的脚本，针对你的系统实际编译软件的地方。通常，此脚本包括运行 configure 等程序来设置软件构建环境，以及运行 make 来实际编译软件。

对于 spec 文件的这一节，没有可用的特殊指令。不过，rpm 会设置多个 shell 变量，它们的值可能对该脚本有用。

以下 shell 变量可在 spec 文件的所有脚本中使用：

- **RPM_SOURCE_DIR** — RPM 源码目录的位置。默认为 `/usr/src/distribution/` 下的 sources，但可以通过 `/etc/rpmrc` 或 `~/.rpmrc` 中的配置值覆盖。
- **RPM_BUILD_DIR** — RPM BUILD 目录的位置。默认为 `/usr/src/distribution/BUILD`。此值也可以被覆盖。
- **RPM_DOC_DIR** — 此软件包文档目录所放置的位置。默认值为 `/usr/doc`。
- **RPM_OPT_FLAGS** — 用于为目标架构（i386）生成优化代码的编译器选项字符串。在编译软件时，通常与 make 一起使用。
- **RPM_OS** — 指示构建过程中所使用的操作系统（不仅仅是 Linux！）的字符串。
- **RPM_ARCH** — 指示构建过程中所使用的架构的字符串。
- **RPM_ROOT_DIR** — 构建过程所有步骤中使用的根目录。
- **RPM_BUILD_ROOT** — 构建过程的安装和打包阶段使用的根目录。
- **RPM_PACKAGE_NAME** — 软件包的名称。
- **RPM_PACKAGE_VERSION** — 软件包中软件的版本。
- **RPM_PACKAGE_RELEASE** — 软件包的发布版本。

## 安装阶段

在安装阶段，会运行命令将软件实际安装到你的系统上。此阶段结束时，软件将被安装到系统上，并已完成编译和格式化，可以运行，正如它在最终用户系统上所需要的那样。执行此操作的 shell 脚本位于 spec 文件的 %Install 节中。

在打包阶段（下一节描述）放入软件包的文件，取自工作文件系统中的常规位置。它们的位置、所有者和权限会被记录在软件包中，以便在安装软件包时，在用户的系统上具有相同的属性。因此，安装阶段完整且正确地设置文件至关重要。

## 打包阶段

在此阶段，实际创建软件包文件（二进制和源码 RPM）。安装阶段放入文件系统的文件会被收集起来，连同 spec 文件中的信息一起放入二进制软件包文件中。然后，用于生成软件包的所有材料会被收集并捆绑到一个源码 RPM 软件包中，该软件包可以使用（一组类似的工具和库）在日后重新生成该软件包。

spec 文件的 `%files` 节列出了将放入软件包的文件系统中的文件和目录。这些将与构建过程的安装阶段放到文件系统中的文件相对应。

`%files` 节支持以下指令和选项：

- `%doc` — 标记文档文件。这些文件会放在最终用户系统上的 `/usr/doc` 下的某个目录中。不要将此用于手册页或其他必须位于最终用户系统特定位置的文件。请注意，使用此指令列出的路径是相对于 BUILD 目录的，而不是常规文件系统。例如，在清单 17.1 中，使用 `%doc` 指令列出的 NEWS 文件指的是 `/usr/src/distribution/BUILD/ed-0.2/NEWS`，当安装此软件包时，该文件将被放置到用户系统的 `/usr/doc/ed-0.2/NEWS`。
- `%config` — 标记配置文件。这些文件在用户机器上的移除和升级操作期间会得到特殊处理。
- `%dir` — 指示一个目录。这会使 rpm 打包该指示目录及其所有子目录中的所有文件。
- `-f filename` — 与 `%files` 节一起使用的 `-f` 选项表示从单独的文件读取文件列表。例如，以下行：

  `%files -f edlist`

  将从文件 `/usr/src/distribution/BUILD/ed-0.2/edlist` 读取文件列表，而不是从 spec 文件读取。

> **注意：** 在文件列表中列出目录时要小心。如果文件列表中的某个项是一个目录，rpm 会将其解释为 `%dir` 项并读取其中的所有文件。如果目录不正确，最终可能会在软件包中放入大量（而且不是正确的）文件。

在此阶段结束时，二进制软件包文件位于 RPMS/i386 目录中，源码软件包文件位于 SRPMS 中。

## 打包杂项

本节提供一些杂项提示，帮助你调试软件包构建过程。此外，还描述了一些主要发行版在其软件包中使用的约定。在构建软件包时，你可能会想使用类似的技术。

