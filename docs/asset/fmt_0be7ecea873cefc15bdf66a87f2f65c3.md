
```
# rpm -bp amanda-2.3.0.spec
* Package: amanda
* Package: client
* Package: server
+ umask 022
+ echo Executing: %prep
Executing: %prep
+ cd /usr/src/redhat
+ cd /usr/src/redhat/BUILD
+ rm -rf amanda-2.3
+ gzip -dc /usr/src/redhat/SOURCES/amanda-2.3.0.tar.gz
+ tar -xwvf -
drwxr-xr-x 3/20      0 May 19 22:10 1996 amanda-2.3.0/
--rw-r--r-- 3/20     1389 May 19 22:11 1996 amanda-2.3.0/COPYRIGHT
--rw-r--r-- 3/20     1958 May 19 22:11 1996 amanda-2.3.0/Makefile
--rw-r--r-- 3/20    11036 May 19 22:11 1996 amanda-2.3.0/README
--rw-r--r-- 3/20     2010 May 19 22:11 1996 amanda-2.3.0/man/antape.8
drwxr-xr-x 3/20      240 May 19 22:11 1996 amanda-2.3.0/tools/
--rw-r--r-- 3/20     437 May 19 22:11 1996 amanda-2.3.0/munge
```

通过查看输出，很难发现源码已经解压。如果我们查看 `/usr/src/redhat/BUILD`，我们将看到 amanda 树：

```
# cd /usr/src/redhat/BUILD
# ls -l
total 3
drwxr-xr-x 3/20      240 May 19 22:11 1996 amanda-2.3.0
```

在快速查看之后，源码似乎解压了。但是，我们精心制作的文件在哪里？为什么 `tools/munge` 没有被修改？

### 20.3.4 应用补丁

也许我们的 `%prep` 脚本太简单了。我们需要应用补丁。因此让我们在 spec 文件中添加两项：

1. 指向我们补丁文件的标签行
2. `%prep` 脚本中的 `%patch` 宏

足够简单。在 spec 文件的顶部，与其他标签一起，我们添加：

`Patch: amanda-2.3.0-linux.patch`

然后我们将我们的 `%prep` 脚本看起来像这样：

`%prep`

`%setup`

`%patch -p 1`

那里，应该就可以了。让我们再次尝试那个 `-bp` 选项：

```
# rpm -bp amanda-2.3.0.spec
* Package: amanda
* Package: client
* Package: server
+ umask 022
+ echo Executing: %prep
Executing: %prep
+ cd /usr/src/redhat
+ cd /usr/src/redhat/BUILD
+ rm -rf amanda-2.3
+ gzip -dc /usr/src/redhat/SOURCES/amanda-2.3.0.tar.gz
+ tar -xwvf -
drwxr-xr-x 3/20      0 May 19 22:10 1996 amanda-2.3.0/
--rw-r--r-- 3/20     1389 May 19 22:11 1996 amanda-2.3.0/COPYRIGHT
--rw-r--r-- 3/20     1958 May 19 22:11 1996 amanda-2.3.0/Makefile
--rw-r--r-- 3/20    11036 May 19 22:11 1996 amanda-2.3.0/README
--rw-r--r-- 3/20     2010 May 19 22:11 1996 amanda-2.3.0/man/antape.8
drwxr-xr-x 3/20      240 May 19 22:11 1996 amanda-2.3.0/tools/
--rw-r--r-- 3/20     437 May 19 22:11 1996 amanda-2.3.0/munge
```

## 292 真实世界的包构建

```
drwxr-xr-x 3/20      O May 19 22:11 1996 amanda-2.3.0/tools/
-rwxr-xr-x 3/20      2437 May 19 22:11 1996 amanda-2.3.0/tools/munge
+ [ 0 -ne 0]
+ cd amanda-2.3.0
+ cd /usr/src/redhat/BUILD/amanda-2.3.0
+ chown -R root .
+ chmod -R a+X,g-w,o- -
+ echo Patch #0:
+ patch -pi -s
+ exit 0
#
```

没有太大区别，直到最后，，我们看到补丁被应用了。让我们查看构建区域，看看配置文件是否在那里：

```
# cd /usr/src/redhat/BUILD/amanda-2.3.0/config
# ls -l
total 58
-rw-r--r-- 1 root root      7518 May 19 1996 config-common.h
-rw-r--r-- 1 root root      1846 Nov 20 20:46 config.h
-rw-r--r-- 1 root root      2081 May 19 1996 config.h-aix
-rw-r--r-- 1 root root      1690 May 19 1996 config.h-bsdnl
...
-rw-r--r-- 1 root root      1830 May 19 1996 config.h-ultrix4
-rw-r--r-- 1 root root           0 Nov 20 20:46 config.h.orig
-rw-r--r-- 1 root root      7196 Nov 20 20:46 options.h
-rw-r--r-- 1 root root      7236 May 19 1996 options.h-vanilla
-rw-r--r-- 1 root root           0 Nov 20 20:46 options.h.orig
#
```

好多了。这些零长度的 `.orig` 文件表明补丁已经应用到 `config.h` 和 `options.h` 上。在 `tools` 目录下，`munge` 也被修改了。这些源码已经准备好构建！

### 20.3.5 让 RPM 构建

我们知道源码已经就绪。知道 `%script` 也就绪。如果我们让 RPM 构建 amanda，不应该有意外。让我们使用 `-bc` 选项在 `%build` 脚本完成后停止：

```
# rpm -bc amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
```

## 20.3 使用 RPM 进行构建

```
echo Executing: %build
Executing: %build
+ cd /usr/src/redhat/BUILD
+ amanda-2.3.0
+ make
```

```
Making all in common-src
make[1]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/common-src'
../tools/munge Makefile.in
make[2]: Entering directory '/usr/src/redhat/BUILD/amanda-2.3.0/common-src'
cc -g -I./../config -o error.o
cc -g -I./../config -c alloc.o -o alloc.o
```
