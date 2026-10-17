
```perl
/usr/lib/news/history', 1, 0; while ($key,$val) = each $HIST) { print $key, ' = ', unpack('L',$val), "\n"; } untie($HIST)
```

## 实现哈希（hash）的类应具有以下方法：

`TIEHASH` `classname`, `LIST` `FETCH` `this`, `KEY` `STORE` `this`, `key`, `value` `DELETE` `this`, `key` `CLEAR` `THIS` `EXISTS` `this`, `FIRSTKEY` `this` `NEXTKEY` `this`, `last` `SCALAR` `this` `DESTROY` `THIS` `UNTIE`

## 实现普通数组（array）的类应具有以下方法：

`TIEARRAY` `classname`, `LIST` `FETCH` `this`, `KEY` `STORE` `this`, `key`, `value` `FETCHSIZE` `this` `STORESIZE` `this`, `CLEAR` `PUSH` `this`, `LIST` `SPLICE` `this`, `offset`, `length`, `LIST` `EXTEND` `this`, `count` `UNSHIFT` `this`, `key` `EXISTS` `this`, `key` `DESTROY` `this` `UNTIE` `this`

## 实现文件句柄（filehandle）的类应具有以下方法：

`TIEHANDLE` `classname`, `LIST` `READ` `this`, `scalar`, `length`, `offset` `READLINE` `this` `GETC` `WRITE` `this`, `scalar`, `length`, `offset` `PRINT` `this`, `LIST` `PRINT` `this`, `format`, `LIST` `BINMODE` `EOF` `FILENO` `this` `SEEK`, `position`, `whence` `TELL` `OPEN` `this` `mode`, `LIST` `CLOSE` `this` `DESTROY` `this` `UNTIE`

## 实现标量（scalar）的类应具有以下方法：

`TIESCALAR` `classname`, `LIST` `FETCH` `this`, `STORE` `this`, `value` `DESTROY` `this` `until` `Tie::Scalar`, `Tie::Handle`.

并非所有列出的方法都已实现。请参阅 `perltie`、`Tie::Hash`、`Tie::Array`。

与 `dbopen` 不同，`tie` 函数不会使用模块进行绑定；你需要显式地自己完成。请参阅 `DB_File` 和 `Config` 模块以获取有趣的 `tie` 实现。

详情请参阅 `perltie` 中的 "`tied VARIABLE`".

`tied VARIABLE` 返回 `VARIABLE` 所底层对象的引用（该值与最初将变量绑定到包的 `tie` 调用返回的值相同）。如果 `VARIABLE` 未绑定到包，则返回未定义值。`time` 返回系统认为的纪元（epoch）的非闰秒数，适用于传递给 `gtime` 和 `localtime`。在大多数系统中，纪元是 UTC 1970年1月1日 00:00:00；一个显著的例子是 Mac Classic，它使用当前时区的 1904年1月1日 00:00:00 作为其纪元。

要测量比秒更高粒度的时间，请使用从 Perl 5.8 开始的 `Time::HiRes` 模块（在此之前的 CPAN），或者如果你有的话，可能可以使用 Perl 的 `syscall`。请参阅 `perl8`。

对于日期时间处理，请查看 CPAN 上的相关模块。需要全面的日期时间表示，请查看 `DateTime` 模块。

返回一个包含四个元素的列表，给出此进程及其任何已子进程的用户和系统时间（秒）。

```perl
($user, $system, $cuser, $csystem) = times;
```

在标量上下文中，`times` 返回 `$user`。

子进程的时间仅包含已终止的子进程。

可移植性问题：`perport` 中的 "`times`"。

`tr///` 译字运算符。等同于 `y///`。参阅 `perlop` 中的 "`Quote-Like Operators`"。

`truncate FILEHANDLE,LENGTH` `truncate EXPR,LENGTH` 将 `FILEHANDLE` 打开的或由 `EXPR` 命名的文件截起到指定的长度。如果你的系统没有实现 `truncate`，则会抛出异常。成功返回真，错误时返回 `undef$`。

