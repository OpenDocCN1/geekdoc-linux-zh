
你可能想要使用的软件并不都可用 `rpm` 软件包形式提供，或者不提供你所需的确切形式。许多复杂程序具有只能在编译时选择的选项，而许多小型、特定用途的应用程序仅以源代码形式存在。Fedora Core 提供了将你需要的源代码编译为二进制应用程序所需的所有工具。首先，我们将介绍从源 `rpm` 文件构建，然后操纵源 `rpm` 文件，最后从源压缩包进行构建。

> **注意**
>
> 对于其他软件包格式，你可以使用 `File Roller` 应用程序（在“附件”菜单中找到）轻松显示、浏览、读取和解压缩文件的内容，包括诸如 `tarball` 或压缩的 `tar` 归档（可通过其 `.gz` 或 `.tgz` 扩展名识别）等遗留归档。`File Roller` 也支持其他压缩文件，例如使用 `compress` 命令创建的文件（以 `.Z` 结尾）或 `bzip2` 文件（以 `.bz2` 结尾）。`File Roller` 客户端还可以在 `gzip` 和 `bzip2` 格式之间转换压缩归档。

### 从 src.rpm 文件构建 RPM

一条经验法则是，即使目录已在 `/usr/src/redhat` 设置好如下结构，你也永远不应该以 `root` 用户身份构建 `rpm`：

