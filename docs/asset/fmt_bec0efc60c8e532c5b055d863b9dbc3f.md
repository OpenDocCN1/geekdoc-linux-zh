
# 附录 B

## 替代工具

每当热门 PHP 工具的讨论出现时，对话通常围绕文本编辑器或编码 IDE 展开。哪种拥有最好的语言支持、语法高亮、代码解析等等？不幸的是，由于过分关注文本编辑器，一些优秀的非编码工具有时会被忽视。与其重复通常关于一个编辑器优于另一个编辑器的争论，本附录向你展示了一些你可以在开发周期中使用的工具——那些不会立即生成代码的工具，但你可能发现它们在整体开发过程中占据着关键位置。

### MySQL 工具

当你管理 MySQL 数据库时，你通常有两个主要选择作为管理工具：标准的命令行工具集，或图形界面。尽管许多老练的系统管理员持相反态度，使用图形工具完成工作绝对没有任何问题。虽然命令行接口提供了对数据库的无限控制权，但它无法与良好的图形用户界面在帮助促进管理工作流程方面的速度和清晰度相媲美。

如果你在寻找一套好的基于 GUI 的 MySQL 管理工具，你只需要看看 MySQL AB 自己的 `MySQL Administrator` 和 `MySQL Query Browser`。

#### MySQL Administrator

`MySQL Administrator` 是一个功能丰富的 GUI 管理工具，用于维护 MySQL 数据库。主要界面如 figure B.1 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_373_0.png)

`MySQL Administrator` 允许你执行以下操作：

- 查看实时服务器信息，包括连接信息和统计、内存统计、MySQL 内部变量及配置设置的值等。
- 查看不同的服务器日志：错误日志、慢查询日志、通用日志（仅限本地主机）。
- 控制 MySQL 进程本身（仅限本地主机）。
- 执行备份和还原操作，甚至安排定期备份。
- 管理服务器的用户访问权限和特权。
- 使用内置的 MySQL 表编辑器创建和编辑完整的数据库，包括表。

`MySQL Administrator` 适用于 Windows、Linux 和 Mac OS X；`MySQL Administrator` 可从 MySQL 网站免费下载：http://www.mysql.com/products/administrator/。

#### MySQL 查询浏览器

`MySQL Query Browser` 是一个图形用户界面（GUI），允许你针对 MySQL 数据库测试和运行各种查询。从某种意义上说，它是命令行客户端的增强版 GUI，你可以参考图 B.2。你还可以像使用标准电子表格程序或桌面数据库应用程序一样使用 `MySQL Query Browser`——你可以调出数据行，并在查询浏览器中直接编辑它们。除了输入和执行查询以及操作数据之外，它还包含 `MySQL Administrator` 中的 MySQL 表编辑器，允许你以可视化方式创建和编辑数据库和表。

![](img/ab27c6ac898db1f934d39fa127b14657_374_0.png)

