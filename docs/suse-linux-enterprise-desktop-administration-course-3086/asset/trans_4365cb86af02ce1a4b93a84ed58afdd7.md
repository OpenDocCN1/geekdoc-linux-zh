
6. 通过输入验证目录是否已删除
```
ls
```
7. 通过输入删除 `~/my_dir/login` 文件
```
rm ~/my_dir/login
```
8. 你会看到一条警告消息，提示文件受写保护。通过输入 `y` 确认警告。
9. 通过输入验证文件是否已删除
```
ls ~/my_dir/login
```
10. 通过输入删除 `/home/geeko/my_dir/` 目录中以“a”开头的所有文件
```
rm -i ~/my_dir/a*
```
11. 通过输入 `y` 确认每个警告。
12. 通过输入删除包含其内容的 `/home/geeko/my_dir/` 目录
```
rm -r ~/my_dir
```
13. 通过输入 `y` 确认每个警告。
14. 通过输入验证目录是否已删除
```
ls ~/my_dir
```
15. 关闭终端窗口。

## 链接文件

Linux 中的文件系统格式将数据和 administration 信息分开。不同文件系统格式的数据组织方式不同。

每个文件都由一个 inode（index node 或 information node）描述。要查看 inode 编号，可以输入 `ls -i`。

每个 inode 为 128 字节，包含有关该文件除文件名外的所有信息。这包括所有者详细信息、访问权限、大小、各种时间详细信息（修改时间、访问时间、inode 修改时间）以及指向该文件数据块的链接等信息。

ln 命令创建链接。链接是对文件的引用。通过链接，你可以使用文件的不同名称从文件系统的任何位置访问文件。文件本身在系统上仅存在一次，但可以以不同的名称找到。

Linux 识别两种类型的链接：

- 硬链接
- 符号链接

你可以使用 `ln` 命令创建 *硬链接*，它指向已存在文件的 inode。此后，可以在两个名称下访问文件——即文件本身的名称和链接的名称，并且你无法再分辨哪个名称先存在或原始文件和链接有何不同。

以下是使用 ln 命令的示例：

```text
geeko@da10:~/sell > ls -li
total 4
88658 -rw-r--r-- 1 geeko users 82 2004-04-06 14:21 old
geeko@da10:~/sell > ln old new
geeko@da10:~/sell > ls -li
total 8
88658 -rw-r--r-- 2 geeko users 82 2004-04-06 14:21 old
88658 -rw-r--r-- 2 geeko users 82 2004-04-06 14:21 new
geeko@da10:~/sell >
```

硬链接只能在文件和链接位于同一文件系统（同一分区）时使用，因为 inode 编号仅在同一文件系统内唯一。

你可以使用 ln 命令和选项 -s 创建符号链接。符号链接分配有自己的 inode——链接引用一个文件，因此始终可以区分链接和实际文件。

以下是创建符号链接的示例：

```text
geeko@da10:~/sell > ls -li
total 4
88658 -rw-r--r-- 1 geeko users 82 2004-04-06 14:21 old
geeko@da10:~/sell > ln -s old new
geeko@da10:~/sell > ls -li
total 4
88658 -rw-r--r-- 1 geeko users 82 2004-04-06 14:21 old
88657 lrwxrwxrwx 1 geeko users 3 2004-04-06 14:27 new -> old
geeko@da10:~/sell >
```

使用符号链接，可以克服文件系统的限制，因为显示的是对象的名称，而不是对象本身。缺点是，如果对象及其对应名称不再存在，符号链接可能会指向一个不存在的对象。

如果你在上述示例中删除文件 old，new 将指向一个不存在的文件。在 ls 输出中你无法看到链接已损坏：

```text
geeko@da10:~/sell > rm old
geeko@da10:~/sell > ls -li
total 0
88657 lrwxrwxrwx 1 geeko users 3 2004-04-06 14:27 new -> old
geeko@da10:~/sell >
```

符号链接的一个优点是你可以创建指向目录的链接。

