
## 服务器的自定义

服务器通常需要特殊配置以适应不同的网络地址族、超时、并发和其他功能。这种自定义是通过继承上一节中描述的四种服务器之一来实现的。可以定义以下类属性来定制底层网络套接字的基本设置：

（注：此处原文似乎存在重复或逻辑跳跃，已按语意翻译）

## 应用程序编程

本章描述了与互联网协议相关的模块，包括 HTTP、XML-RPC、FTP 和 SMTP。Web 编程主题如 CGI 脚本见第 23 章“Web编程”。处理常见互联网格式的模块见第 24 章“互联网数据处理与编码”。

网络相关库的组织是 Python 2 和 3 之间存在差异的地方。为了后续考虑，本章假设使用 Python 3 组织，因为它更有逻辑。然而，库提供的功能在版本之间几乎相同。在适用情况下，每个节都会注明 Python 2 的模块名称。

### ftplib

`ftplib` 模块实现了 FTP 协议的客户端。很少直接使用此模块，因为 `urllib` 包提供了更高级的接口。然而，如果你想对 FTP 连接的底层细节有更多控制，此模块可能仍然有用。为了使用它，了解 FTP 协议的一些细节可能会有帮助，该协议在 RFC 959 中描述。

定义了一个类用于建立 FTP 连接：

创建一个表示 FTP 连接的对象。`host` 是指定名称的字符串。`user`、`password` 和 `acct` 可选指定用户名、密码和账户。如果没有提供参数，则必须显式调用 `connect()` 和 `login()` 方法启动实际连接。如果提供了 `host`，则会自动调用 `connect()`。如果提供了 `user`、`password` 和 `acct`，则调用 `login()`。`timeout` 是以秒为单位的超时时间。

FTP 的实例 `f` 有以下方法：

```
f.abort()
```

停止正在传输的文件。这可能取决于远程服务器。

## 第 22 章 网络应用程序编程

```python
f.close()
```

关闭 FTP 连接。调用此方法后，无法再对 FTP 对象 `f` 执行任何后续操作。

```python
f.connect(host [, port [, timeout]])
```

向给定的主机和端口打开 FTP 连接。`host` 是指定主机名的字符串；`port` 是 FTP 服务器的整数端口，默认为 21；`timeout` 是以秒为单位的超时时间。如果在调用 `FTP()` 时提供了主机名，则无需调用此方法。

```python
f.cwd(pathname)
```

将服务器上的当前工作目录更改为 `pathname`。

```python
f.delete(filename)
```

从服务器上删除该文件名。

```python
f.dir([dirname, ... callback]])
```

生成由 'LIST' 命令产生的目录列表。`dirname` 可选提供要列出的目录名称。此外，如果提供了任何额外的参数，它们将直接作为额外的参数传递给 'LIST'。最后一个参数 `callback` 是一个函数，用作回调函数来处理返回的目录列表数据。该回调函数的工作方式与 `retrlines()` 方法使用的回调函数相同。默认情况下，此方法将目录列表打印到 `sys.stdout`。

```python
f.login(user, [passwd [, acct]])
```

使用指定的用户名、密码和账户登录服务器。`user` 是提供用户名的字符串，默认为 'anonymous'；`password` 是包含密码的字符串，默认为空字符串 ''；`acct` 是字符串，默认为空字符串。如果在调用 `FTP()` 时已提供了这些信息，则无需调用此方法。

```python
f.mkd(pathname)
```

在服务器上创建一个新目录。

```python
f.transfercmd(command [, rest])
```

与 `transfercmd()` 相同，但返回的是一个元组 `(sock, size)`，其中 `sock` 是对应数据连接的对象，`size` 是预期的数据字节大小，如果无法确定大小则为 `None`。

```python
f.pwd()
```

返回一个包含服务器上当前工作目录的字符串。

```python
f.quit()
```

通过向服务器发送 'QUIT' 命令来关闭 FTP 连接。

```python
f.rename(oldname, newname)
```

重命名服务器上的文件。

```python
f.retrbinary(command, callback [, blocksize [, rest]])
```

返回使用二进制传输模式在服务器上执行命令的结果。

`command` 是指定适当的文件检索命令的字符串，几乎总是 'RETR filename'。`callback` 是在每当接收到一个数据块时被调用的回调函数。`rest` 是字符串形式的数据，`blocksize` 是要使用的最大大小，默认为 8192 字节。`rest` 是文件中的可选字段。如果提供，它将指定你想要从文件中开始传输的位置。然而，并非所有的 FTP 服务器都支持此项，因此可能会导致 `error_reply` 异常。

```python
f.retrlines(command [, callback])
```

返回使用文本传输模式在服务器上执行命令的结果。

`command` 是指定命令的字符串，通常类似于 'RETR filename'。`callback` 是在每当接收到行数据时被调用的回调函数。该回调函数调用时接收一个参数，即一个包含数据的字符串。如果省略 `callback`，则返回的数据将打印到 `sys.stdout`。

```python
f.rmd(pathname)
```

从服务器上删除一个目录。

```python
f.sendcmd(command)
```

向服务器发送简单命令并返回服务器响应。`command` 是包含命令的字符串。此方法应仅用于不涉及数据传输命令。

```python
f.set_pasv(pasv)
```

设置被动模式。`pasv` 是一个布尔标志，为 `True` 时开启被动模式，为 `False` 时关闭。默认情况下，被动模式开启。

```python
f.size(filename)
```

返回 `filename` 的字节大小。如果由于原因无法确定大小，则返回 `None`。

```python
f.storbinary(command, file [, blocksize])
```

在服务器上执行命令并使用二进制传输模式传输数据。

`command` 是指定底层命令的字符串。它几乎总是 'STOR filename'，其中 `filename` 是你想放置在服务器上的文件名。`file` 是一个打开的文件对象，通过 `file.read(blocksize)` 读取数据并传输到服务器。`blocksize` 是传输中使用的块大小。默认为 8192 字节。

```python
f.storlines(command, file)
```

在服务器上执行命令并使用文本传输模式传输数据。

`command` 是指定底层命令的字符串。通常是 'STOR filename'。

`file` 是一个打开的文件对象，通过 `file.readline()` 读取数据并发送到服务器。

```python
f.transfercmd(command [, rest])
```

通过 FTP 数据连接启动传输。如果正在使用主动模式，它将发送 'PORT' 或 'EPRT' 命令并接受服务器生成的连接。如果正在使用被动模式，它将发送 'EPSV' 或 'PASV' 命令，然后连接服务器。无论何种情况，数据连接已建立，并发出 `command` 中的 FTP 命令。此函数返回一个响应数据连接的 socket 对象。可选参数指定起始位置。可选参数指定起始位置。可选参数指定起始位置。可选参数指定起始位置。

示例

以下示例展示了如何使用 `urllib` 获取文档：

```python
from urllib.request import urlopen

u = urlopen("http://example.com")
contents = u.read()
```

```
Connection: Keep-Alive
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept-Encoding: gzip
Accept-Language: en
Accept-Charset: iso-8859-1
```

## http 包

### 可选数据

http 包包含用于编写客户端和服务器以及状态管理（cookie）的模块。超文本传输协议（HTTP）是一种基于文本的简单协议，工作如下：

```
HTTP/1.0 200 OK
Content-type: text/html
Content-length: 72883 bytes
```
