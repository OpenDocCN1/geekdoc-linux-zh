
- 空原型的代码引用不再被特殊对待。它们像其他代码引用一样接收一个参数（即使它们选择忽略）。

`%hash sub {}` 和 `@array sub {}` 现在测试子程序是否为哈希的每个键（或数组的每个元素）返回真值

### 智能匹配更改

自 Perl 5.10.0 以来，Perl 开发者对智能匹配运算符进行了多处更改。这些更改当然改变了使用智能匹配的 `switch` 语句的行为。这些更改也出现在 5.10.1 版本，并将保留在后续的 5.10 版本中。

当出现在 `--` 运算符的左侧时，它就像任何普通的标量一样。

`def %hash always` 始终为 false（因为 `undef` 不能作为哈希的键）。不会对其进行隐式转换（如 perl 5.10.0 中的情况）。

`$scalar @array` 总是会将智能匹配分发到数组。它会尝试数组中的某个元素是否满足 `$scalar -- $element`。这是对旧行为的扩展，旧行为是测试数组是否包含该标量。

智能匹配运算符的完整分发表见 `perlyn` 中的“Smart matching in detail（智能匹配详情）”。

## 智能匹配与重载

根据基于最右侧参数类型进行分发的规则，当一个对象重载 `--` 出现在运算符的右侧时，重载程序始终会被调用（带有第 3 个参数作为真值，参见 `overload`）。然而，当对象出现在左侧时，只有当最右侧参数是简单标量时，才会调用重载程序。这样，智能匹配跨数组的分发性就不会被破坏，其他与复杂类型（代码、哈希、正则表达式）相关的行为也是如此。因此，智能匹配字符串化重载程序的编写者主要需要担心与标量进行比较，并可能涉及重载；其他常见情况将被自动一致地处理。

`--` 现在将拒绝在对象上工作（以避免依赖对象的底层结构）。（然而，如果对象重载了字符串化或数值化运算符，并且如果启用了 `overload fallback`，则将继续像往常一样使用它们。）

## 其他不兼容更改

许多 Unicode 属性的定义已发生更改，以匹配当前的 Unicode 标准。这些属性列在“Unicode overhaul（Unicode 大调整）”之上。此更改可能会破坏期望旧定义的代码。

`bookkeys` 已移动到哈希操作组。这破坏了二进制兼容性。

文件句柄（Filehandles）现在始终会被变为 `IO::File`。

之前的行为是：如果文件句柄被加载到内存中，则将其变为 `FileHandle`（一个空代理类），否则将其变为 `IO::Handle`。

`use feature :5.10*` 的语义发生了微调。更多信息请参见“Modules and Pragmatism（模块与实用主义）”。

Perl 开发者现在使用 `git` 而不是 `Perforce`。这应该是一个纯内部的更改，仅对核心开发人员相关。然而，你可能会因为该更改看到 perl 的细微差异。例如，在 `Test::Harness` 2.x 到 3.x 升级的一些细节中，实验性的 `Test::Harness::Straps` 模块已被移除。更多细节请参见“Modules and Pragmatism”。

作为 `ExtUtils::MakeMaker` 升级的一部分，`ExtUtils::MakeMaker::bytes` 和 `ExtUtils::MakeMaker::vmsish` 模块已从此发行版中移除。

`Module::CoreList` 不再包含 `%patchlevel hash 长度长度 undef 返回 undef`。

不支持的 C API 函数不再声明为 `static`，以防止泄漏到 Perl 的公共 API。

为了支持引导过程，`miniperl` 在构建时不再支持正则引擎的 UTF-8。

这允许构建在设置了 `PERL_UNICODE` 和 UTF-8 区域设置的情况下完成。如果没有这些，就会出现引导问题，因为 `miniperl` 无法加载正则引擎的 UTF-8 组件，因为这些组件没有被构建。

`miniperl` 的 `@INC` 现在仅限于 `-I...`、`$ENV{PERL5LIB}` 的分割以及 `"."`。在 `#line XXX` 指令后现在需要一个空格或换行符。

绑定文件句柄（Tied filehandles）现在有一个额外的方法 `EOF`，提供 `EOF` 类型。为了更好地匹配所有其他流控制语句，`foreach` 可能不再能作为属性使用。

