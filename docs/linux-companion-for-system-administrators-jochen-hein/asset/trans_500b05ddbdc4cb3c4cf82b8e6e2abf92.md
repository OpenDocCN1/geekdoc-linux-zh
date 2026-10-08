

```bash
(Linux):> updatedb --localpaths=/home/jochen \
  --output=update.db
(Linux):> locate -d update.db:/var/lib/locatedb passwd.tab
```

**列表 10.7** 创建用户的 locate 数据库。

应该输入 `updatedb` 命令（例如，参见列表 10.32），以便定期更新数据库。通常，数据库位于 `/var/lib` 目录。数据库的名称（locateddb）通常由 `updatedb` 创建，但可以通过设置变量 `LOCATION_DB` 来覆盖它。因此，可以为每个 CD-ROM 创建一个数据库。通过 `-d` 参数，你还可以指定用冒号分隔的数据库名称，供 `locate` 搜索。

在下面的示例（列表 10.8）中，在 `~/locate` 目录下创建了一个名为 `cd_linux2_1.codes` 的数据库，包含 CD 的内容。一旦创建完成，可以使用带有 `-d~/locate/cd_linux2_1.codes` 选项 `locate` 命令来搜索该数据库。

```bash
(Linux):# export LOCATE_DB="/locate/cd_linux2_1.codes
(Linux):# export SEARCHPATHS='CD'
(Linux):# export PRUNEREGEX=' '
(Linux):# updatedb
(Linux):# locate -d cd_linux2_1.codes ftape
```

**列表 10.8** 为 CD 创建搜索数据库。

该系统的缺点是 UNIX 数据库必须尽可能频繁地更新，否则将找不到最新的文件，或者已删除的文件仍会显示。搜索本身也不像 `find` 命令那样灵活。你不能搜索数据、所有者或等内容，只能搜索文件名。此外，运行 `updatedb` 的成本相对较高，因为它会在整个硬盘上执行一次 `find` 操作。

总而言之，如果你的系统上有许多用户，并且计算机有足够的“空闲”时期来更新数据库，那么使用 `locate` 总是值得的。如果你发现自己在系统上经常按名称搜索文件，那么在私有系统上使用 `locate` 是明智的；在我自己的系统上，`updatedb` 每四小时就会被调用一次。

## 10.1.3 程序 xyz 在哪里？

如果你正在查找包含在搜索路径（!）中的可执行文件的完整名称，可以跳过 `find` 冗长的搜索。你不应该使用 `find` 程序，而应该使用 `which` 命令。在 `tsh` 中，它是 shell 的内部命令。bash 用户使用别名 `-path`。在某些 UNIX 系统中，该命令也称为 `ewhat` 或 `whence`。

`which` 命令在 `PATH` 变量指定的完整路径中搜索所需文件名。处理路径的顺序与 shell 遵循的顺序完全相同。

```bash
(Linux):$ which awk
/usr/bin/awk
```

### 10.9 使用 which

通过 `whereis` 命令，你不仅可以找到程序，还能找到相应的帮助页（man pages）。`-b` 选项仅搜索程序，`-m` 仅搜索帮助页。附加选项和搜索路径可以在 `whereis` 的帮助页中找到。

可以使用 bash 命令类型 `-all -path` 来判断路径中是否存在两个版本的程序（例如在 `/usr/bin` 和 `/usr/local/bin` 中），以及其中哪一个会被启动。这在安装了新程序版本但旧版本仍在使用的情况下非常有用。

当需要指向程序的路径时，像 `which` 这样的程序总是明智的。这适用于 shell 脚本的安装和适配，以及错误检测。像 `strings` 和 `ldd` 等程序作用于文件而非搜索路径中的程序。

## 10.1.4 这是什么种类型的文件？

UNIX 系统由海量文件组成。文件数量数量没有那么多，但已经足够多：文本文件、二进制程序、shell 脚本、图像、图画等。通常，可以使用文件名或更准确地说，使用扩展名来确定文件类型，但这种窍门并不总是有效。`file` 程序打开文件并尝试在 `/etc/magic` 文件中寻找匹配条目。这些“魔术 ID”（magic IDs）和类似内容被用于确定文件类型。有时，`file` 的输出惊奇地准确，而另一些程序会偏离目标。列表 10.10 显示了 `file` 的示例输出。

```bash
(Linux):> file /vminux /bin/ls announce
/vminux: Linux/x86 kernel image, version 2.0.30
/bin/ls: ELF 32-bit LSB executable, Intel 80386,
version 1, dynamically linked, stripped
announcement: International language text
```

列表 10.10 file 程序。

`file` 的输出质量取决于 `/etc/magic` 中底层数据库的质量。大多数商业系统的版本较小且过旧，而 LINUX 的实现包含了该文件的非常好的版本。通常还能在新程序中发现定义了单个文件类型，这样该文件就可以被轻松更新。

| 附加信息和来源 |
| :--- | :--- |
| ftp 服务器 | ftp.deshaw.com |
| ftp 路径 | /pub/file |
| 文件名 | file-X.YY.tar.gz |
| 大小: | 约 80 KB |

## 10.1.5 其他辅助工具

还有几个主要用于 shell 的辅助工具。编写 shell 脚本时，你至少应该熟悉这些命令。`basename` 命令将文件名与路径分离。如果名称不包含目录，它提供不带路径的文件名。`dirname` 命令的工作方式与 `basename` 类似。然而，它的输出只有目录路径。

## 10.1.6 参数长度过长

经常有一系列文件被重命名。不幸的是，该命令一次只能重命名一个文件（`mv *.c *.bak` 不起，因为 shell 对通配符进行了展开）。相反，你可以使用小型 `for` 循环、`mv` 命令，或者带有 `-n -i` 选项的 `xargs` 命令。列表 10.15 中的示例将当前目录下所有以 *.c` 结尾的文件复制到 `backups` 目录，并为每个文件名添加 `.bak` 扩展名。

