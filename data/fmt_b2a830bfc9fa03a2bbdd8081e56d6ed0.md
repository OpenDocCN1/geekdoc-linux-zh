
```php
print("Tobias Ratchiller and Till Gerken.\n\tCopyright (c) 2000, New Riders Publishing\n\n");

exit;
```
```
// 第一个参数是日志文件名
$logfile = $argv[1];

// 第二参数是邮件主题
$subject = $argv[2];

// 初始化主体变量
$body = '';

// 从 stdin 获取传递的提交消息
$fp = fopen("php://stdin", "r") or die("Fatal Error: could not read from stdin.");

while(!feof($fp))
{
  $body = fgets($fp, 64);
}

fclose($fp);

// 将消息发送给所有指定的收件人
for($i=2; $i<count($argv); $i++) {
  mail($argv[$i], $subject, $body);
}

// 记录消息
$fp = fopen($logfile, "a") or die("Fatal Error: could not write logfile " . $logfile . " for writing");
fputs($fp, "$subject\n");
fputs($fp, "$body\n");
fputs($fp, "................................\n");
fclose($fp);
```

为什么使用 PHP 进行命令行脚本？尽管它最初被设计为 Web 语言，但 PHP 的演进已使其能够用于此类任务。只需将 PHP 编译为独立二进制文件，你就可以像 Perl 一样将其作为脚本解释器。在 UNIX 系统上，你可以将文件的第一设置为脚本解释器：

```php
#!/usr/bin/php
```

通过设置可执行位，你可以像调用 UNIX 系统上的任何其他普通执行文件一样调用它：
```bash
tobias@dev:home/tobias > chmod +x script.php
tobias@dev:home/tobias > ~/script.php
```

在 Windows 上，你可以将 `.php` 文件扩展名与解释器关联以实现结果。
脚本展示了命令行脚本所需的两个重要概念：访问脚本参数和从标准输入读取。PHP 会自动设置一个数组 `$argv`，其中脚本文件名作为第一个条目，并将所有参数分配给脚本。这实际上是 C 语言的行为。就像在 C 中一样，另一个变量 `$argc` 包含参数数量。当然，你也可以使用 `$argv`。例如，如果你用用 `php script.php foo` 调用 PHP 脚本，`$argv[1]` 将包含第一个参数 `foo`。

代码中另一个值得注意的部分是从标准输入读取。PHP 4.0 允许你使用 `fopen()` 使用所谓的 PHP 流。为了在命令行上接受用户输入或从另一个程序读取数据，可以使用 `php://stdin`。脚本使用它来读取 CVS 提供的日志消息；你也可以使用类似的函数提示输入。列表 5.3 显示了它的运行情况。

### 列表 5.3 使用 PHP 输入/输出流提示用户输入。

```php
function readln() {
    // 初始化返回值
    $ret = '';
    // 从 stdin 读取直到用户按下回车键
    $fp = fopen("php://stdin","r") or die("Fatal Error: could not read from ~stdin");
    do {
        $char = fread($fp, 1);
        $ret .= $char;
    } while($char != "\n");
    return($ret);
}

print("Please enter your firstname:\n");
$firstname = readln();
print("You entered: $firstname\n");
```

其他可用的流还有 `php://stdout` 和 `php://stderr`。这提供了一种有效且独立平台的方法来访问标准输入、标准输出和标准错误。

## 传统的客户端/服务器架构

在过去，传统的非 Web 应用程序负责处理从用户输入到应用程序逻辑到数据存储的所有工作。这三个实体相互交织，使得在不影响其他部分的情况下，更改其中某一个变得困难，甚至是不可能的。如果你想为多个用户提供这样的应用程序，你就会面临问题：如果数据格式发生变化怎么办？如果要求你更改应用程序逻辑怎么办？你必须为所有用户提供一份新的本地副本，这对于大型系统来说是种不可行的方案。

随着面向对象的分析、设计和编程原则的出现，业务应用程序变得组件化了。用户界面通常部署在工作站上，而数据逻辑托管在大型机上。“客户端/服务器”一词被用来描述这种分层的分离。二层客户端/服务器架构提供了基本的任务分离。客户端（或第一层）负责向用户展示数据（用户界面），服务器（或第二层）负责为客户端提供数据并处理应用程序逻辑。到目前为止，你会发现二层模型在第二层（服务器）中结合了不同的概念：数据服务和应用程序逻辑。应用程序逻辑是程序的核心，负责数据验证、处理规则等。

这两种概念在二层架构中的交织引入了扩展性、重用性和维护方面的问题。以最近引入欧元为例：如果应用程序没有将逻辑与数据清晰地分离，那么两层都需要更改，以及数据存储格式。使用多层方法，所有概念都可以被清晰地分离。

## PHP 与多层应用程序