Perl 的命令行开关 `-P` 已在 5.10.0 版本中弃用并被移除。可以使用 CPAN 模块 `Filter::cpp` 作为替代方案。

## 弃用 (DEPRECATIONS)

随着时间的推移，Perl 开发者发现必须弃用我们之前作为核心发行版部分发布的功能或模块。我们深知对 Perl 进行不向后兼容更改会为构建或维护 Perl 软件的开发者带来多大的痛苦和挫败感。你可以相信，当我们弃用某项功能或语法时，这不是我们轻率的决定。有时，我们选择弃用某些功能或语法是因为发现它们设计或实现得不佳。有时是因为它们阻碍了功能的实现或导致了性能问题。有时，原因更为复杂。在可能的情况下，我们会尝试在至少一个主要版本内以之前的形式为开发者保留弃用的功能。因此，只要一个弃用的功能没有积极干扰我们维护和扩展 Perl 的能力，我们会尽可能将其保留在那里。

以下项目现已被弃用：

- **superl**

`superl` 不再是 Perl 的一部分。它曾提供一种在不支持 `setuid` 权限的系统上模拟它的机制。

- **使用 "=" 表示属性列表**

Perl 解析器的一个意外导致这些构造体都是等价的：

```
my $spi := 4; my $spi = 4; my $spi : 4;
```

其中 `being` 被视为属性列表的开始，该列表在 `=` 之前结束。由于空格在此处不重要，所有这些都被解析为空的属性列表，因此上述内容等价于（且更好的写法是）：

```
my $spi = 4;
```

因为属性处理是针对空列表进行的。

事实如此，`that :=` 不能作为新标记使用，否则会在静默中更改现有代码的含义。因此，这种特定形式现在已标记弃用，并可能变成语法错误。如果绝对需要空属性列表（例如，由于代码生成器），请在 `=` 之前添加一个空格以避免警告。

- **UNIVERSAL->import()**

`UNIVERSAL->import()` 方法现已弃用。尝试向 `UNIVERSAL` 语句传递参数将导致弃用警告。

- **使用 "goto" 跳入构造**

使用 `goto` 从外部作用域跳转到内部作用域现已弃用。这种稀有的用法在实现上引起了问题。

- **\N{name} 中的自定义字符名称看起来像**

在 `\N{name}` 中，`name` 可以是任何内容。标准 Unicode 名称的范围非常有限，但自定义转换器可以创建完全由标点符号组成的名称。现在弃用创建不以字母开头且不包含字母数字以外其他字符的名称。由于 `\N` 增加了含义（参见 "\N experimental escape"），看起来像大括号包含的量词将失效。例如，`\n{3,4}` 现在意味着到 4 可能是。

## 弃用模块 (Deprecated Modules)

以下模块将在未来的版本中从核心移除，并应从 CPAN 安装。需要这些模块的 CPAN 发行版应将它们添加到依赖列表中。

如果你发布了打包版本的 Perl（作为更大系统的一部分），你应该仔细考虑核心弃用的影响。你可能希望考虑 `patch/deprecate.pm` 以提供针对你的打包系统或发行版的弃用警告，与你的打包系统或发行版管理从单个软件包提供功能的版本过渡到后期管理员需要安装多个软件包来获取该功能的阶段的方式保持一致。

你可以通过从 CPAN 安装相关模块来消除这些弃用警告。要安装所有模块的最新版本，只需安装 `Task::Deprecations_5_12`。

`Switch`

`Switch` 存在 Bug 应该被避免。你可能会发现 Perl 新的 `given/when` 特性是一个合适的替代。更多信息请参见 `perlyn` 中的“Switch statements”。

赋值给用于子程序中的 `:locked` 属性

带有 `attributes` pragma 的 `unique` 已不再是 Perl 公共 API 的一部分。调用它现在会产生弃用警告，并将在未来的版本中移除。它也被列为 API 的一部分，但从未文档化，且仅在 `to.c` 以及 5.10 之前的 `regcomp.c` 中使用。在核心中，它已被一个静态函数取代。

`Class::ISA`

`Pod::Plainer`

`Shell`

在 5.12.0 发布前的最终测试期间，几位开发者发现当前的生产代码使用了这些古老的库，其中一些位于 Perl 核心内部。因此，决策者（pumpking）准许了他们延缓执行。他们将在 5.14.0 版本中开始警告这些库将要弃用，并在 5.16.0 版本中将其移除。

