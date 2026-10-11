
`value` 可以是 `yes` 或 `default`。如果值是 `yes`，`Configure` 会执行该规则。如果值是 `default`，`Configure` 将进行最佳猜测。表 16.3 描述了当前的规则。

## 表 16.3. 配置文件 - 规则部分

| 规则 | 描述 |
| --- | --- |
| SOCKS | 如果为 yes，则将 socks 库的路径添加到 `EXTRA_LIBS`，否则假设在 `-Lusr/local/lib` 查找 Socks。 |
| SOCKS5 | 如果为 yes，则将 socks5 库的路径添加到 `EXTRA_LIBS`，否则假设在 `-Lusr/local/lib` 查找 Socks5。 |
| IRIENIX | 仅在你运行 SIRIX 时有效。 |
| IRIX32 | 如果运行使用 n32 库的 IRIX 版本，`Configure` 将使用这些代替 o32 库。 |
| PARANOID | 在 1.3 版本中引入。允许模块控制 `Configure` 的工作方式。如果 `PARANOID` 为 yes，`Configure` 将打印模块执行的代码。 |
| EXPAT | 将 James Clark 的包整合到 Apache 中。默认如果存在 `lib/expat-lite/` 目录则包含它。 |
| DEV_RANDOM | 仅在编译 `mod_auth_digest` 时使用。 |
| WANTHSAREX | Apache 需要 POSIX 正则实现。Henry Spencer 优秀的正则表达式包已包含在 Apache 中并可以使用。 |

请务必检查 Apache 软件包附带的文档以获取规则部分的更改。请务必检查配置文件，并根据你的 Apache 实现将任何规则设置为适当的值。

## 编译 Apache

在你拥有了适用于你的 Apache 实现的正确设置的配置文件后，下一步是构建 Apache。在执行构建之前，你需要确保配置设置正确。然后配合 `Configure` 命令一起使用它。下面的对话框演示了这一点：

```
$$ cd src

$ configure ./configure

Using using config-file: Configuration

Creating Makefile

+ configured for Linux platforms

+ setting C compiler to gcc

+ setting C pre-processor to gcc

+ checking for system headers

+ adding modules

+ checking size of various data types

+ doing sanity check on compiler and options

Creating Makefile in support

Creating Makefile in regex

Creating Makefile in unix

Creating Makefile in ap

Creating Makefile in include

Creating Makefile in include/lite

Creating Makefile in modules/standard

$ make
```

你的输出应该与之前的示例相似。`Configure` 命令用于创建构建 Apache 所需的 Makefile。你需要构建 Apache。下面的显示了如何启动构建过程：

```
$$ make

--=regex

[1] Nothing to be done for "all"

--=unix

$ modules/standard

$ = gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppatlite.c

gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppat

gcc -DLINUX=2 -USE_HSREGEX -o httplibstand.a /libtibain.a /usr/unix/libos.a

-o http buildd.o modules.httplibstand
```

你的输出应该与之前的示例相似。`Configure` 命令用于创建构建 Apache 所需的 Makefile。你需要构建 Apache。接下来的对话显示了如何启动构建过程：

```
$$ make

--=regex

[1] Nothing to be done for "all"

--=unix

$ modules/standard

$ = gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppatlite.c

gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppat

gcc -DLINUX=2 -USE_HSREGEX -o httplibstand.a /libtibain.a /usr/unix/libos.a

-o http buildd.o modules.httplibstand
```

你的输出应该与之前的示例相似。`Configure` 命令用于创建构建 Apache 所需的 Makefile。你需要构建 Apache。接下来的对话显示了如何启动构建过程：

```
$$ make

--=regex

[1] Nothing to be done for "all"

--=unix

$ modules/standard

$ = gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppatlite.c

gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppat

gcc -DLINUX=2 -USE_HSREGEX -o httplibstand.a /libtibain.a /usr/unix/libos.a

-o http buildd.o modules.httplibstand
```

你的输出应该与之前的示例相似。`Configure` 命令用于创建构建 Apache 所需的 Makefile。你需要构建 Apache。接下来的对话显示了如何启动构建过程：

```
$$ make

--=regex

[1] Nothing to be done for "all"

--=unix

$ modules/standard

$ = gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppatlite.c

gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppat

gcc -DLINUX=2 -USE_HSREGEX -o httplibstand.a /libtibain.a /usr/unix/libos.a

-o http buildd.o modules.httplibstand
```

你的输出应该与之前的示例相似。`Configure` 命令用于创建构建 Apache 所需的 Makefile。你需要构建 Apache。接下来的对话显示了如何启动构建过程：

```
$$ make

--=regex

[1] Nothing to be done for "all"

--=unix

$ modules/standard

$ = gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppatlite.c

gcc -c -I/usr/unix -I -DLINUX=2 -USE_HSREGEX -USE_EXPAT -I./lib/exppat

gcc -DLINUX=2 -USE_HSREGEX -o httplibstand.a /libtibain.a /usr/unix/libos.a

-o http buildd.o modules.httplibstand
```
