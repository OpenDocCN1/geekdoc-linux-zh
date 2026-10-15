
```
[root@server1 conky-1.9.0]# make
Making all in src
make[1]: Entering directory '/home/user1/Downloads/conky-1.9.0/src'
make all-am
make[2]: Entering directory '/home/user1/Downloads/conky-1.9.0/src'
gcc -DHAVE_CONFIG_H -I -DSYSTEM_CONFIG_FILE="/usr/local/etc/conky/conky.conf" -CPPAGLIBDIR="/usr/local/lib/conky" -I/usr/include/freetype2 -I/usr/include/libpng16 -I/usr/include/uuid -I/usr/include/glib-2.0 -I/usr/lib64/glib-2.0/include -Wall -W -MT conky_conf.cookie.o -MD -MP -MF .deps/conky_conf.cookie.tmp -o conky_conf.cookie.o -f 'conf_cookie.c' | echo '' > /conky_cookie.c
mv -f .deps/conky_conf.cookie.tmp .deps/conky_cookie.o
gcc -DHAVE_CONFIG_H -I -DSYSTEM_CONFIG_FILE="/usr/local/etc/conky/conky.conf" -CPPAGLIBDIR="/usr/local/lib/conky" -I/usr/include/freetype2 -I/usr/include/libpng16 -I/usr/include/uuid -I/usr/include/glib-2.0 -I/usr/lib64/glib-2.0/include -Wall -W -MT conky_mpd.o -MD -MP -MF .deps/conky_mpd.tmp -o conky_mpd.o -f 'mpd.c' | echo '' > ./mpd.c
mv -f .deps/conky_mpd.tmp .deps/conky_mpd.o
gcc -DHAVE_CONFIG_H -I -DSYSTEM_CONFIG_FILE="/usr/local/etc/conky/conky.conf" -CPPAGLIBDIR="/usr/local/lib/conky" -I/usr/include/freetype2 -I/usr/include/libpng16 -I/usr/include/uuid -I/usr/include/glib-2.0 -I/usr/lib64/glib-2.0/include -Wall -W -MT conky_libclient.o -MD -MP -MF .deps/conky_libclient.tmp -o conky_libclient.o -f 'libclient.c' | echo '' > /conky_libclient.c
mv -f .deps/conky_libclient.tmp .deps/conky_libclient.o
gcc -DHAVE_CONFIG_H -I -DSYSTEM_CONFIG_FILE="/usr/local/etc/conky/conky.conf" -CPPAGLIBDIR="/usr/local/lib/conky" -I/usr/include/freetype2 -I/usr/include/libpng16 -I/usr/include/uuid -I/usr/include/glib-2.0 -I/usr/lib64/glib-2.0/include -Wall -W -MT conky_libclient.o
```

# 第 11 章压缩、系统备份与软件安装

在安装 RPM 软件包后，RPM 数据库（存储在 `/var/lib/rpm` 目录下的文件）会更新，其中包含该软件包及其包含的文件信息。要查询安装后的完整包名称，可以使用软件包的常用名称配合 `rpm` 命令的 `-q`（query）选项来实现：

```
[root@server1 ~]# rpm -q bluefish
bluefish-2.2.10-8.fc28.x86_64
[root@server1 ~]#
```

此外，你可以在上述命令中添加 `-i`（info）功能，以显示 `bluefish` 软件包的详细信息：

```
[root@server1 ~]# rpm -qi bluefish
Name : bluefish
Version : 2.2.10
Release : 8.fc28
Architecture : x86_64
Install Date : Sat 29 Sep 2019 11:29:11 AM EDT
Group : Unspecified
Size : 1635419
License : GPLv3+
Signature : RSA/SHA256, Tue 13 Feb 2019 04:34:43 AM EST, Key ID 0e8e7e69db62fb1
Source RPM : bluefish-2.2.10-8.fc28.src.rpm
Build Date : Tue 13 Feb 2019 04:29:42 AM EST
Build Host : buildvm-10.phx2.fedoraproject.org
Relocations : (not relocable)
Packager : Fedora Project
Vendor : Fedora Project
URL : http://bluefish.openoffice.n/
Summary : Web development application for experienced users
Description : 
Bluefish 是一个为经验丰富的网页设计师和程序员设计的强大编辑器。Bluefish 支持许多编程和标记语言，但它专注于动态和交互式网站的编辑。
[root@server1 ~]# _
```

由于红帽包管理器跟踪所有已安装的文件，你可以通过 `-q -l`（list）选项后接 RPM 名称来列出软件包包含的所有文件，从而找到 `bluefish` 程序的可执行文件。以下命令列了 `bluefish` 软件包的前 10 个文件：

```
[root@server1 ~]# rpm -ql bluefish
/usr/bin/bluefish
/usr/lib/lib64/bluefish
/usr/lib64/bluefish/about.so
/usr/lib64/bluefish/charmap.so
/usr/lib64/bluefish/entities.so
/usr/lib64/bluefish/htmlbar.so
/usr/lib64/bluefish/infbrowser.so
/usr/lib64/bluefish/snippets.so
/usr/lib64/bluefish/zencoding.so
/usr/share/licenses/bluefish
/usr/share/licenses/bluefish/COPYING
[root@server ~]#
```

从上面的输出中你可以看到可执行文件的路径为 `/usr/bin/bluefish`，它位于 `PATH` 变量中的一个目录下。在桌面环境中执行时，你将看到图 11-4 所示的屏幕。

![](img/255973d661f18692a98dbc628624ab00_618_0.png)

图 11-4 的 `bluefish` 程序

相反，你可以使用 `rpm` 命令的 `-q` 和 `-f`（file）选项后接文件名，查找特定文件属于哪个 RPM 软件包：

```
[root@server ~]# rpm -qf /usr/bin/bluefish
bluefish-2.2.10-8.fc28.x86_64
[root@server ~]#
```

要从系统中移除 RPM 软件包，你可以使用 `rpm` 命令的 `-e` 选项；所有属于该软件包也将被删除。要删除 `bluefish` 和 `bluefish-shared-data` RPM 软件包并验证删除情况，可以使用以下命令：

```
[root@server1 ~]# rpm -e bluefish bluefish-shared-data
[root@server1 ~]# rpm -q bluefish bluefish-shared-data
package bluefish is not installed
package bluefish-shared-data is not installed
[root@server1 ~]#
```

表 11-9 显示了用于 `rpm` 命令的常用选项列表。

| 选项 | 说明 |
| :--- | :--- |
