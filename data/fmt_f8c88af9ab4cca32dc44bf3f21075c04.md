
```
# rpm -bb cdplayer-1.0.spec
* Package: cdplayer
Executing: %prep
...
+ exit 0
Executing: %build
...
+ exit 0
Executing: %install
...
+ exit 0
Executing: special doc
+ exit 0
Binary Packaging: cdplayer-1.0-1
Finding dependencies...
Requires (2): libc.so.5 libcurl.so.2.0
/usr/doc/cdplayer-1.0-1
/usr/doc/cdplayer-1.0-1/README
/usr/local/bin/cdp
/usr/local/bin/cdplayer
/usr/local/man/man1/cdp.1
93 blocks
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/cdplayer-1.0-1.i386.rpm
+ umask 022
+ echo Executing: '%clean'
Executing: '%clean'
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ exit 0
#
```

在执行了 `%prep`、`%build` 和 `%install` 部分并处理了任何特殊文档文件之后，RPM 创建二进制包文件。在示例输出中，我们看到首先 RPM 执行自动依赖检查。它通过确定包中包含的可执行程序需要哪些共享库来做到这一点。接下来，RPM 实际上将文件归档为要打包的文件，可选地对包文件进行签名，并输出成品。

RPM 输出的最后一部分看起来像 spec 文件中某个部分正在被执行。在我们的例子中，没有 `%clean` 部分。然而，如果存在，RPM 将执行该部分中的任何命令。在缺少 `%clean` 部分的情况下，RPM 只是发出常规的 `cd` 命令并正常退出。

### 12.1.5. `rpm -ba`: 执行 `%prep`, `%build`, `%install`, 打包 (bin, src)

`-ba` 选项指示 RPM 执行构建包的所有阶段。通过这一条命令，RPM 执行以下操作：

1. 解包原始源代码。
2. 应用补丁（如果需要）。
3. 构建软件。
4. 安装软件。
5. 创建二进制包文件。
6. 创建源代码包文件。

对于一条命令来说，这是相当繁重的工作！以下是其实际操作示例：

```
# rpm -ba cdplayer-1.0.spec
* Package: cdplayer
Executing: %prep
...
+ exit 0
Executing: %build
...
+ exit 0
Executing: %install
+ exit 0
Executing: special doc
...
+ exit 0
Binary Packaging: cdplayer-1.0-1
...
Executing: %clean
...
+ exit 0
Source Packaging: cdplayer-1.0-1
cdplayer-1.0.spec
cdplayer-1.0.tgz
80 blocks
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/cdplayer-1.0-1.src.rpm
#
```

与之前的示例一样，RPM 执行 `%prep`、`%build` 和 `%install` 部分，处理任何特殊文档文件，创建二进制包文件，并自我清理。

构建过程的最后一步是创建源代码包文件。如输出所示，它由 spec 文件和原始源代码组成。源代码包可选地包含一个或多个补丁文件，尽管在我们的例子中，`cdplayer` 不需要任何补丁。

在使用 `-ba` 选项的构建结束时，软件已成功构建并打包为二进制和源代码形式。但我们还可以使用几个其他构建时选项。其中之一是 `-bl` 选项。

### 12.1.6. `rpm -bl`: 检查文件列表

还有最后一个选项可以与 `rpm -b` 一起使用，但与其他选项不同，这些选项指示构建过程在哪个阶段停止，而这个选项对指定 spec 文件中的 `%files` 列表执行各种检查。当 `-l` 添加到 `rpm -b` 时，该命令执行以下操作：

- 展开 spec 文件的 `%files` 列表，并检查每个列出的文件是否实际存在。
- 通过检查每个列出的可执行文件来确定软件需要哪些共享库。
- 确定包提供了哪些共享库。

为什么有必要进行所有这些检查？什么时候会有用？请记住，`%files` 列表必须手动生成。通过使用 `-bl` 选项，创建 `%files` 列表所需的步骤如下：

- 编写 `%files` 列表
- 使用 `-bl` 选项检查 `%files` 列表
- 对 `%files` 列表进行任何必要的更改

可能需要多次迭代这些步骤，但最终列表检查会通过。使用 `-bl` 选项检查 `%files` 列表显然比开始长达两小时的包构建，结果在最后才发现列表中包含拼写错误的文件名要好得多。

以下是 `-bl` 选项的示例操作：

```
# rpm -bl cdp-1.0.spec
Package: cdp
File List Check: cdp-1.0-1
Finding dependencies ...
Requires (2): libc.so.5 libncurses.so.2.0
#
```

从输出中很难确切看出 RPM 在做什么，但如果我们加上 `-vv`，就可以获得更多一些信息：

```
# rpm -bl -vv cdp-1.0.spec
D: Switched to BASE package
D: Source(0) = sunsite.unc.edu:/pub/Linux/apps/sound/cds/cdp-1.0.tgz
D: Switching to part: 12
D: fileFile =
D: Switched to package: (null)
D: Switching to part: 2
D: fileFile =
D: Switching to part: 3
D: fileFile =
D: Switching to part: 4
D: fileFile =
D: Switching to part: 10
D: fileFile =
D: Switched to package: (null)
* Package: cdp
File List Check: cdp-1.0-1
D: ADDING: /usr/doc/cdp-1.0-1
D: ADDING: /usr/doc/cdp-1.0-1/README
D: ADDING: /usr/local/bin/cdp
D: ADDING: /usr/local/bin/cdplay
D: ADDING: /usr/local/man/man1/cdp.1
D: md5(/usr/doc/cdp-1.0-1/README) = 2c149b2f1a4ad e5418131a19b242601c
D: md5(/usr/local/bin/cdp) = 0fa2a72f8121c75f0d1c52f456798d6
D: md5(/usr/local/bin/cdplay) = da1d8cd98f00b204e9800998ecf8427e
D: md5(/usr/local/man/man1/cdp.1) = b32cc867ae50e2bfdad67b00004adfa
Finding dependencies ...
D: Adding require: libncurses.so.2.0
D: Adding require: libc.so.5
Requires (2): libc.so.5 libncurses.so.2.0
#
```

### 12.1.7. `--short-circuit`：强制构建从特定阶段开始

尽管听起来很危险，但 `--short-circuit` 选项可以是你的好朋友。此选项用于软件包的初始开发阶段。在本章前面，我们探讨了在 RPM 构建过程的不同阶段停止构建。使用 `--short-circuit`，我们可以从不同的阶段开始构建过程。

`--short-circuit` 的一个有用场景是你试图让软件正确构建时。想想那样的情景——你在对源代码进行修改（hacking away at the sources），尝试构建，遇到错误，然后再修改代码以修复该错误。如果没有 `--short-circuit`，你必须执行以下步骤：

1. 对源代码进行修改。
2. 使用 `tar` 创建一个新的源代码归档。
3. 使用类似 `rpm -bc` 的命令开始构建。
4. 发现另一个 bug。
5. 回到步骤 1。

相当麻烦！由于 RPM 的构建过程设计为从原始 tar 文件中的源代码开始，除非你的修改进入了该 tar 文件，否则它们不会在下次构建中使用。（如第 10 章所述，如果原始源代码需要修改，修改应作为单独的一组补丁保留。然而，在开发期间，每次对原始源代码进行修改时都不生成补丁是更有意义的。）