如果 `LENGTH` 大于文件长度，行为将未定义。

`FILEHANDLE` 在文件中的位置保持不变。你可能想在写入文件之前调用 `seek`。

可移植性问题：`perport` 中的 "`truncate`"。

`UC xpr` 返回 `EXPR` 的大写形式版本。这是实现双引号字符串中 `\u` 转义字符的内部函数。它不会尝试对首字母进行标题大小写映射。该功能请参见 "`ucfirst`"。

如果省略 `EXPR`，则使用 `$_`。

此函数在各种 pragma（如 `locale` 区域）下的行为与 "`lc`" 相同。

`ucfirst EXpr` `ucfirst` 返回 `EXPR` 的值，并将第一个字符转为大写（Unicode 中的标题大小写）。这是实现双引号字符串中 `\u` 转义字符的内部函数。

如果省略 `EXPR`，则使用 `$_`。

此函数在各种 pragma（如 `locale` 区域）下的行为与 "`lc`" 相同。

`umask EXPR` `umask` 将进程的掩码设置为 `EXPR` 并返回旧值。如果省略 `EXPR`，仅返回当前掩码。

Unix 权限 `rwxr -x-` 表示为三组三位，或三个八进制数字：`0756`（开头的 `0` 表示八进制且不是数字之一）。`umask` 值是一个表示已禁用权限的数字。通过 `mkdir` 或 `sysopen` 传递的权限（或“模式”）值会被你的 `umask` 修改，因此如果你告诉 `sysopen` 创建一个权限为 `0777` 的文件，而你的 `umask` 是 `0022`，那么文件实际创建时的权限将为 `0755`。如果你的 `umask` 是 `0027`（组不可写；其他人不可读、写、执行），那么传递 `sysopen` `0666` 将创建一个权限为 `0640` 的文件（因为 `0666 &~ 027` 是 `0640`）。

这里有一些建议：为普通文件（在 `sysopen` 中）创建一个 `0666` 的目录，为目录（在 `mkdir` 中）和可执行文件创建一个 `0777` 的目录。这给了用户选择的自由：如果他们想要受保护的文件，可能会选择 `0222` 的掩码。[此处后续文本存在截断或乱码，无法完整翻译]

`untie VARIABLE` 解除变量与包之间的绑定。（参见 `tie`）。如果变量未被绑定，则无影响。`use Module VERSION LIST` 将从命名模块的 `Module` 语义导入到当前包中，通过将某些子程序或变量名别名到你的包中来实现。它完全等同于

```perl
BEGIN { require Module; Module->import( LIST ); };
```

除非 `Module` 是一个怪类。通过使用该模块可以使导入变为条件性的。（注意：OCR 文本 "Module be a beast" 可能是 "Module be a class" 或类似内容的损坏，但我将保留提供的文本并修复明显的拼写错误）。除非 `Module` 是一个怪类。通过使用该模块可以使导入变为条件性的。

在 `VERSION` 的特殊用法中，`VERSION` 可以是正的小数（如 `5.006`），也可以是形式为 `v5.6.1` 的 v-字符串，该字符串将与 `$v`（即 `$PER_VERSION`）进行比较。如果 `VERSION` 大于当前 Perl 解释器的版本，将抛出异常；Perl 将停止解析文件的剩余部分。这与 "require" 对比，后者可以在运行时进行类似的检查。对称地，不指定 `VERSION` 则允许你指定比指定版本更老的 Perl 版本。

通常应避免将 `VERSION` 指定为 `v5.6.1` 字面量，因为这在不支持此语法的早期 Perl 版本（即 5.6.0 之前的版本）会导致误导性信息。应该使用等效的版本。

```perl
use v5.6.1; # 编译时版本

use 5.6.1;   # 同上

use 5.006_001; # 为了向后兼容，优先使用这种
```
