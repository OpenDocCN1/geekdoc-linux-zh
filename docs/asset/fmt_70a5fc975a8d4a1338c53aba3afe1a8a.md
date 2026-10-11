
> 如果你迫切想知道细节：`bzip2` 使用“Burrows-Wheeler 变换”将输入中经常出现的子串编码为单个字符序列。这个中间结果根据单个字符的“局部频率”进行排序，排序后的结果在经过游程编码后，使用霍夫曼方案进行编码。然后，霍夫曼码以非常紧凑的方式写入文件。

> 那 `bzip2` 呢？`bzip` 是 `bzip2` 的前身，它在块变换后使用算术编码而不是霍夫曼编码。然而，作者决定避开算术编码，因为其周围存在各种软件专利问题。

与 `gzip` 类似，`bzip2` 接受一个或多个文件名作为压缩参数。这些文件会被压缩版本替换，其文件名以 `.bz2` 结尾。

`-c` 和 `-d` 选项分别对应 `gzip` 的同名选项。然而，“质量选项” `-1` 到 `-9` 的工作方式不同：它们确定压缩期间使用的块大小。默认值为 `-9`，而 `-1` 并不会带来显著的速度提升。

`-9` 使用 900 KiB 的块大小。这对应于解压时约 3.7 MiB 的内存占用（压缩时为 7.6 MiB），这在现代硬件上应该不成问题。进一步增加块大小似乎不会带来明显的优势。——值得注意的是，*压缩*时块大小的选择决定了*解压*时所需的内存量，如果你使用多吉字节的 PC 为内存很小的计算机（烤面包机、机顶盒、……）准备 `.bz2` 文件，这一点值得牢记。`*bzip2(1)*` 对此有更详细的说明。

类比 `gzip` 和 `gunzip`，使用 `bunzip2` 来解压使用 `bzip2` 压缩的文件。（这实际上是 `bzip2` 程序的另一个名称：你也可以使用 "`bzip2 -d`" 来解压文件。）

### 11.5 使用 zip 和 unzip 归档和压缩文件

为了与 Windows 计算机或互联网交换数据，使用广泛流行的 ZIP 文件格式通常是有意义的（尽管如今许多 Windows 上的文件归档程序也可以处理 `.tar.gz`）。在 Linux 上，有两个独立的程序 `zip`（用于创建归档）和 `unzip`（用于解包归档）。

根据你的发行版不同，你可能需要单独安装这些程序。例如，在 Debian GNU/Linux 中，有两个不同的软件包，`zip` 和 `unzip`。

`zip` 程序以类似 PKZIP 等程序的方式结合归档和压缩。在最简单情况下，它收集命令行上传递的文件：

```text
$ zip test.zip file1 file2
  adding: file1 (deflated 66%)
  adding: file2 (deflated 62%)
$
```

此处 `test.zip` 是结果归档的名称。

你可以使用 `-r` 选项告诉 `zip` 递归下降到子目录中：

```text
$ zip -r test.zip ziptest
  adding: ziptest/ (stored 0%)
  adding: ziptest/testfile (deflated 62%)
  adding: ziptest/file2 (deflated 62%)
  adding: ziptest/file1 (deflated 66%)
```

使用 `-@` 选项时，`zip` 从标准输入读取要归档的文件名：

```text
$ find ziptest | zip -@ test
  adding: ziptest/ (stored 0%)
  adding: ziptest/testfile (deflated 62%)
  adding: ziptest/file2 (deflated 62%)
  adding: ziptest/file1 (deflated 66%)
```

你可以省略归档文件名称中的 `.zip` 后缀。

`zip` 知道两种将文件添加到归档的方法。`stored` 表示文件未经压缩存储，而 `deflated` 表示已压缩（百分比表示文件被压缩了*多少*——即“*deflated*”的程度）。

62%"，例如，意味着归档内的文件仅为其原始大小的 38%）。`zip` 会自动选择更合理的处理方式，除非你使用 `-0` 选项完全禁用压缩。

如果你以一个现有的 ZIP 归档作为第一个参数调用 `zip`，且没有指定其他任何内容，则要归档的文件会被*追加*到归档中，位于现有内容之上（同名文件将被覆盖）。在这种情况下，`zip` 的行为与 `tar` 和 `cpio` 不同（特此说明）。如果你希望得到一个"干净"的归档，你必须先移除该文件。

除了盲目地添加文件外，`zip` 还支持其他几种操作模式：`-u` 选项"更新"归档，仅当命令行中指定的文件比归档中已存在的同名文件更新时才将其添加到归档中（对于尚未存在于归档中的指定名称文件，无论如何都会添加）。`-f` 选项"刷新"归档——归档内的文件会被命令行中的更新版本覆盖，但前提是这些文件已经存在于归档中（不会添加全新的文件到归档中）。`-d` 选项将命令行中的文件名视为归档内的文件名，并删除这些文件。

较新版本的 `zip` 还支持 `-F5`（"文件系统同步"）模式：此模式通过基本上执行 `-u` 的操作并将那些未在命令行中列出的文件从归档中删除（或者在 `-r` 的情况下，删除目录搜索过程中的一部分）来"同步"归档与文件系统。与完全重构归档相比，这种方法的优点是归档中预先存在且未变更的文件无需再次压缩。

`zip` 支持各种选项，你可以使用 `zip -h` 查看列表（或使用 `-h2` 查看更详细的列表）。手册页 `zip(1)` 也很有用。

你可以使用 `unzip` 再次解包 ZIP 归档（这也可能是来自 Windows 机器的 ZIP 归档）。最好先使用 `-v` 选项 peek 一下归档内部，看看里面有什么——这可能会为你省去处理子目录（或缺失目录）的麻烦。

```
$ unzip -v test
Archive:  test.zip
Length  Method   Size  Cmpr  Date   Time  CRC-32  Name
--------  ----------  ------  ----  ---------- -----  ---------  ----------------
     0   Stored         0   0% 2012-02-29 09:29  00000000  ziptest/
   16163 Defl:N     6191  62% 2012-02-29 09:46  0d9df6ad  ziptest/testfile
   18092 Defl:N     6811  62% 2012-02-29 09:01  4e46f1a1  ziptest/file2
   35147 Defl:N    12119  66% 2012-02-29 09:01  6777f57c  ziptest/file1
--------          ----------  -----  ---------  ----------------
   69402         25121   64%                    4 files
```

仅将归档名称作为唯一参数调用 `unzip` 即可解包归档：

```
$ mv ziptest ziptest.orig
$ unzip test
Archive:  test.zip
 creating: ziptest/
 inflating: ziptest/testfile
 inflating: ziptest/file2
 inflating: ziptest/file1
```

使用 `-d` 选项可以在当前目录以外的目录解包归档。如有必要，该目录会首先创建：

```
$ unzip -d dir test
Archive:  test.zip
creating: dir/ziptest/
inflating: dir/ziptest/testfile
inflating: dir/ziptest/file2
inflating: dir/ziptest/file1
```

如果在命令行中指定特定文件，则只会解包这些文件：

```
$ rm -rf ziptest
$ unzip test ziptest/file1
Archive:  test.zip
inflating: ziptest/file1
```

在这种情况下，`ziptest` 目录也会被创建。

或者，你可以使用 `-x` 选项有选择地排除某些文件不被解包：

```
$ rm -rf ziptest
$ unzip test -x ziptest/file1
Archive:  test.zip
creating: ziptest/
inflating: ziptest/testfile
inflating: ziptest/file2
```

你还可以使用 shell 搜索模式来解包特定文件（或阻止它们被解包）：
