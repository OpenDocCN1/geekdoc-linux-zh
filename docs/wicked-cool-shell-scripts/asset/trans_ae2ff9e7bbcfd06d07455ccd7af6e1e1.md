

## 运行脚本

要更改 Terminal 窗口的标题，只需将你想要的新标题作为参数输入给 titleterm 即可。

## 结果

该命令没有明显的输出，正如清单 11-4 所示。

```
$ titleterm $(pwd)
$
```

> 清单 11-4：运行 titleterm 脚本将终端标题设置为当前目录

然而，它会立即将 Terminal 窗口的标题更改为当前工作目录。

## 修改脚本

只需在你的登录脚本中添加一个小的修改（.bash_profile 或其他，取决于你使用的登录 shell），你就可以让 Terminal 窗口标题始终显示当前工作目录。要使此代码显示你的当前工作目录，例如，你可以在 tcsh 中使用：

```
alias precmd 'titleterm "$PWD"' [tcsh]
```

或在 bash 中使用：

```
export PROMPT_COMMAND="titleterm \"\$PWD\"" [bash]
```

只需将上述命令之一放入你的登录脚本中，从下次打开 Terminal 窗口开始，你会发现每次进入新目录时窗口标题都会改变。非常实用。

## #81 生成 iTunes 库的摘要列表

如果你使用 iTunes 一段时间，你肯定会拥有庞大的音乐、有声读物、电影和电视节目列表。不幸的是，尽管 iTunes 功能强大，但它没有简单的方法以简洁易读的格式导出你的音乐列表。幸运的是，编写一个提供此功能的脚本并不难，正如清单 11-5 所示。此脚本依赖于 iTunes 的“与其它应用程序共享 iTunes XML”功能已启用，因此在运行此脚本之前，请确保在 iTunes 首选项中已启用它。

## 代码

```
#!/bin/bash
# ituneslist--Lists your iTunes library in a succinct and attractive
# manner, suitable for sharing with others, or for synchronizing
# (with diff) iTunes libraries on different computers and laptops

itunehome="$HOME/Music/iTunes"
ituneconfig="$itunehome/iTunes Music Library.xml"

musiclib="$(grep '>Music Folder<' "$ituneconfig" | cut -d/ -f5- | \
cut -d< -f1 | sed 's/%20/ /g')"

echo "Your library is at $musiclib"

if [ ! -d "$musiclib" ] ; then
echo "So: Confused: Music library $musiclib isn't a directory?" >&2
exit 1
fi

exec find "$musiclib" -type d -mindepth 2 -maxdepth 2 \! -name '.*' -print \
| sed 's|$musiclib||'
```

清单 11-5：ituneslist 脚本

## 工作原理

像许多现代计算机应用程序一样，iTunes 希望其音乐库位于标准位置——在本例中为 ~/Music/iTunes/iTunes Media——但如果你愿意，也可以将其移至其他位置。脚本需要能够确定不同的位置，这通过从 iTunes 首选项文件中提取 Music Folder 字段值来完成。这就是管道在 1 处完成的工作。

首选项文件（$ituneconfig）是一个 XML 数据文件，因此需要进行一些裁剪才能识别确切的 Music Folder 字段值。以下是 Dave 的 iTunes 配置文件中 iTunes Media 值的样子：

```
file://localhost/Users/taylor/Music/iTunes/iTunes %20Media/
```

有趣的是，iTunes Media 值实际上存储为完全限定的 URL，因此我们需要去掉 file://localhost/ 前缀。这就是第一个 cut 命令的工作。最后，由于 OS X 中的许多目录包含空格，并且 Music Folder 字段以 URL 的形式保存，该字段中的所有空格都映射为 %20 序列，需要在继续之前通过 sed 调用将其恢复为空格。

确定 Music Folder 名称后，现在可以轻松地在两台 Mac 系统上生成音乐列表，然后使用 diff 命令比较它们，从而轻松查看哪些专辑是某一系统独有的，也许可以同步它们。

## 运行脚本

此脚本没有命令行参数或标志。

## 结果

如果你拥有庞大的音乐收藏，脚本的输出可能会很大。清单 11-6 显示了 Dave 音乐收藏输出的前 15 行。

```
$ ituneslist | head -15
Your library is at /Users/taylor/Music/iTunes/iTunes Media/
Audiobooks/Andy Weir
Audiobooks/Barbara W. Tuchman
Audiobooks/Bill Bryson
Audiobooks/Douglas Preston
Audiobooks/Marc Seifer
Audiobooks/Paul McGann
Audiobooks/Robert Louis Stevenson
iPod Games/Klondike
Movies/47 Ronin (2013)
Movies/Mad Max (1979)
Movies/Star Trek Into Darkness (2013)
Movies/The Avengers (2012)
Movies/The Expendables 2 (2012)
Movies/The Hobbit The Desolation of Smaug (2013)
```

清单 11-6：运行 ituneslist 脚本打印 iTunes 收藏中的前几项

## 修改脚本

好吧，这并不是严格意义上对脚本的修改，但由于 iTunes 库目录以完全限定的 URL 保存，尝试使用可通过网络访问的 iTunes 目录，然后将该目录的 URL 用作 XML 文件中的 Music Folder 值会很有趣。 。 。

## #82 修复 open 命令

OS X 的一个不错的创新是添加了 open 命令，它允许你轻松启动几乎任何类型文件的适当应用程序，无论是图形图像、PDF 文档还是 Excel 电子表格。open 的问题在于它有点古怪。如果你想让它启动指定的应用程序，你必须包含 -a 标志。而且如果你没有指定确切的应用程序名称，它会抱怨并失败。这正是像清单 11-7 中这样的包装脚本的完美工作。
