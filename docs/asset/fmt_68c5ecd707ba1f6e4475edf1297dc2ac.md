
返回一个操作方式与普通 `writer` 相似的对象，但字典写入输出行。`fieldnames` 指定了将写入文件的顺序和属性。`restval` 是当写入的字典缺少 `fieldnames` 中的某个字段名时的值。`extrasction` 是一个字符串，指定当写入的字典具有未列在 `fieldnames` 中的键时的操作。`extrasction` 的默认值为 `'raise'`，它会抛出一个 `ValueError` 异常。可以使用值 `'ignore'`，在这种情况下字典中的值将被忽略。`dialect` 和 `fmtparams` 的意义与 `writer()` 相同。

一个 `DictWriter` 实例 `w` 支持以下方法：

`w.writerow(row)`

向文件写入单行数据。`row` 必须是一个将字段名映射到值的字典。

`w.writerows(rows)`

写入多行数据。`rows` 必须是传递给 `writerow()` 方法的行序列。

`Sniffer()`

创建一个 `Sniffer` 对象，用于尝试自动检测 CSV 文件的格式。

`Sniffer` 实例 `s` 具有以下方法：

```python
s.sniff(sample, delimiters)
```

查看 `sample` 中的数据并返回一个表示数据格式的适当 `Dialect` 对象。`sample` 是 CSV 文件的一部分，包含至少一行数据。如果提供了 `delimiters`，它是一个包含可能的字段分隔符字符的字符串。

```python
s.header(sample)
```

查看 `sample` 中的 CSV 数据，如果第一行看起来像一组列标题，则返回 True。

## 方言 (Dialects)

`csv` 模块中的许多函数和方法都涉及一个特殊的 `dialect` 参数。该参数的目的是适应 CSV 文件的不同格式规范（CSV 没有官方的“标准”格式）——例如逗号分隔值与制表符分隔值之间的差异、引号规范等。

方言通过继承 `Dialect` 类并定义提供给 `reader()` 和 `writer()` 函数的相同属性集（`delimiter`, `doublequote`, `escapechar`, `lineterminator`, `quotechar`, `quoting`, `skipinitialspace`）来定义。

使用以下工具函数来管理方言：

```python
register_dialect(name, dialect)
```

在名称 `name` 下注册一个新的 `Dialect` 对象 `dialect`。

```python
unregister_dialect(name)
```

移除名为 `name` 的 `Dialect` 对象。

```python
get_dialect(name)
```

返回名为 `name` 的 `Dialect` 对象。

```python
list_dialects()
```

返回所有注册方言的列表。目前只有内置方言：'excel' 和 'excel-tab'。

## 示例

```python
import csv
# 读取一个基础 csv 文件
f = open('scomods.csv','r')
for row in csv.reader(f):
    lastname, firstname, street, city, zip = row
    print("{0}, {1} {2} {3} {4}".format(*row))

# 使用 DictReader 代替
f = open('address.csv')
r = csv.DictReader(f, ['lastname','firstname','street','city','zip'])
for row in r:
    print("{row['lastname']}}, {row['firstname']} {row['street']} {row['city']} {row['zip']}".format(**row))

# 写入一个基础 csv 文件
data = [
    ['Elwood', '1060 W Addison', 'Chicago', 'IL', '60613'],
    ['McGovern', 'Jack', '4802 N Broadway', 'Chicago', 'IL', '60640'],
]
f = open('address.csv','w')
w = csv.writer(f)
w.writerows(data)
f.close()
```

## email 包

`email` 包提供了各种函数和对象，用于表示、解析和处理编码为 MIME 标准的电子邮件消息。

涵盖 `email` 包的每一个细节是不现实的，大多数读者可能也不感兴趣。因此，本节的其余部分重点关注两个常见的实际问题——解析电子邮件消息以提取有用信息，以及创建电子邮件以便使用 `smtpl` 模块发送。

## 解析电子邮件

在顶层，`email` 模块提供了两个解析消息的函数：

```python
message_from_file(f)
```

解析从文件对象 `f` 读取的电子邮件消息。

```python
message_from_str(str)
```

解析从字符串 `str` 读取的电子邮件消息。

在顶层，`email` 模块提供了两个解析消息的函数：

| 操作 |  |
| :--- | :--- |
| `message_from_file(f)` | 解析从文件对象 `f` 读取的电子邮件消息。 |
| `message_from_str(str)` | 解析从字符串 `str` 读取的电子邮件消息。 |

（注：OCR 文本在提供的片段后半部分似乎出现了乱码。我已根据标准的 Python `email` 模块文档和可见片段重建了逻辑结构。）

## 554 第 24 章 数据处理与编码

返回列表的元素是元组 `(name, value)`，其中 `name` 是参数名，`value` 是 `get_param()` 方法返回的值。

```python
m.get_payload([{, decode}])
```

返回消息的负载（payload）。如果消息是简单消息，则返回包含正文的字节字符串。如果消息是多部分消息（multipart），则返回一个包含所有子部分的列表。对于多部分消息，`i` 指定了列表中可选的索引。如果提供了该索引，则只返回该消息组件。要解码负载，将根据可能存在的任何 'Content-Transfer-Encoding' 头部进行解码（例如 'quoted-print'、'base64' 等）。要解码简单非多部分消息的负载，将 `i` 设置为 `None` 并 `decode`，或使用关键字参数指定 `decode`。需要强调的是，负载是以包含内容的字节字符串形式返回的。如果负载代表 UTF-8 或其他编码的文本，你将需要对结果使用 `decode()` 方法来对其转换。

```python
m.unxform()
```

返回 UNIX 风格的 'From ...' 行（如果有）。

```python
m.is_multipart()
```

如果 `m` 是多部分消息，则返回 True。

```python
m.walk()
```

创建一个生成器，遍历消息的所有子部分，每个子部分也由一个 `Message` 实例表示。该迭代是对多部分消息的深度优先遍历。通常，此函数可以用于解析多部分消息的所有组件。

最后，`Message` 实例具有几个与低级解析过程相关的属性。

```python
m.preamble
```

出现在多部分消息中、位于指示头部结束的空行与标记消息第一个子部分的第一个多部分边界字符串之间的任何文本。

```python
m.epilogue
```

消息中出现在最后一个多部分边界字符串和消息末尾之后的任何文本。

```python
m.defects
```

解析消息时发现的所有消息缺陷的列表。更多详细信息，请参阅 `email.errors` 模块的在线文档。

下面的示例说明了在解析邮件消息时如何使用 `Message` 类。以下代码读取邮件消息，打印有用头部的简短摘要，并保存任何附件。

```python
import email
import sys

f = open(sys.argv[1],"r")  # 打开消息文件
m = email.message_from_file(f)  # 解析消息
```

```python
# 打印发送者/接收者的简短摘要
print("From      : %s" % m['from'])
print("To        : %s" % m['to'])
print("Subject   : %s" % m['subject'])
print("**")
```
