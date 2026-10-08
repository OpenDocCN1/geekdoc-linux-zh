

## 32 使用基于正则表达式的搜索

你可以使用 `re.search()` 函数配合基于正则表达式的模式。请查看下面的示例。

```python
>>> import re
>>> s = "Kunal is a bad boy"
>>> if re.search("K", s): print "Match!" # char literal
Match!
>>> if re.search("[A-Z]", s): print "Match!" # char class
# match either at-sign or capital letter
Match!
>>> if re.search("\d", s): print "Match!" # digits class
```

## 33 处理 bzip2 (.bz2) 压缩格式

你可以使用 `bz2` 模块通过 bzip2 压缩算法来读取和写入数据。
- `bz2.compress()`：用于 bz2 压缩
- `bz2.decompress()`：用于 bz2 解压缩

```python
# File: bz2-example.py
import bz2
MESSAGE = "Kunal is a bad boy"
compressed_message = bz2.compress(MESSAGE)
decompressed_message = bz2.decompress(compressed_message)
print "original:", repr(MESSAGE)
print "compressed message:", repr(compressed_message)
print "decompressed message:", repr(decompressed_message)

# Output:
# [~/src/python $:] python bz2-example.py
# original: 'Kunal is a bad boy'
# compressed message: 'Bzh1A\x83Y\xc4\x6f\x9b\x00\x00\x02\x15\x00e\x00\n\x80\x84\x8a \x00\n\x00\x0c\x84\r\n\x83\c\x2\x0\x8\xdf\x5\x9b\x19\x80\n\xf8\x00\xd9\xc2\xc2\xd4\x86\x0\x86 z\xc\xe0\'
# decompressed message: 'Kunal is a bad boy'
```

## 34 在 Python 中使用 SQLite 数据库

由于 SQLite 无需任何配置且性能卓越，它正迅速成为非常流行的嵌入式数据库。你可以使用 `sqlite3` 模块来操作 SQLite 数据库。

```python
>>> import sqlite3
>>> connection = sqlite3.connect("test.db")
>>> curs = connection.cursor()
>>> curs.execute("""create table item
... (id integer primary key, itemno
... text unique,
... scandesc text, descr text, price
... real)""")
<sqlite3.Cursor object at 0x1004a2b30>
```

## 35 处理 zip 文件

你可以使用 `zipfile` 模块来处理 zip 文件。

- `zipfile.ZipFile(filename [, mode [, compression [, allowZip64]]])`：打开一个 zip 文件，该文件可以是文件路径（字符串）或类文件对象。
- `zipfile.close()`：关闭归档文件。在退出程序之前必须调用 `close()`，否则关键记录可能不会被写入。
- `zipfile.extract(member [, path [, pwd]])`：将归档文件中的成员提取到当前工作目录。`member` 必须是其完整名称（或 zinfo 对象）。`path` 指定提取到的不同目录。`member` 可以是文件名或 zinfo 对象。`pwd` 是用于加密文件的密码。

## 36 使用 UNIX 风格通配符搜索文件名

你可以使用 `glob` 模块根据 UNIX shell 使用的规则来查找所有匹配模式的路径名。`*`、`?` 以及用 `[]` 表示的字符范围将会被匹配。

```python
>>> import glob
>>> glob.glob('[/.0-9]_*.*)'
['/1.gif', '/2.txt']
>>> glob.glob('*.gif')
['1.gif', 'card.gif']
>>> glob.glob('?.gif')
['1.gif']
```

## 37 执行基本文件操作（复制、删除和重命名）

你可以使用 `shutil` 模块在高级别执行基本文件操作。该模块适用于普通文件，因此不适用于命名管道、块设备等特殊文件。

- `shutil.copy(src, dst)`：将文件 src 复制到文件或目录 dst。
- `shutil.copyfile(src, dst)`：从 src 复制文件权限到 dst。
- `shutil.move(src, dst)`：将文件或目录移动到 dst。
- `shutil.copytree(src, dst, symlinks [, ignore])`：递归复制 src 处的整个目录。
- `shutil.rmtree(path [, ignore_errors [, onerror]])`：删除整个目录。

## 38 从 Python 执行 UNIX 命令

这在 Python 3 中不可用——你需要改用 `subprocess` 模块。

```python
>>> import commands
>>> commands.getoutput('ls')
'bz2-example.py\ntest.py'
```

## 39 读取环境变量

你可以使用 `os` 模块来收集操作系统特定的信息：

```python
>>> import os
>>> os.path.module
'posixpath'
>>> print os.sysconf
'/usr/lib/python2.6/posixpath'
>>> os.environ
{'en_US\n': "X_term-color", "SHELL": "/bin/bash", "LESSCLOSE": "/usr/bin/lesspipe", "Xs": "", "XDG_SESSION_COOKIE": "925c4644957c791c784656354ad\x568-1257673132.347986.1177197325", "SHLVL": "1", "SSH_TTY": "/dev/pts/2", "PWD": "/home/kunal", "LESSOPEN": "/usr/bin/lesstpipe"}
>>> os.name
'posix'
>>> os.linesep
'\n'
```

