
| 2. 至少学习到第四课。 |

下一页有一张 VIM 快速查表。你可以随时复制并将其贴在显示器侧面。

## soundtraining.net

加速 IT 培训

vim 快速查表

## 一些常用的 vim 命令

按下 `<ESC>`（退出）键确保你处于普通模式，然后执行：

- `:q` 不保存退出
- `:wq` 保存并退出（写入并退出）
- `x` 删除单个字符
- `i` 插入文本
- `dw` 删除到单词末尾（`d2w` 删除两个单词，`d3w` 删除三个单词）
- `d$` 删除到行尾
- `dd` 删除整行（`2dd` 删除两行，`23dd` 删除 23 行）
- `u` 撤销上一个命令
- `U` 修复一整行
- `<CTRL>R` 重做上一个命令
- `p` 将上一次删除的内容放在光标后
- `r` 替换光标下的字符

`cw` 是“更改单词”命令，删除该单词（从光标到右侧）并使你进入“插入”模式

`cs` 是“更改行”命令，删除该行（从光标到右侧）并使你进入“插入”模式

`<SHIFT>G` 移动到文件末尾，`[number]<SHIFT>G` 移动到命令指定的行，例如 `1<SHIFT>G` 移动到第 1 行。

`/[search term]` 在文件中向前搜索搜索项。例如，`"/apache"`将搜索文件中下一个“apache”单词。

`? [search term]` 在文件中反向搜索搜索项。例如，`"?apache"`将搜索光标之前文件中最后一次出现的“apache”单词。

- `:s /[old]/[new]` 将把最后一个 "old" 替换为 "new"。例如，`:s/blue/red` 将把最后一个 "blue" 替换为 "red"
- `:s /[old]/[new]/g` 将把当前行中所有的 "old" 替换为 "new"。例如，`:s/blue/red` 将把当前行中所有的 "blue" 替换为 "red"。
- `#,$$s/[old]/[new]/g` 将在 # 符号指定的行范围内将所有的 "old" 替换为 "new"。
- `!` 允许你执行外部命令
- `set nu` 开启行号显示
- `nohlsearch` 关闭搜索项的高亮

## 使用 grep

`grep` 是一种在 Unix 世界用于辅助搜索的过滤实用工具。`grep` 是信息系统和技术领域最有用的工具之一。

一些示例：

- `#grep red blue` 将显示蓝色文件文件中包含“red”单词的文本行
- `#rpm -qa | grep smb` 将显示所有名称中包含“smb”的已安装 RPM

这里有一个使用 grep 的方便方法。假设你需要找到包含特定文本字符串的文件（或多个文件）。使用带有 `-r` 和 `-H` 选项的 `grep` 来查找包含该特定字符串的所有文件（记住 Linux 中的所有内容都是区分大小写的）。默认情况下，`grep` 只打印该字符串。如果你正在寻找包含该文本字符串的文件，你还必须告诉 `grep` 文件名。`-H` 命令就起到了作用。

在以下语句中，`-H` 打印文件名，`-r` 从起始点（`lists/`）递归搜索字符串 `PHPMAILERHOST`：

```
$ grep -Hr PHPMAILERHOST lists/
```

在以下语句中，`-H` 打印文件名，`-r` 从起始点（`lists/`）递归搜索字符串 `PHPMAILERHOST`：

```
$ grep -Hr PHPMAILERHOST lists/
```

(注：由于原文中存在重复段落，翻译已按原文结构呈现)

基于 Red Hat 的 Linux 发行版（如 RHEL、CentOS 和 Fedora）包含一个位于 `/bin` 的名为“service”的脚本。`service` 脚本的作用本质上与上述命令相同，但形式更简单：

```bash
#service nfs start
#service nfs stop
#service nfs status
#service nfs restart
```

在使用基于 RedHat 的产品（如 RHEL、Fedora、 CentOS）时，你可以输入“service”然后按两次 Tab 键，来查看可以使用 service 命令调用的各种服务。

注意：当你从源码编译应用程序时，如果不为每个编译的程序创建自定义脚本，你将无法使用此页面列出的工具。这就是使用发行版厂商编译的应用程序而不是自己编译的好处之一。

