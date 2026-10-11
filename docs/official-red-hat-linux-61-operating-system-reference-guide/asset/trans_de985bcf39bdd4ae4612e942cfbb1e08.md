

由于升级实际上是卸载和安装的组合，因此你可能会遇到这些模式下的任何错误，另外还有：如果 RPM 认为你试图升级到一个*旧*版本的包，你会看到：

```
# rpm -Uvh foo-1.0-1.i386.rpm
foo    package foo-2.0-1 (which is newer) is already installed
error: foo-1.0-1.i386.rpm cannot be installed
#
```

若要使 RPM 仍然执行“升级”，请在命令行中使用 `--oldpackage`：

```
# rpm -Uvh --oldpackage foo-1.0-1.i386.rpm
foo    ########################################
#
```

### 6.2.4 刷新

刷新包与升级类似：

```
# rpm -Fvh foo-1.2-1.i386.rpm
foo    ########################################
#
```

RPM 的刷新选项会将命令行上指定包的版本与系统中已安装包的版本进行比对。当 RPM 的刷新选项处理已安装包的新版本时，它会将其升级到该新版本。然而，如果系统中不存在同名已安装的包，RPM 的刷新选项将不会安装该包。这与 RPM 的升级选项不同，因为无论旧版本的包是否已安装，升级操作都会安装包。

RPM 的刷新选项适用于单个包或一组包。如果你刚刚下载了大量不同的包，并且只想升级那些已安装在系统上的包，这将特别有用。使用刷新选项意味着你无需在下载的包中挑选并删除不需要的包，然后才使用 RPM。

在这种情况下，你只需发出以下命令：

```
# rpm -Fvh *.rpm
```

RPM 将自动仅升级那些已安装的包。

### 6.2.5 查询

查询已安装包数据库是通过 `rpm -q` 完成的。一个简单的用法是 `rpm -q foo`，它将打印已安装包 foo 的包名称、版本和发行编号：

```
# rpm -q foo
foo-2.0-1
#
```

除了指定包名称，你还可以使用以下选项与 `-q` 配合使用来指定要查询的包。这些称为*包规格选项*。

- `-a` 查询所有当前已安装的包。
- `-f <file>` 将查询拥有 `<file>` 的包。
- `-p <packagefile>` 查询包 `<packagefile>`。

有多种方式可以指定要显示关于已查询包的哪些信息。以下选项用于选择你要搜索的信息类型。这些称为*信息选择选项*。

- `-i` 显示包信息，如名称、描述、发行版本、大小、构建日期、安装日期、供应商及其他杂项信息。
- `-l` 显示该包“拥有”的文件列表。
- `-s` 显示包中所有文件的状态。
- `-c` 显示标记为文档的文件列表（man 手册页、info 页、README 等）。
- `-c` 显示标记为配置文件的文件列表。这些是安装后你需要修改以将包适应于你的系统的文件（sendmail.cf、passwd、inittab 等）。

对于显示文件列表的选项，你可以在命令行中添加 `-v` 以熟悉的 `ls -l` 格式获取列表。

### 6.2.6 验证

验证包是将包安装的文件信息与原始包的相同信息进行对比。除了其他事项，验证会对比每个文件的大小、MD5 校验和、权限、类型、所有者和组。

命令 `rpm -V` 验证一个包。你可以使用查询中列出的任何*包选择选项*来指定要验证的包。一个简单的用法是 `rpm -V foo`，它验证 foo 包中的所有文件是否与其最初安装时相同。例如：

- 验证包含特定文件的包：
  ```
  rpm -Vf /bin/vi
  ```
- 验证所有已安装的包：
  ```
  rpm -Va
  ```
- 根据 RPM 包文件验证已安装的包：
  ```
  rpm -Vp foo-1.0-1.i386.rpm
  ```

如果你怀疑你的 RPM 数据库已损坏，这可能会有用。

如果一切验证正常，将没有输出。如果有任何差异，它们将被显示。输出的格式是一个 8 个字符的字符串，一个表示配置文件的可能的“c”，然后是文件名。8 个字符中的每一个表示该文件的一个属性与记录在 RPM 数据库中该属性值之间的比较结果。单个“.”（句点）意味着测试通过。以下字符表示某些测试失败：

