
# 函数 257

| 结构 | 功能 |
| :--- | :--- |
| `foreach variable (list-values) { statements; }` | 处理值列表 (list-values)，例如由数组生成的列表；变量操作数被连续赋值列表中的值。 |
| `for(init-expr, test-expr, incr-expr) { statements; }` | 在只要测试表达式 (test-expr) 为真，就会执行语句。第一个表达式 `init-expr` 在循环开始前执行。第三个表达式 `incr-expr` 在循环内语句执行后执行。 |
| `LABEL:while(expression) { statements; }` | 只要测试表达式为真，就执行语句。 |
| `do { statements; } until(expression)` | 只要测试表达式为假，就执行语句。 |

（注：OCR 剩余文本存在重复或乱码。我已提供了上述唯一内容。）

# 子程序组件 261

| 字符 | 描述 |
| :--- | :--- |
| `\D` | 非数字字符：`[^0-9]+` |
| `\S` | 非空白字符：`[\n\t\r\f]+` |
| `\Bpattern` | 任何不是单词的模式 |

![](img/3db93a7d263e3b589612548bc59abfdb_278_0.png)

# 子程序组件

| 组件 | 描述 |
| :--- | :--- |
| `@_` | 一个用于存储参数列表的数组。（数组被组合为该数组的单个元素。） |
| `sub name (statements;)` | 子程序定义。 |
| `sub name;` | 子程序声明。 |
| `sub name (type-list);` | 原型声明。 |
| `function-name(arguments);` | 函数调用。 |
| `function-name;` | 函数调用。 |
| `&function-name arguments;` | 函数调用。 |
| `my(object-list)` | 限制在子程序或块中的局部变量。 |
| `local(object-list)` | 全局对象的局部版本，当前子程序和块以及其他调用的子程序均可见。 |
| `\array-name` | 数组引用（用于参数列表以维护数组的完整性）。 |

![](img/3db93a7d263e3b589612548bc59abfdb_278_1.png)

# 附录 B

## Tcl 和 Tk

Tcl 是由 John Ousterhout 于 1987 年在加利福尼亚大学伯克利分校开发的通用命令语言。它最初被设计用于自定义应用程序，现在已成为一门功能完善的语言。与 Perl 一样，你可以编写 Tcl 脚本，开发自己的 Tcl 程序。Tcl 经常与 Tk 结合使用创建图形化应用程序。Tk 用于创建窗口等图形化元素，而 Tcl 则负责管理用户输入等编程操作。与 Java 一样，Tcl 和 Tk 都是跨平台应用程序。

Tcl 是一种解释型语言，像 Perl 一样，它在自己的 shell 中运行。`tclsh` 是调用 Tcl shell 的命令。你也可以创建文件，在其中调用 Tcl shell 并列出 Tcl 命令，从而有效地创建一个 Tcl 程序。Tcl 语言及其应用的一个显著优势是它与 C 语言完全兼容。Tcl 库可以直接整合到 C 程序中。

Tk 应用程序扩展了 Tcl，增加了用于创建和管理窗口、图标和文本字段等图形化对象的命令。Tk 命令使用 X-Window 系统创建图形对象。与直接使用 X11 工具包相比，使用 Tk X-Window 对象是一种更简单的方法。通过 Tk，你可以轻松地为程序创建复杂的基于窗口的用户界面。

Tk 语言根据不同类型的图形化对象（如窗口、按钮和滚动条）进行组织。每种组件被称为 `widget`（小部件）。每种组件都有其自己的命令，你可以通过该命令创建组件。例如，你可以使用 `button` 命令创建一个按钮，或使用 `window` 命令创建一个窗口。一种组件被视为一个类（class），而创建组件的命令被称为类命令（class command）。该命令将创建该类的特定实例，即该类型的特定组件。

Tk 在 X-Window 系统下运行，在其中它使用自己的 shell——`wish` shell——来执行 Tk 命令。要运行 Tk 程序，你首先需要启动 X-Window 系统，然后使用 `wish` 命令启动 `wish` shell。这将打开一个你可以在其中运行 Tk 命令的窗口。

