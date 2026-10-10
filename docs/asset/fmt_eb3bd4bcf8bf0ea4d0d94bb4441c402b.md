
```bash
$ gzip mydata
$ ls
mydata.gz
```

要解压缩 gzip 文件，可以使用带有 `-d` 选项的 `gzip` 命令，或者使用 `gunzip` 命令。这些命令会解压缩扩展名为 `.gz` 的压缩文件，并用相同根名但没有 `.gz` 扩展名的解压缩版本替换它。当你使用 `gunzip` 时，甚至不需要输入 `.gz` 扩展名；`gunzip` 和 `gzip -d` 会默认假设它。表 10-7 列出了不同的 gzip 选项。

```bash
$ gunzip mydata.gz
$ ls
mydata
```

> **提示** 在你的桌面上，你可以通过文件管理器定位存档文件并双击它来提取存档的内容。你也可以右键单击并选择“用存档管理器打开”。这将启动 File Roller 应用程序，该程序会打开存档并列出其内容。然后你可以选择提取存档。如果存档已压缩，File Roller 将使用适当的工具解压缩存档（bzip2、zip 或 gzip），然后提取存档（tar）（参见第 4 章）。

你还可以压缩已存档的 tar 文件。这将生成扩展名为 `.tar.gz` 的文件。压缩的存档文件通常用于通过网络传输非常大的文件。

```bash
$ gzip myarch.tar
$ ls
myarch.tar.gz
```

你可以使用 `tar z` 选项单独压缩 tar 文件成员，该选项会调用 `gzip`。使用 `z` 选项时，`tar` 会在将文件放入存档之前调用 `gzip` 对文件进行压缩。

| 选项 | 执行 |
| :--- | :--- |
| `-c` | 将文件的压缩版本发送到标准输出；列出的每个文件单独进行压缩:<br>`gzip -c mydata preface > myfiles.gz` |
| `-d` | 解压缩压缩文件；或者你可以使用 `gunzip`:<br>`gzip -d myfiles.gz`<br>`gunzip myfiles.gz` |
| `-h` | 显示帮助列表。 |
| `-l file-list` | 显示列出的每个文件的压缩和解压缩大小:<br>`gzip -l myfiles.gz` |
| `-r directory-name` | 递归搜索指定目录并压缩其中所有文件；搜索从当前工作目录开始。当与 `gunzip` 一起使用时，指定目录的压缩文件将被解压缩。 |
| `-v file-list` | 对于每个压缩或解压缩的文件，显示其名称及其大小的减少百分比。 |
| `-num` | 确定压缩的速度和大小；范围从 `-1` 到 `-9`。较小的数字提供更高的速度但较低的压缩率，导致文件较大但压缩和解压缩速度快。因此，`-1` 提供最快的压缩，但文件最大；`-9` 导致文件非常小，但压缩和解压缩所需时间更长。默认值为 `-6`。 |

**表 10-7 gzip 选项**

然而，使用 `z` 选项压缩成员的存档无法更新，也无法向其中添加内容。所有成员都必须被压缩，并且必须同时添加。

### compress 和 uncompress 命令

你还可以使用 `compress` 和 `uncompress` 命令来创建压缩文件。它们生成具有 `*.Z*` 扩展名的文件，并使用与 `gzip` 不同的压缩格式。`compress` 和 `uncompress` 命令使用得不是很广泛，但你偶尔可能会遇到 `*.Z*` 文件。你可以使用 `uncompress` 命令来解压缩 `*.Z*` 文件。`gzip` 工具是标准的 GNU 压缩实用程序，应该用它代替 `compress`。

### 使用 bzip2 进行压缩

另一种流行的压缩实用程序是 `bzip2`。它使用 Burrows-Wheeler 块排序文本压缩算法和霍夫曼编码来压缩文件。命令行选项在设计上与 `gzip` 相似，但并不完全相同。（参见 `bzip2` 手册页以获取完整列表。）你使用 `bzip2` 命令压缩文件，并使用 `bunzip2` 解压缩。`bzip2` 命令创建扩展名为 `*.bz2*` 的文件。你可以使用 `bcat` 将压缩数据输出到标准输出。`bzip2` 命令按块压缩文件，允许你指定块的大小（较大的块提供更高的压缩率）。与使用 gzip 一样，你可以使用 bzip2 来压缩 tar 存档文件。以下示例将 `mydata` 文件压缩为 bzip 压缩文件，扩展名为 `.bz2`：

```bash
$ bzip2 mydata
$ ls
mydata.bz2
```

要解压缩，对 bzip 文件使用 `bunzip2` 命令。

```bash
$ bunzip2 mydata.bz2
```

### 使用 Zip

Zip 是一种压缩和存档实用程序，其模型基于 PKZIP，最初用于 DOS 系统。Zip 是一种跨平台实用程序，用于 Windows、Mac、MS-DOS、OS/2、Unix 和 Linux 系统。Zip 命令可以处理由 PKZIP 创建的存档，并可以使用 *Zip* 存档。你使用 `zip` 命令压缩文件。这将创建扩展名为 `*.zip*` 的 Zip 文件。如果没有列出文件，`zip` 将压缩数据输出到标准输出。你还可以使用 `-` 参数让 `zip` 从标准输入读取。要压缩目录，你包括 `-r` 选项。第一个示例对文件进行存档和压缩：

```bash
$ zip mydata
$ ls
mydata.zip
```

下一个示例对 `reports` 目录进行存档和压缩：

```bash
$ zip -r reports
```

支持全套存档操作。使用 `-f` 选项，你可以用较新版本更新 Zip 存档中的特定文件。`-u` 选项替换或添加文件，而 `-d` 选项从 Zip 存档中删除文件。还有用于加密文件、进行 DOS 到 Unix 的行结尾转换以及包含隐藏文件的选项。

要解压缩并提取 Zip 文件，你使用 `unzip` 命令。

```bash
$ unzip mydata.zip
```
