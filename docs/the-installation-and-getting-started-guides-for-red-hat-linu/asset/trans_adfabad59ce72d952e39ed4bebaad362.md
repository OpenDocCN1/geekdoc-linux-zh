

对于显示文件列表的那些选项，你可以在命令行中添加 -v 来以熟悉的 ls -l 格式获取列表。

## 验证

验证一个包会将从该包安装的文件信息与原始包中的相同信息进行比较。在其他方面，验证会比较每个文件的大小、MD5 校验和、权限、类型、所有者和组。rpm -V 用于验证一个包。你可以使用查询时列出的任何包选择选项来指定你希望验证的包。简单用法是 rpm -V foo，它会验证 foo 包中的所有文件是否与最初安装时相同。例如：

- 要验证包含特定文件的包
  `rpm -Vf /bin/vi`
- 要验证所有已安装的包
  `rpm -Va`
- 要将已安装的包与 RPM 包文件进行验证：
  `rpm -Vp foo-1.0-1.i386.rpm`

如果怀疑你的 RPM 数据库已损坏，这会很有用。

如果一切验证正常则不会有输出。如果存在任何差异，它们将被显示。输出格式为 8 个字符的字符串，可能的 "c" 表示配置文件，然后是文件名。8 个字符中的每一个都表示文件的某个属性与 RPM 数据库中记录的该属性值比较的结果。单个 "."（句点）表示测试通过。以下字符表示某些测试失败：

- 5
  MD5 校验和
- S
  文件大小
- L
  符号链接
- T
  文件修改时间
- D
  设备
- U
  用户
- G
  组
- M
  模式（包括权限和文件类型）

如果看到任何输出，请自行判断是否应删除或重新安装该包，或以某种方式修复问题。

## 用 RPM 给朋友留下深刻印象

RPM 是一款非常有用的工具，既可用于管理系统，也可用于诊断和修复问题。理解所有选项的最佳方式是查看一些示例。

- 假设你不小心删除了一些文件，但不确定删除了什么。如果你想验证整个系统并查看可能丢失的内容，你会输入：

```
rpm -Va
```

如果某些文件丢失或似乎已损坏，你可能需要重新安装该包，或先卸载然后重新安装该包。

- 假设你遇到一个不认识的文件。要找出哪个包拥有它，你会输入：

```
rpm -qf /usr/X11R6/bin/xjewel
```

输出看起来像：

```
xjewel-1.6-1
```

- 我们可以将上面两个示例结合在以下场景中。假设 `/usr/bin/paste` 出现问题。你想验证拥有该程序的包，但不知道是哪一个包。只需输入：
  ```
  rpm -Vf /usr/bin/paste
  ```
  适当的包将被验证。

- 如果你正在使用某个程序并想了解更多关于它的信息，你可以输入以下命令来查找“拥有”该程序的包附带了哪些文档（本例中为 ispell）：
  ```
  rpm -qdf /usr/bin/ispell
  ```
  输出将为：
  ```
  /usr/man/man4/ispell.4
  /usr/man/man4/english.4
  /usr/man/man1/unqsq.1
  /usr/man/man1/tryaffix.1
  /usr/man/man1/sq.1
  /usr/man/man1/munchlist.1
  /usr/man/man1/ispell.1
  /usr/man/man1/findaffix.1
  /usr/man/man1/buildhash.1
  /usr/info/ispell.info.gz
  /usr/doc/ispell-3.1.18-1/README
  ```

- 你找到一个新 koules RPM，但不知道它是什么。要了解有关它的一些信息，请输入：
  ```
  rpm -qip koules-1.2-2.i386.rpm.
  ```

输出将为：

```
Name         : koules Distribution: Red Hat Linux Colgate
Version      : 1.2        Vendor: Red Hat Software
Release      : 2          Build Date: Mon Sep 02 11:59:12 1996
Install date : (none)     Build Host: porky.redhat.com
Group        : Games      Source RPM: koules-1.2-2.src.rpm
Size         : 614939
Summary      : SVGAlib action game; multiplayer, network
Description  :
This arcade-style game is novel in conception and excellent
in execution. No shooting, no blood, no guts, no gore. The
play is simple, but you still must develop skill to play.
This version uses SVGAlib to run on a graphics console.
```

- 现在你想查看 koules RPM 安装了哪些文件。你会输入：

```
rpm -qlp koules-1.2-2.i386.rpm
```

输出为：

```
usr/man/man6/koules.6
/usr/lib/games/kouleslib/start.raw
/usr/lib/games/kouleslib/end.raw/
/usr/lib/games/kouleslib/destroy2.raw
/usr/lib/games/kouleslib/destroy1.raw
/usr/lib/games/kouleslib/creator2.raw
/usr/lib/games/kouleslib/creator1.raw
/usr/lib/games/kouleslib/colize.raw
/usr/lib/games/kouleslib
/usr/games/koules
```

这些只是几个示例。随着你使用该系统，你会发现 RPM 有更多用途。

