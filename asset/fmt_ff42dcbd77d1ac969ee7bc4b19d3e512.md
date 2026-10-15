
返回分组匹配的文本。如果没有指定分组，则返回整个匹配项。如果给出分组数字或名称，则返回该分组匹配的文本。如果分组不存在，则抛出 `IndexError`。

```
m.groups([default])
```

返回包含所有分组匹配文本的元组。如果没有指定参数，则返回空元组。

```
m.groupdict([default])
```

返回一个包含匹配所有命名子分组的字典。如果没有指定参数，则返回空字典。

```
m.start(group)
m.end(group)
```

两个方法返回匹配分组的子字符串的起始和结束索引。如果省略分组，则使用整个子字符串。如果分组未参与匹配，则返回 `None`。

```
m.span(group)
```

返回一个二元组 `(m.start(group), m.end(group))`。如果分组未参与匹配，则返回 `(None, None)`。如果省略分组，则使用整个子字符串。

```
m.pos
```

传递给 `search()` 或 `match()` 函数的 `pos` 值。

```
m.endpos
```

传递给 `search()` 或 `match()` 函数的 `endpos` 值。

```
m.lastindex
```

最后匹配的分组的数值索引。如果没有匹配任何分组，则为 `None`。

```
m.lastgroup
```

最后匹配的分组名称。如果没有匹配命名分组或模式中不存在命名分组，则为 `None`。

```
m.re
```

产生此 `MatchObject` 实例的 `match()` 或 `search()` 方法的正则表达式对象。

```
m.string
```

传递给 `match()` 或 `search()` 的字符串。

# 示例

以下示例展示了如何使用 `re` 模块在字符串中搜索、提取数据并替换文本模式。

```
import re
text = "Gu will be out of the office from 12/15/2012 - 1/3/2013."

# 一个用于日期的正则模式。
datepat = re.compile('\(\d+)/(\d+)/(\d+)')

# 查找并打印所有日期
for m in datepat.finditer(text):
    print(m.group())
```

由于你提供的原文包含大量的 OCR（光学识别）错误导致的重复和损坏，我已作为高级文档工程师为你过滤了冗余部分，并对核心技术内容进行了准确的翻译和格式化处理。

## string 287

```python
# 查找所有日期，但以不同的格式打印
monthnames = [None, 'Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
              'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
for m in datetime.finder(text):
    print("%s %s, %s" % (monthnames[int(m.group(1))], m.group(2), m.group(3)))
```

```python
# 将所有日期替换为欧洲格式（日/月/年）
def fix_date(text):
    return "%s/%s/%s" % (m.group(2), m.group(1), m.group(3))
newtext = datepat.sub(fix_date, text)
```

```python
# 另一种替换方式
newtext = datepat.sub(r'\d/\d/\d', text)
```

# Notes

- 关于正则表达式理论和实现的详细信息，可以在编译器构造相关的教科书中找到。Jeffrey Friedl 编写的书籍《Mastering Regular Expressions》（O'Reilly & Associates, 1997）可能也会帮助。
- 使用 `re` 模块最困难的部分是编写正则表达式模式。编写模式时，可以考虑使用如 Kodos (`http://kodos.sourceforge.net`) 等工具。

# string

`string` 模块包含了许多用于处理字符串的常量和函数。它还包含了用于实现新字符串格式器的类。

## Constants

以下常量定义了各种字符集，这些集合在各种字符串处理操作中可能有用。

| 常量 | 说明 |
|---|---|
| `ascii_letters` | 包含所有小写和大写 ASCII 字母的字符串。 |
| `ascii_lowercase` | 字符串 'abcdefghijklmnopqrstuvwxyz'。 |
| `ascii_uppercase` | 字符串 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'。 |
| `digits` | 字符串 '0123456789'。 |
| `hexdigits` | 字符串 '0123456789abcdefABCDEF'。 |
| `letters` | 小写和大写字母的拼接。 |
| `lowercase` | 包含当前区域设置下特定小写字母的字符串。 |
| `octdigits` | 字符串 '01234567'。 |
| `punctuation` | ASCII 标点符号字符字符串。 |
| `printable` | 可打印字符字符串——字母、数字、标点和空白字符的组合。 |
| `uppercase` | 包含当前区域设置下特定大写字母的字符串。 |
| `whitespace` | 包含所有空白字符的字符串。这通常包括空格、制表符、换行符、返回、分页和垂直制表符。 |

注意，这些常量某些（例如 `letters` 和 `uppercase`）会取决于系统的区域设置。

## Formatter Objects

字符串的 `str.format()` 方法用于执行高级的字符串格式化操作。如第 3 章“类型与对象”和第 4 章“运算符与表达式”所示，它可以访问字符串或映射的项、对象的属性以及其他相关操作。`string` 模块定义了一个 `Formatter` 类，可用于实现你自定义的格式化操作。该类暴露了实现字符串格式化操作的各个部分，并允许对其进行自定义。

```python
Formatter()
```

创建一个新的 `Formatter` 实例。`Formatter` 实例支持以下操作。

```python
f.format(format_string, *args, **kwargs)
```

格式化 `format_string`。默认情况下，输出与调用 `format_string.format(*args, **kwargs)` 相同。例如 `f.format("{name} is {0:d} years old", 39, name="Dave")` 会创建字符串 "Dave is 39 years old"。

```python
f.vformat(format_string, args, kwargs)
```

一个实际执行 `f.format()` 工作的方法。`args` 是位置参数的元组，`kwargs` 是关键字参数的字典。如果你已已经在元组和字典中捕获了参数信息，使用此方法速度更快。

```python
f.parse(format_string)
```

创建一个用于解析格式化字符串 `format_string` 内容的迭代器。`format_string` 遍历字符串并产生 `(literal_text, field_name, format_spec, conversion)` 元组。`literal_text` 是紧接括号 `{ ... }` 中指定的下一个格式之前的任何字面文本。如果没有前导文本，它可能为空字符串。`field_name` 是指定格式指定符中字段名的字符串。如果指定符为 `'{0:d}'`，则字段名是冒号后面出现的格式指定符 `'d'`（如上例所示）。如果未指定，它将为空字符串。`conversion` 是包含转换器（如果有）的字符串。在上例中，它是 `None`，但如果指定符为 `'{0:s:d}'`，它将是 `'s'`。`field_name`、`format_spec` 和 `conversion`。

```python
f.get_field(fieldname, args, kwargs)
```

从 `args` 和 `kwargs` 中提取与 `fieldname` 关联的值。`fieldname` 是由所示 `parse()` 方法返回的字符串如 "0" 或 "name"。返回一个元组 `(value, key)`，其中 `value` 是字段值，`key` 用于在 `args` 或 `kwargs` 中定位该值。如果 `key` 是整数，则是 `args` 中的索引。如果是字符串，则用于 `kwargs`。`fieldname` 可能包含额外的索引和属性查找，例如 `'.0.name'` 或 `'0[name]'`。在这种情况下，

```
struct 291
```
