
如你所示，在搜索软件包时，`apt-cache` 和 `aptitude` 工具是最容易使用的，并且返回的结果最详尽。

## 第 19 章：添加、删除和更新软件

### 列出软件包信息

一旦你找到了感兴趣的软件包，就有许多等的方法可以获取有关该软件包及其内容的更详细信息。然而，由于 `apt-cache` 和 `aptitude` 工具返回最好的搜索结果，因此使用它们来显示你已识别的任何软件包是有意义的。例如，要查找上一节列出的 `xacs21` 软件包的信息，你可以使用 `apt-cache show xemacs21` 或 `aptitude show xemacs21` 命令，两者返回的信息几乎相同。以下示例显示了 `aptitude show xemacs21` 命令的输出，它稍微详细一些：

```
$ aptitude xemacs21
Package: xemacs21
New: yes
State: installed
Automatically installed: no
Version: 21.4.18-ubuntu
Priority: optional
Section: universe/editors
Maintainer: OHURA <ohura@debian.org>
Uncompressed Size: 49.2k
Depends: xemacs21-mule (21.4.18-ubuntu) | xemacs21-nomule (21.4.18-ubuntu) | xemacs21-gnome-mule (21.4.18-ubuntu) | xemacs21-gnome-wann (21.4.18-ubuntu) | xemacs21-gnome-nomule (21.4.18-ubuntu)
Conflicts: xemacs, emacs-widget
Replaces: xemacs, emacs-widget
Provided by: xemacs21-nomule, xemacs21-gnome-mule, xemacs21-gnome-wann, xemacs21-gnome-mule
Description: 高可定制文本编辑器
Emacs 是一个功能完备的语言，带有邮件阅读器、新闻阅读器、网络浏览器、针对更多编程语言以及大多数人在一生中遇到的其他格式的专用编辑器等。此软件包的存在是为了安装真正的 Emacs 软件包。此输出提供的关于指定软件包的信息可能比你想要知道的还要多，但谨慎谨慎总是比较好的。
```

### 列出软件包的内容

在某些情况下，你可能想要列出系统中已安装软件包相关的所有文件。要做到这一点，你可以使用 `dpkg` 命令的 `-L` 选项，后跟想要列出内容的软件包名称。以下是列出我系统中 `emacs21` 软件包内容的示例输出：

```
$ dpkg -L emacs21

/

/usr/bin

/usr/bin/emacs21-x

/usr/share

/usr/share/emacs

/usr/share/emacs/21.4

/usr/share/emacs/21.4/etc

/usr/share/emacs/21.4/etc/21.4.1

/usr/share/applications

/usr/share/applications/emacs21-desktop

/usr/share/doc

/usr/share/doc/emacs21

/usr/share/doc/emacs21/README.Debian

/usr/share/doc/emacs21/copyright

/usr/share/doc/emacs21/changelog.Debian

/usr/lib

/usr/lib/emacs

/usr/lib/emacs/21.4

/usr/lib/emacs/21.4/i486-linux-gnu

/usr/lib/menu
```

能够识别系统中已安装软件包所提供的文件，在你考虑删除某个软件包时这会非常有帮助，可以确保这样做不会删除你想要保留的文件。下一节将描述如何查找哪个软件包提供了特定文件。

## 提示

你可以使用 `apt-file` 工具来列出尚未安装的软件包所提供的文件，命令为 `apt-file list package`，其中 `package` 是你感兴趣的软件包名称。`apt-file` 工具将在本章稍后的“确定哪个软件包提供了缺失的文件”部分进行更详细的描述。

### 确定现有文件提供的软件包

在运行 Ubuntu 了一段时间并安装、更新和删除了一些软件包后，你可能好奇系统中的某个文件是由哪个软件包提供的。使用 `dpkg` 命令的 `--search` 选项可以很容易确定，如下例所示，我好奇哪个软件包提供了 `/usr/bin/ar` 归档工具：

```
$ dpkg --search /usr/bin/ar

binutils:/usr/bin/ar
```

如果你知道要查找的工具在你的路径中，但你不想确定它物理所在的目录，你可以使用 Shell 技巧，将一个现有命令的输出作为另一个命令的输入。在这种情况下，结合 `which` 命令（用于确定应用程序的完整路径）和 `dpkg --search` 命令，可以产生完全相同的输出：

```
$ dpkg --search (which ar)

binutils:/usr/bin/ar
```

在搜索文件时，`dpkg --search` 命令找不到由安装后创建的符号链接。如果你试图查找一个存在的文件但无法找到，请确保该文件不是符号链接；如果是，请搜索它实际指向的文件。这有时需要尝试几次，如下例所示：

```
$ dpkg --search /usr/bin/emacs

dpkg: /usr/bin/emacs not found.
```

```
$ ls -l /usr/bin/emacs

/usr/bin/emacs -> /etc/alternatives/emacs
```

```
$ dpkg --search /etc/alternatives/emacs

dpkg: /etc/alternatives/emacs not found.
```

```
$ ls -l /etc/alternatives/emacs

/etc/alternatives/emacs -> /usr/bin/emacs21-x
```

```
$ dpkg --search /usr/bin/emacs21-x

emacs21: /usr/bin/emacs21-x
```

虽然有时很麻烦，但符号链接通常不是软件包的一部分，你必须找出属于软件包的文件。

## 提示

在确定特定文件提供的软件包时，你可能想使用的另一个软件包管理工具是 `locate`。该工具在 Ubuntu 系统上默认安装，但可以通过 `apt-get`、`aptitude` 或 Synaptic 软件包管理器轻松安装。安装后，你可以使用 `locate -S` 命令搜索提供该文件的软件包，如下例：

```
$ locate -S /usr/bin/emacs

emacs21-bin-common: /usr/bin/emacsclient.emacs21

emacs21: /usr/bin/emacs21-x

emacs21: /usr/bin/emacs21
```

## 确定哪个包提供了缺失的文件

识别提供系统中未安装文件的软件包有些棘手，当你尝试构建一个源码需要系统中不存在的某个文件的软件时，或者当你尝试链接一个需要缺失库的软件时，这是一个常见的问题。遗憾的是，执行此类搜索的工具 `apt-file` 实用程序在 Ubuntu 系统上默认没有安装，但你可以轻松地使用 `apt-file`、`aptitude` 或 Synaptic 包管理器（Synaptic Package Manager）进行安装。安装完成后，你必须首先运行 `sudo apt-file update` 命令更新你正在使用的存储库中可用的用户级软件包。

一旦该命令完成，你就可以使用 `apt-file search` 命令搜索提供文件的包（即使该包尚未安装在你的系统中），例如所示，它查找与 `libpowersave` 库相关的包：

```
$ ls -l /usr/lib/power*

ls: /usr/lib/power*: No file or directory
$ apt-file search libpowersave.so

libpowersave-dev: /usr/lib/libpowersave.so

libpowersave-10: /usr/lib/libpowersave.so.10

libpowersave-10: /usr/lib/libpowersave.so.10.3
```
