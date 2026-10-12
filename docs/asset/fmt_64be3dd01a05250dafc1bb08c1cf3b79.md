
以下是一个列表的开头，它在本节中分段显示。每个列表后都会有一段讨论来解释正在发生什么。

```
1 dnl 用于 bogusapp 的自动配置脚本
2 dnl Kurt Wall <k@xmission.com>
3 dnl
4 dnl 使用 `autoconf` 处理此文件以生成 `configure`
--script
5 AC_INIT(bogusapp)
6 AC_CONFIG_HEADER(config.h)
```

第 6 行在源码树的根目录下创建一个名为 `config.h` 的头文件，它只包含来自你头文件的预处理器符号。通过在源代码中包含此文件并使用其中包含的符号，你的程序应该在可能落地的每个系统上顺利且无缝地编译。`autoconf` 从一个名为 `config.in` 的输入文件创建 `config.h`，该文件包含了你的所有`#defines`。幸运的是，`autoconf` 附带了一个非常实用的名为 `autohader` 的脚本，它可以生成 `config.h.in`。`autohader` 通过读取 `configure-ure.in`、作为 `autoconf` 发布版一部分的文件 `acconfig.h` 以及一个来生成 `config.h.in`。

源码树中的`./acconfig.h`用于存储预处理器符号。好消息是，在你开始抱怨不得不再创建一个另一个文件之前，这个`./acconfig.h`只需要包含在其他任何地方未定义的预处理器符号。更好情况下，它们可以具有占位值。这个简单的文件需要包含合法的定义的 C 风格预处理器符号，以便 `autoloader` 和 `autoconf` 能够读取并利用。请参阅光盘上的`acconfig.h`文件以获取示例。

```
7
8 test -z "$LDLLAGS" && LDFLAGS="-I/usr/include" AC_SUBST(CFLAGS)
9
10 dnl Tests for UNIX variants
11 dnl
12 AC_CANONICAL_HOST
```

`AC_CANONICAL_HOST` 代表 GNU 对宿主系统的理解。它输出一个格式为`cpu-company-system`的名称。例如，在我其中一个系统中，`AC_CANONICAL_HOST` 将机器报告为`i586-unknown-linux`。

```
13
14 dnl Tests for programs
15 dnl
16 AC_PROG_CC
17 AC_PROG_LEX
18 AC_PROG_AWK
19 AC_PROG_YACC
20 AC_CHECK_PROG(SHELL, bash, /bin/bash, /bin/sh)
21
22 dnl Tests for libraries
23 dnl
24 AC_CHECK_LIB(socket, socket)
25 AC_CHECK_LIB(resolv, res_init, [echo "res_init() not in --libresolv])
26 [echo "res_init() found in libresolv"]
```

第 25 行演示了如何为 `autoconf` 宏编写自定义命令。第三和第四参数是对应`action_if_found`和`action_if_not_found`的 shell 命令。由于 m4 引用和定界符的特殊性，通常建议使用 m4 的引号字符（`{` 和 `}`）来界定使用 `'` 或 `' '` 的命令，以保护它们免受 shell 扩展的影响。

```
27
28 dnl Tests for header files
29 dnl
30 AC_CHECK_HEADER(kill.h)
31 AC_CHECK_HEADERS([[resolv.h termio.h curses sys/time.h fcntl.h sys/fcntl.h memory])
```

### 使用 autoconf 创建自配置软件

第 5 章

第 31 和第 32 行说明了延续多行参数的正确方法。使用 `\` 字符通知 m4 和 shell 换行，并用 m4 的引号定界符包裹整个参数。

```
33 AC_DECL_SYS_SIGLIST
34 AC_HEADER_STDC
35
36 dnl Tests for typedefs
37 dnl
38 AC_TYPE_GETGROUPS
39 AC_TYPE_SIZE_T
40 AC_TYPE_PID_T
41
42 dnl Tests for structures
43 AC_HEADER_TIME
44 AC_STRUCT_TIMEZONE
45
46 dnl Tests of compiler behavior
47 dnl
48 AC_C_BIGENDIAN
49 AC_C_INLINE
50 AC_CHECK_SIZEOF(int, 32)
```

第 48 行将生成一个警告，说明 `AC_TRY_RUN` 在调用时没有为交叉编译提供默认值。你可以忽略此警告。

```
51
52 dnl Tests for library functions
53 dnl
54 AC_FUNC_GETLOADAVG
55 AC_FUNC_MMAP
56 AC_FUNC_UTIME_NULL
57 AC_FUNC_VFORK
58
59 dnl Tests of system services
60 dnl
61 AC_SYS_INTERPRETER
62 AC_PATH_X
63 AC_SYS_RESTARTABLE_SYSCALLS
```

第 63 行将生成一个警告，说明 `AC_TRY_RUN` 在调用时没有为交叉编译提供默认值。你可以忽略此警告。

```
64
65 dnl Tests in this section exercise a few of `autoconf’s
66 -generic macros
67 dnl First, let’s see if we have a usable void pointer type
68 dnl
69 AC_MSG_CHECKING(for a usable void pointer type)
```

![](img/66f6e6c242a0e6a79aeee4012c6ff547_78_0.png)

`AC_MSG_CHECKING` 在屏幕上打印 "checking"，后面跟着一个空格和传递的参数，在本例中为 "a usable void pointer type."此宏允许你模拟 `autoconf` 向用户报告其活动的方式，让用户知道`configure`正在做什么。这比明显的屏幕假死要好得多。

```
AC_TRY_COMPILE([{
    char *ptr;
    void *xalloc();
    ptr = (char *) xalloc();
});
AC_DEFINE(HAVE_VOID_POINTER,
    AC_MSG_RESULT(usable void pointer),
    AC_MSG_RESULT(no void pointer type))
```
