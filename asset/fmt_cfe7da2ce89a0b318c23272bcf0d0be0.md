
```
m.readline()
```

返回从当前文件位置开始的一行输入。

```
m.resize(newsize)
```

将内存映射对象调整为包含 `newsize` 大小。

```
m.seek(pos, whence)
```

将文件位置设置为新值。`pos` 和 `whence` 的含义与文件对象的 `seek()` 方法相同。

```
m.size()
```

返回文件的长度。此值可能大于内存映射区域的大小。

```
m.tell()
```

返回文件指针的值。

# 第 19 章操作系统服务

## 372 第 19 章 操作系统服务

```python
m.write(string)
```

将字节字符串写入到当前文件指针指向的文件。

```python
m.write_byte(byte)
```

在当前文件指针位置的内存中写入单个字节。

### 注意事项

- 虽然 UNIX 和 Windows 提供的 `mmap()` 函数略有不同，但该模块可以通过依赖这两个函数共有的可选访问参数来以可移植的方式进行使用。例如，`mmap(fileno, length, access=ACCESS_WRITE)` 在 UNIX 和 Windows 上均可工作。
- 某些内存可能只能与系统页面大小倍倍的长度配合，该大小包含在常量 `mmap.PAGESIZE` 中。
- 在 SVR4 系统上，可以通过对具有适当权限打开的文件 `/dev/zero` 调用 `mmap()` 来获取匿名映射内存。
- 在 BSD 系统上，可以通过带有负数文件描述符和 `mmap.MAP_ANON` 标志的 `mmap()` 来获取匿名映射内存。

## msvcrt

`msvcrt` 模块提供了对 Microsoft Visual C 运行时库中许多有用函数的访问。该模块仅在 Windows 上可用。

```python
getch()
```

读取按键并返回该字符。如果没有按键按下，此操作将阻塞。如果按下的键是特殊键，调用将返回 `\u000` 或 `\x00`，随后的调用将返回键码。此函数不会向控制台回显字符，无法用此函数读取 Ctrl+C。

```python
getwch()
```

与 `getch()` 相同，但返回的是 Unicode 字符。

```python
getche()
```

与 `getch()` 相同，但字符会被回显（如果可打印的话）。

```python
getw()
```

与 `getch()` 相同，但返回的是 Unicode 字符。

```python
get_oshandle(fd)
```

返回文件描述符 `fd` 的文件句柄。如果 `fd` 无法识别则抛出 `OSError`。

```python
heapin()
```

强制 Python 内存管理器将未使用的块返回给操作系统。这仅在 Windows NT 上有效，并在失败时抛出 `OSError`。

```python
kbhit()
```

如果有按键正在等待读取，则返回 `True`。

```python
locking(fd, mode, nbytes)
```

根据来自 C 运行时的文件描述符锁定文件的部分区域。`nbytes` 是相对于当前文件指针要锁定的字节数。`mode` 为以下值之一：

| 设置 (Setting) | 描述 (Description) |
| :--- | :--- |
| 0 | 解锁文件区域 (LK_UNLCK) |
| 1 | 锁定文件区域 (LK_LOCK) |
| 2 | 锁定文件区域；非阻塞 (LK_NBLCK) |
| 3 | 写入锁定 (LK_RLCK) |
| 4 | 写入锁定；非阻塞 (LK_NBLRLCK) |

尝试获取超过约 10 秒的锁将导致 `IOError` 异常。

```python
open_oshandle(handle, flags)
```

从文件句柄 `handle` 创建 C 运行时描述符。`flags` 是 `os._O_APPEND`、`os._O_RDONLY` 和 `os._O_TEXT` 的位或。返回一个整数描述符，可以作为 `fdopen()` 的参数用于创建文件对象。

```python
putch(char)
```

在不进行缓冲的情况下向控制台打印字符 `char`。

```python
putwch(char)
```

与 `putch()` 相同，但 `char` 是 Unicode 字符。

```python
setmode(fd, flags)
```

设置文件描述符 `fd` 的行尾转换模式。`flags` 对于文本模式为 `os._O_TEXT`，对于二进制模式为 `os._O_BINARY`。

```python
unget(char)
```

导致字符 `char` 被“推回”到控制台缓冲区。它将是 `get()` 或 `getwch()` 下一次读取的字符。

```python
ungetwch(char)
```

与 `ungetch()` 相同，但 `char` 是 Unicode 字符。

> 注意
>
> 有多种 Win32 扩展可访问微软基础类（MFC）、COM 组件、图形用户界面等。这些主题远超本书的范围，但 Mark Hammond 和 Andrew Robinson 编写的《Python Programming on Win32》（O'Reilly & Associates, 2000）提供了其中许多主题的详细信息。此外，http://www.python.org 维护了一份供 Windows 使用的贡献模块列表。

## 第 19 章 操作系统服务

相关：

`winreg` (第 408 页)

## optparse

`optparse` 模块为处理 `sys.argv` 提供的 UNIX 风格命令行选项提供高级支持。使用该模块的简单示例见第 9 章。`optparse` 的使用主要关注 `OptionParser`。

```python
OptionParser(**args)
```

创建一个新的命令行选项解析器并返回 `OptionParser` 实例。提供多种可选关键字参数来控制配置。这些关键字参数在以下列表中描述：

| 关键字参数 (Keyword Argument) | 描述 (Description) |
| :--- | :--- |
| add_help_option | 是否支持特殊的帮助选项（-help 和 -h）。默认设置为 True。 |
| conflict_handler | 指定冲突命令行选项的值。可以设置为 'error'（默认值）或 'resolve'。在 'error' 模式下，如果向解析器添加冲突选项，将抛出 `optparse.OptionConflictError` 异常。在 'resolve' 模式下，冲突将被解决。 |
| description | 提供选项描述的字符串。 |
| formatter | 用于格式化文本的 `Formatter` 类实例。 |
| option_class | 用于存储选项信息的 Python 类。 |
| option_list | 用于填充解析器的选项列表。默认情况下此列表为空。 |
| prog | 用于帮助信息的程序名称。 |
| version | 传递给 `OptionParser()` 的版本字符串（如果有）。仅当你想使用标准 -v 或 --version 选项时。 |

```python
p = OptionParser()
```

`OptionParser` 的实例 `p`，它支持以下方法：

```python
p.add_option(name1, ..., nameN, **parms])
```

向 `p` 添加新选项。`name1`、`name2` 等是选项的所有名称。例如，你可以包含短名 '-f' 和长名 '--file'。在选项名称之后，一组可选的关键字参数指定如何处理该选项。这些参数在以下列表中描述：

| 关键字参数 (Keyword Argument) | 描述 (Description) |
| :--- | :--- |
| action | 解析选项时执行的操作。可选值如下：'store'--读取并存储参数。如果没有指定 action，这是默认值。 |
| 'store_const' | 选项不接受参数，但在遇到选项时存储通过 const 关键字指定的常量。 |
| 'store_true' | 类似于 'store_const'但在解析选项时存储布尔值 True。 |
| 'store_false' | 类似于 'store_true'但存储的是 False。 |
| 'append' | 解析时将参数添加到列表中。当使用同一个命令行选项指定多个值时使用此。 |
| 'count' | 选项不接受参数，但存储一个计数值。每遇到一次参数，计数器就会加 1。 |
| callback | 遇到选项时调用通过 callback 关键字指定的调调函数。 |
