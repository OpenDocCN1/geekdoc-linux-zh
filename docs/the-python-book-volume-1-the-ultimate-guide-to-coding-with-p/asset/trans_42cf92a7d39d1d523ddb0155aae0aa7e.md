

# 使用 Python 工作

listdir(path) : 类似于 `ls`，返回一个列表，其中包含给定路径下的目录和文件内容。

## 示例：

```
>>> os.listdir("/home/homer")
['.gnome2', 'pulse', '.gconf', '.gconf.d', 'beagle', '.gnome2', 'private', '.gksu_lock', 'Public', '.ICEauthority', 'bash_history', 'compiz', 'gvfs', 'update-notifier', 'cache', 'Desktop', 'Videos', 'profile', 'config', '.esd_auth', '.viminfo', '.sudo_as_admin_successful', 'mbox', 'xsession-errors', 'bashrc', 'Music', 'dbus', '.local', 'gstreamer-0.10', 'Documents', '.gtk-bookmarks', 'Downloads', 'Pictures', 'pulse-cookie', '.nautilus', 'examples', 'desktop', 'Templates', '.bash_logout']
```

mkdir(path[, mode]) : 使用给定的数字权限代码创建目录。默认权限为 0777。

makedirs(path[, mode]) : 递归创建给定路径（包括其所有目录）。默认权限为 0777。

## 示例：

```
>>> import os
>>> path = "/home/kunal/greatdir"
>>> os.makedirs( path, 0755 );
```

rename (old,new) : 将文件或目录 "old" 重命名为 "new"。如果 "new" 是一个目录，则会引发错误。在 Unix 和 Linux 上，如果 "new" 已存在且是一个文件，只要用户有相应权限，它就会被静默替换。

renames (old,new) : 类似于 `rename`，但如有必要还会递归创建任何缺失的目录。

rmdir(path) : 从指定路径移除目录。如果该路径下已有文件，你需要使用 `shutil.rmtree()`。

# subprocess:

call(*popenargs, **kwargs) : 使用参数运行命令。进程完成后，它返回 `returncode` 属性。

## 示例：

```
>>> import subprocess
>>> print subprocess.call(["ls","-l"])
total 3684688
drwx------ 5 kunaldo staff
170 Aug 19 01:37 Desktop
drwx------ 10 kunaldo staff
340 Jul 26 08:30 Documents
drwx------ 50 kunaldo staff
1700 Aug 19 12:59 Downloads
drwx------ 9 127 kunaldo staff
4318 Aug 19 01:43 Dropbox
drwx------ 42 kunaldo staff
1428 Aug 12 15:17 library
drwx------ 3 kunaldo staff
102 Jul 3 23:23 Movies
drwx------ 4 kunaldo staff
136 Jul 6 08:32 Music
drwx------ 5 kunaldo staff
170 Aug 12 11:26 Pictures
drwx--xr-x 5 kunaldo staff
170 Jul 3 23:23 Public
--rw--r--r-- 1 kunaldo staff
18865556848 Aug 16 21:02 androidsk.tar
drwx--xr-x 5 kunaldo staff
170 Aug 16 21:05 sdk
drwx--xr-x 19 kunaldo staff
646 Aug 19 01:47 src
--rw--r--r-- 1 root staff
367 Aug 16 20:36 umbrella0.log
```

STD_INPUT_HANDLE: 标准输入设备。最初，这是控制台输入缓冲区。

STD_OUTPUT_HANDLE: 标准输出设备。最初，这是活动控制台屏幕缓冲区。

STD_ERROR_HANDLE: 标准错误设备。最初，这是活动控制台屏幕缓冲区。

## 第 2 节：IPython：一个现成的 Python 系统 shell 替代品

在第 1 节中，我们向你介绍了 Python 模块，这些模块让你能够使用纯 Python 非常轻松地执行系统 shell 相关任务。利用这些特性，你可以构建一个功能完备的 shell，并在此过程中省去大量 Python 样板代码。然而，如果你是一个喜欢一切现成的人，那么你很幸运。IPython 提供了一个强大且交互式的 Python shell，你可以将其作为你的主要 shell 使用。IPython 支持 Python 2.6 到 2.7 以及 3.1 到 3.2。它支持两种类型的 Python shell：基于终端的和基于 Qt 的。

需要重申的是，IPython 完全由 Python 实现，并提供了 100% 符合 Python 规范的 shell 接口，因此你在第 1 节中学到的一切都可以在 IPython 中毫无问题地运行。

IPython 在大多数 Linux 发行版中已经可用。请搜索你的发行版软件仓库来查找它。如果你找不到，你也可以使用 `easy_install` 或 PyPI 来安装它。

IPython 提供了许多有趣的功能，使其成为一个出色的 shell 替代品……

## Tab 补全：

Tab 补全提供了一种极好的方式来探索你正在使用的任何 Python 对象。它还能帮助你避免拼写错误。

## 示例：

```
In [3]: import o  (hit tab)
objc    opcode    operator
optparse os       os2emxpath
```

```
In [3]: import os
```

```
In [4]: os.p  (hit tab)
os.pardir      os.pathconf_names
os.popen       os.popen4
os.path        os.pathsep
os.popen2      os.putenv
os.pathconf    os.pipe
os.popen3
```

内置对象浏览器：你可以在任何 Python 对象后面添加 `?` 来查看其详细信息，例如类型、基类、字符串形式、命名空间、文件和文档字符串。

## 示例：

```
In [28]: os.path?
Type: module
Base Class: <type 'module'>
String Form: <module 'posixpath' from '/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/posixpath.py'>
Namespace: Interactive
File: /System/Library/Frameworks/
```

