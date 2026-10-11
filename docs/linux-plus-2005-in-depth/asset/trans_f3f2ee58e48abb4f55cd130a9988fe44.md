
# 压缩、备份和软件安装

```
chmod 644 /usr/local/share/rdesktop/keymaps/*
mkdir -p /usr/local/man/man1
cp doc/rdesktop.1 /usr/local/man/man1
chmod 644 /usr/local/man/man1/rdesktop.1
[root@server1 rdesktop-1.3.1]# _
```

在编译并复制到适当目录后（README 文件通常包含程序的位置），你可以删除源代码和 tar 包，并找到程序的主二进制文件，如下例所示：

```
[root@server1 rdesktop-1.3.1]# cd ..
[root@server1 root]# rm -rf rdesktop-1.3.1
[root@server1 root]# rm -f rdesktop-1.3.1.tar.gz
[root@server1 root]# which rdesktop
/usr/local/bin/rdesktop
[root@server1 root]# _
```

接下来，你可以查看 `rdesktop` 手册页，然后切换到桌面环境并运行命令 `rdesktop remote_server_name` 连接到运行远程桌面协议的远程 Windows 服务器，如图 12-3 所示。

![](img/09bf13b782f71165e17bb3839040c96a_497_0.png)

# 使用 RPM 安装程序

红帽软件包管理器（Red Hat Package Manager）格式是通过互联网分发 Linux 软件最广泛使用的格式。该格式的软件包文件名表明软件编译所针对的硬件架构，并以 .rpm 扩展名结尾。以下输出表明 bluefish RPM 软件包（一种网页编辑器）版本 0.1.13-1.1 是为 Fedora Core 2 (fc2) 在 Intel i386 平台上编译的：

```
[root@server1 root]# ls -F
Desktop/ bluefish-0.1.13-1.1.fc2.i386.rpm
[root@server1 root]# _
```

要安装 RPM 软件包，你可以使用 **rpm** 命令的 -i 选项。此外，你可以使用 -v 和 -h 选项分别在安装过程中打印详细信息和哈希标记。以下命令使用这些选项安装 bluefish RPM 软件包：

```
[root@server1 root]# rpm -ivh bluefish-0.1.13-1.1.fc2.i386.rpm
Preparing... ################################################ [100%]
1:bluefish ################################################ [100%]
[root@server1 root]# _
```

![](img/09bf13b782f71165e17bb3839040c96a_498_0.png)

## 注意

某些 RPM 软件包要求先在你的系统上安装其他 RPM 软件包；这些被称为**软件包依赖项**。如果你尝试安装具有软件包依赖项的 RPM 软件包，你会收到一条错误消息，指示需要先安装哪些 RPM 软件包。安装这些先决软件包后，你可以成功安装所需的 RPM 软件包。

安装完成后，RPM 数据库（存储在 /var/lib/rpm 目录中的文件中）包含关于软件包及其包含文件的信息。要在安装后查询完整的软件包名称，你可以使用 rpm 命令的 -q（查询）选项后跟软件包的通用名称：

```
[root@server1 root]# rpm -q bluefish
bluefish-0.1.13-1.1.fc2
[root@server1 root]# _
```

此外，你可以向上述命令添加 -i（信息）选项以显示 bluefish 软件包的详细软件包信息：

```
[root@server1 root]# rpm -qi bluefish
Name : bluefish Relocations: (not relocatable)
Version : 0.13 Vendor: http://dag.wieers.com/apt/
Release : 1:1. fc2.dag Build Date: 15 May 2004 07:57:46 AM
Install Date: 01 Aug 2005 08:56:44 PM Build Host: localhost
Group Development/Tools Source RPM: bluefish-0.13-1.1.fc2.dag.src.rpm
Size : 5883879 License: GPL
Signature: DSA/SHA1, 15 May 2004 08:13:04 AM, Key ID a20e52146b8d79e6
Packager : Dag Wieers <dag@wieers.com>
URL : http://bluefish.openoffice.nl/
Summary : Graphical Web development application for experienced users
Description :
Bluefish is a GTK+ HTML editor for the experienced Web designer or programmer. It is not finished yet, but already a very powerful site-creating environment. Bluefish has extended support for programming dynamic and interactive Web sites. There is, for example, a lot of PHP support.
[root@server1 root]# _
```

由于红帽软件包管理器会跟踪所有已安装的文件，因此你可以使用 -q 和 -l（列表）选项后跟软件包名称来列出软件包中包含的所有文件，从而找到 bluefish 程序的可执行文件：

