
```perl
$decomposed_string = decompose($string, [$useCompatMapping]),
reordered_string = reorder($string), $composed_string = compose($string), ($processed, $unprocessed) = splitOnLastAfter($normalized), $processed = normalize_partial($form, $unprocessed), $processed = NFD_partial($unprocessed), $processed = NFC_partial($unprocessed), $processed = NFKD_partial($unprocessed), $processed = NFKC_partial($unprocessed)
```

# 快速检查

```perl
$result = checkNFD($string), $result = checkNFC($string), $result = checkNFKD($string), $result = checkNFKC($string), $result = checkFCD($string), $result = checkFCC($string), $result = check($form_na, $string)
```

# 字符

```perl
$canonical_decomposition = getCanon($code_point),
$compatibility_decomposition = getCompat($code_point),
$code_point_composite = getComposite($code_point_here, $code_point_next), coining_class = getCoinClass($code_point),
$may_be_composed_with_prev_char = isComp($code_point), $is_exclusion = isExclusion($code_point), $is_singleton = isSingleton($code_point), $is_non_decomposition = isNonDecomp($code_point), $is_Full_Composition_Exclusion = isComp($code_point), $NFD_partial($unprocessed) = NFD_partial($unprocessed), $NFC_partial($unprocessed) = NFC_partial($unprocessed), $NFKD_partial($unprocessed) = NFKD_partial($unprocessed), $NFKC_partial($unprocessed) = NFKC_partial($unprocessed)
```

以下变量的作用方式有所不同：

```
Awk Perl scalar @ARGV ARGV[0] FILENAME
$ARGV FNR $ - FS (whatever you like) NF $Fld, or so such NR
$. OFMT # OFS $, ORS \ RL length(&$) RS $/ RSTART length(`
```

你不能对 `$RS` 使用模式，只能使用字符串。

当有疑问时，运行 `awk` 构建 `-a 2p` 并查看其输出。

## C/C++ 陷阱

严谨的 C 和 C++ 程序员应该注意以下几点：

- `if` 和 `while` 必须使用大括号。
- 必须使用 `elsif` 而不是 `else if`。
- C 语言中的 `break` 和 `continue` 关键字在 Perl 中分别变为 `last` 和 `next`。
- 与 C 不同，这些关键字在 `{ }` 结构内部不起作用。请参考 perlyn 中的“Loop Control”。
- `switch` 语句被称为 `given/when`，且仅在 Perl 5.0 或更高版本中可用。
- perlyn 中的“Switch Statements”。
- Perl 中的变量以 `$`、`*` 或 `//` 开头。在大多数正则表达式或定义或运算符下，可能会将 C/C++ 注释解释为除法运算符。
- 你无法获取任何内容的地址，尽管 Perl 中有一个类似的运算符是反斜杠 `\`，它会创建一个引用。
- `ARGV` 是大写的。`$ARGV[0]` 相当于 C 语言的 `argv[1]`，`ARGV[0]` 以此结尾。
- 系统调用如 `link()`、`unlink()`、`rename()` 成功返回非零，失败返回 0。
- 然而，`system()` 成功时返回零。
- 信号处理器处理的是信号而不是数字。使用 -1 来查找与我们的系统对应的信号。

## JavaScript 陷阱

谨慎的 JavaScript 程序员应该注意以下几点：

- 在 Perl 中，二进制 `+` 始终是加法。`$string1 + $string2` 会将两个字符串转换为数字并相加。要拼接两个字符串，请使用 `.` 运算符。
- 一元运算符 `+` 在 Perl 中不适用。它的存在是为了避免语法歧义。
- 与 `for...in` 不同，Perl 的 `for`（也写成 `foreach`）不允许左侧为任意表达式。它必须是一个变量：

```
for my $variable (keys %hash) { ... }
```

- 此外，不要忘记其中的键，因为 `foreach my $kv (%hash)` 会遍历键和值，这通常没有用处（`$kv` 将会是一个键，然后是值，依此类推）。
- 要遍历数组的索引，请使用 `my $i (0 .. $#array) {}`。
- `foreach my $v (@array) {}` 遍历值。
- Perl 要求在 `for`、`while`、`foreach` 等后面加上大括号。
- 在 Perl 中，`else if` 写为 `elsif`。
- `? :` 的优先级高于赋值。在 JavaScript 中，可以写成：

`condition ? do_something() : variable = 3`

当条件为假时才会给变量赋值。在 Perl 中，你需要括号。

```perl
$condition ? do_something() : ($variable = 3);
```

- 或者直接用 `if`。
- Perl 要求用分号分隔语句。
- 使用 `my` 声明的变量只影响声明之后的代码。你不能写 `$x = 1; my $x;` 并让第一次赋值影响该变量。相反，它会赋值给之前外部作用域中的 `$x` 或全局变量。
- 注意，该变量在后续语句之前是可见的。这意味着在 `my $x = 1 + $x` 中，第二个 `$x` 指的是之前声明的那个。
- `my` 变量的作用域是块，而不是当前函数。如果你写 `{my $x}; $$;`，第二个 `$` 指的不是块内部声明的那个。
- 对象的存在无法作为变量访问。`with(object) { method() }` 最接近的 Perl 等价物是 `for`，它将 `$_` 别名为该对象：

`for($object) { $_->method(); };`

- 调用方法的对象或类将作为方法的参数之一传递，而不是作为一个独立的值。

## Sed 陷阱

## Shell 陷阱

精明的 Shell 程序员应该注意以下几点：

- 反引号运算符在进行变量插值时，不考虑命令中是否存在单引号。
- 与 `csh` 不同，反引号运算符不对返回值进行翻译。
- Shell（尤其是 `csh`）会对每行命令执行多个层级的替换。Perl 只在某些结构（如双引号、反引号、角括号和搜索模式）中进行替换。Shell 逐部分解释脚本。Perl 在执行之前会编译整个程序（BEGIN 块除外，它们在编译时执行）。参数通过 `@ARGV` 获取，而不是 `$1`、`$2` 等。环境变量不会自动作为独立的标量变量。Shell 的测试使用 `=`、`!`、`!=` 进行字符串比较，使用 `-eq`、`-ne`、`-lt` 进行数值比较。这与 Perl 相，Per 使用 `eq`、`ne`、`lt` 进行字符串比较，使用 `==`、`!=`、`<` 进行数值比较。

## Perl 陷阱

经验丰富的 Perl 程序员应该注意以下几点：

- 注意许多操作在列表上下文中的行为与在标量上下文中不同。详见 perdata。
- 尽可能避免裸字（bareword），特别是全小写的裸字。
- 你无法通过肉眼判断一个裸字是函数还是字符串。通过在函数调用时使用字符串和括号，你就永远不会混淆。
