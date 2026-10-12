

# 第 9 章

看起来更好，但请记住，函数名、方法名和类名在 PHP 中都是大小写不敏感的：`Mandate` 和 `mandate` 将指向同一个实体。

通过 `define()` 或 `const` 创建的已定义常量通常以大写字母表示。在全局作用域中通过 `define()` 创建的常量应以前缀特有的字符序列开头，以防止与其他地方定义的常量发生冲突（参见 PHP 手册中许多此类实践的例子）。对于类常量则不需要这样做，因为它们的名字已经由类名（或在类定义内部的 `self::`）作为前缀。

由于这种区分已经内置于 PHP 的语法中，与其他语言相比，区分变量/属性名与函数/方法名的规则是不必要的；但在类与函数之间不存在这样的区分。你可以有一个名为 `foo` 的类和一个名为 `foo` 的函数，区分它们的唯一方式是 `$v = new Foo();` 使用类，而 `$v = foo();` 使用函数。

> `$v=foo::foo();` 则是另一回事——换言之，这是连编译都无法通过的内容；构造函数不能以静态方式调用，静态函数也不能作为构造函数使用。

从语法角度来看，类、变量和属性最好用名词或名词短语来描述。请使用你在描述代码功能的口语化描述中会使用的那些词性。数组和其他集合应使用复数形式的名字（$children, $pages）。布尔值的属性应以“is”或“has”或其他表示谓词的方式作为名字开头（$isValid, $can_be_deleted）。类应以名词命名（UserFactory, NonPlayerCharacter）；抽象类可以加上 `Abstract_` 或 `Abstract` 前缀，以防止试图意外地从它们创建对象（AbstractCollection, Abstract_Document），而结构 `FooFactory` 是一种常见的约定，用于表示提供返回类 `Foo` 新对象的静态方法的类。函数和方法可以用动词命名（$traversePath(), anneal(), be_wonderful()），允许使用形容词、副词，偶尔也可以用名词来命名常量（COLOR_GREEN, QUICKLY, GOLDEN_RATIO）。

## 篡改语法规则

某些关于编码风格的规则可以通过将违规操作转化为解析错误来强制执行。如果你知道自己在做什么，你可以编辑 `zend_language_parser.y` 和 `zend_language_scanner.l` 文件并重新构建 PHP。

例如，如果你想排除使用诸如 `if(): … endif;` 等结构的可能性，你可以从词法文件中删除匹配 `endif`、`endwhile`、`endfor`、`endforeach`、`enddeclare` 和 `endwhile` 的模式（所有这些出现在 `<ST_IN_SCRIPTING>` 上下文中）；并从 yacc 文件中删除相应的 `T_END*` 令牌声明和产生式规则：

```text
unchecked_statement:
    T_IF ' ' expr ')' ':' inner_statement_list new_elseif_list new_else_single T_ENIF ','

while_statement:
    ":" inner_statement_list T_ENWHILE ';'

for_statement:
    ":" inner_statement_list T_ENDFOR ';'

foreach_statement:
    ":" inner_statement_list T_ENDFOREACH ';'

declare_statement:
    ' ; ' inner_statement_list T_ENDECLARE ';' 

switch_case_list:
    ' : ' case_list T_ENDSWITCH ';' |  
    ' : ' '; ' case_list T_ENDSWITCH ';'
```

另外，删除 `new_else_list` 和 `new_else_single` 产生式的整体内容。由于 `while_statement`、`for_statement`、`foreach_statement` 和 `declare_statement` 现在都归约为单一规则 `statement`，且没有相关的代码，这些产生式本身现在是多余的。你可以用 `statement` 替换 `while_statement` 的出现位置（它出现在 `unchecked_statement` 的产生式中一次，具体取决于你的修改上下文，原文意指 `while_statement` 作为被替换项），移除 `while_statement` 的产生式，从而获得一个略小且更简单的解析引擎。

*注：根据原文逻辑，此处意在说明移除那些特定的产生式规则后，对应的非终结符号不再需要独立的产生式。*

当然，这会破坏任何使用了如今已被禁止的结构编写的代码。

## 缓存

如果一个页面每天更新一次，但每天被访问数千次，这意味着相同的计算每天被重复执行数千次，产生相同的结果。执行一次并保留结果以供后续所有请求使用，可以带来巨大的节省潜力。