- `5` -- MD5 校验和
- `S` -- 文件大小
- `L` -- 符号链接
- `T` -- 文件修改时间
- `D` -- 设备
- `U` -- 用户
- `G` -- 组
- `M` -- 模式（包括权限和文件类型）

如果你看到任何输出，请根据你的最佳判断决定是应删除或重新安装包，或以其他方式修复问题。

## 6.3 用 RPM 给朋友留下深刻印象

RPM 是一个非常有用的工具，既用于管理系统，也用于诊断和修复问题。理解所有选项的最佳方法是查看一些示例。

- 假设你意外删除了一些文件，但不确定删除了什么。如果你想验证整个系统并查看可能缺失了什么，你会输入：

```bash
rpm -Va
```

如果某些文件缺失，或者看起来已损坏，你应该重新安装包或卸载然后重新安装包。

- 假设你遇到了一个你不认识的文件。要找出哪个包拥有它，你会输入：

```bash
rpm -qf /usr/X11R6/bin/xjewel
```

输出看起来像这样：

```
xjewel-1.6-1
```

- 我们可以将上述两个示例结合到以下场景中。假设你在使用 /usr/bin/paste 时遇到问题。你想验证拥有该程序的包，但你不知道那是哪个包。只需输入：

```
rpm -Vf /usr/bin/paste
```

相应的包将被验证。

- 想了解关于特定程序的更多信息？你可以通过输入以下内容来找到随“拥有”该程序的包（在本例中是 ispell）一起提供的文档：

```
rpm -qdf /usr/bin/ispell
```

输出将是：

```
/usr/man/man4/ispell.4
/usr/man/man4/english.4
/usr/man/man1/unsg.1
/usr/man/man1/tryaffix.1
/usr/man/man1/sq.1
/usr/man/man1/munchlist.1
/usr/man/man1/ispell.1
/usr/man/man1/findaffix.1
/usr/man/man1/builddash.1
/usr/info/ispell.info.gz
/usr/doc/ispell-3.1.18-1/README
```

- 假设你找到一个新的 koules RPM，但不知道它是什么。要了解一些关于它的信息，输入：

```
rpm -qip koules-1.2-2.i386.rpm
```

输出将是：

```
Name : koules               Distribution: Red Hat Linux Colgate
Version : 1.2               Vendor: Red Hat Software
Release : 2                 Build Date: Mon Sep 02 11:59:12 1996
Install date: (none)        Build Host: porky.redhat.com
Group : Games               Source RPM: koules-1.2-2.src.rpm
Size : 614939
Summary : SVGA/ib action game; multiplayer, network
```

Description :
This arcade-style game is novel in conception and excellent in execution. No shooting, no blood, no guts, no gore. The play is simple, but you still must develop skill to play. This version uses SVGAlib to run on a graphics console.

- 现在你想查看 koules RPM 安装哪些文件。你会输入：

```
rpm -qlp koules-1.2-2.i386.rpm
```

输出是：

```
/usr/man/man6/koules.6
/usr/lib/games/kouleslib/start.raw
/usr/lib/games/kouleslib/end.raw
/usr/lib/games/kouleslib/destroy2.raw
/usr/lib/games/kouleslib/destroy1.raw
/usr/lib/games/kouleslib/creator2.raw
/usr/lib/games/kouleslib/creator1.raw
/usr/lib/games/kouleslib/colize.raw
/usr/lib/games/kouleslib
/usr/games/koules
```

这些只是几个例子。当你使用系统时，你会发现 RPM 有很多其他用途。

## 6.4 其他 RPM 资源

有关 RPM 的更多信息，请查看 man 手册页、帮助屏幕（`rpm --help`）以及 [http://www.rpm.org/](http://www.rpm.org/) 上可用的 RPM 文档。

还有一本 RPM 书可用。它名为 *Maximum RPM*，可从 Red Hat、当地书店及在线书店购得。它包含大量关于 RPM 的信息，既适用于最终用户，也适用于包构建者。