# Tcl 和 Tk 软件产品

Tcl 和 Tk 的当前版本以及此处列出的其他产品可从 Tcl/Tk 网站免费获取，地址为 http://sunscript.com：

| 产品 | 描述 |
| :--- | :--- |
| Tcl | Tcl 编程语言和解释器（当前版本 8.0）：`tcl8.tar.gz` |
| Tk | Tk 编程语言（当前版本 8.0）：`tk8.0.tar.gz` |
| SpecTcl | Tcl/Tk GUI 生成器；创建 GUI 用户界面：`SpecTcl1.1.tar.gz` |
| Tcl Plugin | Tcl/Tk 网页插件（当前版本 2.0）；Tcl/Tk 查看器（Tcells）：`tclplugin1.1.386.rpm` |
| TclHttpd | Tcl/Tk Web 服务器：`tclhttpd.tar.Z` |

# Tcl 列表操作

| 命令 | 功能 |
| :--- | :--- |
| `set list values` | 创建列表并为其赋值值。 |
| `lsearch(list, pattern)` | 在列表元素中搜索模式。 |
| `lindex(list, index)` | 返回列表中被索引元素的值。 |
| `length(list)` | 返回列表中的元素数量。 |
| `insert(list, index, value-list)` | 在索引后插入一个新元素。 |

# 常用 Tcl 命令 265

| 命令 | 功能 |
| :--- | :--- |
| `lreplace(list, index, value-list)` | 用新值替换索引的元素。 |
| `append(list, value-list)` | 在列表末尾追加新值。 |
| `concat(lists)` | 将多个列表的元素合并为一个。 |
| `list(str, delim)` | 使用分隔符分割字符串。 |
| `join(list)` | 将元素连接为字符串。 |
| `lsort(list)` | 按字母顺序排序列表。 |

![](img/3db93a7d263e3b589612548bc59abfdb_282.png)

# 赋值与变量

| 命令 | 功能 |
| :--- | :--- |
| `set` | 为变量赋值。 |
| `global` | 声明全局变量。 |
| `incr` | 递增整数。 |
| `unset` | 删除变量。 |
| `upvar` | 在不同作用域引用变量。 |
| `variable` | 声明命名空间。 |
| `array` | 执行数组操作。 |
| `expr` | 执行数学表达式。 |

# 控制结构与过程

| 结构/过程 | 功能 |
| :--- | :--- |
| `if` | 条件命令，带有 `else` 分支。 |
| `switch` | 选择。 |
| `while` | `while` 循环。 |
| `for` | `for` 循环。 |
| `break` | 强制退出循环。 |
| `continue` | 跳过剩余部分并继续迭代。 |
| `proc` | 定义 Tcl 过程。 |
| `return` | 从过程返回。 |
| `source` | 读取并执行文件中的 Tcl 命令。 |
| `uplevel` | 在不同作用域执行命令。 |

# 文件命令

| 命令 | 功能 |
| :--- | :--- |
| `file` | 获取文件信息。 |
| `open` | 打开文件。 |
| `close` | 关闭文件。 |
| `eof` | 检查文件结束。 |
| `fcopy` | 复制到另一个文件。 |
| `flush` | 刷新输出。 |
| `glob` | 使用通配符匹配文件名。 |
| `read` | 从文件中读取块。 |
| `seek` | 设置偏移量。 |
| `tell` | 返回当前偏移量。 |
| `socket` | 打开 TCP/IP 网络连接。 |

# 输入输出命令

| 命令 | 功能 |
| :--- | :--- |
| `format` | 使用格式说明格式化字符串（类似于 C 中的 `sprintf`）。 |
| `scan` | 使用格式说明读取并转换字符串中的元素（类似于 C 中的 `scanf`）。 |
| `gets` | 读取输入行。 |
| `puts` | 输出字符串。 |

# 几何布局管理器

| 命令 | 功能 |
| :--- | :--- |
| `pack` | 将组件并排排列。 |
| `grid` | 在行和列的网格中排列组件。 |
