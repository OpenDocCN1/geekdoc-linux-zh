
在这个示例中，`build` 命令的唯一其他参数是软件包的规范文件（spec file）名称。可以使用通配符来构建多个软件包，但在我们的示例中，我们只使用一个。

让我们看看构建过程中 RPM 的输出：

```
* Package: cdplayer
+ umask 022
+ echo Executing: `%prep
Executing: `%prep
+ cd /usr/src/redhat/BUILD
+ cd /usr/src/redhat/BUILD
+ rm -rf cdplayer-1.0
+ gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz
+ tar -xvzf -
drwxrwxr-x root/users           0 Aug  4 22:30 1996 cdplayer-1.0/
-rw-r--r-- root/users       17982 Nov 10 01:10 1995 cdplayer-1.0/COPYING
-rw-r--r-- root/users           627 Nov 10 01:10 1995 cdplayer-1.0/ChangeLog
-rw-r--r-- root/users           482 Nov 10 01:11 1995 cdplayer-1.0/INSTALL
.
.
.
-rw-r--r-- root/users       2728 Nov 10 01:10 1995 cdplayer-1.0/struct.h
-rw-r--r-- root/users          730 Nov 10 01:10 1995 cdplayer-1.0/vol.c
-rw-r--r-- root/users       2806 Nov 10 01:10 1995 cdplayer-1.0/volume.c
-rw-r--r-- root/users       1515 Nov 10 01:10 1995 cdplayer-1.0/volume.h
+ [ 0 -ne 0 ]
+ cd cdplayer-1.0
+ cd /usr/src/redhat/BUILD/cdplayer-1.0
+ chown -R root:root .
+ chmod -R a+rX,g-w,o-w .
+ exit 0
```

输出继续下去，但让我们在此暂停一下，讨论一下到目前为止发生了什么。

在输出的开始，RPM 显示软件包名称（`cdplayer`），设置 umask，并开始执行 `%prep` 部分。得益于 `%setup` 宏，RPM 随后进入构建区域目录，删除任何现有的旧源代码，并从原始的压缩 tar 文件中提取源代码。虽然每个文件在提取时都会列出，但为了节省空间，我们省略了大部分列出的文件。

`%setup` 宏继续将目录更改为 `cdplayer` 的顶级源代码目录，并正确设置文件所有权和权限。正如你所见，它为你做了很多工作。

接下来，让我们看看 `%build` 部分的输出：

```
+ umask 022
+ echo Executing: `%build
Executing: `%build
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ make
gcc -Wall -O2 -c -I/usr/include/ncurses cdp.c
gcc -Wall -O2 -c -I/usr/include/ncurses color.c
gcc -Wall -O2 -c -I/usr/include/ncurses display.c
gcc -Wall -O2 -c -I/usr/include/ncurses misc.c
gcc -Wall -O2 -c -I/usr/include/ncurses volume.c
volume.c: In function ‘mix_set_volume’:
volume.c:67: warning: implicit declaration of function ‘ioctl'
gcc -Wall -O2 -c -I/usr/include/ncurses hardware.c
gcc -Wall -O2 -c -I/usr/include/ncurses database.c
gcc -Wall -O2 -c -I/usr/include/ncurses getline.c
gcc -o cdp cdp.o color.o display.o misc.o volume.o hardware.o database.o
g getline.o -I/usr/include/ncurses -L/usr/lib -lncurses
groff -Tascii -man cdp.1| compress >cdp.1.Z
\ exit 0
```

这里没有任何意外。在设置 umask 并将目录更改为 `cdplayer` 的顶级目录之后，RPM 执行了我们在规范文件中放入的 `make` 命令。输出的其余部分来自 `make`，因为它实际上正在构建软件。接下来是 `%install` 部分：

```
+ umask 022
+ echo Executing: %install
Executing: %install
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ make install
chmod 755 cdp
chmod 644 cdp.1.Z
cp cdp /usr/local/bin
ln -s /usr/local/bin/cdp /usr/local/bin/cdplay
cp cdp.1 /usr/local/man/man1
+ exit 0
```

就像前面的部分一样，RPM 再次设置 umask 并将目录更改为正确的目录。然后它执行 `cdplayer` 的安装目标，将新构建的软件安装在构建系统上。那些仔细研究过规范文件的人可能已经注意到，README 文件不是安装部分的一部分。这不是问题，正如我们所见：

```
+ umask 022
+ echo Executing: special doc
Executing: special doc
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ DOCDIR=/usr/doc/cdplayer-1.0-1
+ rm -rf /usr/doc/cdplayer-1.0-1
+ mkdir -p /usr/doc/cdplayer-1.0-1
+ cp -a README /usr/doc/cdplayer-1.0-1
+ exit 0
```

