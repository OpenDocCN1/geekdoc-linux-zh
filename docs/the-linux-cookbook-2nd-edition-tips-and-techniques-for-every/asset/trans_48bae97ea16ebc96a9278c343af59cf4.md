

⇒ 将当前目录下所有 `.DOC` Word 文件转换为最大行宽为 40 个字符的 \LaTeX 文件，输入：

```
$ word2x -f latex -w 40 *.DOC [RET]
```

## 26.5.2 将 Word 转换为纯文本

要将 Word 文件转换为纯文本，请使用 word2x 并将 “text” 作为 -format 选项的参数给出。

⇒ 要将 Word 文件 resume.doc 转换为名为 resume 的纯文本文件，输入：

```
$ word2x -f text resume.doc resume [RET]
```

要将转换结果发送到标准输出，请将连字符字符 (-) 作为要使用的输出文件。这对于将纯文本转换通过管道传递给处理文本的其他工具很有用，例如 grep，这是一个用于搜索文本的工具（参见 Recipe 14.1 [Searching Text for a Word]，第 333 页）。

⇒ 要不区分大小写地在 Word 文件 resume.doc 的文本中搜索字符串 “linux”，输入：

```
$ word2x resume.doc - | grep -i linux [RET]
```

这些命令将 Word 文件 resume.doc 转换为文本并输出该文本中所有包含字符串 “linux” 的行（如果有），且不区分大小写。原始 resume.doc 文件保持不变。

## 26.6 从专有格式转换文本

使用 Recipe 9.3.6 [Listing Text in Binary Files]，第 228 页，来输出保存在专有格式文件中的任何文本字符串。这并不总是有效，因为并非所有专有格式都以 ASCII 字符串保存文本，但通常值得尝试。

⇒ 要查看文件 HCX1010A.BIN 中的所有 ASCII 字符串，输入：

```
$ strings HCX1010A.BIN | less [RET]
```

## 26.7 管理 ZIP 归档

Unzip
DEB: unzip
RPM: unzip
WWW: http://www.info-zip.org/

ZIP 文件压缩将一个或多个文件压缩成一个带有 .zip 扩展名的单一新文件。这就是大多数刚接触 Linux 或 UNIX 的人想到“文件归档”时的想法。但在 UNIX 世界中，文件归档和压缩是独立的工具，尽管它们通常相辅相成。我们制作压缩的 tar 归档（参见 Recipe 8.5 [Managing File Archives]，第 199 页）。然后我们可以用 gzip 或 bzip2 压缩这些归档或任何其他文件（参见 Recipe 8.4 [Using File Compression]，第 196 页）。

在与其他操作系统用户发送和接收文件组时，通常使用 ZIP 归档格式。zip 和 unzip 工具可以像其他操作系统的流行 PKZIP 工具一样创建和提取 ZIP 归档。

以下配方展示了如何使用这些工具。

### 26.7.1 压缩文件

使用 zip 来制作文件或文件组的 ZIP 归档。它以要创建的 ZIP 归档的名称和要放入归档中的文件规范作为参数。

为归档名称指定 .zip 扩展名是可选的；如果归档已存在，则给定的文件将被添加到归档中。

⇒ 这里有两种使用方法。

- 要制作一个包含当前目录下所有 .png 文件的 ZIP 归档文件 zippy.zip，输入：
- $ zip zippy *.png [RET]
- 要将当前目录下所有 .tiff 文件添加到已存在的 ZIP 归档文件 zippy.zip 中，输入：
- $ zip zippy *.tiff [RET]

指定目录时，如果只给出目录名，则只有该目录（而不是其内容）会被包含在归档中。在目录中指定通配符将包含其包含的文件和任何子目录名，但不会进入这些子目录以包含其中可能包含的任何文件。使用 ‘-r’ 选项可递归进入指定的目录，从而包含其全部内容。

⇒ 要制作一个包含当前目录下所有文件的 ZIP 归档 zippy.zip，输入：

```
$ zip zippy * [RET]
```

如果当前目录包含任何目录，则这些目录名会被包含在 ZIP 归档中，但不会包含其任何内容。

⇒ 要制作一个包含当前目录下所有文件以及 addons 目录下所有文件的 ZIP 归档 zippy.zip，输入：

```
$ zip zippy * addons/* [RET]
```

此命令将当前目录中的所有文件放入名为 zippy.zip 的归档中，同时也添加 addons 目录中的所有文件，但不会添加 addons 可能包含的任何子目录的内容。

⇒ 要制作一个包含整个 addons 目录树的 ZIP 归档 zippy.zip，输入：

```
$ zip zippy -r addons/* [RET]
```

### 26.7.2 解压缩文件

使用 unzip 解压缩存储在 ZIP 归档中的文件。给定归档的名称作为参数时，它会提取该归档包含的所有文件。与 zip 一样，给出 .zip 扩展名是可选的。

⇒ 要解压缩 ZIP 归档 blueprints.zip 中的所有文件，输入：

```
$ unzip blueprints.zip [RET]
```

有时在真正解压缩之前先查看 ZIP 归档内部是个好主意，以了解解压缩会带来什么——如果一个 ZIP 归档包含一百个文件而你并不期望它们，先解压缩可能会很不方便。

这就是 -t 选项派上用场的地方，我在真正解压缩归档之前总是使用它。这只是测试归档中包含的文件，以确保归档文件没有损坏。随着 unzip 运行测试，它会列出归档中的每个文件。此命令不会解压缩任何文件。

⇒ 要测试 ZIP 归档 blueprints.zip 是否有错误，从而列出其包含的所有文件，输入：

```
$ unzip -t blueprints.zip [RET]
```

## 26.8 使用其他跨平台转换工具

有更多工具可用于将来自其他平台的文件转换为可在 Linux 上使用的格式；下表描述了其中一些。