由于你的 PHP 应用程序与处理器之间隔着多层中间软件，指令通过这些层过滤到硬件，结果再过滤回来，因此在过程中有几个点可以短路。在任意两个这样的层之间，都有一个接口，你可以想象那里有一个助手，它记住了人们对信息的先前请求以及作为结果提供的信息，因此如果相同的请求再次出现，它可以立即提供该信息。

在 PHP 层面，有两个主要接口可以有效利用缓存。你可以生成页面的静态版本并提供这些静态页面，而不是每次重新生成；你可以将 PHP 应用程序的源代码存储为预解析格式，以便 Zend 引擎直接执行，而无需额外编译源代码的步骤；或者你可以两者兼做。

### 源代码预解析

当运行 PHP 程序时，源代码被加载、解析并编译为字节码（为 Zend 引擎模拟的假想处理器设计的机器代码），然后执行该字节码。市面上有几种产品可以保存这些编译后的字节码，下表列出了其中一些较优秀的产品（按字母顺序排列）。

| 产品 | URL |
| :--- | :--- |
| afterBÜRNER*Cache | http://bwcache.bware.it/cache.htm |
| Alternative PHP Cache | http://pecl.php.net/package/APC |
| PHP Accelerator | http://www.php-accelerator.co.uk/ |
| Turck MMCache | http://turck-mmcache.sourceforge.net/ |
| Zend Optimizer | http://zend.com/store/products/zend-optimizer.php |

就稳健性和有效性而言，Zend 自己的产品显然很难被超越，但使用它需要购买 Zend Encoder 来生成字节码。也要注意 APC 是作为 PECL 扩展分布的。

当程序再次被调用时，字节码被检索并直接提供给 Zend 引擎，跳过解析和编译阶段。所有这些产品都会检查源文件和字节码文件的修改日期，以确定前者自后者生成以来是否已更改，并在必要时重新解析和重新*编译*（原文为 re-ache，疑为 re-cache 或 re-compile 的笔误，此处按上下文逻辑译为重新处理/重新编译，但鉴于原文有 typo，且后文提到 re-parse，这里直译为“重新加速/重新处理”较为合适，结合语境译为“重新缓存”或保持原意“重新处理”）。*更正：原文 "re-ache" 极可能是 "re-cache" 或 "re-create" 的拼写错误，但在翻译中我们应忠实于原文意图，这里暂译为“重新处理”*。一些产品，如 Zend Optimizer，还可以（正如名字所暗示的那样）对字节码进行优化以提高性能，包括许多在 PHP 本身无法模拟的优化（因为优化器在更低的层面操作，在那里单个 PHP 语句可能对应于可以独立操作的几条字节码指令）。

一般来说，使用字节码缓存只需遵循其安装说明即可，无需对 PHP 程序的源代码做任何更改。因此，这通常是可以实现的最简单却最显著的软件级性能提升方法之一。

注意，特别是对于优化字节码缓存，各种脚本速度所做出的改变将是非线性的：这并不是简单地所有脚本都快 20% 或两倍快的问题。某些脚本会比其他脚本按比例快，尽管最坏的情况只是某些脚本没有明显变快。因此，在未安装缓存的情况下对网站进行性能分析的结果，与安装缓存后网站的性能概况没有直接关联。

### 输出预生成

与字节码缓存不同，保存生成的输出以便稍后重新显示确实涉及对你网站运行方式的更改。给定页面的第一件事是确定它是否需要运行，或者它是否可以使用其输出的缓存副本。

### PEAR::Cache 和 PEAR::Cache_Lite

自然，PEAR 包含提供缓存输出以供后续请求使用的软件包。

`Cache_Lite` 提供了一种简单且快速的机制，将页面或部分页面的输出存储为文件，以便稍后按需读取。以下示例使用它来缓存一个简单的字符串：

```php
<?php
require_once 'Cache/Lite.php';

$cid = '42'; // 这用于标识使用哪个缓存文件；
// 任何可以记住的唯一内容都可以；如果你正在以这种方式
// 缓存整个页面，其 URL 是一个自然的选择。

$options = array(
        'cacheDir' => '/cachefiles/', // Cache_Lite 仅支持文件存储；
                                      // 你需要在这里指定一个
                                      // 适当的目录。

        'lifetime' => 3600            // 我们将强制每小时更新一次。
);

$Cache_Lite = new Cache_Lite($options);

if ($data = $Cache_Lite->get($cid)) {
```

