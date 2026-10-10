
具有上述描述的相同语法和 `.list` 文件扩展名的简单文本文件。

以下是名为 `/etc/apt/sources.list.d/buster-backports.list` 的文件内容：

```
deb http://deb.debian.org/debian buster-backports main contrib non-free
deb-src http://deb.debian.org/debian buster-backports main contrib non-free
```

### 列出软件包内容和查找文件

可以使用名为 `apt-file` 的工具在软件包索引中执行更多操作，例如列出软件包的内容或查找包含特定文件的软件包。此工具可能未默认安装在您的系统中。在这种情况下，通常可以使用 `apt-get` 来安装它：

```
# apt-get install apt-file
```

安装后，您需要更新用于 `apt-file` 的软件包缓存：

```
# apt-file update
```

这通常只需几秒钟。之后，您就可以使用 `apt-file` 了。

要列出软件包的内容，请使用 `list` 参数，后跟软件包名称：

```
# apt-file list unrar
unrar: /usr/bin/unrar-nonfree
unrar: /usr/share/doc/unrar/changelog.Debian.gz
unrar: /usr/share/doc/unrar/copyright
unrar: /usr/man/man1/unrar-nonfree.1.gz
```

> **提示** 您也可以使用 `apt list` 代替 `apt-file list`。

您可以使用 `search` 参数在所有软件包中搜索文件，后跟文件名。例如，如果您想知道哪个软件包提供了名为 `libSDL2.so` 的文件，可以使用：

```
# apt-file search libSDL2.so
libSDL2-dev: /usr/lib/x86_64-linux-gnu/libSDL2.so
```

答案是软件包 `libSDL2-dev`，它提供了文件 `/usr/lib/x86_64-linux-gnu/libSDL2.so`。

`apt-file search` 和 `dpkg-query` 的区别在于，`apt-file search` 也会搜索未安装的软件包，而 `dpkg-query` 只能显示属于已安装软件包的文件。

## 指导性练习

- 1. 使用 `dpkg` 安装名为 `package.deb` 的软件包的命令是什么？
- 2. 使用 `dpkg-query`，查找包含名为 `7zr.1.gz` 文件的软件包。
- 3. 如果软件包 `file-roller` 依赖于 `unzip`，您能否使用 `dpkg -r unzip` 从系统中移除名为 `unzip` 的软件包？如果不能，正确的方法是什么？
- 4. 使用 `apt-file`，如何查找包含文件 `unrar` 的软件包？
- 5. 使用 `apt-cache`，显示软件包 `gimp` 信息的命令是什么？

## 探索性练习

- 1. 假设有一个存储库，包含 `xenial` 发行版的 Debian 源软件包，托管在 `http://us.archive.ubuntu.com/ubuntu/`，并且包含 `universe` 组件的软件包。应该添加到 `/etc/apt/sources.list` 中的相应行是什么？
- 2. 在编译程序时，您遇到了一个错误消息，抱怨系统上没有头文件 `zzip-io.h`。如何找出哪个软件包提供了该文件？
- 3. 即使系统中有依赖于该软件的包，如何使用 `dpkg` 忽略依赖警告并移除软件包？
- 4. 如何使用 `apt` 获取更多关于名为 `midori` 的软件包的信息？
- 5. 在使用 `apt` 安装或更新软件包之前，应该使用哪个命令来确保软件包索引是最新的？

## 总结

在本课中，您学习了：

- 如何使用 **dpkg** 安装和移除软件包。
- 如何列出已安装的软件包和软件包内容。
- 如何重新配置已安装的软件包。
- 什么是 **apt**，以及如何使用它安装、升级和移除软件包。
- 如何使用 **apt-cache** 搜索软件包。
- `/etc/apt/sources.list` 文件是如何工作的。
- 如何使用 **apt-file** 显示软件包的内容，或查找包含特定文件的软件包。

讨论了以下命令：

**dpkg -i**

安装单个软件包，或安装以空格分隔的软件包列表。

**dpkg -r**

移除一个软件包，或移除以空格分隔的软件包列表。

**dpkg -I**

检查软件包，提供有关所安装软件及其所需依赖项的详细信息。

**dpkg --get-selections**