```
[root@server1 root]# rpm -ql bluefish
/usr/bin/bluefish
/usr/share/application-registry/bluefish.applications
/usr/share/applications/bluefish.desktop
/usr/share/bluefish
/usr/share/bluefish/bluefish_splash.png
/usr/share/bluefish/custom_menu.default
/usr/share/bluefish/encodings.default
/usr/share/bluefish/filetypes.default
/usr/share/bluefish/funcref_css.xml
/usr/share/bluefish/funcref_html.xml
/usr/share/bluefish/funcref_php.xml
/usr/share/bluefish/funcref_python.xml
/usr/share/bluefish/highlighting.default
/usr/share/bluefish/icon_c.png
/usr/share/bluefish/icon_cfm.png
/usr/share/bluefish/icon_dir.png
/usr/share/bluefish/icon_html.png
/usr/share/bluefish/icon_image.png
/usr/share/bluefish/icon_java.png
/usr/share/bluefish/icon_pascal.png
/usr/share/bluefish/icon_php.png
/usr/share/bluefish/icon_python.png
/usr/share/bluefish/icon_r.png
/usr/share/bluefish/icon_unknown.png
/usr/share/bluefish/icon_xml.png
/usr/share/doc/bluefish-0.13
/usr/share/doc/bluefish-0.13/AUTHORS
/usr/share/doc/bluefish-0.13/COPYING
/usr/share/doc/bluefish-0.13/README
/usr/share/doc/bluefish-0.13/TODO
/usr/share/locale/bg/LC_MESSAGES/bluefish.mo
/usr/share/locale/cs/LC_MESSAGES/bluefish.mo
/usr/share/locale/da/LC_MESSAGES/bluefish.mo
/usr/share/locale/de/LC_MESSAGES/bluefish.mo
/usr/share/locale/el/LC_MESSAGES/bluefish.mo
/usr/share/locale/es/LC_MESSAGES/bluefish.mo
/usr/share/locale/fi/LC_MESSAGES/bluefish.mo
/usr/share/locale/fr/LC_MESSAGES/bluefish.mo
/usr/share/locale/hu/LC_MESSAGES/bluefish.mo
/usr/share/locale/it/LC_MESSAGES/bluefish.mo
/usr/share/locale/ja/LC_MESSAGES/bluefish.mo
/usr/share/locale/nl/LC_MESSAGES/bluefish.mo
/usr/share/locale/no/LC_MESSAGES/bluefish.mo
/usr/share/locale/pl/LC_MESSAGES/bluefish.mo
/usr/share/locale/pt/LC_MESSAGES/bluefish.mo
/usr/share/locale/pt_BR/LC_MESSAGES/bluefish.mo
/usr/share/locale/ro/LC_MESSAGES/bluefish.mo
/usr/share/locale/ru/LC_MESSAGES/bluefish.mo
/usr/share/locale/sr/LC_MESSAGES/bluefish.mo
/usr/share/locale/sv/LC_MESSAGES/bluefish.mo
/usr/share/locale/ta/LC_MESSAGES/bluefish.mo
/usr/share/locale/zh_CN/LC_MESSAGES/bluefish.mo
/usr/share/mime-info/bluefish.keys
/usr/share/mime-info/bluefish.mime
/usr/share/pixmaps/bluefish-icon.png
/usr/share/pixmaps/gnome-app-list-bluefish.png
[root@server1 root]#
```

从上面的输出中，你可以看到可执行文件的路径名是 **/usr/bin/bluefish**，它位于我们 **PATH** 变量中的某个目录中。在桌面环境中执行时，你会看到图 12-4 中描绘的屏幕。

![](img/09bf13b782f71165e17bb3839040c96a_501_0.png)

相反，你可以使用 **rpm** 命令的 **-q** 和 **-f**（文件）选项后跟文件名来查找某个文件属于哪个软件包：

```
[root@server1 root]# rpm -qf /usr/bin/bluefish
bluefish-0.13-1.1.fc2
[root@server1 root]#
```

要从系统中删除软件包，你可以使用 rpm 命令的 -e 选项；属于该软件包的所有文件也将被删除。要删除 bluefish 软件包并验证其删除，你可以使用以下命令：

```
[root@server1 root]# rpm -e bluefish
[root@server1 root]# rpm -q bluefish
package bluefish is not installed
[root@server1 root]# _
```

表 12-8 显示了与 rpm 实用程序一起使用的常见选项列表。

**表 12-8 与 rpm 实用程序一起使用的常见选项**

| 选项 | 描述 |
| :--- | :--- |
| -a, --all | 显示系统上安装的所有软件包名称（与 -q 选项一起使用时） |
| -e, -erase | 从系统中删除指定的软件包 |
| -F, --freshen | 仅当系统上存在旧版本时，升级指定的软件包 |
| -f, --file | 显示指定文件所属的软件包（与 -q 选项一起使用时） |
| -h, --hash | 在屏幕上打印哈希标记以指示安装进度（与 -i 选项一起使用时） |
| -i, --install | 安装指定的软件包（前提是使用 -q 选项时） |

