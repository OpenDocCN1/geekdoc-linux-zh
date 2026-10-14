
# 第8章：文件管理

文件管理工具包括分割、比较和压缩文件、制作备份存档以及跟踪文件修订的工具。其他管理工具用于确定文件内容、更改其时间戳。

## 8.1 确定文件类型和格式

当我们谈论文件类型时，指的是它所包含的数据类型，这可能包括文本、可执行文件或其他数据；当我们谈论文件格式时，指的是数据的组织方式。`file` 工具可以分析文件的类型和格式。

- 要确定 `README.txt` 的类型：

```bash
file README.txt
```

输出：`ASCII text`。

- 要确定 `image.jpg` 的类型，输入：

```bash
file image.jpg
```

输出：`JPEG image data, ...`。

- 要确定 `script.sh` 的类型，输入：

```bash
file script.sh
```

输出：`POSIX shell script, ASCII text`。

- 要确定 `archive.tar.gz` 的类型，输入：

```bash
file archive.tar.gz
```

输出：`gzip compressed data, ...`。

## 8.2 更改时间戳

使用 `touch` 更改文件的时间戳。如果文件不存在，`touch` 会创建一个空文件，其时间戳为当前时间。

- 要更新 `file` 的访问时间和修改时间：

```bash
touch file
```

- 要将 `file` 的访问时间更改为特定时间，使用：

```bash
touch -a 202301011200 file
```

- 要将 `file` 的修改时间更改为特定时间，使用：

```bash
touch -m 202301011200 file
```

- 要同时将 `file` 的访问时间和修改时间更改为特定时间，使用：

```bash
touch -t 202301011200 file
```

- 要将 `file` 的修改时间更改为“昨天”，使用：

```bash
touch -d "yesterday" file
```

- 要将 `file` 的修改时间更改为“明天”，使用：

```bash
touch -d "tomorrow" file
```

- 要将 `file` 的修改时间更改为过去 10 天前，使用：

```bash
touch -d "10 days ago" file
```

- 要将 `file` 的修改时间更改为 2023 年 5 月 1 日 10:30，使用：

```bash
touch -d "2023-05-01 10:30" file
```

- 要将 `file` 的访问时间及修改时间都更改为 2023 年 5 月 1 日 10:30，使用：

```bash
touch -d "2023-05-01 10:30" file
```

## 8.3 分割文件

`split` 工具可以将一个文件分割成多个小文件。例如，假设你有一个大文件 `large.txt`，大小为 10MB，你想将其分割成每个 2MB 的小文件。

- 要将 `large.txt` 分割成每个 2MB 的文件，输入：

```bash
split -b 2M large.txt
```

该命令会创建名为 `large.txt.aa`、`large.txt.ab`、`large.txt.ac`、`large.txt.ad` 和 `large.txt.ae` 的文件。

- 要指定输出文件的前缀，输入：

```bash
split -b 2M large.txt part_
```

该命令会创建名为 `part_aa`、`part_ab`、`part_ac`、`part_ad` 和 `part_ae` 的文件。

- 要使用数字后缀代替字母后缀，输入：

```bash
split -b 2M -d large.txt part_
```

该命令会创建名为 `part_00`、`part_01`、`part_02`、`part_03` 和 `part_04` 的文件。

- 要按行数分割文件，输入：

```bash
split -l 500 large.txt
```

该命令会将 `large.txt` 分割成每个包含 500 行的文件。

- 从分割的文件重构原始文件，输入：

```bash
cat large.mp3.* > large.mp3
rm large.mp3.*
```

在此示例中，使用 `rm` 工具在原始文件重构后删除所有分割文件。

## 8.4 比较文件

有许多工具可以用不同的方式比较文件内容；这些食谱展示了如何使用其中一些。这些工具对于比较文件中的文本段特别有用，但并不是你使用它们的唯一方法。

### 8.4.1 确定两个文件是否不同

使用 `cmp` 来确定两个文件是否不同。它接受两个文件名作为参数，如果文件包含相同的数据，`cmp` 不输出任何。然而，如果文件不同，`cmp` 会输出文件中出现第一个差异的字节位置和行号。

- 要确定文件 `master` 和 `backup` 是否不同，输入：

```bash
cmp master backup
```

### 8.4.2 查找文件差异

使用 `diff` 比较两个文件并输出差异报告（有时称为“diff”），该报告包含两个文件之间不同的文本。差异报告的格式使得其他工具（即 `patch` - 见 Recipe 8.4.3 [使用差异报告修补文件]，第 102 页）可以使用它使文件与与之比较的文件完全相同。

要比较两个文件并输出差异报告，将文件名作为参数传递给 `diff`。

- 要比较文件 `manuscript.old` 和 `manuscript.new`，输入：

```bash
diff manuscript.old manuscript.new manuscript.diff
```

差异报告输出到标准输出；要将其保存到文件，请将输出重定向到要保存的文件：

```bash
diff manuscript.old manuscript.new > manuscript.diff
```

在前面的示例中，差异报告被保存到名为 `manuscript.diff` 的文件。

差异报告旨在与 `patch` 等命令配合使用，以便将差异应用到文件中。有关 `diff` 及其输出格式的更多信息，请参见 Info `diff.info`，现在的 `Top`。

要查看两个输出之间的差异，使用 `diff` 而不是 `diff diff`；它不是输出差异报告，而是以两列并排的形式输出文件，用空格分隔。第一个文件中不同的行仅以 '<' 显示，而只出现在第二个文件中的行以 '>' 开头。

- 要在屏幕上并排查看文件 `laurel` 和 `hardy`，并在列之间指示任何差异，输入：

```bash
diff laurel hardy | less
```

要输出三个文件之间的差异，使用 `diff3`。

- 为文件 `larry`、`curly` 和 `moe` 输出差异报告，并输出到名为 `stooges` 的文件中，输入：

```bash
diff3 larry curly moe > stooges
```

### 8.4.3 使用差异报告修补文件

要将差异报告中的差异应用到报告中所比较的原始文件，使用 `patch`。它接受要修补的文件名和差异报告文件名（或 `patchfile`）作为参数。然后它将补丁中指定的更改应用到原始文件。这对于分发不同版本的文件特别有用——小的补丁文件比大型源代码更容易通过网络传输。

- 要用补丁文件 `manuscript.diff` 更新原始文件 `manuscript.new`，输入：

```bash
patch manuscript.new manuscript.diff
```

## 8.5 压缩文件

文件压缩对于存储或传输大文件非常有用。当你压缩一个文件时，它会缩小体积并节省磁盘空间。文件压缩使用算法来更改文件中的数据：要使用压缩文件中的数据，必须先解压缩以恢复原始数据（以及原始文件大小）。

以下食谱解释了如何压缩文件。

### 8.5.1 压缩文件

使用 `gzip` (GNU zip) 压缩文件。它接受要压缩的文件或多个文件名作为参数；它写入指定文件的压缩版本，在文件名后添加 `.gz` 扩展名，并删除原始文件。

- 要压缩文件 `war-and-peace`，输入：

```bash
gzip war-and-peace
```

此命令压缩文件 `war-and-peace` 将其放入新文件 `war-and-peace.gz` 中；然后 `gzip` 删除原始文件 `war-and-peace`。

### 8.5.2 解压缩文件

要访问压缩文件的内容

- 要扩展文件 `war-and-peace.gz`，输入：

```bash
gunzip war-and-peace.gz
```

此命令扩展文件 `war-and-peace.gz` 并将其放入名为 `war-and-peace` 的新文件中；然后 `gunzip` 删除压缩文件 `war-and-peace.gz`。
