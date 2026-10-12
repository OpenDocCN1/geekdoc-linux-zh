
```bash
[root@redhat httpPerf-0.8]# make
makeing all in lib
make[1]: Entering directory `/root/httpPerf-0.8/lib'
gcc -c -DHAVE_CONFIG_H -I.. -I.. -I.. -I../lib -DNDEBUG -D_GNU_SOURCE -D_XOPEN_SOURCE -g -O2 -Wall getopt.c
gcc -c -DHAVE_CONFIG_H -I.. -I.. -I.. -I../lib -DNDEBUG -D_GNU_SOURCE -D_XOPEN_SOURCE -g -O2 -Wall getopti.c
gcc -c -DHAVE_CONFIG_H -I.. -I.. -I.. -I../lib -DNDEBUG -D_GNU_SOURCE -D_XOPEN_SOURCE -g -O2 -Wall sst_writev.c
ar r libutil.a getopt.o getopti.o sst_writev.o ranlib libutil.a
make[1]: Leaving directory `/root/httpPerf-0.8/lib'
makeing all in gen
make[1]: Entering directory `/root/httpPerf-0.8/gen'
gcc -c -DHAVE_CONFIG_H -I.. -I.. -I.. -I../lib -DNDEBUG -D_GNU_SOURCE -D_XOPEN_SOURCE -g -O2 -Wall timer.c
gcc  -o httpperf httpperf.o object.o call.o conn.o sess.o core.o event.o http.o timer.o \
                  gen/libgen.a stat/libstat.a lib/libutil.a -lssl -lcrypto -lm
gcc -c -DHAVE_CONFIG_H -I. -I. -I./lib -DNDEBUG -D_GNU_SOURCE -D_XOPEN_SOURCE -g -O2 -Wall idleconn.c
gcc  -o idleconn idleconn.o -lssl -lcrypto -lm
```

此命令完成后，您将获得一个已编译的应用程序，但尚未安装。下一步是安装该应用程序。

### 安装软件

最后一步是安装软件。这通常使用大多数 `Makefiles` 中包含的 `make install` 命令完成。目标目录通常可以通过 `--prefix` 选项设置。`make install` 命令将安装相应的二进制文件和文档文件，包括手册页。

> **考试技巧**
>
> 大多数 `install` 命令可以作为普通用户运行，不需要 root 权限。只有当将软件安装到受保护的目录时才需要 root 权限。

```bash
[root@redhat httpperf-0.8]# make install
making install] in lib
make[1]: Entering directory `/root/httpperf-0.8/lib'
make[1]: Nothing to be done for `install'.
make[1]: Leaving directory `/root/httpperf-0.8/lib'
making install] in gen
make[1]: Entering directory `/root/httpperf-0.8/gen'
make[1]: Nothing to be done for `install'.
make[1]: Leaving directory `/root/httpperf-0.8/gen'
making install] in stat
make[1]: Entering directory `/root/httpperf-0.8/stat'
make[1]: Nothing to be done for `install'.
make[1]: Leaving directory `/root/httpperf-0.8/stat'
./mkinstalldirs /bin /usr/local/man/man1
/usr/bin/install -c httpperf /bin/httpperf
/usr/bin/install -c -m 644 ./httpperf.man /usr/local/man/man1/httpperf.1
[root@redhat httpperf-0.8]#
```

完成了！现在您可以使用您的新应用程序。`README` 文件应指定要运行的可执行文件的名称及其默认安装位置。

### 管理共享库

#### 2.2 安装和包管理

- **管理共享库。** 确定可执行程序对共享库的依赖关系，并在必要时安装这些库。涉及使用以下命令：`ldd`、`ldconfig`。涉及编辑以下文件：`/etc/ld.so.conf`

编写源代码时，大多数程序员不会重写通用操作的代码。这些操作只编写一次，然后被许多其他程序员重复使用。这些通用操作存储在所谓的 `库` 中。为了成功编译和运行应用程序，它需要访问编写时所使用的库。一些源代码会将库编译到最终的可执行文件中，因此可执行文件运行时不需要这些库。这些被称为 `静态编译` 的应用程序。其他应用程序仅在编译期间链接到库，并且之后必须能够访问库文件。这些被称为 `动态编译` 的应用程序。虽然静态编译每个应用程序似乎很有优势，但静态编译会使应用程序比动态编译版本大得多。

Linux 的共享库存储在多个路径中，例如：

- `/lib`—主要共享库
- `/usr/lib`—补充库
- `/usr/X11R6/lib`—X Window 的共享库

共享库通常遵循以下命名约定：

`libraryname`-major-minor-patch.so

`so` 扩展代表“共享对象”。在 `libcrypt-2-1-3.so` 的例子中，您可以看出：

- 库的名称是 `libcrypt`。
- 主版本是 2。
- 次版本是 1。
- 补丁级别是 3。

在许多情况下，共享库文件将存在符号链接。这些命名如下：

- `libraryname.so`
- `libraryname.so.major`

使用上面的示例，可能存在两个名称如下的链接：

- `libcrypt.so`
- `libcrypt.so.2`

这些链接允许软件指向它们而不是实际文件。这样，次要版本和补丁级别可以改变而不会破坏关联关系。

##### 查看所需的共享库

如果您想查看应用程序使用了哪些库，请使用以下命令：

```bash
ldd file_name
```

例如，要查看 `wget` 使用了哪些库：

```bash
norbert:/usr/bin# ldd wget
      libc.so.6 => /lib/libc.so.6 (0x40020000)
      /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

这意味着 `wget` 使用了库 `libc.so, version 6,` 和 `ld-linux.so, version 2`。

##### 设置库路径

如果应用程序找不到它所需的共享库，它会报告错误并退出。如果该库不在标准路径中，您可以将非标准路径添加到 `LD_LIBRARY_PATH` 环境变量中，以便搜索它。例如：

```bash
export LD_LIBRARY_PATH=/usr/newpath
```

这将把 `/usr/newpath` 添加到库的搜索目录列表中。

##### 配置共享库

如果共享库是手动安装的，而不是通过 RPM 这样的包服务安装的，则必须手动通知系统使用新库。库配置文件名为 `/etc/ld.so.conf`，其中包含要搜索的目录列表。如果您将库手动安装到未列在 `ld.so.conf` 文件中的新目录中，应将新目录添加到该文件中。该文件的一个示例如下：

```text
/usr/lib
/usr/X11R6/lib/Xaw3d
/usr/X11R6/lib
```

请注意，`/lib` 目录未被列出；由于系统必需库驻留在那里，它被默认包含在内。为了增强系统性能，会创建一个缓存文件，其中包含这些目录中的所有库。每次更改 `ld.so.conf` 文件时，都需要更新此缓存文件。使用以下命令更新缓存文件 `/etc/ld.so.cache`：`ldconfig`

可选的 `-v` 参数会在扫描时列出目录中找到的所有库。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_137_0.png)

`ld.so.cache` 文件是使用 `ldconfig` 从 `ld.so.conf` 文件创建的。

### Red Hat 包管理器

#### 2.2 安装和包管理
