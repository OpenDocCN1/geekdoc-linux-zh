
```perl
$insert = "AAA";

s{

($char) # 查找指定的

 # 字符。

(?-$char) # 再次查找它，但不包含

 # 匹配到的

 # 字符串，以便下次搜索

 # 也能找到它。

}

$char .$insert # 将指定的

 # 字符与要插入的

 # 字符串拼接

}lex: | 使用扩展模式，评估

 # 替换模式并

 # 匹配所有可能的字符串。

print("\n");
```

此示例使用扩展模式直接在正则表达式内部添加注释。这使得注释能够直接与特定的模式元素联系起来。匹配模式并没有直接反映最初设定的“在两个重复字符之间插入字符串”的目标。相反，示例被静静地重新表述了。新的目标是：如果 `$char` 后面紧跟着 `$char`，则将所有的 `$char` 实例替换为 `$char`（例如将 `$insert` 变量附加到 `$char` 变量之后）。如你所示，结果是相同的。记住，有时你需要跳出框架。

## 表 8.12 Perl 替换运算符示例（续）

| 我该如何... | 答案 |
|--- | --- |
| 在替换模式中执行两层变量替换： | `s/(\w+)/$1/egeg;` 这是一个二级变量插值的简单示例。如果 `\$firstVar = "AAA"` 且 `$\$ = '\$firstVar$`，那么在进行两次替换后 `\$` 将等于 AAA。关键在于替换模式被评估了两次。这种技术非常强大，它可以用于开发带有变量插值的错误消息。

```perl
$errMsg = "File too large";
$fileName = "DATA.OUT";
$_ = 'Error: $errMsg for the file named $fileName';
s/(\w+)/$1/eg;
print;
```

运行此程序时，它会显示：
Error: File too large for the file named DATA.OUT
`$errMsg` 和 `$fileName` 变量的值根据需要插值到替换模式中。 |

表 8.13 显示了如何使用替换运算符。

## 表 8.13 替换运算符示例

| 我该如何... | 答案 |
|--- | --- |
| 统计给定字母在字符串中出现的次数： | `$cnt = tr/Aa//;`

执行此语句后，`$cnt` 存储字母 a 在 `_` 中出现的次数。`tr` 运算符没有忽略字符串大小写的选项，因此需要指定大写和小写。 |
| 关闭每个字符的高位位： | `tr [ -7];`

此语句使用方括号来分隔字符列表。注意，括号对之间可以使用空格来增强可读性。八进制值用于指定字符范围——创建一个简单的查找表可以进行替换。 |

表 8.14 包含了 `split` 函数的一些示例。有关 `split` 函数的详细信息，请参阅 Perl 文档。

## 表 8.14 `split` 函数示例

| 我该如何... | 答案 |
|--- | --- |
| 将字符串拆分为单词： | 
```
s/^\s+//
@array = split;
```

执行此语句后，`@array` 是一个单词数组。在拆分字符串之前，需要移除开头的空白。如果不这样做，`split` 将创建一个空白作为第一个元素的数组，这可能不是你想要的。 |

### 表 8.14 `split` 函数示例（续）

| 我该如何... | 答案 |
|--- | --- |
| 将 `$line` 中的字符串拆分为单词： | 
```
s/\s+//
@array = split(/\W/, $line);
```

执行此语句后，`@array` 是一个单词数组。 |
| 将字符串拆分为字符： | `@array = split('');` 执行此语句后，`@array` 是一个字符数组。`split` 识别空模式作为字符分隔符。 |
| 根据分隔符将字符串拆分为字段： | `@array = split(/:/);` 执行此语句后，`@array` 包含分隔符之间的值——在本例中分隔符是冒号。如果存在重复的分隔符（例如 `"::"`），会创建一个空元素。使用 `/+/` 作为分隔符可以消除空元素。 |

## Tcl

正则表达式在 Tcl 中四主要用途：

- `glob` 函数——用于查找匹配模式的文件。
- `string match` 函数——用于查找匹配模式的文本。
- `regexp` 函数——用于查找匹配模式的文本。`regexp` 比 `string match` 拥有更强大的元字符。
- `regsub` 函数——用于替换匹配模式的文本。

这些函数在各自的章节中都有描述。

## `glob` 函数

`glob` 函数是创建匹配模式的文件列表的一种方法。列表 8.4 显示了如何处理目录中的所有文件（对比列表 8.2）。

## 列表 8.4 tcl_glob——使用 Tcl glob 命令处理目录中的所有文件

```tcl
#!/usr/bin/tcl

foreach file [glob *] {

  puts "$file is being processed."

}
```

该脚本的使用示例：

```tcl
% chmod +x tcl_glob

% ls

foo.c  bar.c  david

% ./tcl_glob

foo.c is being processed.

bar.c is being processed.

david is being processed.
```

`glob` 函数接受多个模式作为参数。列表 8.5 显示了如何创建 project_a 和 project_b 目录以及当前目录下的所有文本文件列表。

## 列表 8.5 tcl_glob_multi——使用带有多个模式的 Tcl glob 命令

```tcl
#!/usr/bin/tcl

set filelist [glob {project_a,b}/*.txt]

puts $filelist
```

该脚本的使用示例：

```tcl
% chmod +x tcl_glob_multi

% ./tcl_glob_multi

project_a/one.txt  project_b/two.txt readme.txt
```

此示例在模式周围使用大括号以避免 Tcl 的命令替换。事实上，将模式包含在大括号中是一个好主意。

表 8.15 列出了 `glob` 函数使用的元字符。

## 表 8.15 Tcl `glob` 函数的元字符

| 元字符 | 含义 |
| --- | --- |
| `?` | 问号匹配任意单个字符。 |
| `*` | 星号匹配任意或多个字符。 |
| `[ ]` | 方括号创建一个字符列表。方括号内的所有字符都用于匹配或不匹配单个字符。例如，`[xyz]` 匹配 x、y 或 z，但不匹配 xx 或任何其他组合。无论列表中有多少个字符，字符列表都只匹配单个字符。你可以使用 `[a-e]` 作为 `[abcd]` 的简写。 |
| `{}` | 大括号用于模式扩展。例如，`x(y,z)` 匹配 xy 或 xz，而不匹配其他文本。它在处理目录时非常有用。 |

### `string match` 函数

当你只需要在某些文本中找到基本模式时，可以使用 `string match` 函数。它使用的元字符与 Bash 用于文件名的使用的几乎相同。表 8.16 列出了你可以与 `string match` 函数使用的元字符。

`string match` 函数通常被用作 `if` 语句中条件表达式的一部分：

```tcl
if [string match (f*|$file)] (

  puts "$file starts with an f"

)
```

你也可以将 `string match` 函数的返回值赋值给变量：

```tcl
set options "color, fixed, logging, maxsize"

set pattern "*log*"

set options_lc [string tolower $options]

set is_logging_set [string match $pattern $options_lc]
```