```text
# tree /usr/src/redhat
/usr/src/redhat
|-- BUILD
`-- RPMs
    |-- athlon
    |-- i386
    |-- i486
    |-- i586
    |-- i686
    `-- noarch
`-- SOURCES
`-- SPECS
`-- SRPMS
```

使用 `mkdir` 命令，在你的主目录中重新创建此目录树结构；你可以将新目录命名为 `redhat`（或你喜欢的任何名称）。你甚至可能希望创建一个新用户专门用于构建 `rpm` 和源代码。（你可以非 `root` 身份进行编译；你只是无法像普通用户那样将软件安装到整个系统。）

构建 `rpms` 的配置信息保存在三个位置：

- `/usr/lib/rpm/*/macros`—系统范围默认值。
- `/etc/rpm/macros.*`—保存系统范围变更的地方。
- `~/.rpmmacros`—保存用户特定变更的地方。

因为我们需要告诉 `rpm` 我们不会使用系统范围的默认构建位置作为我们的用户，我们可以

```text
$ echo "%_topdir $HOME/redhat" > $HOME/.rpmmacros
```

> **提示**
>
> 这里，我们使用 `>` 而不是 `>>`，以便如果文件中已有内容则将其清空。`>>` 结构用于将信息追加到文件。

为了选择一个临时目录

```text
$ echo "%_tmppath $HOME/tmp" >> $HOME/.rpmmacros
```

为了设置任何编译器优化标志（这里，我们以使用 `Athlon` 处理器为例），我们将使用

```text
$ echo "-o3 -march=athlon" >> $HOME/.rpmmacros
```

要作为普通用户重新构建 `src.rpm` 文件，你可以使用

```text
$ rpmbuild --recompile packagename.src.rpm
```

成功构建后，你可以在 `~/redhat/RPMS/athlon` 中找到二进制文件。你可以以 `root` 身份安装它们：

```text
# rpm -Uvh --replacepkgs --replacefiles packagename.rpm
```

如果构建失败，错误消息将指引你找到解决方案（通常是因为依赖项未满足）。你会发现，在从源代码编译之前，许多以 `-devel` 命名的软件包是必需的。安装缺失依赖项的软件包并重试编译。

## 处理源 RPM 文件

你可能希望出于自己的用途修改源软件包，例如添加文档、更改默认设置或修补源代码本身。Fedora Core 以源 `RPM` 文件的形式提供其发行版的源代码。你可以访问可下载 `CD` 镜像的第 4 和第 5 盘上的源代码，或从 Fedora Core `FTP` 站点获取它们。

> **提示**
>
> `RPM` 文件的一个重要部分称为 `.spec` 文件，即规格文件。它告诉 `RPM` 在编译、安装和清除期间如何针对特定的源文件进行操作。

作为一个例子，我们将使用在 `http://elektron.its.tudelft.nl/~rbos36/mdkfree type2.html` 找到的信息（该页面现在已被作者移除）来修改 Fedora Core 提供的 `freetype2` 库，以启用字节码解释器。解释器的代码默认被禁用，因为存在不影响个人使用的再发行许可问题。启用解释器将改善 `TrueType` 字体的渲染效果。我们使用 Red Hat 7.3 的文件作为示例，但 `FC4` 的源文件也应该有效。

首先通过安装源 `RPM` 软件包开始工作，使用 `rpm -i`。（注意，这里我们按照网页示例以 `root` 身份构建；通常你应该作为普通用户构建软件包。）在我们的例子中，获取 `freetype-2.1.9-2.src.rpm` 并使用 `rpm -i` 安装它。源代码文件被放置在 `/usr/src/redhat/SOURCES`。

将源文件（它是一个压缩的 `tar` 文件）复制到 `/tmp`，然后在那里 `cd`（更改目录）以解包和修改它：

```text
# cp freetype-2.1.9.tar.bz2 /tmp
# cd /tmp
```

因为它是一个 `.bz2`（`BZip2` 压缩）`tar` 文件，使用以下命令解包：

```text
# tar xjvf freetype-2.1.9.tar.bz2
```

并 `cd` 到新的目录：

```text
# cd freetype-2.1.9
```

使用你选择的文本编辑器，编辑文件 `include/freetype/config/ftoption.h` 并找到该行

```text
#undef  TT_CONFIG_OPTION_BYTECODE_INTERPRETER
```

将其更改为

```text
#define  TT_CONFIG_OPTION_BYTECODE_INTERPRETER
```

保存并退出文本编辑器。

接下来，重新创建压缩归档：

```text
# cd /tmp
# tar cfj freetype-2.1.9.tar.bz2 ./freetype-2.1.9/
```

将其放回你的源目录中：

```text
# mv freetype-2.1.9.tar.bz2 /usr/src/SOURCES
```

现在编辑 `/usr/src/redhat/SPECS` 中的 `.spec` 文件，更改以 `Release` 开头的行，以增加其中找到的数字。（通过这样做，我们正在更改版本号，因此不会与我们要替换的应用程序版本冲突。）如果需要，请对 `%description` 行进行任何更改以描述你的修改，并保存该文件。

使用以下命令构建二进制 `RPM`：

```text
# rpmbuild -bb freetype.spec
```

在构建过程中，`RPM` 将检测到补丁并询问你关于补丁的问题；按 `y` 表示“是”以继续。

新的 `RPM` 包（实际上有四个）位于 `/usr/src/redhat/RPMS/i386`。我们只需要名为 `freetype-2.1.9` 的那个；你可以使用 `rpm -Uvh` 进行安装。（这就是为什么我们要更改版本号；如果没有更改，`RPM` 不会升级到“相同”的版本。如果我们没有更改版本号，可以使用 `--replacepackages --replacefiles` 选项强制安装。）

字体服务器需要重启才能使用新库，因此我们使用如第 14 章“自动化任务”中所示的 `service` 命令。

```
# service xfs restart
```

享受你的新外观——这得益于字体渲染效果的提升。

## 从源代码包编译

从源代码编译应用程序并不那么困难。大多数源代码都作为压缩的源代码 *tarball* 提供——也就是说，使用 `gzip` 或 `bzip2` 压缩的 `tar` 文件。压缩文件通常会解压为一个包含多个文件的目录。作为一个普通用户来编译源代码总是个好主意，这样可以限制损坏或恶意代码可能造成的损害，因此请在你的主目录中创建一个名为 `source` 的目录。

从你下载源代码包的任何位置开始，使用 `tar` 的 `-C` 选项将其解压到 `~/source` 目录：

```
$ tar zxvf package.tar.gz -C ~/source
$ tar jxvf package.tar.bz2 -C ~/source
```

如果你不确定使用了哪种文件压缩方法，请使用 `file` 命令来确定：

```
$ file packagename
```

现在，更改目录到 `~/source/packagename`，寻找一个名为 `README`、`INSTALL` 或类似名称的文件。如果有必要，请打印该文件，因为它包含如何编译和安装软件的具体说明。通常，编译源代码的步骤是：

```
$ ./configure
```
