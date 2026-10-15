
这个示例展示了三点内容：

- 1. 你可以将模式存储在变量中，然后将这些变量传递给 `string match` 函数。这有助于改进程序文档并保持源代码的整洁。
- 2. 你不需要显式地测试你正在查找的整个单词。这个示例使用了模式 `*log*`，允许用户在指定选项时具有灵活性。因此，以下字符串将匹配：`turn_log_on`, `logging_on` 和 `log_on`。
- 3. 你可以使用 `string tolower` 函数来消除需要同时检查大写和小写模式的问题。

如果在 `options` 变量中找到了 `log_on=true` 模式，则 `is_logging_set` 的值为 1；否则，它的值为 0。

## regexp 函数

`regexp` 函数的工作原理与 Perl 中的 `m//` 函数几乎完全相同。它允许比 `string match` 函数更丰富的元字符。表 8.17 列出了 `regexp` 函数使用的元字符。

### 表 8.17 Tcl regexp 函数的元字符

| 元字符 | 元含义 |
| :--- | :--- |
| `^` | 这个元字符——脱字符（caret）——匹配字符串的开头。它是两个模式锚点之一——另一个锚点是 `$` 元字符。 |
| `.` | 这个元字符——点（period）匹配任何字符。 |
| `$` | 这个元字符匹配字符串的结尾。它是两个模式锚点之一——另一个锚点是 `^` 元字符。 |
| `|` | 这个元字符——称为分支（alternation）允许你指定两个可以使匹配成功的值。例如，`*alb*` 意味着目标变量必须包含 `*a*` 或 `*b*` 字符匹配才能成功。 |
| `[]` | 方括号允许你创建一个字符类。例如，如果目标字符串中包含 `*a*`、`*b*` 或 `*c*` 中的任何一个，则 `[abc]` 求值为真。 |
| `()` | 括号允许你影响模式求值的顺序，并作为模式内存的形式。 |
| `*` | 星号量符强制前一个组件匹配零或多次。 |
| `+` | 加号量符强制前一个组件匹配一次或多次。 |
| `?` | 问号量符强制前一个组件匹配零或一次。 |

表 8.17 中的所有元字符都与 Perl 的元字符具有相同含义。我不会在本节中重复相同的材料，我将重点关注 `regexp` 函数的不同之处。

`regexp` 函数使用此语法：
`regexp ?switches? pattern target ?match? ?subMatch ...?`
`regexp` 有三个可用的开关：

- `-nocase` 此选项导致目标中的大写字符被视为小写字符。
- `-indices` 此选项影响 `match` 和 `subMatch` 变量。`match` 和 `subMatch` 变量不再包含匹配的实际文本，而是包含匹配文本的起始和结束索引的列表。
- `--` 此选项（两个破折号）表示没有更多选项了。如果你的模式以破折号开头，这将非常有用。

如果可以匹配模式，`regexp` 函数返回 1，如果不能则返回零。
如果指定了 `match` 变量，它将被赋值为匹配模式的文本。如果使用了 `-indices` 选项，`match` 变量包含匹配文本的起始和结束索引。例如：

```
% tcl
tcl>set target "Time and Again"
tcl>regexp "^(.)" $target match
1
tcl>puts $match
T
```

`match` 变量被赋值为 `T` 是因为 `^-` 模式匹配了目标的第一个字符。
如果指定了 `subMatch` 变量，它们将被赋值为任何匹配括号内子表达式的文本。如果使用了 `-indices` 选项，`match` 变量包含匹配文本的起始和结束索引。例如：

```
% tcl
tcl>set target "Time and Again"
tcl>regexp "^(.)" $target match subMatch1 subMatch2
1
tcl>puts $match
T
tcl>puts $subMatch1
T
tcl>puts $subMatch2
i
```

让我们快速看一个使用 `-indices` 选项的示例：

```
% tcl
tcl>set target "Time and Again"
tcl>regexp -indices {^.} $target match
1
tcl>puts $match
0
```

你可以为 `regexp` 的 `match` 和 `subMatch` 参数使用任何变量名。在这些示例中使用 `.match` 和 `subMatch` 仅仅是为了区分返回的两种值。

## regsub 函数

`regsub` 函数用于替换文本中的模式。它使用与 `regexp` 函数列表相同的元字符。请参阅表 8.17 以获取 `regsub` 函数可用的元字符列表。

`regsub` 函数使用此语法：
`regsub ?switches? pattern target replacement`
`regsub` 有三个可用的开关：

- `-nocase` 此选项导致目标中的大写字符被视为小写字符。
- `-all` 此选项替换模式的所有实例，而不仅仅是第一个。
- `--` 此选项（两个破折号）表示没有更多选项了。如果你的模式以破折号开头，这将非常有用。

如果可以匹配模式，`regsub` 函数返回 1，如果不能则返回零。
如果指定了 `match` 变量，它将被赋值为匹配模式的文本。如果使用了 `-indices` 选项，`match` 变量包含匹配文本的起始和结束索引。

## 总结

让我们看一个 `regsub` 的简单示例：

```
% tcl
tcl>set target "Time and Again"
tcl>regsub "^(.)" $target match
1
tcl>puts $match
T
```
