

# 选项

- `-h`
  打印帮助信息。
- `-V`
  打印版本号。
- `-o` `OPTION[ OPTION…]`
  挂载选项。
- `-u`
  卸载。
- `-q`
  静默模式。
- `-z`
  延迟卸载。

# 参见

`mount(8)`, `mount_fuse(8)`, `ulockmgr_server(1)`。

# 主页

有关 fusermount 和 FUSE 项目的更多信息，请访问 <http://fuse.sourceforge.net/>。

# 作者

FUSE 由 Miklos Szeredi <miklos@szeredi.hu> 编写。

本手册页由 Daniel Baumann <daniel.baumann@progress-technologies.net> 编写。

# 名称

`fwupdmgr` - fwupd 客户端工具

# 摘要

`fwupdmgr` `[-verbose]`

# 描述

本手册页简要介绍了 `fwupdmgr` 命令。
`fwupdmgr` 允许管理员更新固件。

# 选项

此程序遵循标准的 GNU 命令行语法，长选项以两个短横线（`--`）开头。选项摘要如下。

1. `--help`
   显示选项摘要。
2. `--verbose`
   显示额外的调试信息。
3. `--allow-reinstall`
   允许重新安装现有的固件版本。
4. `--allow-older`
   允许降级固件版本。
5. `--offline`
   在可能的情况下以离线方式执行安装。

# 命令

此程序接受带有可变参数数量的命令。

- `get-details`
  获取固件文件的详细信息。
- `get-devices`
  获取支持固件更新的硬件列表。
- `get-updates`
  获取连接硬件的更新列表。
- `update`
  将所有固件更新到最新可用版本。
- `install`
  在此硬件上安装固件文件。
- `install-prepared`
  现在安装准备好的更新。
- `clear-results`
  清除上次更新的结果。
- `refresh`
  从远程服务器刷新元数据。
- `get-results`
  获取上次更新的结果。

# 作者

本手册页由 Richard Hughes <richard@hughsie.com> 编写。

# 名称

`gawk` - 模式扫描和处理语言

# 摘要

`gawk` `[ POSIX 或 GNU 风格选项 ]` `-f` `program-file` `[ — ]` `file ...`
`gawk` `[ POSIX 或 GNU 风格选项 ]` `[ — ]` `program-text` `file ...`

# 描述

Gawk 是 GNU 项目中 AWK 编程语言的实现。它符合 POSIX 1003.1 标准中对语言的定义。此版本基于 Aho、Kernighan 和 Weinberger 在《The AWK Programming Language》一书中对该语言的描述。Gawk 提供了 Brian Kernighan 的 awk 当前版本中的附加功能，以及许多 GNU 特有的扩展。

命令行由 gawk 本身的选项组成，awk 程序文本（如果未通过 -f 或 --file 选项提供），以及要在预定义的 awk 变量 ARGC 和 ARGV 中提供的值。

当 gawk 通过 --profile 选项调用时，它开始收集程序执行的剖析统计信息。在此模式下，Gawk 运行速度较慢，并在完成后自动在文件 awkprof.out 中生成执行剖析报告。请参阅下文中的 --profile 选项。

Gawk 还集成了一个调试器。通过向命令行提供 --debug 选项，可以开始交互式调试会话。在此执行模式下，gawk 加载 AWK 源代码，然后提示输入调试命令。Gawk 只能调试通过 -f 选项提供的 AWK 程序源码。调试器在《GAWK: Effective AWK Programming》中有详细记载。

# 选项格式

Gawk 选项可以是传统的 POSIX 风格单字母选项，也可以是 GNU 风格的长选项。POSIX 选项以单个 “-” 开头，而长选项以 “--” 开头。长选项既提供 GNU 特有功能，也提供 POSIX 强制功能。

Gawk 特有选项通常使用长选项形式。长选项的参数要么通过等号与选项连接，中间没有空格，要么作为下一个命令行参数提供。只要缩写保持唯一，长选项可以缩写。

此外，每个长选项都有一个对应的短选项，以便在 #! 可执行脚本中使用该选项的功能。

# 选项

*Gawk* 接受以下选项。首先列出标准选项，然后按短选项字母顺序列出 *gawk* 扩展选项。

- `-f` `program-file`
  `--file` `program-file`
  从文件 `program-file` 中读取 *AWK* 程序源码，而不是从第一个命令行参数中读取。可以使用多个 `-f`（或 `--file`）选项。

- `-F` `fs`
  `--field-separator` `fs`
  使用 `fs` 作为输入字段分隔符（**FS** 预定义变量的值）。

