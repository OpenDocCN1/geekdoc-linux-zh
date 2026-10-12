
```python
if not m.is_multipart():
    # 简单消息。只打印负载
    payload = m.get_payload(decode=True)
    charset = m.get_content_charset('iso-8859-1')
    print(payload.decode(charset))
else:
    # 多部分消息。遍历所有子部分并
    # 1. 打印 text/plain 段
    # 2. 保存任何附件
```

```python
for s in m.walk():
    filename = s.get_filename()
    if filename:
        print("Saving attachment: %s" % filename)
        data = s.get_payload(decode=True)
        open(filename,"wb").write(data)
    else:
        if s.get_content_type() == 'text/plain':
            payload = s.get_payload(decode=True)
            charset = s.get_content_charset('iso-8859-1')
            print(payload.decode(charset))
```

在这个示例中，需要强调的是消息的负载可能始终返回字节字符串。如果负载代表文本，你需要根据设置的字符集对其进行解码。示例中的 `m.get_content_charset()` 和 `payload.decode()` 操作正在执行这种转换。

## 编写电子邮件

要编写电子邮件，你可以创建一个 `Message` 对象的实例（它定义在 `email.message` 模块中），或者使用通过解析邮件消息创建的 `Message` 对象（见上一节）。

```python
Message()
```

创建一个初始为空的新消息。

`m` `Message` 实例支持以下方法，用于向消息填充内容、头部和其他信息。

```python
m.add_header(name, value, params)
```

添加新的消息头部。`name` 是头部的键，`value` 是头部的值，`params` 是提供额外参数的关键字集。例如，`add_header('Foo', 'Bar', span='major')` 会向消息添加头部行 'Foo: Bar; span="major"'。

```python
m.as_string(unixform)
```

将整个消息转换为字符串。`unixform` 是一个布尔标志。如果设置为 `True`，则 UNIX 风格的 'From...' 将作为第一行出现。默认，`unixform` 为 `False`。

```python
m.attach(payload)
```

向多部分消息添加附件。`payload` 必须是另一个 `Message` 对象（例如 `email.mime.MIMEText`）。在内部，`payload` 被附加到一个跟踪消息不同部分的列表中。如果消息不是多部分消息，

```python
m.defects(name, value)
```

删除一个头部。

```python
m.replace(name, value)
```

替换一个头部。

```python
m.set_boundary(boundary)
```

设置边界。

```python
m.set_charset(charset)
```

设置字符集。

```python
m.set_type(ctype)
```

设置 ctype。

```python
m.set_payload(payload, charset)
```

设置负载。

```python
m.set_type(type, charset)
```

设置类型。

```python
m.set_unixform(unixform)
```

设置 UNIX 风格的 'From...' 行。

```python
m.defects(name, value)
```

删除一个头部。

```python
m.replace(name, value)
```

替换一个头部。

设置边界。

```python
m.set_charset(charset)
```

设置字符集。

```python
m.set_type(ctype)
```

设置 ctype。

```python
m.set_payload(payload, charset)
```

设置负载。

# 558 第 24 章 互联网数据处理与编码

或省略，系统会自动确定合适的边界。`subparts` 是一个 `Message` 对象的序列，构成了消息的内容。`params` 表示可选的关键字参数和值，这些值会被添加到消息的 'Content-type' 头部中。一旦创建了多部分消息（multipart message），可以使用 `Message.attach()` 方法添加额外的子部分。

```
MIMEText(data, subtype [, charset])
```

定义在 `mime.text` 中。创建一个包含文本数据的消息。`data` 是一个包含消息负载的字符串。`subtype` 指定类型，是一个字符串，例如 'plain'（默认值）或 'html'。`charset` 是字符集，默认为 'us-ascii'。消息可能会根据其内容进行编码。

接下来的示例展示了如何使用本节中的类来组合并发送邮件消息：

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.audio import MIMEAudio

sender = "jonnogiggy@die.net"
receiver = "davesdabe@az.com"
subject = "Faders up!"
body = "I never should have moved out of Texas. -J\n"
audio = "TexasFuneral.mp3"

m = MIMEMultipart()
m['to'] = receiver
m['from'] = sender
m['subject'] = subject

m.attach(MIMEText(body))
part = MIMEAudio(open(audio,"rb").read(),"mpeg")
part.add_header("Content-Disposition", "attachment", filename=audio)
m.attach(part)

# 发送邮件
s = smtplib.SMTP()
s.connect()
s.sendmail(sender, [receiver], m.as_string())
s.close()
```

### 注意事项

- 一些建议自定义和配置选项尚未讨论。读者应查阅在线文档以获取该模块的高级用法。
- email 包至少有四个版本，其底层编程接口发生了变化（例如模块重命名、类移动到不同位置等）。本节记录了版本 4.0 的接口，该接口同时用于 Python 2.6 和 Python 3.0。如果你正在处理遗留代码，基本概念仍然适用，但你可能需要调整类和模块的位置。

# hashlib

`hashlib` 模块实现了多种安全哈希和消息算法，如 MD5 和 SHA1。要计算哈希值，首先需要调用以下函数之一，其名称与所表示的算法相同：

| 函数 | 描述 |

||||

| `md5()` | MD5 哈希 (128 位) |

| `sha1()` | SHA1 哈希 (160 位) |

| `sha224()` | SHA224 哈希 (224 位) |

| `sha256()` | SHA256 哈希 (256 位) |

| `sha384()` | SHA384 哈希 (384 位) |

| `sha512()` | SHA512 哈希 (512 位) |

由这些函数中任一个返回的摘要对象实例 `d` 具有以下接口：

| 方法或属性 | 描述 |

|---|||

| `d.update(data)` | 使用新数据更新哈希。`data` 必须是字节字符串。重复调用等同于一次性调用拼接后的数据。 |

| `d.digest()` | 返回原始字节字符串格式的摘要值。 |

| `d.hexdigest()` | 返回一个文本字符串，其摘要值编码为一系列十六进制数字。 |

| `d.copy()` | 返回摘要的副本。副本保留了原始摘要的内部状态。 |

| `d.digest_size` | 结果哈希的大小（单位为字节）。 |

| `d.block_size` | 哈希算法的内部块大小（单位为字节）。 |

该模块还提供了另一种构造接口：