Windows、Linux 和 Mac OS X 版本可在 MySQL 处获取：[http://www.mysql.com/products/query-browser/](http://www.mysql.com/products/query-browser/)。

现在你的应用程序已经启动并运行，服务器也已针对峰值性能进行了调整。但你的数据库查询是否尽可能精简高效？找出答案的唯一方法是使用基准测试工具。

大多数 MySQL 基准测试工具的运行方式大致相同：你提供一个要运行的查询，该工具将运行该查询大量次数，通常使用并发连接。通过对某些“较重”的查询（通常可在 MySQL 慢查询日志中找到）进行彻底的测试和实验，你可以改善应用程序瓶颈处的执行时间和服务器负载。

#### MySQL Super Smack

`MySQL Super Smack` 最初由 Sasha Pacheco 开发，是一个独立的压力测试工具，用于 MySQL 和 PostgreSQL。`MySQL Super Smack` 接受一个或多个包含查询的文件，并以指定的并发连接数，对每个查询对目标数据库进行预定义次数的猛烈攻击。

`MySQL Super Smack` 可在 http://vegan.net/tony/supersmack/ 获取。

#### MyBench

`MyBench` 是由 MySQL 专家 Jeremy Zawodny 创建的基于 Perl 的基准测试工具。与 `MySQL Super-Smack` 一样，它可用于向目标 MySQL 机器发送大量连接和查询，并给出其承受攻击表现的清晰结果。由于它是用 Perl 编写的，你可以轻松地按意愿进行修改和扩展。缺点是大的测试批次可能会占用机器资源，因此最好将此工具运行在目标 MySQL 服务器以外的另一台机器上，以避免结果受到污染。

`MyBench` 可在 Jeremy Zawodny 的网站获取：http://jeremy.zawodny.com/mysql/mybench/。

### 版本控制

你可能需要考虑在你的开发生命周期或工作流中引入某种形式的版本控制系统，如果你还没有的话。版本控制系统提供了一种在开发过程中存储代码历史快照的方法，并允许多个开发人员将文件检入和检出仓库，从而控制代码库的演变。当今使用最广泛的两款开源版本控制系统是 CVS 和 Subversion。

CVS 和 Subversion 都是支持相同基本功能的版本控制系统：文件版本的历史记录，以及支持多开发人员及检入/检出功能。CVS 自 1989 年以来一直存在，是许多开发人员的长期最爱。Subversion 较新，最初出现于 2000 年末，但由于其功能集超出了在 CVS 中找到的“标准”功能，因此正迅速吸引拥趸。诸如原子提交、“安全”的文件重命名、文件和目录复制以及 WebDAV 支持等功能，是许多开发人员如今选择 Subversion 的一些原因。如果你正在寻找一个功能健壮且客户端和服务器端支持良好的功能集，Subversion 可能是你最好的选择。如果你追求稳定性、记录以及在许多开发工具中内置的支持，CVS 可能更受青睐——尽管最近越来越多的开发包正在获得 Subversion 支持。

无论你选择哪种，尽早部署某种版本控制都是个好主意——它使多开发人员项目更容易管理，并可以在新代码实际上导致新的严重 bug 或回归问题时提供安全保障。

CVS 可在 https://www.cvshome.org/ 获取。

Subversion 可在 http://subversion.tigris.org/ 获取。

### UML 工具

如果你深入系统架构和设计领域，很有可能你最终会与 UML 打交道。如果你不熟悉 UML，简而言之，它是一种对应用程序或其他系统的结构、行为、架构和流程进行建模和表示的方法。你可以使用 UML 对系统或应用程序的不同方面进行图解，包括类结构、用户交互、对象交互、流程等，类似于你可能使用 Visio、Kivio 或其他相关工具制作的流程图和其他图表。

UML 有九种图表类型，但从开发人员的角度来看，其中最重要的一种是类图。类图有助于你规划你的各种类以及这些类之间的关系。

如果你在 PHP 工作流中使用 UML，你有几个工具可供选择——一些流行的免费工具是 ArgoUML 和 Umbrello。

#### ArgoUML

`ArgoUML` 是由 Tigris.org 社区创建的基于 Java 的 UML 编辑器。它支持八种主要的 UML 图表类型，可以帮助你快速规划对象、关系和行为。从 PHP 开发人员角度来看，`ArgoUML` 的主要功能之一是它能够自动从 UML 类图生成有效的 PHP5 类骨架（以及 C#、Java、C++ 和 PHP4），如图 B.3 所示。

你只需在 UML 中创建你的类图，并告诉 `ArgoUML` 要生成什么代码以及在哪里生成代码，这样你就节省了键入类结构的时间，让你能够直接进入代码的核心：实现。`ArgoUML` 还提供有关你类结构的机器生成建议，并具备集成的待办事项列表。

`ArgoUML` 可作为桌面 Java 应用程序获取，既可通过下载获取，也可通过 JavaWebStart 从互联网运行，网址为 http://argouml.tigris.org/。

![](img/ab27c6ac898db1f934d39fa127b14657_377_0.png)

图 B.3

#### Umbrello

`Umbrello` 是另一种 UML 图解应用程序，类似于 `ArgoUML`。`Umbrello` 现在是 KDE 开发人员工具包的一部分，支持许多主要的 UML 图表类型，包括类图、用例图、状态图和序列图。从 1.4 版本开始，`Umbrello` 可以生成 PHP5 类骨架，以及几种其他编程语言的代码，如图 B.4 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_378_0.png)

