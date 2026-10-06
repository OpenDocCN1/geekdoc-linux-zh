

## 第二部分：使用 Fedora RHEL

| 格式 | 扩展名 | 描述 |
|---|---|---|
| tar and gzip 文件 | .tgz | 对于使用 gzip 压缩的 tar 归档文件，常见的做法是使用 .tgz 扩展名。 |
| bzip2 | .bz2 | 文件使用 bzip2 程序压缩。 |
| Tar/压缩 | .tar .xz | 使用 tar 归档并使用 UNIX compress 命令进行压缩的文件。 |
| Linux 软件映射 | .lsm | 文件包含归档文件的内容。 |
| Debian 二进制包 | .deb | 文件是 Debian 发行版使用的二进制包。（稍后请参阅本章后半部分关于如何将 Debian 转换为 Red Hat 格式的描述。） |
| RPM 包管理 | .rpm | 文件是 Fedora 使用的二进制包。该格式也适用于其他 Linux 发行版。 |

## 表 5-2：Linux 文档格式

| 格式 | 扩展名 | 描述 |
|---|---|---|
| 超文本标记语言 | .html .htm | 文件为超文本格式，供 Web 浏览器程序（如 Mozilla）阅读。 |
| PostScript | .ps | 文件为 PostScript 格式，输出到 PostScript 打印机上。 |
| SGML | .sgml | 文件为 SGML，一种标准文档格式。SGML 通常用于生成后期可以转换为各种格式的文档。 |
| DVI | .dvi | 文件为 DVI，是 LaTeX 处理工具的输出格式。使用 dvips 和 dvjij 命令将这些文件转换为 PostScript 或惠普的 PCL。 |
| 纯文本 | | Fedora 中没有后缀后缀的文件有时是纯文本文件（ASCII 格式）。（注意：Linux 中的所有命令，如 /usr/bin 和 /usr/sbin 中的命令，都没有扩展名。如果你有一个没有扩展名的文件，最好在进行任何操作之前先使用 `file` 命令。事实上，对之前未测试过的文件使用 `file` 可以防止问题，例如，一个包含系统恶意内容的 .txt 文件。） |

## 第 5 章：访问和运行应用程序

如果你不确定文件的格式，请如下所示使用 `file` 命令：

```
$ file filename
```

该命令可以你它是 GNU tar 文件、RPM、gzip 还是其他文件格式。（如果文件被重命名并丢失了扩展名，这是一个很好的技巧）。