![](img/9129877170834ca9d5fdac5319bf5f12_235_0.png)

## 练习 7-5：链接文件

在本练习中，使用 ln 命令为 ~/my_file 文件创建一个符号链接，为 ~/my_file1 文件创建一个硬链接。

## 完成此练习的详细步骤

要链接文件，请执行以下操作：

1. 打开一个终端窗口。
2. 要在主目录中为 my_file 文件创建符号链接，输入
```bash
ln -s ~/my_file softlink
```
3. 要在主目录中为 my_file1 文件创建硬链接，输入
```bash
ln ~/my_file1 hardlink
```
4. 通过输入显示链接
```bash
ls -l
```
请注意，符号链接标识了它所链接到的文件，并且链接计数器（列在文件权限和所有者之间的数字）对于 my_file1 文件和硬链接为 2。
5. 关闭终端窗口。

## 目标 6—在 Linux 上查找文件

在本目标中，你将学习如何查找文件和程序。

如果文件名称不完全已知，可以使用两个通配符“?”（表示任意字符）和“*”（表示零个、一个或多个字符）。

假设存在以下文件：

- File
- file
- File1
- File1a
- File1b
- File2
- File2a
- MyFile

表 7-18 显示了三种不同搜索字符串的结果。

| 搜索字符串 | 找到的文件 |
|---|---|
| `File?` | File1<br>File2 |
| `File*` | File<br>File1<br>File1a<br>File1b<br>File2<br>File2a |
| `?ile*` | File<br>file<br>File1<br>File1a<br>File1b<br>File2<br>File2a |

表 7-18

下面介绍以下工具：

- 图形搜索工具
- find
- which
- type

## 图形搜索工具

有时你需要找到一个文件以便编辑它，但你不知道它在文件系统中确切的位置。你可能知道该文件的名称或仅知道其一部分名称。

另一次，你可能需要一份在过去两天内修改过或超过特定大小的所有文件列表。

如果你在“更多应用程序”搜索栏中输入 search，会找到两个应用程序——桌面搜索工具（Search）和 GNOME 搜索工具（Search for Files）。

![](img/9129877170834ca9d5fdac5319bf5f12_236_0.png)

- *Search (Search)*—当你在桌面搜索工具中输入搜索词时，一旦停止输入，就会显示包含该搜索词的文档列表。结果包括桌面上的各种类型文件，从 OpenOffice.org 文件到 PDF，再到访问过的网站。见图 7-3。

![](img/9129877170834ca9d5fdac5319bf5f12_237_0.png)

**图 7-3**

桌面搜索工具可以通过选择 Search > Preferences 配置。Search 选项卡允许你配置索引进行的时间。见图 7-4。

![](img/9129877170834ca9d5fdac5319bf5f12_238_0.png)

Indexing 选项卡允许你配置搜索索引中包含或排除的内容。见图 7-5。

![](img/9129877170834ca9d5fdac5319bf5f12_239_0.png)

**图 7-5**

- *Search for Files (GNOME Search Tool)—*此工具允许你搜索诸如文件大小、日期或文件所有者等信息。

当你从应用程序浏览器中选择 GNOME 搜索工具时，会出现图 7-6 所示的对话框。

在 Name Contains 字段中，输入要查找的文件名的部分。 从 Look in folder 下拉列表中选择要搜索的目录。 选择 Find 开始搜索过程。 所有匹配的文件和目录都将显示在下部窗口中，并附带其位置的详细信息。

当你打开 **Select more options** 下的菜单时可以进行进一步设置。 从 **Available options** 下拉列表中选择一个搜索规则。 见图 7-7。

当你选择 **Add** 时，会添加一个新文本字段，允许你输入该选项所需的信息。 要删除搜索规则，请选择规则旁边的 **Remove** 按钮。

![](img/9129877170834ca9d5fdac5319bf5f12_240_0.png)

图 7-6

![](img/9129877170834ca9d5fdac5319bf5f12_240_1.png)

图 7-7