多层系统的概念在 20 世纪 90 年代初流行起来，现在已确认为 90 年代后期和 21 世纪初的架构。多层架构（称为三层架构）提供了更大的扩展性、更低的维护成本和更高的组件重用率。三层架构提供了一种技术中立的方法，通过采用标准接口的供应商构建客户端/服务器应用程序，为每个逻辑层提供服务。看看图 5.5 中的三层模型——作为应用程序开发者，你不觉得它眼熟吗？第一层是轻客户端——翻译到 Web 应用程序领域，就是浏览器。中间层（应用）显然是作为应用程序主机的 Web 服务器，而第三层由 RDBMS（关系型数据库管理系统）组成。

### 图 5.5 多层应用程序层

| 层 | 组件 |
| :--- | :--- |
| I. 客户端 (UI) | 业务对象 |
| II. 应用服务器 | Java Beans |
| III. 数据服务器 | COM 控制 |

## COM

组件对象模型 `COM` 是微软开发的一种软件架构，它允许将软件块抽象为二进制组件。`COM` 定义了组件互操作的标准以及组件必须具备的特定特性。它不依赖于任何编程语言；事实上，微软正努力将 `COM` 建立为一种开放的 IETF（互联网工程任务组组）标准。任何合规的应用程序和编程语言都可以访问 `COM` 对象；例如，通过 Visual Basic、Delphi 或 PHP。

`COM` 解决的问题是：如何设计系统，使得来自不同供应商的二进制软件组件能够运行？对于这个问题，DLL 的概念失败得非常惨。。由于 DLL 缺乏版本控制，任何两个暴露相同接口的 DLL 都无法在同一个系统上。让我们举个例子：你有一个服务器监控应用程序，它不断检查服务器是否宕机并记录收集到的数据。你有一个前端，带有漂亮的统计数据，以及一些在服务器无法访问时做出恰当响应的逻辑。软件的后端可以是执行实际监控的 DLL。假设 `ServerSpy.dll` 暴露了一个函数 `is_reachable()`，它接收一个服务器名称，并在服务器可访问时返回 `true`，不可访问时返回 `false`。我们还没有定义监控什么种服务器——事实上，它可以是 Web 服务器、邮件服务器、名称服务器或任何其他系统，函数声明以及后端设计都需要更改。唯一需要更改的是函数 `is_reachable()` 的实现。

使用 DLL 时，你在系统上只能有一个监控服务——要么是 Web 服务器监控，要么是邮件监控等。如果你安装另一个 DLL，它会覆盖上一个。你的应用程序无法让用户在它们之间进行选择。这种情况已经改变了，我们认为这是 PHP 演变过程中最剧烈的转变之一。当前版本不仅允许你在 Win32 系统上访问 COM 控制，还允许你在任何带有 Java 虚拟机 `JVM` 的系统上执行 Java 方法。

企业级对象重用有三种架构：微软的 `COM`、Sun Microsystems 的 `JavaBeans/RMI` 以及对象管理组的 `CORBA`。目前使用最广泛的是 `COM`，因为 Windows 系统被广泛使用（见下节关于使用 PHP 和 COM 的详细信息）。然而，具有异构环境的企业将更倾向于通过广泛的平台支持使用 Java 或 R/3 系统。例如，可以通过 `JavaBeans`（或 `COM` 对象）通过业务 API `BAPI` 接口访问 R/3 系统，使你能够将 SAP 业务框架集成到你的应用程序层中。思考这将为电子商务系统带来的可能性：你可以有效地将前端在线商店与后端的企业仓储应用程序相结合。

# 196 第 5 章 Web 应用程序策略

要在远程系统上创建 DCOM 组件实例，请将主机作为第二个参数传递给构造函数。例如：

```
$comp = new COMObject("My.Component", "remote.server.com");
```

在 PHP 3.0 中，你无法使用 COM 类；相反，你需要使用 `com_load()`、`com_invoke()`、`com_set()` 和 `com_get()` 函数。我们的示例如列表 5.5 所示。

## 列表 5.5 使用 PHP 3.0 版本的基础 COM 示例。

```php
$Amount = 1000; // 要转换的金额
$Scurr_from = "DEM"; // 原始货币的 ISO 货币符号
$Scurr_to = "ITL"; // 目标货币符号
```

```php
// 实例化新的 COM 对象
$conv = com_load("Softing.EDConverter") or die("Unable to instantiate\n=Euro-Converter");
```

```php
// 在 COM 对象实例上执行方法
$ret = com_invoke($conv, "Triangulate", "10000", "ITL", "DEM") or
die("Exception triggered by Triangulate() on line ".__LINE__);
```

```php
// 打印结果
print($ret);
```

这些函数（在 PHP 4.0 中不可用）的语法如下：

- **`com_load(string component_name)`**
  实例化一个 COM 组件并创建其引用。返回的整数值必须在随后的 `com_()` 调用中通过。如果发生错误，则返回 false 并抛出警告。
