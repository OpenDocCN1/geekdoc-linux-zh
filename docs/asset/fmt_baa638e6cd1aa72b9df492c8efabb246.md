
等待，OCR 文本末尾有一些重复和杂质。我将根据提供的文本清理逻辑流。

（重新评估文本的最后部分）：编译完成后，可以通过输入以下命令将这些二进制程序拷贝到文件系统的正确位置：

```bash
[rootserver1 rdesktop-1.3.1]# make install
mkdir -p /usr/local/bin
install rdesktop /usr/local/bin
```

```bash
strip /usr/local/bin/rdesktop
chmod 755 /usr/local/bin/rdesktop
mkdir -p /usr/local/share/rdesktop/keymaps/
cp keymaps?? keymaps??* /usr/local/share/rdesktop/keymaps/
cp keymaps/common /usr/local/share/rdesktop/keymaps/
cp keymaps/modifiers /usr/local/share/rdesktop/keymaps/
chmod 644 /usr/local/share/rdesktop/keymaps/*
```

## 使用 RPM 安装程序

Red Hat 包管理器格式是通过互联网分发的 Linux 软件最常用的格式。这种格式的软件包的文件名指明编译软件的架构，并以 `.rpm` 扩展结尾。以下输出表示 `bluefish` 软件包（一个网页）0.13：

要安装 RPM 软件包，可以使用 `rpm` 命令的 `-i` 选项。此外，你可以使用 `-v` 和 `-h` 选项分别在安装期间打印冗余信息和哈希标记。以下命令使用这些选项安装了 `bluefish` 软件包：

```bash
[server1]# rpm -ivh bluefish-0.13-1.1.fc2.i86.rpm
Preparing...########################## [100%]
1:bluefish ######################## [100%]
```

> 某些 RPM 软件包要求系统中安装其他 RPM 软件包；这些被称为软件包依赖。如果你尝试安装带有依赖关系的 RPM 软件包，将收到一个指示需要安装哪些 RPM 软件包的错误消息。安装这些这些软件包后，你就可以成功安装所需的 RPM。

完成后，RPM 数据库（存储在 `/var/lib/rpm` 目录的文件）包含了软件包及其包含的文件的信息。要在安装后查询完整包名，可以使用 `rpm` 命令的 `-q`（查询）选项，后跟软件包的通用名称：

```bash
[server1]# rpm -q bluefish
bluefish-0.13-1.1.fc2
```

此外，你可以在上述命令中添加 `-i`（信息）选项以显示 `bluefish` 软件包的详细包信息：

```bash
[server1]# rpm -qi bluefish
Name : blue Relocations: (not relocatable)
Version : 0.13 Vendor: http://dag.wieers.com/apt/
Release : 1.1.fc2.dag Build Date: 15 May 2004 07:57:46 AM
Install Date: 01 Aug 2005 08:56:44 PM
Build Host: localhost
```

### 软件安装 553

组：Development/Tools

RPM: `bluefish-0.13-1.1.fc2.dag.src.rpm`

大小：5883879

许可证：GPL

签名：DSA/SHA1, 2004年5月15日 上08:13:04, Key ID `a20e52146b8d79e6`

打包：Dag Weiers <dag@weiers.nl>

URL：http://bluefish.openoffice.nl/

摘要：面向经验用户的图形化 Web 开发应用程序

描述：

Bluefish 是面向经验丰富的网页设计师或程序员的 GTK+ HTML 编辑器。它尚未完成，但已经是一个非常强大的创建环境。Bluefish 对编程动态和交互式网站提供了扩展支持，例如提供了大量的 PHP 支持。

```
[root@server1]# _
```

由于红帽包管理器（RPM）跟踪所有安装的文件，你可以使用 `-q` 和 `-l`（列出）选项加上包名来列出包内的所有文件，从而找到 `bluefish` 程序的可执行文件：

```
[root@server1]# rpm -ql bluefish
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
/usr/share/bluefish/funcref_php.png
/usr/share/bluefish/funcref_python.png
/usr/share/bluefish/highlighting.default
/usr/share/bluefish/icon_c.png
/usr/share/bluefish/icon_cfml.png
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
```

`/usr/share/doc/bluefish-0.13`

`/usr/share/doc/bluefish-0.13/AUTHORS`

`/usr/share/doc/bluefish-0.13/COPYING`

`/usr/share/doc/bluefish-0.13/README`

`/usr/share/doc/bluefish-0.13/TODO`

`/usr/share/locale/bg/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/cs/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/da/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/de/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/el/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/es/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/fi/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/fr/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/hu/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/it/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/ja/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/nl/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/no/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/pl/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/pt_PT/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/pt_BR/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/ro/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/ru/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/sr/LC_MESSAGES/bluefish.mo`

`/usr/share/locale/sv/LC_MESSAGES/bluefish.mo`
