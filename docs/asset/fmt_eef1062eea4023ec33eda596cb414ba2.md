
- 控制你安装的版本。发行版并不总是保持所有软件包的最新版本，特别是软件包的插件。
- 更好地理解包是如何工作的。

## 16.2 解压 C 源码包

软件包的源码通常以 `tar.gz`、`tar.bz` 或 `tar.xz` 文件的形式出现，你应该按照第 2.18 节描述的方法解压文件。

在解压之前，请使用 `tar tf` 或 `tar zvf` 验证压缩包的内容，因为某些软件包不会在你提取压缩包的目录中创建自己的子目录。

如下所示输出意味着该包可能可以解压：

```
package-1.23/Makefile.in
package-1.23/README
package-1.23/main.c
package-1.23/bar.c
-- snip --
```

然而，你可能会发现并不是所有文件都在同一个目录中（例如上一个示例中的 `package-1.23`）：

```
Makefile
README
main.c
-- snip --
```

解压这样的压缩包可能会让你的当前目录变得一团糟。为了避免这种情况，请在解压压缩包内容之前创建一个新目录并进入该目录。

最后，要小心包含类似如下绝对路径文件的软件包：

```
/etc/passwd
/etc/inetd.conf
```

你不会遇到此类内容，但如果你真的遇到了，请从系统中删除该压缩包。它可能包含木洛马或其他恶意代码。

一旦你解压了源码压缩包的内容并面前有一了一堆文件，请尝试对该软件包有一个初步了解。特别要寻找名为 `README` 和 `INSTALL` 的文件。始终先查看任何 `README` 文件，因为它们包含了软件包的描述、简短手册、安装提示和有用信息。许多软件包还附带 `INSTALL` 文件，其中包含了如何编译和安装软件包的说明。请特别关注编译选项和定义。

除了 `README` 和 `INSTALL` 文件外，你还会发现其他软件包文件，它们大致分为三类：

- 归属于 make 系统的文件，例如 `Makefile`、`Makefile.in`、`configure` 和 `CMakeLists.txt`。一些旧的软件包附带有一个你可能需要修改的 `Makefile`。

### 使用独立的构建目录

如果你想尝试这些选项中的某些项，可以创建独立的构建目录。要这样做，可以在系统中的任何位置创建一个新目录，然后从该目录运行原始包源码目录中的 `configure` 脚本。你会发现 `configure` 在你的新构建目录中创建一个符号链接场（symbolic link farm），其中所有的链接都指向原始包目录中的源码树。（某些开发者更倾向于以这种方式进行打包，因为原始源码树永远不会被修改。如果你想使用同一个源包为多个平台或配置选项集进行构建，这同样有用。）

## 16.3.4 环境变量

你可以通过环境变量来影响 `configure`。`configure` 脚本会设置 make 变量。最重要的是 `CPPFLAGS`、`CFLAGS` 和 `LDFLAGS`。注意，`configure` 对环境变量可能非常挑剔。例如，对于头文件目录，你应该使用 `CPPFLAGS` 而不是 `CFLAGS`，因为 `configure` 往往独立于编译器运行预处理器。

在 `bash` 中，将环境变量传递给 `configure` 最简单的方法是在命令行中将变量赋值放在 `./configure` 之前。例如，为预处理器定义一个 `DEBUG` 宏，使用此命令：

```
$ CPPFLAGS=-DEBUG ./configure
```

你也可以将变量作为选项传递给 `configure`；例如：

```
$ ./configure CPPFLAGS=-DEBUG
```

当 `configure` 不知道去哪里查找第三方包含文件和库时，环境变量 特别有用。例如，要让预处理器在 `include_dir` 中搜索，运行此命令：

```
$ CPPFLAGS=-include_dir ./configure
```

如第 15.2.6 节所示，要让链接器在 `lib_dir` 中链接，使用此命令：

