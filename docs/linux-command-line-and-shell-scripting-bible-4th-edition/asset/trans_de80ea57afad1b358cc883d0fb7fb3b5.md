

推荐：libgdbm6 (>= 1.16), libncursesw6 (>= 6), libpre3
建议：zsh-doc
主页：https://www.zsh.org/
下载大小：707 kB
APT 来源：http://us.archive.ubuntu.com/ubuntu focal/main amd64 Packages
描述：拥有许多功能的 shell

Zsh 是一个 UNIX 命令解释器（shell），可用作交互式登录 shell 以及 shell 脚本命令处理器。在标准 shell 中，zsh 与 ksh 最为相似，但包含许多增强功能。Zsh 具有命令行编辑、内置拼写纠正、可编程命令补全、shell 函数（支持自动加载）、历史记录机制以及众多其他功能。

$

> **注意**
> **`apt show` 命令并不表示该包已安装在系统上。它仅显示软件仓库中的详细包信息。**

通过 apt 无法获取的一项详细信息是列出与特定软件包相关的所有文件。要获取此列表，你需要直接使用 dpkg 命令：

```
dpkg -L package_name
```

下面是一个使用 dpkg 列出作为 acl 包一部分安装的所有文件的示例：

```
$ dpkg -L acl
/.
/bin
/bin/chacl
/bin/getfacl
/bin/setfacl
/usr
/usr/share
/usr/share/doc
/usr/share/doc/acl
/usr/share/doc/acl/copyright
/usr/share/man
/usr/share/man/man1
/usr/share/man/man1/chacl.1.gz
/usr/share/man/man1/getfacl.1.gz
/usr/share/man/man1/setfacl.1.gz
/usr/share/man/man5
/usr/share/man/man5/acl.5.gz
/usr/share/doc/acl/changelog.Debian.gz
$
```

你还可以进行反向操作——查找特定文件属于哪个包：

```
dpkg --search *absolute_file_name*
```

注意，为了使此操作生效，你需要使用绝对文件引用：

```
$ dpkg --search /bin/getfacl
acl: /bin/getfacl
$
```

输出显示 getfacl 文件是作为 *acl* 包的一部分安装的。

## 使用 apt 安装软件包

既然你已经了解了如何查看系统上的软件包信息，本节将指导你进行软件包安装。首先，你需要确定要安装的包名。如何找到特定的软件包？使用带有 search 命令的 *apt*：

```
apt search *package_name*
```

search 命令的优点在于你不需要在 *package_name* 周围插入通配符。通配符是隐含的。默认情况下，search 命令显示那些包名或包描述中包含搜索词的软件包，这有时可能会产生误导。如果你希望将输出限制为仅包名，请包含 --names-only 选项：

```
$ apt --names-only search zsh
```

正在排序... 完成
全文搜索... 完成
fizzsh/focal,focal 1.0.9-1 all
    友好的交互式 ZShell

zsh/focal 5.8-3ubuntu1 amd64
    拥有许多功能的 shell

zsh-antigen/focal,focal 2.2.3-2 all
    管理你的 zsh 插件

zsh-autosuggestions/focal,focal 0.6.4-1 all
    为 zsh 提供类似 Fish 的快速/无干扰自动建议

zsh-common/focal,focal 5.8-3ubuntu1 all
    Zsh 的架构无关文件

zsh-dev/focal 5.8-3ubuntu1 amd64
    拥有许多功能的 shell（开发文件）

zsh-doc/focal,focal 5.8-3ubuntu1 all
    zsh 文档 - info/HTML 格式

zsh-static/focal 5.8-3ubuntu1 amd64
    拥有许多功能的 shell（静态链接）

zsh-syntax-highlighting/focal,focal 0.6.0-3 all
    为 zsh 提供类似 Fish shell 的语法高亮

zsh-theme-powerlevel9k/focal,focal 0.6.7-2 all
    powerlevel9k 是 zsh 的一个主题，使用 powerline 字体

zshdb/focal,focal 1.1.2-1 all
    Z-Shell 脚本的调试器
$

一旦找到你想要安装的包，使用 apt 安装它就像下面这样简单：

```
apt install package_name
```

输出将显示关于该软件包的基本信息，并询问你是否要继续安装：