要启动你自己编译的程序，你必须找到启动该程序的脚本或二进制文件。通常，源代码中会包含一个 README 文件，告知你默认的安装路径。或者，你可以使用 `find` 工具按名称在文件系统中搜索文件。

## Linux 压缩与归档工具

归档（Archiving）是将多个文件存储在一个文件中，以简化备份、移动和传输。压缩（Compression）则使用各种算法存储文件和目录，以占用更少的磁盘或磁带空间。常见的做法是先创建一个归档文件，然后对其进行压缩。

`tar` 是一种常用的归档工具。它将许多文件保存在单个用于磁带或磁盘的归文件中，并允许从该归文件中恢复单个文件。

### 思考点：缩写“tar”

缩写“tar”源于短语“tape archive”（带存档）。

Tar 的用法：

```bash
#tar [option] [file]
#tar -cf demofile.tar file1.txt file2.txt file3.txt 将创建一个包含 file1.txt、file2.txt 和 file3.txt 的归文件 demofile.tar。
#tar -tvf demofile.tar 将详细列出归文件 demofile.tar 中的所有文件。
#tar -xf demofile.tar 将从归文件“demofile.tar”中提取所有文件。
```

RedHat Linux 中常见的压缩工具包括 (.gz)、bzip2 (.bz2) 和 zip (.zip)。用于每种类型文件的压缩工具分别是 gzip、bzip2 和 zip。用于每种压缩格式的解压缩工具分别是 gunzip、bunzip2 和 unzip。

### 压缩用法：

```bash
#gzip [filename]
#gunzip [filename]
#bzip2 [filename]
#bunzip2 [filename]
#zip [filename]
#unzip [filename]
```

由于其高压缩率且在大多数 UNIX/Linux 系统上可用，因此推荐使用 bzip2。bzip2 也可以从多个文件创建一个单一压缩文件。

zip 和 unzip 与 Windows 文件压缩工具 PKZIP 2.04 及更高版本兼容。

## 学生练习 2.3：归档与压缩

在以下练习中，你将学习如何使用常用的归档和压缩工具创建一个“tar 包”（tarball）并对其进行压缩。

1. 输入以下命令切换到 root 用户并切换目录到 `/demo`：

   `su -`

   `Password:p@ss5678`

   `#cd /demo`

2. 再次使用 `touch` 命令在 `/demo` 中创建三个文件：

   `#touch file1 file2 file3`

3. 输入“ls”命令确认 file1、file2 和 file3 是否存在。

4. 使用以下命令为三个文件创建一个名为 `files.tar` 的 tar 包（带存档）：

   `#tar cvf files.tar file*`

5. 使用以下命令查看 tar 包的内容：

   `#tar tvf files.tar`

6. 使用以下命令查看 tar 包的大小：

   `#ls -l`

7. `files.tar` 的大小有多大？

   应该是 10,240 字节。

8. 使用以下命令压缩 tar 包：

   `#gzip files.tar`

9. 双击向上方向键返回“ls -l”命令并按回车。

10. 注意到 `files.tar` 已重命名为 `files.tar.gz`，表示它是一个 gzip 压缩文件。`files.tar.gz` 的大小有多大？

     现在应该大约 141 字节。

11. 现在，使用以下命令解压 `files.tar.gz`：

    `#gunzip files.tar.gz`

12. 双击向上方向键返回“ls -l”命令并按回车。

13. 注意到 .gz 扩展名已被删除，`files.tar` 回到了原始大小。

14. 使用以下命令删除 tar 包：

    `#rm -rf files.tar`

你可以使用 bzip2 和 bzip2 命令执行类似的操作。此外，通过使用 gzip 的“z”开关或 bzip2 的“j”开关，可以在一次操作中创建并压缩 tar 包：

1. 在 `/demo` 目录下，执行以下命令：

   `#tar cvfj files.tar.bz2 file*`

2. 使用“ll”命令显示 `/demo` 的内容。

3. 注意到 `files.tar.bz2` 现在已压缩。它的大小有多大？

4. `files.tar.gz` 的大小有多大？

   在这种情况下，用 bzip2 压缩的 tar 包应该比用 gzip 压缩的 tar 包 小一点。

5. 使用以下命令查看内容：

   `#tar -jf files.tar.bz2`

6. 注意到 .gz 扩展名已被删除（此处应为 .bz2）。
