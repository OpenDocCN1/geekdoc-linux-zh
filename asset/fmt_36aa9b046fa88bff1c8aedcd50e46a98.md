
```python
from operator import itemgetter
def remove(list):
    d = dict(map(setitem, list, [None]*len(list)))
    return list(d.keys())
```

## 26 性能

许多 Python 程序使用对应的 C。使用这些模块可以显著提升复杂应用的性能。

示例：

```
>>> Pickle of Pickle, cstring10
instead of StringO
```

## 计算最后 27 可迭代对象的最大值、最小值和和

以下函数或列表：

```python
import bisect
bisect.insert(list, item, [low, high])
```

项按顺序插入列表。如果 `item` 已在列表中，新条目将插入到现有条目的右侧。

## 30 使用数组

`array` 模块提供了一种在程序中使用数组的高效方法。`array` 模块定义以下类型：

`array(typecode, [initializer])`

一旦你创建了数组对象，你就可以对其使用许多方法。这里是一些重要的示例：

`array.count(x)`: 返回 `x` 在数组中出现的次数。

`array.extend(x)`: 将 `x` 添加到数组末尾。

`array.reverse()`: 反转数组顺序。

## 使用基于正则表达式的搜索

你可以使用基于正则表达式的表达式调用函数。查看下面的示例：

```python
>>> import re
>>> s = "Kunal is a bad"
>>> if re.search('K', s):
    print("# char literal")

Match:
>>> if re.search('[A-Z]', s):
    print("# char literal")

Match:
>>> if re.search('\d', s):
    print("# digits char")
```

## 使用 `bzip2` (`bz2`) 压缩

你可以使用 `bzip2` 通过 bzip2 算法读写数据。

```python
import bzip2
MESSAGE = "Kunal is a bad"
compressed_message = bzip2.compress(MESSAGE)
compressed_message = bzip2.decompress(compressed_message)
print("original:", MESSAGE)
print("compressed:", compressed_message)
print("decompressed:", compressed_message)
```

示例：

```python
>>> import bzip2
>>> original = "Kunal is a bad"
>>> compressed_message = bzip2.compress(original)
>>> print(compressed_message)
```

## 在 Python 中使用 SQLite 数据库

SQLite 是一种快速且流行的嵌入式数据库，因为它具有零配置和卓越的性能。你使用 `sqlite3` 模块来操作 SQLite 数据库。

```python
>>> import sqlite3
>>> connection = sqlite3.connect('test item.db')
>>> cursor = connection.cursor()
>>> cursor.execute('''CREATE TABLE text (id INTEGER PRIMARY KEY, name TEXT, desc TEXT, price REAL)''')
>>> cursor.execute('INSERT INTO text (name, desc, price) VALUES(?,?,?)', ('Widget', 'A very strange widget', 19.99))
```

## 处理 zip 文件

你可以使用 `zipfile` 模块来处理文件。

```python
import zipfile
with zipfile.ZipFile('example.zip', 'w') as zipf:
    zipf.write('file.txt')

with zipfile.ZipFile('example.zip', 'r') as zf:
    zf.extract('file.txt')
```

## 执行基本操作（复制、重命名、删除和重命名）

你可以使用 `shutil` 模块进行高级别文件操作。该模块适用于你的普通文件，但无法适用于管道、块设备和目录等特殊文件。

```python
shutil.copy(src_file, dst_file)
将 src_file 复制复制到 dst_file。
shutil.move(src_dir, dst_dir)
将 src_dir 目录移动到 dst_dir。
shutil.copytree(src_dir, dst_dir, symlinks=False)
递归地复制整个目录到 src。
shutil.rmtree(path, errors=ignore)
删除整个目录。
```

## 在 Python 中执行 Unix 命令

在 Python 中，你可以使用 `subprocess` 模块来运行“命令”。

示例：

```python
>>> import subprocess
>>> result = subprocess.run(['ls', '-l'], capture_output=True, text=True)
>>> print(result.stdout)
```

### 读取变量

你可以使用 `os` 模块获取特定于环境的信息。

示例：

```python
>>> import os
>>> os.environ.get('posix')
'/usr/lib/python3'
>>> print(os.environ.get('PATH'))
'/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin'
```

## 使用 UNIX 风格的通配符搜索文件名

你可以使用 `glob` 模块根据 Unix shell 符号（如 `*` 和 `[?]`）查找匹配模式的文件。

```python
>>> import glob
>>> glob.glob('*.txt')
['file1.txt', 'file2.txt']
>>> glob.glob('file?.txt')
['file1.txt', 'file2.txt']
>>> glob.glob('file[1-2].txt')
['file1.txt', 'file2.txt']
```

## 发送邮件

你可以使用 `smtplib` 通过 SMTP（简单邮件传输协议）发送邮件。

```python
smtplib.SMTP([host, port])
# 示例（使用 Gmail 邮件）
import smtplib
# 使用你自己的邮件地址
fromaddr = 'from@gmail.com'
toaddr = 'to@gmail.com'
msg = 'Hello Python. Here is the message!'
## 凭据
# 使用自己的凭据和用户名
username = 'username@gmail.com'
password = 'password'
## 实际服务器
server = smtplib.SMTP('smtp.gmail.com', 587)
# Google Mail 使用凭据方法
server.starttls()
server.login(username, password)
server.sendmail(fromaddr, toaddr, msg)
server.quit()
# 旧版本的 Red Hat Linux 已移动到 http://archive.redhat.com/pub/redhat/linux/
```

## 设置种子

你可以使用 `random` 生成各种随机数。最常用的是 `random.seed()`，它初始化随机数生成器。如果省略，将在首次导入时使用系统时间。

## 使用默认浏览器打开网页

`webbrowser` 模块提供了使用默认浏览器打开网页的方法。

```python
# 示例（使用默认浏览器打开 google.com）
import webbrowser
webbrowser.open('http://google.com')
```

## 创建哈希

`hashlib` 模块支持各种哈希算法。

```python
# 示例（文本的摘要）
import hashlib
hash = hashlib.md5()
hash.update(b'Hello world')
print(hash.hexdigest())
```

## 处理 CSV（逗号分隔值）