- `-v` `var=val`
  `--assign` `var` = `val`
  在程序开始执行之前，将值 `val` 分配给变量 `var`。这些变量值可用于 *awk* 程序的 **BEGIN** 规则。

- `-b`
  `--characters-as-bytes`
  将所有输入数据视为单字节字符。换句话说，在尝试将字符串作为多字节字符处理时，不关注区域设置信息。`--posix` 选项会覆盖此选项。

- `-c`
  `--traditional`
  以*兼容性*模式运行。在兼容性模式下，*gawk* 的行为与 Brian Kernighan 的 *awk* 完全相同；不识别任何 *GNU 特有*扩展。有关更多信息，请参阅下文中的 **GNU 扩展**。

- `-C`
  `--copyright`
  在标准输出上打印短版的 *GNU* 版权信息消息并成功退出。

- `-d`[`file`]
  `--dump-variables`[=`file`]
  将全局变量的排序列表及其类型和最终值打印到 `file`。如果未提供 `file`，*gawk* 将使用当前目录中名为 `awkvars.out` 的文件。
  
  拥有所有全局变量的列表是查找程序中拼写错误的好方法。如果您有一个包含许多函数的大型程序，并且希望确保您的函数没有无意中使用了您本打算设为局部的全局变量，您也会使用此选项。（对于像 `i, j,` 这样简单的变量名，这是一个特别容易犯的错误。）

- `-D`[`file`]
  `--debug`[=`file`]
  启用 *AWK* 程序的调试。默认情况下，调试器从键盘（标准输入）交互式读取命令。可选的 `file` 参数指定包含调试器非交互式执行的命令列表的文件。

- `-e` `program-text`
  `--source` `program-text`
  使用 `program-text` 作为 *AWK* 程序源代码。此选项允许轻松混合使用库函数（通过 `-f` 和 `--file` 选项使用）和输入在命令行上的源代码。它主要旨在用于在 shell 脚本中使用的中大型 awk 程序。

- `-E` `file`
  `--exec` `file`
  类似于 `-f`，但此选项是最后处理的选项。这应与 `#!` 脚本一起使用，特别是用于 CGI 应用程序，以避免通过 URL 在命令行上传入选项或源代码 `(!)`。此选项禁用了命令行变量赋值。

- `-g`
  `--gen-pot`
  扫描并解析 **awk** 程序，并在标准输出上生成 **GNU** **.pot**（可移植对象模板）格式文件，其中包含程序中所有可本地化字符串的条目。程序本身不会执行。有关 **.pot** 文件的更多信息，请参阅 **GNU** *gettext* 发行版。

- `-h`
  `--help`
  在标准输出上打印可用选项的相对简短摘要。（根据 **GNU** *编码标准*，这些选项会导致立即成功退出。）

- `-i` `include-file`
  `--include` `include-file`
  加载一个 **awk** 源库。这使用 **AWKPATH** 环境变量搜索库。如果初始搜索失败，在追加 *.awk* 后缀后将再次尝试。文件只加载一次（即消除重复项），并且代码不构成主程序源码。

- `-l` `lib`
  `--load` `lib`
  加载共享库 `lib`。这使用 **AWKLIBPATH** 环境变量搜索库。如果初始搜索失败，在追加平台默认的共享库后缀后将再次尝试。库初始化例程的预期名称为 **dl_load()。**

- `-L` [`value`]
  `--lint`[=`value`]
  对在其他 **awk** 实现中可疑或不可移植的结构提供警告。如果带有可选参数 **fatal**，lint 警告将变为致命错误。这可能会非常严厉，但使用它肯定有助于鼓励开发更整洁的 **awk** 程序。如果带有可选参数 **invalid**，则仅对实际上无效的事项发出警告。（这尚未完全实现。）

- `-M`
  `--bignum`
  强制对数字使用任意精度算术。如果 *gawk* 未编译为使用 **GNU MPFR** 和 **MP** 库，则此选项无效。

- `-n`
  `--non-decimal-data`
  在输入数据中识别八进制和十六进制值。*请谨慎使用此选项！*

- `-N`
  `--use-lc-numeric`
  此选项强制 *gawk* 在解析输入数据时使用区域设置的十进制点字符。尽管 **POSIX** 标准要求此行为，且当 `--posix` 生效时 *gawk* 会这样做，但默认情况下是遵循传统行为，即使在十进制点不是句点的区域设置中，也使用句点作为十进制点。