如果你想将软件包从上述格式之一转换，可以使用 `alien` (http://freshmeat.net/projects/alien)。虽然 alien 不被认为足够稳定以用于系统包，但它可以作为在你的 Fedora 系统上尝试某些软件包的良好工具。

## 从源码编译并安装

如果你需要的包没有二进制版本，或者你只是想根据需要定制包，你始终可以从源代码安装该包。开始之前，你可以从 Fedora 软件仓库获取任何包的源码（SRPM）版本（详情请参见附录 A）。你可以修改源码并重新构建以适应你的需求。

没有提供 RPM 格式的软件包通常以 tarball（通过 `tar` 工具将一组文件分组成单个格式的文件）的形式存在，并经过了压缩（通常通过 `gzip` 工具）。虽然从源码归档文件安装应用程序的具体指令各异，但许多 .bz2、.tar.bz2、.tgz、.gz 和 .tar 格式的包都遵循基本步骤。

> 提示：在从源码安装之前，你需要安装各种软件开发包。如果你有磁盘空间，我建议你安装 Fedora 安装过程中推荐的所有软件开发包。

以下是 C 语言软件开发工具的最小列表：

- gcc — 包含 gcc（GNU C 编译器）编译器。
- make — 包含用于从 Makefile 构建二进制文件的 `make` 命令。
- glibc — 包含重要的共享库、C 库和标准数学库。
- glibc-devel — 包含用于创建可执行文件的标准头文件。
- kernel-devel — 包含 Linux 内核源码，重建内核时需要。
- rpm-build — 包含用于从源码构建 RPM 包的 `rpmbuild` 工具。
- libc — 基于 libc 5 编写的程序所需的库，旧版应用程序可以在 glibc (libc 6) 系统上运行。如果你使用 C++，有许多包可以获取，特别是 libstdc++ 和 libstdc++-devel。

## 安装 SRPM 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A 获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改，其中 package 是软件包的名字。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改，其中 package 是软件包的名字。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tgz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 访问和运行应用程序

如果你不确定文件的格式，请如下所示使用 `file` 命令：

```
$ file filename
```

该命令可以你它是 GNU tar 文件、RPM、gzip 还是其他文件格式。（如果文件被重命名并丢失了扩展名，这是一个很好的技巧）。

如果你想将软件包从上述格式之一转换，可以使用 `alien` (http://freshmeat.net/projects/alien)。虽然 alien 不被认为足够稳定以用于系统包，但它可以作为在你的 Fedora 系统上尝试某些软件包的良好工具。

## 从源码编译并安装

如果你需要的包没有二进制版本，或者你只是想根据需要定制包，你始终可以从源代码安装该包。开始之前，你可以从 Fedora 软件仓库获取任何包的源码（SRPM）版本（详情请参见附录 A）。你可以修改源码并重新构建以适应你的需求。

没有提供 RPM 格式的软件包通常以 tarball（通过 `tar` 工具将一组文件分组成单个格式的文件）的形式存在，并经过了压缩（通常通过 `gzip` 工具）。虽然从源码归档文件安装应用程序的具体指令各异，但许多 .bz2、.tar.bz2、.tgz、.gz 和 .tar 格式的包都遵循基本步骤。

> 提示：在从源码安装之前，你需要安装各种软件开发包。如果你有磁盘空间，我建议你安装 Fedora 安装过程中推荐的所有软件开发包。

以下是 C 语言软件开发工具的最小列表：

- gcc — 包含 gcc（GNU C 编译器）编译器。
- make — 包含用于从 Makefile 构建二进制文件的 `make` 命令。
- glibc — 包含重要的共享库、C 库和标准数学库。
- glibc-devel — 包含用于创建可执行文件的标准头文件。
- kernel-devel — 包含 Linux 内核源码，重建内核时需要。
- rpm-build — 包含用于从源码构建 RPM 包的 `rpmbuild` 工具。
- libc — 基于 libc 5 编写的程序所需的库，旧版应用程序可以在 glibc (libc 6) 系统上运行。如果你使用 C++，有许多包可以获取，特别是 libstdc++ 和 libstdc++-devel。

## 安装 SRPM 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tgz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 访问和运行应用程序

如果你不确定文件的格式，请如下所示使用 `file` 命令：

```
$ file filename
```

该命令可以你它是 GNU tar 文件、RPM、gzip 还是其他文件格式。（如果一个文件被重命名并丢失了扩展名，这是一个很好的技巧）。

如果你想将软件包从上述格式之一转换，可以使用 `alien` (http://freshmeat.net/projects/alien)。虽然 alien 不被认为足够稳定以用于系统包，但它可以作为在你的 Fedora 系统上尝试某些软件包的良好工具。

## 从源码编译并安装

如果你需要的包没有二进制版本，或者你只是想根据需要定制包，你始终可以从源代码安装该包。开始之前，你可以从 Fedora 软件仓库获取任何包的源码（SRPM）版本（详情请参见附录 A）。你可以修改源码并重新构建以适应你的需求。

没有提供 RPM 格式的软件包通常以 tarball（通过 `tar` 工具将一组文件分组成单个格式的文件）的形式存在，并经过了压缩（通常通过 `gzip` 工具）。虽然从源码归档文件安装应用程序的具体指令各异，但许多 .bz2、.tar.bz2、.tgz、.gz 和 .tar 格式的包都遵循基本步骤。

> 提示：在从源码安装之前，你需要安装各种软件开发包。如果你有磁盘空间，我建议你安装 Fedora 安装过程中推荐的所有软件开发包。

以下是 C 语言软件开发工具的最小列表：

- gcc — 包含 gcc（GNU C 编译器）编译器。
- make — 包含用于从 Makefile 构建二进制文件的 `make` 命令。
- glibc — 包含重要的共享库、C 库和标准数学库。
- glibc-devel — 包含用于创建可执行文件的标准头文件。
- kernel-devel — 包含 Linux 内核源码，重建内核时需要。
- rpm-build — 包含用于从源码构建 RPM 包的 `rpmbuild` 工具。
- libc — 基于 libc 5 编写的程序所需的库，旧版应用程序可以在 glibc (libc 6) 系统上运行。如果你使用 C++，有许多包可以获取，特别是 libstdc++ 和 libstdc++-devel。

## 安装 SRPM 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tgz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 访问和运行应用程序

如果你不确定文件的格式，请如下所示使用 `file` 命令：

```
$ file filename
```

该命令可以你它是 GNU tar 文件、RPM、gzip 还是其他文件格式。（如果一个文件被重命名并丢失了扩展名，这是一个很好的技巧）。

如果你想将软件包从上述格式之一转换，可以使用 `alien` (http://freshmeat.net/projects/alien)。虽然 alien 不被认为足够稳定以用于系统包，但它可以作为在你的 Fedora 系统上尝试某些软件包的良好工具。

## 从源码编译并安装

如果你需要的包没有二进制版本，或者你只是想根据需要定制包，你始终可以从源代码安装该包。开始之前，你可以从 Fedora 软件仓库获取任何包的源码（SRPM）版本（详情请参见附录 A）。你可以修改源码并重新构建以适应你的需求。

没有提供 RPM 格式的软件包通常以 tarball（通过 `tar` 工具将一组文件分组成单个格式的文件）的形式存在，并经过了压缩（通常通过 `gzip` 工具）。虽然从源码归档文件安装应用程序的具体指令各异，但许多 .bz2、.tar.bz2、.tgz、.gz 和 .tar 格式的包都遵循基本步骤。

> 提示：在从源码安装之前，你需要安装各种软件开发包。如果你有磁盘空间，我建议你安装 Fedora 安装过程中推荐的所有软件开发包。

以下是 C 语言软件开发工具的最小列表：

- gcc — 包含 gcc（GNU C 编译器）编译器。
- make — 包含用于从 Makefile 构建二进制文件的 `make` 命令。
- glibc — 包含重要的共享库、C 库和标准数学库。
- glibc-devel — 包含用于创建可执行文件的标准头文件。
- kernel-devel — 包含 Linux 内核源码，重建内核时需要。
- rpm-build — 包含用于从源码构建 RPM 包的 `rpmbuild` 工具。
- libc — 基于 libc 5 编写的程序所需的库，旧版应用程序可以在 glibc (libc 6) 系统上运行。如果你使用 C++，有许多包可以获取，特别是 libstdc++ 和 libstdc++-devel。

## 安装 SRPM 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tgz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 访问和运行应用程序

如果你不确定文件的格式，请如下所示使用 `file` 命令：

```
$ file filename
```

该命令可以你它是 GNU tar 文件、RPM、gzip 还是其他文件格式。（如果一个文件被重命名并丢失了扩展名，这是一个很好的技巧）。

如果你想将软件包从上述格式之一转换，可以使用 `alien` (http://freshmeat.net/projects/alien)。虽然 alien 不被认为足够稳定以用于系统包，但它可以作为在你的 Fedora 系统上尝试某些软件包的良好工具。

## 从源码编译并安装

如果你需要的包没有二进制版本，或者你只是想根据需要定制包，你始终可以从源代码安装该包。开始之前，你可以从 Fedora 软件仓库获取任何包的源码（SRPM）版本（详情请参见附录 A）。你可以修改源码并重新构建以适应你的需求。

没有提供 RPM 格式的软件包通常以 tarball（通过 `tar` 工具将一组文件分组成单个格式的文件）的形式存在，并经过了压缩（通常通过 `gzip` 工具）。虽然从源码归档文件安装应用程序的具体指令各异，但许多 .bz2、.tar.bz2、.tgz、.gz 和 .tar 格式的包都遵循基本步骤。

> 提示：在从源码安装之前，你需要安装各种软件开发包。如果你有磁盘空间，我建议你安装 Fedora 安装过程中推荐的所有软件开发包。

以下是 C 语言软件开发工具的最小列表：

- gcc — 包含 gcc（GNU C 编译器）编译器。
- make — 包含用于从 Makefile 构建二进制文件的 `make` 命令。
- glibc — 包含重要的共享库、C 库和标准数学库。
- glibc-devel — 包含用于创建可执行文件的标准头文件。
- kernel-devel — 包含 Linux 内核源码，重建内核时需要。
- rpm-build — 包含用于从源码构建 RPM 包的 `rpmbuild` 工具。
- libc — 基于 libc 5 编写的程序所需的库，旧版应用程序可以在 glibc (libc 6) 系统上运行。如果你使用 C++，有许多包可以获取，特别是 libstdc++ 和 libstdc++-devel。

## 安装 SRPM 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

## 安装 tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tgz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .gz 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 安装 .tar.bz2 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。

## 访问和运行应用程序

如果你不确定文件的格式，请如下所示使用 `file` 命令：

```
$ file filename
```

该命令可以你它是 GNU tar 文件、RPM、gzip 还是其他文件格式。（如果一个文件被重命名并丢失了扩展名，这是一个很好的技巧）。

如果你想将软件包从上述格式之一转换，可以使用 `alien` (http://freshmeat.net/projects/alien)。虽然 alien 不被认为足够稳定以用于系统包，但它可以作为在你的 Fedora 系统上尝试某些软件包的良好工具。

## 从源码编译并安装

如果你需要的包没有二进制版本，或者你只是想根据需要定制包，你始终可以从源代码安装该包。开始之前，你可以从 Fedora 软件仓库获取任何包的源码（SRPM）版本（详情请参见附录 A）。你可以修改源码并重新构建以适应你的需求。

没有提供 RPM 格式的软件包通常以 tarball（通过 `tar` 工具将一组文件分组成单个格式的文件）的形式存在，并经过了压缩（通常通过 `gzip` 工具）。虽然从源码归档文件安装应用程序的具体指令各异，但许多 .bz2、.tar.bz2、.tgz、.gz 和 .tar 格式的包都遵循基本步骤。

> 提示：在从源码安装之前，你需要安装各种软件开发包。如果你有磁盘空间，我建议你安装 Fedora 安装过程中推荐的所有软件开发包。

以下是 C 语言软件开发工具的最小列表：

- gcc — 包含 gcc（GNU C 编译器）编译器。
- make — 包含用于从 Makefile 构建二进制文件的 `make` 命令。
- glibc — 包含重要的共享库、C 库和标准数学库。
- glibc-devel — 包含用于创建可执行文件的标准头文件。
- kernel-devel — 包含 Linux 内核源码，重建内核时需要。
- rpm-build — 包含用于从源码构建 RPM 包的 `rpmbuild` 工具。
- libc — 基于 libc 5 编写的程序所需的库，旧版应用程序可以在 glibc (libc 6) 系统上运行。如果你使用 C++，有许多包可以获取，特别是 libstdc++ 和 libstdc++-devel。

## 安装 SRPM 格式的软件

要从 Fedora 源码目录安装源码包，请执行以下操作：

1. 参考附录 A获取获取 Fedora 源码的信息。
2. 将你需要的包下载到当前目录。
3. 使用以下命令安装源码包：

```
# rpm -iv packagename*.rpm
```

（将 packagename 替换为你安装的包名。）从 Fedora 10 开始，源码默认安装在主目录下的 (/usr/src/rpmsbuild/SOURCES) 目录。Spec 文件被复制到 rpmbuild/SPECS。在 Fedora 10 之前，默认路径是 /usr/src/redhat/SOURCES 和 /usr/src/redhat/SPECS。

4. 如下所示进入 SPECS 目录：

```
# cd ~/rpmbuild/SPECS
```

5. 如下所示解压源码（注意你可能需要安装 rpm-build 包）：

```
# rpmbuild -bp packagename*.spec
```

6. 包的源码被安装到 rpmbuild/BUILD/package，其中 package 是软件包的。

7. 你现在可以对 rpmbuild/BUILD/package 中的文件进行更改。查看 README、Makefile 以及其他文件。`rebuild` 选项用于构建。