- **`com_invoke(int com_identifier, string function_name[, mixed argument[1...]])`**
  调用 COM 组件的方法并返回方法的返回值。函数的第一个参数是使用 `com_load()` 创建的有效 COM 标识符。第二个参数必须是组件方法的名称。作为可选的第三个及后续参数，你可以为被调的方法指定参数。此函数在错误时返回 false。

# 三层体系应用程序 197

- **`bool com_set(int com_identifier, string property_name, string property_value)`**
  为 `com_object` 实例化的 COM 对象上的属性分配值。该函数的别名为 `com_propset()` 和 `com_propget()`。成功时返回 true，错误时返回 false。
- **`mixed_get(int com_identifier, string property_name)`**
  返回 `com_object` 实例化的 COM 对象上属性的值。该函数的别名为 `com_propget()`。成功时返回属性值，错误时返回 false。

## PHP 与 Java

Java 是许多企业软件开发者的“主流语言”，正越来越多地应用于开发的各个领域。从 4.0 版本开始，PHP 可以被编译以支持调用原生 Java 函数，这实际上让你能够在多层环境中使用企业级 Java 组件。

安装 Java 支持并不困难。你必须记住以下几点：

- 你需要先在系统上安装 Java 虚拟机 `JVM`；我们有免费提供的开源 Kaffe 10.5 实现。
- PHP 需要使用 APXS 编译为 DSO，这意味着它将作为动态共享模块加载到 Apache 中。你可以在 PHP 分发版的 `INSTALL_DAO` 文件中找到相关说明。

请查看 `ext/java` 目录下的 `README` 文件以获取更多说明。一旦在 PHP 中支持了 Java，其语法与调用 COM 组件的方法相似。事实上，两者都利用了名为“对象重载”的高级 Zend 内部特性。软件工程中的“重载”术语意味着构造根据上下文产生不同的反应。因此，函数重载意味着函数可以根据参数的顺序或类型而不同。

例如，在 C++ 中，你有两个类似的函数声明：

```cpp
void add(int Left, int Right);
void add(double Left, int Right);
```

取决于你向 `add()` 传递 int 值还是 double 值，将调用相应的函数。开发者通常尝试避免此类歧义，因为调试这可能是一场噩梦。

Zend 引擎内部允许类似的函数重载，并利用它来实现对象重载。根据上下文（例如类名），对象可以代表不同的含义：它可以是一个普通的用户定义类，但也可以是复杂得的东西，例如 COM 或 Java 接口。

与 COM 类似，创建新的 Java 对象是通过实例化重载的 Java 类完成的。构造函数参数是要使用的 Java 类：

在返回的对象上，函数的使用方法与 COM 对象相同。要读取和写入属性，必须使用辅助函数（记住，在 COM 模块中，属性可以直接访问的）`getProperty()` 和 `setProperty()`：

```php
$System = new Java("java.lang.System");
printf("Java version = %s", $System->getProperty("java.version"));
```

## 总结

在本章中，你学习了所有 Web 应用程序的基本策略。你知道如何正确处理用户输入，以及如何验证表单并校验其内容。你可以使用模板将代码与布局分离；更进一步，你知道如何协调团队工作，并处理多人协作同一个文件的情况。我们讨论了版本控制系统的优势，并且你可以以清晰的方式在磁盘上构建你的项目。你可以对其进行高级使用。

掌握了这些知识，你现在能够面对现代 Web 开发的挑战了。

# PHPLib: PHP 基础库 201

PHPLib 似乎非常适合有多个开发者的项目。它强制程序员使用相似的接口，并鼓励面向对象编程，这至少可以为应用程序带来更好的结构。此外，由于 PHPLib 要求对 PHP 的高级特性以及一般的 Web 应用程序有一定的了解，它能让团队中的开发者达到相当的知识水平。

由于 PHPLib 是原生 PHP 编写的，它的运行速度没有 PHP 的 C 扩展快。但另一方面，它更加灵活。由于这些库是以类的形式编写的，你可以轻松进行修改以适应你的需求。事实上，你确实需要一些修改；PHPLib 并不是一个开箱即用的产品。你应该意识到你需要自己提供某些函数。

不同 PHPLib 类之间的依赖关系是复杂的；例如，如果不使用库的数据库抽象层，你就无法使用会话管理函数。如果你只需要会话管理，可能使用 PHP 4.0 的会话函数或我们的 PHP 3.0 后期移植版本会更好。尽管如此，请继续读下去——PHPLib 的某些功能绝对能让生活变得更轻松。

## 重要文件

在 PHPLib 分发包中，有两个文件可能需要你修改：`local.inc` 和 `prepend.php3`。

`prepend.php3` 加载所有使用 PHPLib 的页面都应该加载的文件。默认情况下，它加载 MySQL 数据库，并使用 SQL 存储容器进行会话管理。要从 MySQL 切换到 Postgres，你需要更改行：

```php
require($PHPLIB['libdir'] . '/db_mysql.inc'); /* 修改此行以匹配你的
database. / */
```