```
$ sudo apt install zsh
[sudo] rich 的密码：
正在读取软件包列表... 完成
正在构建依赖树
正在读取软件包状态信息... 完成
将要安装以下附加软件包：
  zsh-common
建议的软件包：
  zsh-doc
将要安装以下新软件包：
  zsh zsh-common
升级 0 个，新安装 2 个，移除 0 个，有 56 个未升级。
需要下载 4,450 kB 的归档文件。
此操作完成后，将额外使用 18.0 MB 磁盘空间。
你想要继续吗？ [Y/n] y
获取:1 http://us.archive.ubuntu.com/ubuntu focal/main amd64
zsh-common all 5.8-3ubuntu1 [3,744 kB]
获取:2 http://us.archive.ubuntu.com/ubuntu focal/main amd64
zsh amd64 5.8-3ubuntu1 [707 kB]
在 4 秒内获取了 4,450 kB (1,039 kB/s)
正在选择此前未选择的软件包 zsh-common。
(正在读取数据库 ... 当前已安装 179515 个文件和目录。)
准备解包 .../zsh-common_5.8-3ubuntu1_all.deb ...
正在解包 zsh-common (5.8-3ubuntu1) ...
正在选择此前未选择的软件包 zsh。
准备解包 .../zsh_5.8-3ubuntu1_amd64.deb ...
正在解包 zsh (5.8-3ubuntu1) ...
正在设置 zsh-common (5.8-3ubuntu1) ...
正在设置 zsh (5.8-3ubuntu1) ...
正在处理 man-db (2.9.1-1) 的触发器 ...
$
```

### 注意

在上面的列表中的 apt 命令之前，使用了 sudo 命令。sudo 命令允许你以 root 用户身份运行命令。你可以使用 sudo 命令执行管理任务，例如安装软件。

若要检查安装是否成功处理，只需再次使用带有 --installed 选项的 list 命令。你应该能看到该包出现，表明它已安装。

请注意，在安装请求的软件包时，apt 还要求安装其他软件包。这是因为 apt 会自动为我们解析必要的软件包依赖关系，并安装所需的附加库和软件包。这是许多包管理系统中包含的一个绝佳功能。

## 使用 apt 升级软件

虽然 apt 有助于保护你免受安装软件问题的困扰，但尝试协调包含依赖关系的多软件包更新可能会变得棘手。为了安全地升级系统中所有具有仓库中新版本的所有软件包，请使用 upgrade 命令：

```
apt upgrade
```

注意，此命令不接受任何软件包名称作为参数。这是因为 upgrade 选项将把所有已安装的软件包升级到仓库中可用的最新版本，这对系统稳定性而言更安全。

以下是运行 apt upgrade 命令时的示例输出：

```
$
$ sudo apt upgrade
正在读取软件包列表... 完成
正在构建依赖树
正在读取软件包状态信息... 完成
正在计算升级... 完成
将要安装以下新软件包：
binutils binutils-common binutils-x86-64-linux-gnu build-
essential dpkg-dev
fakeroot g++ g++-9 gcc gcc-9 libalgorithm-diff-perl
libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan5
libatomic1
libbinutils libc-dev-bin libc6-dev libcrypt-dev libcif-
nobfd0 libctf0
libfakeroot libgcc-9-dev libitm1 liblsan0 libquadmath0
libstdc++-9-dev
libtsan0 libubsan1 linux-libc-dev make manpages-dev
将升级以下软件包：
chromium-codecs-ffmpeg-extra eog file-roller fonts-
opensymbol gedit
gedit-common gir1.2-gnomedesktop-3.0 glib-networking glib-
networking-common
glib-networking-services gnome-control-center gnome-
control-center-data
gnome-control-center-faces gnome-desktop3-data gnome-
initial-setup
libgnome-desktop-3-19 libjuh-java libjurt-java libnautilus-
extension1a
libnetplan0 libreoffice-base-core libreoffice-calc
libreoffice-common
libreoffice-core libreoffice-draw libreoffice-gnome
libreoffice-gtk3
libreoffice-help-common libreoffice-help-en-us libreoffice-
impress
libreoffice-math libreoffice-ogltrans libreoffice-pdfimport
libreoffice-style-breeze libreoffice-style-colibre
libreoffice-style-elementary libreoffice-style-tango
libreoffice-writer
libridl-java libuno-cppu3 libuno-cppuhelpergcc3-3 libuno-
purpenvhelpergcc3-3
libuno-sal3 libuno-salhelpergcc3-3 libunoloader-java
nautilus nautilus-data
netplan.io python3-distupgrade python3-uno thermald ubuntu-
drivers-common
ubuntu-release-upgrader-core ubuntu-release-upgrader-gtk
ure
升级 56 个，新安装 32 个，移除 0 个，有 0 个未升级。
需要下载 133 MB 的归档文件。
此操作完成后，将额外使用 143 MB 磁盘空间。
你想要继续吗？ [Y/n]
```

在输出中，请注意 apt 列出了将要升级的软件包，但也列出了因升级而需要安装的新软件包。

upgrade 命令不会在升级过程中移除任何软件包。如果升级过程中需要移除某个软件包，请使用命令

```
apt full-upgrade
```

虽然这看起来可能有些奇怪，但有时为了在发行版升级之间保持同步，确实需要移除软件包。

> 注意

