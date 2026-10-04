

## 7.2 包

如果过程未在任何已知的包中定义，Tcl 解释器将报告错误。如果可以通过加载包来获取该命令，解释器将执行加载操作，并再次评估导致错误的命令行（推测会成功）。

Tcl 解释器将搜索全局变量 `auto_path` 列出的目录中的索引文件。`auto_path` 变量定义在 `init.tcl` 脚本中，该脚本在启动 Tcl 或 Tk 解释器时被加载。

本节将讨论如何生成索引文件，以及如何将你的包目录添加到待搜索的索引列表中。

请注意，当你为一个在命名空间（namespace）中定义过程的包创建索引时，只有导出命令中列出的过程名称会被索引。

## 7.2.2 内部细节：用于包的文件和变量

这些文件和全局变量用于查找和加载包。

`auto_path` 全局变量 `auto_path` 变量包含一个应该从中搜索包索引文件的目录列表。

`auto_path` 变量定义在 `init.tcl` 脚本中，该脚本在启动 `tclsh` 解释器时加载。

在 Unix 系统上，`init.tcl` 可能位于 `/usr/local/lib/tcl18.0` 或某些变体中，取决于你的安装以及 `tclsh` 的修订版本。在 Windows 系统上，`init.tcl` 存储在 `\Program Files\Tcl\lib\tcl18.0` 中，或者取决于你的 Tcl 版本以及你安装 Tcl 解释器的基础目录。

## 第 7 章：命名空间与包

auto_index 全局数组 `auto_index` 数组使用 `pkgIndex.tcl` 文件中定义的过程名称进行索引。与每个索引关联的数据是加载定义该过程的包的命令。

该命令类似于：

```
source /usr/myLibs/package.tcl
```

这些文件包含了该目录下包所定义的过程列表。`pkgIndex.tcl` 文件通过 `pkg_mkIndex` 命令创建。

### pkgIndex.tcl 文件

## 7.2.3 包命令

`package` 命令有多个子命令。这些是你将脚本转换为包的命令。

`pkg_mkIndex` 命令创建一个包索引文件。它在评估脚本时不会被执行，但在安装或测试包时会被求执行。

`pkg_mkIndex` 命令扫描由模式识别的文件中的 `package provide` 命令，并使用该命令中的信息和过程定义，在当前目录下创建一个名为 `pkgIndex.tcl` 的文件。

语法：pkg_mkIndex dir pattern ?pattern?

pkg_mkIndex 创建可用包的索引。当 `package require` 在确定要从何处查找包时，会搜索此索引。

- dir: 正在索引的包所处的目录。

- pattern ?patterns? 全局风格的模式，用于定义将要索引的文件。

## 7.2 包

当 `pkg_mkIndex` 命令完成对匹配模式参数的文件的评估后，它会在 `dir` 目录下创建一个名为 `pkgIndex.tcl` 的文件。`pkgIndex.tcl` 文件包含：

- 匹配模式的文件中定义的包名称。
- 这些包的版本级别。
- 这些包中定义的过程名称。
- 用于加载该包的命令名称。

`pkg_mkIndex` 命令将覆盖任何 `pkgIndex.tcl` 文件。如果你在单个目录中开发多个包，那么每次更新索引时，都需要输入每个文件的名称。在这种情况下，创建一个列出所有文件的双行脚本可能会简单：

```
#!/usr/local/bin/tcl
pkg_mkIndex [pwd] file1.tcl file2.tcl file3.tcl
```

`package provide` 命令定义了该文件中过程所属的包的名称和版本。该命令用于为其他脚本提供过程的脚本：

语法：package provide packageName ?version?

package provide

声明此脚本模块中的过程是包 `packageName` 的一部分。可选地声明此文件代表哪个版本的 `packageName`。

- packageName: 将在此脚本中定义的包的名称。

- ?version?: 该包的版本号。

`pkg_mkIndex` 命令在文件中查找 `package provide` 命令。它使用包名和版本信息在 `pkgIndex.tcl` 文件中生成一个条目，包含包的名称、版本以及该文件中定义的所有过程的列表。

当你在 Tcl 脚本文件中放置 `package provide` 命令时，它告诉 Tcl 解释器文件中的所有过程都是某个包的成员。

你可以使用多个文件来构建你的包，只要每个文件中都有一个 `package provide` 命令。

## 第 7 章：命名空间与包

注意，如果你在一个源文件中有具有不同 `packageName` 参数的 `package provide` 命令，那么该源文件中的所有过程将成为 `package provide` 命令描述的所有包的成员。在这种情况下，如果需要 `package provide` 命令列出的任何包，则所有过程都将被加载。你不能在一个源文件中定义两个独立的、不重叠的包。

如果你放置具有相同 `packageName` 参数但不同 `version` 的多个 `package provide` 命令，索引生成将产生错误。

`package require` 命令声明在特定包中定义的过程将在此脚本中使用。该命令被使用过程的脚本调用。

语法：package require packageName ?version?
package require

告知 Tcl 解释器，在此脚本执行期间可能需要此包。Tcl 解释器将尝试查找该包并准备加载它。

- -exact: 如果存在此标志，则必须存在 `versionNum`。Tcl 解释器将仅加载该版本。
- packageName: 要加载的包名。
- ?version?: 要加载的版本号。如果提供了此参数但不存在 `-exact`，则可能加载 `packageName` 的任何版本。

`package require` 命令检查搜索路径（由 `auto_path` 定义）中的 `pkgIndex.tcl` 文件，并选择与请求版本最佳匹配。如果使用了 `exact` 标志，它将选择该版本的精确匹配。如果定义了 `versionNum` 但未设置 `-exact`，则大于 `versionNum` 的最大次要修订将

## 7.2 包

selected。如果找不到合适的修订版本，`package require` 将产生错误。

一旦确定了适当的文件，就会更新全局数组 `auto_index`。该数组的索引是过程名称，与每个索引关联的数据是加载该文件的 TCL 命令。

通过延迟到需要过程时才加载文件，Tcl 避免了冗长的初始化时间。通过先扫描索引并构建数组，解释器可以一直运行直到需要未定义的命令。此时，解释器加载定义该命令的脚本并继续运行。如果一个包被 `package require` 命令标记，但实际上没有使用该包的命令，Tcl 解释器永远不会加载该文件。

注意当包被自动加载时，它被加载到全局作用域，其中加载过程的代码会被评估。如果你想在命名空间内嵌套命名空间并使用 `package require` 命令找到正确版本的包，你将需要强制加载包。你可以使用 Tcl 命令评估 `package require` 放在 `auto_index` 中的命令。

### 7.2.4 版本号

版本号是由点分隔的一个或两个正整数，例如 `1. 2` 或 `75.19`。
- 字符串中的第一个整数是主修订号。根据一般规则，这仅在包发生重大修改时才会更改。预计在主修订版本内不会有应用程序接口修改，但可能会发生更改，导致在一个主修订版本中运行的代码在另一个中无法运行。
- 第二个整数是要修订号。这对应于中间发布。你可以预期修复漏洞、性能