列出 dpkg 在系统中安装的每个软件包。

**dpkg -L**

打印出特定软件包安装的所有文件列表。

**dpkg-query**

指定文件名后，此命令将打印出安装了该文件的软件包。

**dpkg-reconfigure**

此命令将重新运行软件包的 _post-install_（安装后）脚本，以便管理员可以对软件包的安装进行配置调整。

**apt-get update**

此命令将更新本地软件包索引，以匹配 `/etc/apt/` 目录下配置的存储库中可用的内容。

**apt-get install**

此命令将从远程存储库下载软件包并连同其依赖项一起安装，也可用于安装已下载的 Debian 软件包。

**apt-get remove**

此命令将从系统中卸载指定的软件包。

**apt-cache show**

与 `dpkg -I` 命令一样，此命令可用于显示特定软件包的详细信息。

**apt-cache search**

此命令将在本地 APT 缓存数据库中搜索特定软件包。

**apt-file update**

此命令将更新软件包缓存，以便 `apt-file` 命令可以查询其内容。

**apt-file search**

此命令将搜索文件包含在哪个软件包中。将返回包含该模式的所有软件包列表。

**apt-file list**

此命令用于列出软件包的内容，就像 `dpkg -L` 命令一样。

## 指导性练习答案

1. 使用 dpkg 安装名为 `package.deb` 的软件包的命令是什么？

将 `-i` 参数传递给 dpkg：

```
# dpkg -i package.deb
```

2. 使用 `dpkg-query`，查找包含名为 `7zr.1.gz` 文件的软件包。

将 `-S` 参数添加到 `dpkg-query`：

```
# dpkg-query -S 7zr.1.gz
```

3. 如果软件包 `file-roller` 依赖于 `unzip`，您能否使用 `dpkg -r unzip` 从系统中移除名为 `unzip` 的软件包？如果不能，正确的方法是什么？

不能。`dpkg` 不会解决依赖关系，如果另一个已安装的软件包依赖于它，它将不允许您移除该软件包。在此示例中，您可以先移除 `file-roller`（假设没有软件包依赖于它），然后移除 `unzip`，或者同时使用以下命令移除两者：

```
# dpkg -r unzip file-roller
```

4. 如何使用 `apt-file` 工具找出包含文件 `/usr/bin/unrar` 的软件包？

使用 `search` 参数，后跟路径（或文件名）：

```
# apt-file search /usr/bin/unrar
```

5. 使用 `apt-cache`，显示软件包 `gimp` 信息的命令是什么？

使用 `show` 参数，后跟软件包名称：

```
# apt-cache show gimp
```

## 探索性练习答案

1. 假设有一个存储库，包含 `xenial` 发行版的 Debian 源软件包，托管在 `http://us.archive.ubuntu.com/ubuntu/`，并且包含 `universe` 组件的软件包。应该添加到 `/etc/apt/sources.list` 中的相应行是什么？

源软件包的类型是 `deb-src`，因此该行应为：

```
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial universe
```

该行也可以添加在 `/etc/apt/sources.list.d/` 中的 `.list` 文件内。名称由您决定，但应具有描述性，例如 `xenial_sources.list`。

2. 在编译程序时，您遇到了一个错误消息，抱怨系统上没有头文件 `zzip-io.h`。如何找出哪个软件包提供了该文件？

使用 `apt-file search` 查找包含系统中不存在的文件的软件包：

```
# apt-file search zzip-io.h
```

3. 即使系统中有依赖于该软件的包，如何使用 `dpkg` 忽略依赖警告并移除软件包？

可以使用 `--force` 参数，但除非您确切知道自己在做什么，否则*永远不要*这样做，因为系统存在很大的风险会被置于不一致或“损坏”的状态。

4. 如何使用 `apt-cache` 获取更多关于名为 `midori` 的软件包的信息？

使用 `apt-cache show`，后跟软件包名称：

```
# apt-cache show midori
```

5. 在使用 `apt-get` 安装或更新软件包之前，应该使用哪个命令来确保软件包索引是最新的？

应使用 `apt-get update`。这将下载 `/etc/apt/sources.list` 文件或 `/etc/apt/sources.list.d/` 目录中描述的存储库中的最新软件包索引。

