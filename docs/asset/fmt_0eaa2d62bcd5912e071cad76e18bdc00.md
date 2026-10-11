
这将移除所有缓存软件包和元数据，释放磁盘空间。

## 从仓库下载 RPM

如果你只是想检查软件包而不实际安装它，可以使用 `yumdownloader` 命令。运行该命令会将软件包名称从仓库下载并复制到当前目录。

例如，要从 YUM 仓库将最新版本的 Firefox 软件包下载到当前目录，请输入：

```bash
# yumdownloader firefox
firefox-10.0.5.1.el6.2.x86_64.rpm
```

现在 RPM 软件包位于你的当前目录中，你可以使用各种 `rpm` 命令查询或以不同的方式使用该软件包（如下一节所述）。

## 第10 章：获取与管理软件

### 使用 rpm 安装和删除包

使用 `rpm` 命令安装包，请输入：

```bash
# rpm -i zsh-4.3.17-1.1.31-2.fc16.noarch
```

请注意，使用 `rpm` 安装时提供的是包名，而不仅仅是包的基础名称。如果安装了旧版本的 `zsh`，你可以使用 `-U` 升级包。通常，人们会使用 `-h` 和 `-v` 选项在升级期间打印哈希符号并显示详细输出：

```bash
# rpm -Uvh zsh-4.3.17-1.1.31-2.fc16.noarch
########################### [100%]
Preparing...
zsh ################# [100%]
```

安装 `(-i)` 只有在包尚未安装时才会安装，而升级 `(-U)` 无论包是否已安装都会进行安装。第三种类型名为 freshen `(-F)` 的安装是：如果计算机上已经安装了该包的现有早期版本，则进行安装。例如：

```bash
# rpm -Fvh *.rpm
```

如果你处于一个包含数千个 RPM 的目录中，但只想更新那些已经在系统中安装（早期版本）的包，并跳过那些尚未安装的包，就可以使用 freshen 命令。

你可以在任何安装选项中添加一些有趣的选项。`--replacepkgs` 允许你重新安装已版本的包（如果你不小心删除了某些组件），而 `--oldpackage` 允许你安装某个包的更早版本。

```bash
# rpm -Uvh --replace-pkgs emacs-common-23.3-9.fc16i86
# rpm -Uvh --oldpackage zsh-4.1.0-2-fc16.noarch
```

你可以使用 `-e` 选项删除包。删除包时只需要包的基础名称。例如：

```bash
# rpm -e emacs
```

`rpm -e emacs` 命令将执行成功，因为没有其他包依赖于 `emacs`。然而，它会遗留 `emacs-common`，它是作为 `emacs` 的依赖项安装的。如果你尝试先删除 `emacs-common`，命令将失败并显示“Failed dependencies”（依赖项失败）消息。

### 查询 rpm 信息

一旦安装了包，就可以查询有关该包的信息。使用 `-q` 选项，你可以查看包的信息，包括描述 `(-qi)`、`文件列表 (-ql)`、`文档 (-qd)` 和配置文件 `(-qc)`。

![](img/47358dd1a47f0ba12c47c96b4fe178b7_288_0.png)

## 第三部分：成为 Linux 系统管理员

```bash
# rpm -qi zsh
Name      : zsh
Version   : 4.3.17
Release   : 1.fc16
```

```bash
# rpm -ql zsh
/bin/zsh
/etc/skel/.zshrc
/etc/zlogin
/etc/zlogout
```

```bash
# rpm -qd zsh
usr/share/doc/zsh-4.3.17/FAQ
usr/share/doc/zsh-4.3.17/FEATURES
usr/share/doc/zsh-4.3.17/README
```

```bash
# rpm -qc zsh
/etc/skel/.zshrc
/etc/zlogin
/etc/zlogout
```

有许多选项可以查询 RPM 中包含的任何信息。你可以找到 RPM 安装所需的条件 (`--requires`)、哪个版本的软件包提供了该包 (`--provides`)、在 RPM 安装或删除之前后运行了哪些脚本 (`--scripts`) 以及对 RPM 做了哪些更改 (`--changelog`)

```bash
# rpm -q --requires emacs-common
/bin/sh
/sbin/install-info
/usr/bin/perl
```

```bash
# rpm -q --provides emacs-common
config(emacs-common) = 1:23.3-9-fc16
emacs-common = 1:23.3-9-fc16
```

```bash
# rpm -q --scripts httpd
# Add the "apache" user
-/usr/sbin/useradd -r -d /var/www apache 2>/dev/null ||
postinstall scriptlet (using /bin/sh);
```

```bash
# Register the httpd service
/sbin/chkconfig --add httpd
```

```bash
# rpm -q --changelog httpd
* Mar 05 2012 Jan Kaluza <jkaluza@redhat.com> - 2.2.2-2
 fix #751591 - start httpd after network filesystems
```

在前面的两个示例中，你可以看到 `httpd` 包的脚本在安装时添加了一个 `apache` 用户，并通过 `chkconfig` 配置了 `httpd` 服务。`--changelog` 选项允许你查看为什么对包的每个版本进行了更改。`fix #` 代表已修复的错误，你可以在 http://bugzilla.redhat.com 查找。

使用功能 `--queryformat`，你可以查询不同的信息标签并以你喜欢的任何形式输出它们。运行 `--querytags` 选项可以查看所有的标签：

```bash
# rpm --querytags | less
ARCH
ARCHIVESIZE
BASENAMES
BUGURL
```

```bash
# rpm -q binutils --queryformat "The package is %{NAME} \
and the release is %{RELEASE}"
The package is binutils and the release is 6.fc16
```

你到为止为止的所有查询都是针对本地 RPM 数据库的。通过在这些查询选项中添加 `-p`，你可以查询位于本地目录中的 RPM。`-p` 选项是查看包内部内容的极佳方法，让你在将其安装到系统之前调查它是什么。

如果你还没有获取 `zsh` 包，请获取它并将其放在本地目录中（下载 `zsh`）。然后对它运行查询命令。

```bash
# rpm -qlip zsh-4.3.17-1.fc16.i686.rpm
# rpm -qlp zsh-4.3.17-1.fc16.i686.rpm
# rpm -qdp zsh-4.3.17-1.fc16.i686.rpm
# rpm -Uvh --replacepkgs emacs-common-23.3-9-fc16i86
# rpm -Uvh --oldpackage zsh-4.1.0-2-fc16.noarch
```

### 验证 RPM 包

虽然安装 `(-i)` 只有在包尚未安装时才会安装，而升级 `(-U)` 无论包是否已安装都会进行安装。第三种类型名为 freshen `(-F)` 的安装是：如果计算机上已经安装了该包的现有早期版本，则进行安装。例如：

```bash
# rpm -Fvh *.rpm
```