在习惯性的 umask 和 cd 命令之后，RPM 构建将用于 `cdplayer` 文档目录的路径。然后它清理任何预先存在的目录，并将 README 文件复制到其中。现在应用程序已安装在构建系统上。唯一剩下的事情是创建实际的软件包文件并执行一些清理工作。二进制软件包文件首先被创建：

```
Binary Packaging: cdplayer-1.0-1
Finding dependencies...
Requires (2): libc.so.5 libncurses.so.2.0
usr/doc/cdplayer-1.0-1
usr/doc/cdplayer-1.0-1/README
usr/local/bin/cdp
usr/local/bin/cdplay
usr/local/man/man1/cdp.1
93 blocks
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/cdplayer-1.0-1.i386.rpm
```

第一行说明了一切：RPM 正在为版本 1.0、发布 1 的 **cdplayer** 创建二进制软件包。接下来，RPM 确定 **cdplayer-1.0-1** 需要哪些软件包。这个过程的一部分涉及对软件包中的每个可执行程序运行 **ldd**。在这个例子中，该过程需要库 **libc.so.5** 和 **libncurses.so.2.0**。规范文件中可以包含其他依赖项信息，但在我们的示例中，我们将保持简单。

依赖项信息之后是软件包中包含的每个目录和文件的列表。显示的实际列表是 **cpio** 的输出，这是 RPM 用于打包软件包文件的归档软件。**93 blocks** 也是由 **cpio** 打印的。

**Generating signature: 0** 这一行意味着 RPM 未被指示向软件包文件添加 PGP 签名。然而，在此期间，RPM 仍然添加两个签名，可用于验证软件包文件的大小和 MD5 校验和。最后，我们看到 RPM 已创建二进制软件包文件的确认。

此时，应用程序已构建完成，并且应用程序的文件已打包。不再需要构建过程中创建的任何文件，因此可以将其删除。对于提取到 RPM 构建目录中的源代码，我们可以看到，最坏的情况下，它们将在下次构建软件包时被删除。但如果有需要删除的文件怎么办？好吧，它们可以在 **%clean** 部分中删除：

```
+ umask 022
+ echo Executing: %clean
Executing: %clean
+ cd /usr/src/redhat/BUILD
+ cd cdplayer-1.0
+ exit 0
```

在这个示例中，**cdplayer** 构建期间没有生成构建目录之外的其他文件，因此我们不需要付出额外的努力来清理。

RPM 执行的最后一步是创建源代码软件包文件：

```
Source Packaging: cdplayer-1.0-1
cdplayer-1.0.spec
cdplayer-1.0.tgz
80 blocks
Generating signature: 0
Wrote: /usr/src/redhat/SRPMS/cdplayer-1.0-1.src.rpm
#
```

该文件包含重新创建二进制软件包文件所需的一切，以及它自身的一份副本。在这个例子中，做这件事所需的唯一文件是原始源代码和规范文件。如果需要修改原始源代码，则源代码软件包包含一个或多个补丁文件。与创建二进制软件包时一样，我们看到 `cpio` 的输出列出了每个归档文件以及归档的块大小。

与二进制软件包一样，源代码软件包文件也可以附加 PGP 签名。在我们的案例中，我们看到没有附加 PGP 签名。RPM 的最后一条消息是确认源代码软件包的创建。让我们看看最终产物。首先，看看二进制软件包：

```
# ls -lF /usr/src/redhat/RPMS/i386/cdplayer-1.0-1.i386.rpm
-rw-r--r--- 1 root root 24698 Aug  6 22:22 RPMS/i386/cdplayer-1.0-1.i386.rpm
#
```

注意，我们在基于 Intel 的系统上构建了 `cdplayer`，因此 RPM 将二进制软件包文件放在 `i386` 子目录中。

接下来，看看源代码软件包文件：

```
# ls -lF /usr/src/redhat/SRPMS/cdplayer-1.0-1.src.rpm
-rw-r-r--- 1 root root 41380 Aug  6 22:22 SRPMS/cdplayer-1.0-1.src.rpm
#
```

一切进行得非常完美——我们现在拥有了可供使用的二进制和源代码软件包文件。但有时事情并不那么顺利。

## 11.5. 当事情出错时

这个示例有点童话色彩，因为它第一次就完美地完成了。在现实生活中，往往需要几次尝试才能做对。

### 11.5.1. 构建期间的问题

正如本章前面所暗示的，RPM 可以在构建过程的各个点停止。这允许软件包构建者查看构建目录，确保一切正常进行。如果有问题，在构建过程中停止可以让他们确切地看到出了什么问题以及在哪里。以下是 RPM 在构建过程中可以停止的点的列表：

- 在 `%prep` 部分之后
- 在对 `%files` 列表进行一些粗略检查之后
- 在 `%build` 部分之后
- 在 `%install` 部分之后
- 在二进制软件包创建之后

此外，还有一种方法允许软件包构建者绕过构建过程，并指示 RPM 跳过初始步骤。当应用程序尚未时，这非常有用