```
$ LDFLAGS=-Llib_dir ./configure
```

如果 `lib_dir` 共享库（参见第 15.1.3 节），之前的命令不会设置运行时动态链接器路径。在这种情况下，除了 `-L` 之外，还要使用 `-rpath` 链接选项：

```
$ LDFLAGS="-Llib_dir -rpath=lib_dir" ./configure
```

设置变量时要小心。一个小疏忽就会导致编译器出错并引起 `configure` 失败。例如，假设你忘记了 `-I`，如这里所示：

```
$ CPPFLAGS=-Iinclude_dir ./configure
```

这会产生如下错误：

```
configure: error: C compiler cannot create executables
See 'config.log' for more details
```

深入由该失败尝试生成的 `config.log` 可以得到如下：

```
configure:5037: checking whether the C compiler works
configure:5059: gcc Include_dir conftest.c >&5
gcc: error: Include_dir: No such file or directory
configure:5063: $ = 1
configure:5101: result: no
```

## 16.3.5 Autoconf 目标

一旦 `configure` 正常工作，你会发现它生成的 `Makefile` 除了标准的 `all` 和 `install` 之外，还有许多实用的目标：

- `make clean`: 正如第 15 节所述，这会移除所有对象文件、可执行文件和库。
- `make distclean`: 这与 `make clean` 类似，但它会移除所有自动生成的文件，包括 `Makefile`、`config.h`、`config.log` 等。其核心思想是运行 `make distclean` 后，源码树应该看起来像新解压的发行版。
- `make check`: 软件包带有一系列测试，以验证编译后的程序是否正常工作；`make` 命令会运行这些测试。
- `make install-strip`: 这类似于 `make`，但在安装时会剥离可执行文件和库中的符号表和其他调试信息。剥离后的二进制文件需要的空间少得多。

## 16.3.6 Autoconf 日志

如果在 `configure` 过程中出现问题且原因并不明显，你可以检查 `config.log` 来找到问题。遗憾的是，`config.log` 通常是一个巨大的文件，这可能导致难以定位问题的准确根源。

这种情况的通用方法是到 `config.log` 的末尾（例如通过在 `less` 中输入大写的 `G`），然后向上翻页直到看到问题。然而，末尾有很多内容，因为 `configure` 会导出它的整个环境，包括输出变量、缓存变量和其他定义。因此，与其到末尾再向上翻，不如到末尾并向后搜索字符串，例如 `more details` 或失败的 `configure` 输出结尾附近的其他文本片段。（记住，你可以在 `less` 中使用 `?` 命令启动反向搜索。）错误很有可能就在你的搜索结果附近。

## 16.3. pkg-config

系统中存在大量的第三方库意味着将它们全部保留在一个公共位置可能会变得混乱。然而，为每个包使用单独的前缀（prefix）进行安装会导致构建需要这些第三方库的包时出现困难。例如，如果你想编译 OpenSSH，你需要 OpenSSL 库。你如何告诉 OpenSSH 配置过程 OpenSSL 库的位置以及哪些库是必需的呢？

许多库使用 `pkg-config` 程序不仅是为了通告其文件和库的位置，还为了指定你编译和链接程序所需的精确标志（flags）。其语法如下：

```
$ pkg-config options package1 package2 ...
```

例如，要找到某个流行的压缩库所需的库，你可以运行此命令：

```
$ pkg-config --libs zlib
```

输出应该类似这样：

```
-lz
```

要查看 `pkg-config` 知晓的所有库，包括每个库的简要描述，运行此命令：

```
$ pkg-config --list-all
```

### pkg-config 如何工作

如果你查看其背后，你会发现 `pkg-config` 通过读取以 `.pc` 结尾的配置文件来查找信息。例如，这里是 OpenSSL 库的 `openssl.pc`，如 Ubuntu 系统所示（位于 `/usr/lib/x86_64-linux-gnu/pkgconfig/`）：
