
`wget` 的文档解释说 `http_proxy` 环境变量指定了代理服务器（代表另一计算机执行网络请求的服务器）。现在我们知道 `wget` 是如何获取我的 IP 地址的。该问题的解决方法是移除环境变量并重试，如下例所示：

### 表 59-1：实用的选项

| 选项 | 功能 |
|---|---|
| `-o filename` | 将日志重定向到文件名。在程序完成后，你可以浏览 `strace` 日志，或者通过打开终端窗口并使用 `tail` 命令进行跟踪。 |
| `-f` | 强制跟踪由正在跟踪的程序所产生的子进程（以及孙子进程、曾孙子进程等）。 |
| `-s size` | 告诉程序打印结构内容而不是缩略（节省空间）的版本。此选项告诉 `trace` 在打印参数时最多打印 `size` 个字符。默认值是 32，对于某些程序可能太短了。 |

## 453 使用 valgrind 记录程序错误

| 选项 | 功能 |
| :--- | :--- |
| `-e trace=file` | 强制 `trace` 跟踪影响文件名参数的函数（这包括 `open`、`unlink` 等函数）。使用此选项查看程序使用了哪些文件。 |
| `-e trace=network` | 显示所有网络相关的调用。 |
| `-p process-ID` | 附加正在运行的进程，通过 `process-ID` 识别。（你必须拥有适当权限才能使用此选项） |

`ltrace` 有类似的选项，列在表 59-2 中。

### 表 59-2：实用的跟踪选项

| 选项 | 功能 |
| :--- | :--- |
| `-f` | 强制 `ltrace` 跟踪你运行的程序所产生的子进程（以及孙子进程、曾孙子进程等）。 |
| `-S` | 显示系统调用（类似于 `trace`）以及共享库中定义的调用。 |
| `-C` | 要求每个 C++ 函数的名字（C++ 函数名由 C++ 编译器管理，如果不进行特殊处理很难阅读）。 |
| `-s size` | 此选项告诉 `ltrace` 在显示字符串时最多打印 `size` 个字符。（默认值是 32，对于某些程序可能太短）。 |
| `-n indent` | 按缩进空格对函数进行缩进。（此选项使得复杂的调用更易读）。 |
| `-e function1,function2...` | 仅跟踪对命名函数的调用。 |
| `-E function1,function2...` | 强制 `ltrace` 忽略对 `function1`、`function2` 等函数的调用。 |
| `-l library` | 跟踪在给定库中定义的调用。（例如，要查看对 `libz` 压缩库的调用，使用选项 `-l /usr/lib/z2.so.1`） |

最后一个选项（`-l library`）很棘手，因为你必须知道感兴趣的库的完整路径。使用 `ldd` 来查找程序使用了哪些共享库。例如，要查找 `wget` 需要的共享库，使用以下命令：

```
$ ldd $(wget)

libssl.so.4 => /lib/libssl.so.4

crypto.so.4 => /lib/libcrypto.so.4

ssapi_krb5.so.2 => /lib/libkrb5.so.2

krb5.so.3 => /lib/libkrb5.so.3

liberr.so.2 => /lib/liberr.so.2

crypto.so.3 => /lib/libcrypto.so.3

ldresv.so.2 => /lib/ldresv.so.2

lbd1.so.2 => /lib/lbd1.so.2

libz.so.6 => /lib/libz.so.6

id-linux.so.2 => /lib/libid-linux.so.2
```

## 使用 Valgrind 记录错误

有时，调试是好的。当你让一个程序正常运行，并且已经尽一切确保配置正确后，除非你愿意阅读源码并使用调试器调试，否则最好的办法就是为开发者收集信息。`valgrind` 是程序员的梦想。`valgrind` 运行程序并监控未初始化内存的使用、无效引用和内存泄漏。`valgrind` 包未包含在发行版中，但你可以在 Web 上找到 `valgrind` RPM 包（在 `yum.org/packages` 找到了一个）。

## 454 技巧 59：故障排除

安装 `valgrind` 后，使用起来非常简单。像往常一样运行程序，但将 `valgrind` 放在命令行开头，如下：

```
$ valgrind xmms
```

当 `valgrind` 运行时，消息会发送到标准错误（通常连接到终端窗口），因此你可以获取程序的输出。可以使用 `--logfile=filename` 选项将 `valgrind` 消息重定向到文件：

```
$ valgrind --logfile=/tmp/xmms xmms
```

`valgrind` 通过在模拟 CPU 上运行你的程序并监控所有引用来工作。如果你的程序使用了无效内存，`valgrind` 会报错。你的程序在模拟 CPU 上运行的速度会慢得多。每条消息以一行错误描述开始，然后是堆栈显示错误发生时程序正在做什么（每行都是正在运行程序的进程 ID）。现在你有一组 `valgrind` 消息，该怎么办？

- 如果你是一个程序员并感兴趣帮助开发者，请阅读 `valgrind` 网站上的文档。你将发现如何将 `valgrind` 连接到源码调试器（如 `gdb`）。列表 59-3 显示了我们运行 `xmms` 播放器时 `valgrind` 生成的一些错误消息。

### 列表 59-3：VALGRIND XMMS

```
==1024== Syscall write(buffer) uninitialized or unaddressable byte(s)

==1024== at 0x5FCA68: __libc_write (in /usr/lib/libc-2.3.2)

==1024== at 0xA72EC7F: (within /usr/lib/x86/lib/libc.so.6)

==1024== at 0x5E05D4: _Translate (in /usr/lib/x86/lib/libc.so.6)

==1024== at 0x4A54C8: __memset (in /usr/lib/x86/lib/libc.so.6)

==1024== at 0x22CA45: 12 bytes inside a block of size 1024 alloc'd

==1024== at 0x992800: calloc (in /vg_replace_malloc.c:284)

==1024== at 0xA1E14F: OpenConnection (in /usr/lib/x86/lib/libc.so.6)

==1024== at 0xA5D2B8: SmConnection (in /usr/lib/x86/lib/libSM.so.6)

==1024== at 0x8A0150: sm_init (in /usr/bin/xmms)

==1024== Conditional jump or move depends on uninitialized value(s)

==1024== at 0x18A7AE2: (within /usr/lib/libgtk-1.2.0.9.1)

==1024== at 0x1C28F6: (within /usr/lib/libgtk-1.2.0.9.1)

==1024== at 0x1C3895: gtk_marshal_BOOL__Gtkint (in /usr/lib/libgtk-1.2.0.9.1)

==1024== at 0x18E0F9: (in /usr/lib/libgtk-1.2.0.9.1)
```