## 40 发送电子邮件

你可以使用 `smtplib` 模块通过 SMTP（简单邮件传输协议）客户端接口发送电子邮件。

```python
smtplib.SMTP([host [, port]])
import smtplib
# 使用你自己的发件人和收件人电子邮件地址
fromaddr = 'kunaldeo@gmail.com'
toaddrs = ['toemail1@gmail.com']
msg = 'I am a Python geek. Here is the proof.!'
# 凭证信息
# 运行程序时使用你自己的 Google 邮箱凭证
username = 'kunaldeo@gmail.com'
password = 'xxxxxxxx'
# 实际发送邮件
server = smtplib.SMTP('smtp.gmail.com:587')
# Google 邮箱在 SMTP 连接中使用安全连接
server.starttls()
server.login(username, password)
server.sendmail(fromaddr, toaddrs, msg)
server.quit()
```

## 41 访问 FTP 服务器

`ftplib` 是 Python 中功能完善的 FTP 客户端模块。要建立 FTP 连接，你可以使用以下函数：

```python
ftplib.FTP([host [, user [, passwd [, acct [, timeout]]]]])
host = "ftp.redhat.com"
username = 'anonymous'
password = "kunaldeo@gmail.com"
import ftplib
import urllib2
ftp.serv = ftplib.FTP(host, username, password)
# 下载文件
u = urllib2.urlopen("ftp://ftp.redhat.com/pub/redhat/linux/README")
# 打印文件内容
print(u.read())

# 输出
# C:\src\python [5:] python ftpclient.py
```

旧版本的 Red Hat Linux 已移至 `http://archive.download.redhat.com/pub/redhat/linux/`。

## 42 使用默认 Web 浏览器启动网页

`webbrowser` 模块提供了一种方便的方式来使用默认 Web 浏览器启动网页。

```python
>>> import webbrowser
>>> webbrowser.open('http://google.co.uk')
True
```

## 43 创建安全哈希

`hashlib` 模块支持众多安全哈希算法。

```python
>>> import hashlib
# sha1 摘要
>>> hashlib.sha1('M16 Classified Information 007').hexdigest()
'e224b1543f229cc0cb8935a1eb9593188a1b20c85'
# sha224 摘要
>>> hashlib.sha224('M16 Classified Information 007').hexdigest()
'3d01e2f741000e022404842f905e9b7b977a59b408990ea8355e2c0'
# sha256 摘要
>>> hashlib.sha256('M16 Classified Information 007').hexdigest()
'2fde657333f54d0672fcb39725991c89b2550707cbfc46406efdb33b1c19825e'
# sha384 摘要
>>> hashlib.sha384('M16 Classified Information 007').hexdigest()
'5c4914160f03d7bd1e914d3ec1e74d8d5b99dc192edc133aaf768280092488d4af540bfe9e0e50fc5d3a65c0b63535572d'
# sha512 摘要
>>> hashlib.sha512('M16 Classified Information 007').hexdigest()
'a704ac3d0e6fd3e234578482a315dad29d252c88221f497f94bf85b222dec0a29b809778ae807a0a4ea8ef4f818566140667bfaf73a1dcff192f92c1f3b2'
# MD5 摘要
>>> hashlib.md5('M16 Classified Information 007').hexdigest()
'8e2f1c52ac1461a99a670c826f7126'
```

## 44 随机数播种

你可以使用 `random` 模块生成各种随机数。最常用的是 `random.seed(x)`。它初始化基本随机数生成器；如果省略 x 或为 None，则使用当前系统时间；在模块首次导入时，也使用当前系统时间来初始化生成器。

## 45 处理 CSV（逗号分隔值）文件

CSV 文件在 Web 上的数据交换中非常流行。使用 `csv` 模块，你可以读取和写入 CSV 文件。

```python
import csv
# 将股票数据作为逗号分隔值写入
writer = csv.writer(open('stocks.csv', 'wb', buffering=0))
writer.writerows([
    ('GOOG', 'Google, Inc.', 505.24, 0.47, 0.09),
    ('YHOO', 'Yahoo! Inc.', 27.38, 0.33, 1.22),
    ('CNET', 'CNET Networks, Inc.', 8.62, -0.13, -1.49)
])

# 读取股票数据，打印状态信息
stocks = csv.reader(open('stocks.csv', 'rb'))
status_labels = {-1: 'down', 0: 'unchanged', 1: 'up'}
for ticker, name, price, change, pct in stocks:
    status = status_labels[cmp(float(change), 0.0)]
    print('%s is %s (%.2f%%)' % (name, status, pct))
```

## 46 使用 setup 工具安装第三方模块

`setuptools` 是一个 Python 包，让你可以非常容易地下载、构建、安装、升级和卸载包。

要使用 `setuptools`，你需要从你的发行版的软件包管理器进行安装。安装后，你可以使用 `easy_install` 命令执行 Python 包管理任务。

