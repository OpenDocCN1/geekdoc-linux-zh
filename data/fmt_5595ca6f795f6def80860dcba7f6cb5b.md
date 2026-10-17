
作为元组返回的版本信息（`major`, `minor`, `micro`, `releaselevel`, `serial`）。除 `releaselevel` 外所有值均为整数，后者为 'alpha'、'beta'、'candidate' 或 'final'。

# warnoptions

传递解释器的警告选项。

# winver

用于 Windows 注册表的版本号。

# Functions

可用函数：

```
_clear_type()
```

清除类型缓存。为了优化查找，解释器内部维护了一个小型缓存。通常不需要清除此缓存，但如果你正在尝试追踪内存问题，可以这样做。

```
_current_frames()
```

返回一个映射线程标识符到调用时执行堆栈帧的字典。此信息对于调试工具（例如追踪死锁）有用。在查找数据时线程可能已经在其他地方。

```
displayhook(value)
```

解释器在活动模式下运行时打印表达式的结果。默认情况下，`repr(value)` 的值被打印到标准输出并存储在变量 `value` 中。如果需要，可以重新定义此函数以提供不同的行为。

```
exceptionhook(type, value, traceback)
```

发生未捕捉异常时调用。`type` 是异常类，`value` 是 `raise` 语句提供的值，`traceback` 是回溯对象。默认行为是将异常和回溯打印到标准错误。但是，你可以重新定义此函数以为未捕捉异常提供替代处理（这对于调试器或 CGI 脚本等特殊应用程序可能有用）。

```
exc_clear()
```

清除与最后一个异常相关的所有信息。它只清除调用线程特定的信息。

```
exc_info()
```

返回一个包含正在处理的异常信息的元组 (`type`, `value`, `traceback`)。`type` 是异常类型，`value` 是传递给 `raise` 的参数，`traceback` 是包含异常发生处调用堆栈的回溯对象。如果没有正在处理的异常，则返回 `None`。

```
exit(n)
```

通过抛出 `SystemExit` 异常退出。`n` 是指示状态码的整数退出码。0 值被视为正常（默认值）；非零值被视为异常。如果给 `n` 非整数值，它将打印到 `sys.stderr` 并使用退出码 1。

## 234 第13 章 Python 运行时服务

### getcheckinterval()

返回检查间隔的值，该值指定解释器检查信号、线程切换和其他周期性事件的频率。

### getdefaultencoding()

获取 Unicode 转换中的默认字符串编码。返回类似 'ascii' 或 'utf-8' 的值。默认编码由 `site` 模块设置。

### getdlopenflags()

返回在 UNIX 上加载扩展模块时传递给 C 函数 `dlopen()` 的 `flags` 参数。默认值为 `None`。

### getfilesystemencoding()

返回用于将 Unicode 文件名映射到操作系统使用的文件名的字符编码。在 Windows 上返回 'mbcs'，在 Macintosh OS X 上返回 'utf-8'。在 UNIX 系统上，编码取决于区域设置（`locale`）设置，并返回 `CODESET` 参数的值。可能返回 `None`，在这种情况下将使用系统默认编码。

### _getframe(depth)

从堆栈调用中返回一个帧对象（frame object）。如果 `depth` 被省略或为 0，则返回最顶部的帧。否则，对于当前帧下方指定深度的调用，`_getframe(1)` 返回调用者的帧。如果 `depth` 无效，则抛出 `ValueError`。

### getprofile()

返回由 `setprofile()` 函数设置的分析函数。

### getrecursionlimit()

返回函数的递归限制。

### getrefcount(object)

返回 `object` 的引用计数。

### getsizeof(object, {default})

返回 `object` 以字节为单位的大小。此计算是通过调用 `object` 的 `_sizeof_` 特殊方法完成的。如果未定义，除非用 `default` 参数指定了默认值，否则将生成 `TypeError`。对象可以随任意定义 `_sizeof_`，无法保证该函数的结果是内存使用的真实衡量标准。然而，对于列表或字符串等内置类型，它是准确的。

### gettrace()

返回由 `settrace()` 函数设置的跟踪函数。

### getwindowversion()

返回一个元组 (`major`, `minor`, `build`, `platform`, `text`)，用于描述正在使用的 Windows 版本。`major` 是主版本号。例如，值 4 表示 Windows NT 4.0，值 5 表示 Windows 2000 和 Windows XP 变体。`minor` 是次版本号。例如，0 表示 Windows 2020，而 1 表示 Windows XP。`build` 是 Windows 编译号。`platform` 标识平台并是一个具有以下值之一的整数：0（Windows3.1上的Win32s）、1（Windows 95,98 或 Me）、2（Windows NT, 2000, XP）或 3（Windows CE）。`text` 是包含额外信息的字符串，如 "Service Pack 3"。

## setcheckinterval(n)

设置解释器在检查信号和线程上下文切换等周期性事件之前必须执行的 Python 虚拟机指令数。默认值为 10。

### setdefaultencoding(enc)

设置默认编码。`enc` 是一个如 'ascii' 或 'utf-8' 的字符串。此函数仅在 `site` 模块内部定义，但它可以从用户定义的自定义模块中调用。

### setdlopenflags(flags)

设置传递给 C 函数 `dlopen()` 的标志，该函数用于在 UNIX 上加载扩展模块。库和其他扩展模块解析符号的方式是通过 `dl` 模块中找到的值进行位位或标记的（见第19章“网络编程”——例如，`sys.dlopenflags(dl.RTLD_NOW | dl.RTLD_GLOBAL)`）。

### setprofile(pfunc)

设置可用于实现源码分析器的系统函数。

### setrecursionlimit(n)

更改函数的递归限制。默认值为 1000。操作系统可能会对栈大小实施硬限制，因此设置过高可能会导致 Python 解释器进程因段错误（Segmentation Fault）或访问冲突（Access Violation）而崩溃。

### settrace(tfunc)

设置系统跟踪函数，可用于实现调试器。关于 Python 调试器的信息请参考第11章。

## traceback

`traceback` 模块用于在异常发生后收集并打印程序的堆栈跟踪（stack traces）。该模块中的函数对 `sys.exc_info()` 函数返回的第三项 `traceback` 对象进行操作。该模块的主要用途是用代码非标准的方式报告错误——例如，如果你正在运行深度嵌入在网络服务器中的 Python 程序，并希望将回溯重定向到日志文件。

```
print_tb(traceback [, limit, file=file])
```

将来自 `traceback` 的堆栈跟踪条目打印到文件 `file` 中。如果省略 `limit`，则打印所有条目。如果省略 `file`，则输出发送到 `sys.stderr`。

```
print_exception(type, value, traceback [, limit [, {file}]])
```

将信息和堆栈跟踪打印到文件。`type` 是异常类型，`value` 是异常值。`limit` 和 `file` 与 `print_tb()` 相同。

```
print_exc([{limit [, {file}]])
```

同于将 `print_exception()` 应用于 `sys.exc_info()` 函数返回的信息。

```
format_exc([{limit [, {file}]])
```

返回一个包含与 `print_exc()` 打印相同信息的字符串。

```
print_last([{limit [, {file}]])
```

与 `print_exception()` 相同

```
format_exception_only(type, value)
```

格式化异常。

```
format_exception(type, value, traceback [, limit [, {file}]])
```

格式化异常和堆栈跟踪。

```
format_tb(traceback [, limit])
```

与 `print_tb(traceback, limit)` 相同。

```
format_stack(frame [, limit])
```