## UNICODE 重构

Perl 开发者们共同努力更新 Perl 以与最新的 Unicode 标准保持同步。更改包括：

- Perl 现在可以处理每一个 Unicode 字符属性。新文档 `perluniprops` 包含了所有可非 Unicode 字符属性。默认情况下，Perl 不会暴露 `Unihan`、已弃用或 Unicode 内部属性。有关这些属性的更多细节请见下文；pod 中也有一部分列出了这些属性，并解释了为什么不向外暴露。

- Perl 现在完全支持在正则表达式中使用 `=` 和 `:` 的 Unicode 复合风格：`\p{property=value}` 和 `\p{property:value}`（两者含义相同）。

- Perl 现在完全支持对 `\p{...}` 构造内文本的松散匹配规则。此外，Perl 允许数字包含下划线。

- Perl 接受所有 Unicode 定义的属性和属性值的同义词。

`\X/` 匹配 Unicode 逻辑字符，已扩展以更好地支持各种亚洲语言。现在它被定义为扩展字形簇（`<>`）。之前匹配成功且符合逻辑的内容将继续被接受。此外：

```
\X 不会分割 CRLF 序列。
\X 不匹配包含 ZW 和 ZNJ 字符的序列。
\X 始终至少匹配一个字符，包括初始标记（mark）。标记通常位于基础字符之后，但在 Unicode 中它们可能孤立存在，\X 现在将处理这种情况，例如在行首或 ZWSP 之后。这部分是 `\X` 不再匹配那些以前认为不合逻辑的内容。例如，以前你可能会遇到带重音的 LF 这种无意义的情况。
\X 现在将匹配（韩语）Hangul 音节序列，以及泰语和老语的特殊情况。
```

否则，此更改对于不受影响的语言将是透明的。

使用 `Canonical_Combining_Class` 属性匹配的 `\p{...}` 在之前的 Perl 版本中是完全损坏的。它们现在应该正常工作。

在 Perl 5.12 之前，`Decomposition_Type=Compat` 属性与一个 Perl 扩展同名，这导致匹配了所有正确的值（其中一个有 100 多个错误，另一个有几千个）。Perl 扩展已重命名为 `Decomposition_Type=Noncanonical`（简写：`dt=noncan`）。它的含义与之前的预期相同，即所有非标准分解类型的并集，而 Unicode 兼容只是其中之一。

`\p(Decomposition_Type=Canonical)` 现在包含了 Hangul 音节。

`\p{Uppercase}` 和 `\p{Lowercase}` 现在按照 Unicode 标准规定的方式工作。

我们匹配的每个字符与以前匹配的几个相同。

`\p{Control}` 现在按照 `\p{Control}` 的方式匹配字符。这意味着它将不再匹配私用（`gc=co`）、代理（`gc=cs`）或格式（`gc=cf`）代码点。格式代码点代表了最大的问题。但所有 36 个中要么已正式弃用，要么被强烈建议不要使用。在这36个中，最可能被广泛使用的是软连字符（U+00AD）、以及 BOM、ZWSP、ZNJ、 WJ 以及类似字符，加上双向控制符。

`\p{Alpha}` 现在按照 `\p{Alphabetic}` 的方式匹配字符。在 5.12 之前，Perl 定义了一些并非真正 alpha 内容（所有标记），同时遗漏了许多属于 alpha 内容。`\p{Alnum}` 和 `\p{Word}` 的定义依赖于 Alpha 的定义并随之发生了变化。

`\p{Word}` 不再错误地将非单词字符匹配为分数。

`\p{Print}` 不再匹配行控制符：LT、LF、CR、FF、VT 和 NEL。这使其与标准和文档保持。

`\p{Digit}` 现在按照 `\p{Hex_Digit}` 的方式匹配字符。这意味着除了它匹配的字符 `[A-Fa-f0-9]` 外，它还会匹配 22 个全角等效字符，例如 U+FF10：FULLWIDTH DIGIT。

数字（Numeric）类型已扩展以包含 Unihan。

有一个 Perl 扩展属性名为 "Present_In"，或简写为 'In'。这是 Unicode Age 属性的扩展，但 `\p{In=5.0}` 匹配任何用途被确定为 Unicode 5.0set的代码点。`\p{Age=5.0}` 仅匹配在 5.0 版本精确添加的代码点。