图 B.4

`Umbrello` 可作为 KDE 桌面环境的一部分找到（3.2 或更高版本，Linux），或者你可以直接从 Umbrello 网站（针对 KDE/Linux）下载，网址为 http://uml.sourceforge.net/。

### 索引

## 符号和数字

**{} (花括号)**
- 缩进标准，214–217
- 减少嵌套级别，217–220

**: (冒号)**
- 与类常量 (`:;`)，28–29
- 在 PHP URL 中方案名后 (`://`)，72
- 与 *self* 关键字 (`::`)，7, 27–28

**$ (美元符号)**
- 未用于类常量 (PHP)，29
- `$this` 引用变量 (PHP)，23, 50

**:: (双冒号)。参见** **: (冒号)**

**= (等号) 在相等运算符与赋值运算符中，** 219

**404 处理程序，缓存与，** 226

**" (双引号)**
- 在 `set_exception_handler()` 内的函数名称中，5
- 与字符串的速度，201–205

**‘ (单引号)，与字符串的速度，** 201–205

**/ (斜杠)**
- MySQL 查询的 `/G` 终止符，86
- 在 PHP URL 中方案名后 (`://`)，72

## A

**ab** ApacheBench 程序，208–209

**abort() 方法 (AJAX)，** 277

**abstract 类 (PHP)**
- abstract 关键字，7
- 示例，7–8
- 语言翻译，341–342
- 命名约定，222
- 概述，34–35
- 使用规则，8

**abstract 关键字 (PHP)，** 7

**访问控制 (Apache)。参见** **认证**

**访问控制 (MySQL)**
- `GRANT` 和 `REVOKE` 的替代方案，97–100
- `columns_priv` 表，99, 100
- db 表，98–99, 100
- `GRANT` 命令，94–96
- 重新加载特权表，100
- `REVOKE` 命令，96–97
- 服务器限制，100
- `tables_priv` 表，99, 100
- 用户管理，93–100
- user 表，97–98, 99–100

**访问控制 (PHP)**
- 基本认证，166–171
- 注册表单中的 CAPTCHA 图像，175–177

### 访问控制

- **访问控制（PHP）（续）**
    - 表单身份验证，172–174
    - `HTTP_REFERER` 值，174–175
    - `REMOTE_ADDR` 值，174
    - 服务器变量，174–175
- **访问修饰符（PHP）。另见特定修饰符**
    - Circle 类示例，24–25
    - 语言翻译，337
    - PHP5 增强功能，6
    - 由其指定的可见性，23–24
- `addslashes()` 函数（PHP），113

### AJAX（异步 JavaScript 和 XML）

- 可访问性问题，283–285
- JPCPAINT 库，283
- 描述，273
- DOM 操作，273，281–282
- 更多信息，285
- Google 的 Gmail 应用程序，273
- 处理 `ReadyStateChange` 事件，280
- 处理响应，280–282
- 历史，274–277
- JSPAN 库，283
- 方法，277–278
- 属性，278–279
- JSAJAX 库，282–283
- 支持问题，285
- 与传统 Web 应用的对比，273，274
- 易用性问题，283–285
- 处理浏览器差异，279–280
- XMLHTTP 和 XMLHttpRequest 接口，277–282

```
if (condVar > someVal) {console.log("xxx")}
```

![](img/ab27c6ac898db1f934d39fa127b14657_405_0.png)

### 随时随地携带您的图书馆。

现在，无论您身在何处，都可以在线访问 70 多本完整的 Wrox 书籍！您订阅 **Wrox 参考库** 后，即可获取所有的图表、描述、屏幕截图和代码示例。为了在需要答案的时间和地点获取帮助，请访问 wrox.books24x7.com 并立即订阅！

查找书籍主题：
- ASP.NET
- C# / C++
- 数据库
- 通用
- Java
- Mac
- Microsoft Office
- .NET
- 开源
- PHP/MySQL
- SQL Server
- Visual Basic
- Web
- XML

![](img/ab27c6ac898db1f934d39fa127b14657_405_1.png)

www.wrox.com
