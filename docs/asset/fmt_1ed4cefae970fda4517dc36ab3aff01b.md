
你会看到许多信息，因为 CVS 在你的系统上从仓库下载 gnome-xml 模块中每个文件的最新版本，在当前目录下创建 `gnome-xml` 目录并将文件放入该目录。你只需输入 `cd gnome-xml` 切换目录并访问这些文件。

如果你已经检出一个工作目录，可以使用 CVS `update` 命令更新你的仓库。CVS 更新本质上是将仓库中的更改与你在工作目录中可能做的任何更改进行合并。如果存在冲突，你需要手动解决问题。

在你对这些文件进行工作后，可以使用 CVS `commit` 命令将你的更改整合到仓库。你可以提交特定的文件，也可以提交整个模块。

## 第 23 章：Linux 下的软件开发

当你不再需要某个模块的工作副本时，使用 `cvs release` 命令来指示你不再需要该模块。要删除文件，请使用 `cvs release` 命令；`-d` 标志表示你想要删除文件。

当你与 CVS 仓库一起工作时，在这些仓库之外输入 `cvs log`。

这就是 CVS 的工作原理。要了解更多关于 CVS 的信息，请参考以下资源：

- 输入关于 CVS 的信息
- 输入 `cd usr/src/doc/cvs/` 切换 CVS 目录。在该目录下，有一个名为 FAQ（常见问题解答）的文件以及若干几个关于 CVS 的 PostScript 文件。FAQ 文件可能有点过时，但你仍然可以将其作为有关 CVS 的信息来源。
- 访问以下网站之一阅读关于 CVS 的最新在线信息：
  - www.cvhome.org/
  - www.gnu.org/software/cvs/
  - www.gnu.org/software/cvs/manual/

## Linux 编程主题

在 Linux 下开发软件与在任何 UNIX 系统下开发软件非常相似。大多数 C 和 UNIX 编程问题都是通用的，适用于所有 UNIX 系统。如果你在为 Linux 开发软件，会有几个你想要了解的主题。

本节涵盖了最重要的主题：Linux 中的可执行文件和链接格式 `ELF` 二进制文件。另一个——在应用程序中使用动态链接——与 ELF 相关。我将描述你如何利用动态链接，以及你如何在 Linux 中创建动态链接库。

## 理解可执行文件和链接格式

如果你在 UNIX 中编写过程序，你可能知道当编译并链接程序时，默认的可执行文件命名为 `a.out`。你可能没有意识到，`a.out` 关联着一种文件格式。操作系统必须知道这种文件格式以便加载和运行可执行文件。在早期，Linux 使用 `a.out` 作为其二进制文件。

尽管 `a.out` 格式已经完成了它的使命，但它有两个缺点：

- 共享库很难创建。
- 动态加载库非常繁琐。

使用共享库是理想的，因为共享库允许任何可执行程序共享同一块代码。此外，模块的动态加载变得越来越流行，因为它允许应用程序仅在需要时加载代码块，从而减少程序的内存需求。

## 第五部分：编程 Linux

UNIX 系统实验室 `USL` 开发了可执行文件和链接格式或 `ELF`，这是一种新格式用于 System V Release 4 `SVR4`。`ELF` 格式比 `a.out` 格式更灵活。特别是 `ELF` 在 Linux 中优于旧的 `a.out` 格式：

- `ELF` 格式的共享库创建非常简单。你使用 `gcc -fPIC -c` 编译所有内容，并使用类似 `gcc -shared -Wl,-soname,libXXX.so -o libXXX.so.1.0 *` 的命令将其链接。
- 动态加载（程序在运行时加载代码）更容易。通过动态加载，你可以设计一个具有扩展性的应用程序，使用户以共享库的形式添加新代码。

由于 `ELF` 灵活性的增加，Linux 开发者（特别是 GCC 开发者）决定使用 `ELF` 作为 Linux 的标准二进制格式。默认情况下，新编译器——`gcc 2.7` 版本及更高版本——生成 `ELF` 二进制文件。注意，`gcc` 使用 `a.out` 作为可执行文件的默认名称（如果你不使用 `-o` 指定输出，则会使用它）。尽管可执行文件可能被命名为 `a.out`，但二进制格式是 `ELF`，而不是旧的 `a.out`。如果你想检查可执行文件的二进制格式，使用 `file` 命令。下面的示例显示了如何检查 `/bin/ls`（`ls` 命令的可执行文件）类型：

```
/bin/ls: ELF 32-bit LSB executable, Intel 86, GNU/Linux 2.5, dynamically linked (uses shared libraries), stripped
```

另一方面，`file` 命令对旧的 `a.out` 格式报告如下（可执行文件的默认名称仍为 `a.out`，但格式是 `ELF`）：

```
a.out: ELF 32-bit LSB executable,
```

## 在 Linux 中使用共享库

大多数程序使用共享库。至少，大多数 C 程序使用 `libc.so`，其中 `X` 是版本号。当程序使用一个或多个共享库时，你需要程序的可执行文件以及所有共享库来运行程序。换句话说，如果系统没有提供所有的共享库，你的程序将无法运行。如果你需要一个应用程序，你需要确保所有必要的共享库随你的软件一起分发。

## 检查程序使用的共享库

使用 `ldd` 工具确定可执行文件需要哪些共享库。以下是 `ldd` 对使用 `ELF` 二进制格式的典型程序的报告：

```
linux-gate.so.1 -> (0x0021a00)
libc.so.6 -> /lib/libc.6 (0x008bf00)
/lib/ld-linux.so.2 (0x008a2000)
```

对于像 `gimp` 这样复杂的程序，`ldd` 显示共享库：

```
ldd /usr/bin/gimp
linux-gate.so.1 -> (0x00be800)
libgimpwidgets-2.0.so.0 -> /lib/libgimpwidgets-2.0.so.0 (0x06ae000)
libgimpcolor-2.0.so.0 -> /lib/libgimpcolor-2.0.so.0 (0x06ae000)
/lib/ld-linux.so.2 (0x008a2000)
linux-gate.so.1 -> (0x00be800)
libgimpwidgets-2.0.so.0 -> /lib/libgimpwidgets-2.0.so.0 (0x06ae000)
libgimpcolor-2.0.so.0 -> /lib/libgimpcolor-2.0.so.0 (0x06ae000)
/lib/ld-linux.so.2 (0x008a2000)
linux-gate.so.1 -> (0x00be800)
libgimpwidgets-2.0.so.0 -> /lib/libgimpwidgets-2.0.so.0 (0x06ae000)
libgimpcolor-2.0.so.0 -> /lib/libgimpcolor-2.0.so.0 (0x06ae000)
/lib/ld-linux.so.2 (0x008a2000)
```

## 第 23 章：Linux 下软件开发