许多属性对未分配代码点有了正确的值。受影响的属性有 `Bidi_Class`、`East_Asian_Width`、`Joining_Type`、`Decomposition_Type`、`Hangul_Syllable_Type`、`Numeric_Type` 和 `Line_Break`。

`Default_Ignorable_Code_Point`、`ID_Continue` 和 `ID_Start` 属性符合当前的 Unicode 定义。

早期版本的 Perl 错误包含了某些应该是 Unicode 内部使用的属性。现在在正则表达式中使用这些属性将产生弃用警告信息（启用）。这些属性是：`Other_Alphabetic`、`Default_Ignorable_Code_Point`、`ID_Continue`、`ID_Start`、`Other_Grapheme_Extend`、`Other_Lowercase`、`Other_Math` 和 `Other_Uppercase`。

## Updated Pragma

## MODULES PRAGMATA

## Updated Pragma

从版本 0.74 升级到 0.82。

## warnings

`warnings` 有了一个新的 `warnings ::fatal_enabled()` 函数。它还包含一个新的 `illegalproto` 警告类别。有关此更改，请参见“新或更改的诊断”。

从版本 1.06 升级到 1.09。

## 更新的模块

- `Archive::Extract`

从版本 0.24 升级到 0.38。

- `Archive::Tar`

从版本 1.38 升级到 1.54。

- `Attribute::Handlers`

从版本 0.79 升级到 0.87。

- `AutoLoader`

从版本 5.63 升级到 5.70。

- `B::Concise`

从版本 0.74 升级到 0.78。

- `B::Debug`

从版本 1.05 升级到 1.12。

- `B::Deparse`

从版本 0.83 升级到 0.96。

- `B::Lint`

从版本 1.09 升级到 1.11_01。

- `CGI`

从版本 3.29 升级到 3.48。

- `Class::ISA`

从版本 0.33 升级到 0.36。

> 注意：`Class::ISA` 已弃用，并可能在未来的 Perl 版本中移除。

- `Compress::Raw::Zlib`

从版本 2.008 升级到 2.024。

- `CPAN`

从版本 1.9205 升级到 1.94_56。

- `CPANPLUS`

从版本 0.84 升级到 0.90。

- `CPANPLUS::Dist::Build`

从版本 0.06_02 升级到 0.46。

- `Data::Dumper`

从版本 2.121_14 升级到 2.125。

- `DB_File`

从版本 1.816_1 升级到 1.820。

- `Devel::PPPort` 版本 3.13 升级到 3.19。

- `Digest`

从版本 1.15 升级到 1.16。

- `Digest::MD5`

从版本 2.36_01 升级到 2.39。

- `Digest::SHA`

从版本 5.45 升级到 5.47。

- `Encode`

从版本 2.23 升级到 2.39。

- `Exporter ExtUtils::CBuilder`

从版本 5.62 升级到 5.64_01。

- `ExtUtils::Command`

从版本 0.21 升级到 0.27。

- `ExtUtils::Constant`

从版本 1.13 升级到 1.16。

- `ExtUtils::Install`

从版本 0.2 升级到 0.22。

- `ExtUtils::Maker`

从版本 1.44 升级到 1.55。

- `ExtUtils::Manifest`

从版本 6.42 升级到 6.56。

- `ExtUtils::ParseXS`

从版本 1.51_01 升级到 1.57。

- `File::Fetch`

从版本 2.18_02 升级到 2.21。

- `File::Path`

从版本 0.14 升级到 0.24。

- `File::Temp`

从版本 2.04 升级到 2.08_01。

- `Filter::Simple`

从版本 0.18 升级到 0.22。

- `Filter::Util::Call`

从版本 0.82 升级到 0.84。

- `Getopt::Long`

从版本 1.07 升级到 1.08。

- `IO`

从版本 2.37 升级到 2.38。

- `IO::Zlib`

从版本 1.23_01 升级到 1.25_02。

- `IPC::Cmd`

从版本 1.07 升级到 1.10。

从版本 0.40_1 升级到 0.54。

- `IPC::SysV`

从版本 1.05 升级到 2.01。

- `Locale::Maketext`

从版本 1.12 升级到 1.14。

- `Locale::Maketext::Simple`

从版本 0.18 升级到 0.21。

- `Log::Message`
