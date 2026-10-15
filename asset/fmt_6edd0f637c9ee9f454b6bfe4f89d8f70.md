
```
# rpm -bp amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
+ umask 022
+ echo Executing: %prep
Executing: %prep
+ cd /usr/src/redhat/BUILD
+ cd /usr/src/redhat/BUILD
+ rm -rf amanda-2.3.0
+ gzip -dc /usr/src/redhat/SOURCES/amanda-2.3.0.tar.gz
+ tar -xvzf -
drwxr-xr-x 3/20 0 May 19 22:10 1996 amanda-2.3.0/
-rw-r--r-- 3/20 1389 May 19 22:11 1996 amanda-2.3.0/COPYRIGHT
-rw-r--r-- 3/20 1958 May 19 22:11 1996 amanda-2.3.0/Makefile
-rw-r--r-- 3/20 11036 May 19 22:11 1996 amanda-2.3.0/README
...
-rw-r--r-- 3/20 2010 May 19 22:11 1996 amanda-2.3.0/man/amtape.8
drwxr-xr-x 3/20 0 May 19 22:11 1996 amanda-2.3.0/tools/
-rwxr-xr-x 3/20 2437 May 19 22:11 1996 amanda-2.3.0/tools/munge
+ [ 0 -ne 0 ]
+ cd amanda-2.3.0
+ cd /usr/src/redhat/BUILD/amanda-2.3.0
+ chown -R root.root .
+ chmod -R a+rX,g-w,o-w .
+ echo Patch #0:
Patch #0:
+ patch -p1 -s
+ exit 0
```

直到最后才看到区别，在那里我们看到补丁被应用了。让我们进入构建目录看看我们的配置文件是否在那里：

```
# cd /usr/src/redhat/BUILD/amanda-2.3.0/config
# ls -l
total 58
-rw-r--r--   1 root  root   7518 May 19 1996 config-common.h
-rw-r--r--   1 root  root  1846 Nov 20 20:46 config.h
-rw-r--r--   1 root  root  2081 May 19 1996 config.h.orig
-rw-r--r--   1 root  root  1690 May 19 1996 config.h-basdi1
...
-rw-r--r--   1 root  root  1830 May 19 1996 config.h-ultrix4
-rw-r--r--   1 root  root     0 Nov 20 20:46 config.h.orig
-rw-r--r--   1 root  root  7196 Nov 20 20:46 options.h
-rw-r--r--   1 root  root  7236 May 19 1996 options.h.vanilla
-rw-r--r--   1 root  root     0 Nov 20 20:46 options.h.orig
#
```

好多了。那些零长度的 `.orig` 文件明显表明补丁已经在这里运行过，`config.h` 和 `options.h` 上的日期也是如此。在 `tools` 目录中，`munge` 也已被修改。这些源代码已准备好进行构建！

#### 20.3.5. 让 RPM 执行构建

我们知道源代码已准备好。我们知道 `%build` 脚本已准备好。如果我们让 RPM 构建 `amanda`，应该不会有太多意外。让我们使用 `-bc` 选项在 `%build` 脚本完成后停止操作：

```
# rpm -bc amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
...
echo Executing: %build
Executing: %build
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make
Making all in common-src
make[1]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/common-src'
../tools/munge Makefile.in Makefile.out
make[2]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/common-src'
cc -g -I. -I../config -c error.c -o error.o
cc -g -I. -I../config -c alloc.c -o alloc.o
...
Making all in man
make[1]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
../tools/munge Makefile.in Makefile.out
make[2]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
make[2]: Nothing to be done for 'all'.
make[2]: Leaving directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
make[1]: Leaving directory '/usr/src/redhat/BUILD/amanda-2.3.0/man'
+ exit 0
#
```

正如我们所想的，没有意外。快速查看构建区域，可以看到全套的二进制文件，随时准备安装。因此，看起来最自然的下一步就是让 RPM 安装 `amanda`。

#### 20.3.6. 让 RPM 执行安装

而这正是我们要做的！我们的 `%install` 脚本包含必要的 `make install` 命令，所以让我们试试看：
