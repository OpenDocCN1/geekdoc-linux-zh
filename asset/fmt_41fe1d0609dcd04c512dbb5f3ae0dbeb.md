
# chown: 更改所有者和组

- `chown [options] owner file-list`
- `chown [options] owner:group file-list`
- `chown [options] owner: file-list`
- `chown [options] :group file-list`
- `chown [options] --reference=rfile file-list`

`chown` 工具更改文件的所有者或所属组。只有 root 或属于新组的文件所有者可以更改其所属组。

## 参数

`owner` 是新所有者的用户名或数字 ID。`file-list` 是要更改的所有者或组关联的文件路径列表。`group` 是新组的名称或数字 ID。表 V-9 显示了你可以指定新所有者或组的方式。

### 表 V-9. 指定新所有者或组

| Argument | 含义 |
|---|---|
| `owner` | 文件的新所有者；不更改组 |
| `owner:group` | 文件的新所有者和新组关联 |
| `owner:` | 文件的新所有者；将组更改为所有者的登录组 |
| `:group` | 文件的新组；不更改所有者 |

## 选项

接受第 587 页描述的常用选项。

- `-c` 为每个所有者/组更改的文件显示一条消息。
- `-dereference` 更改符号链接的所有者/组，而不是符号链接本身。默认是 `-no-dereference`。
- `-q` 或 `--silent`、`-f` 当 `chown` 无法更改文件的所有者/组时，防止显示错误消息。
- `-no-dereference`、`-h` 更改符号链接的所有者/组，而不是链接指向的文件（默认）。
- `-recursive`、`-R` 当文件列表中目录时，此选项将遍历目录层次，为遇到的所有文件设置指定的等待者/组。
- `-reference=rfile` 将文件列表中文件的所有者和组关联更改为 `rfile`。
- `-v`、`-v` 为每个文件显示其所有者/组是保留还是已更改。

## 注意事项

`chown` 工具在更改文件所有者时会清除 `setuid` 和 `setgid` 位。

## 示例

以下命令更改 `manuals` 目录下 `chapter1` 文件的所有者。新所有者是 Jen。

```bash
# chown jenny manuals/chapter1
```

以下命令将 `/home/alex/literature` 目录及其所有子目录下所有文件的所有者设置为 `Alex`，并将与它们关联的组设置为 `Alex` 的登录组：

```bash
# chown --recursive alex /home/alex/literature
```

下一个命令将 `literature` 中文件的所有者更改为 `alex`，并更改与这些文件关联的组：

```bash
# chown alex:pubs /home/alex/literature/*
```

最后一个示例将 `manuals` 中文件的组关联更改为 `pubs`，而不改变其所有者文件。执行此命令的用户必须属于 `pubs` 组。

```bash
$ chown :pubs manuals/*
```

# cmp: 比较两个文件

```bash
cmp [options] file1 [file2 [skip2]]
```

`cmp` 工具按字节为单位显示两个文件之间的差异。如果文件相同，`cmp` 将显示第一个差异处的字节数和行号。

# 参数

`file1` 和 `file2` 是 `cmp` 比较的文件路径。如果省略 `file2`，`cmp` 将使用标准输入代替 `file2`；如果省略 `file1`，`cmp` 将读取标准输入代替文件。

`skip1` 和 `skip2` 是十进制数，表示在开始比较之前在每个文件中跳过的字节数。

# 选项

- `-`、`--print-bytes`、`-b` 显示更多信息，包括文件名、字节和行号，以及第一个差异字节的八进制和 ASCII 值。
- `-`、`-ignore-initial=n` 在开始比较之前跳过两个文件中的前 `n` 个字节。
- `-`、`-verbose`、`-` (小写 "I") 不在第一个不同字节的字节处停止，而是继续比较两个文件，并显示每个差异字节的位置和值。位置以从文件开始的十进制字节偏移量显示；字节值以八进制显示。当任一文件遇到 `EOF`（文件结束符）时比较终止。
- `-`、`-silent` 或 `-quiet`、`-s` 抑制 `cmp` 的输出；仅设置退出状态（参见“备注”）。

# 备注

字节和行号从 1 开始计数。

如果文件相同，`cmp` 工具不会显示任何消息；它只设置退出状态。此工具返回文件是否相同或不同。退出状态大于 1 表示发生了错误。

当您使用 `skip1`（以及 `skip2`）时，`cmp` 显示的偏移值是在跳过 `skip1` 和 `skip2` 之后的比较标准字节；参见第 586 页的表 V-1。

`diff`（第 638 页，`cmp`）同样适用于二进制文件和 ASCII 文件。

# 示例

示例使用了下所示的文件 `a` 和 `b`。这两个文件有两个差异。第一个差异是文件 `b` 中的内容被替换为 `lazy`。第二个差异更为微妙：在 `NEWLB` 之前出现了一个 `TAB` 字符。

```bash
$cat a

The quick brown fox jumped over the lazy dog.
```

```bash
$cat b

The quick brown fox jumped over the lazy dog.TAB
```

第一个示例使用不带任何选项的 `cmp` 来比较两个文件。`cmp` 工具报告文件不同，并识别了从文件开始发现第一个差异的偏移量：

```bash
$cmp a b

a b differ: char 39, line 1
```

您可以通过添加 `--print-bytes` 选项来显示该位置字节的值：

```bash
$cmp --print-bytes a b

a b differ: char 39, line 1 is 172 z 163 s
```

`-l` 选项显示两个文件之间所有不同的字节。因为如果差异很多会产生大量输出，您可能希望将输出重定向到文件。以下示例显示了两个差异，`-b` 选项也会显示字节的值。当文件 `a` 具有 `CONTROL—J` (`NEWLINE`) 时，文件 `b` 有一个控制消息显示已到达文件 `a` 的末尾，表示文件 `b` 比文件 `a` 长。

```bash
$cmp -lb a b
```

```
39 172 z    163 s
46 12 ^J     11 ^I
comp: EOF on a
```

# configure: 配置

分布。要使 `configure` 生成带有 `-Wall` 和 `-O2` 标志的 `Makefile`，请使用以下

```bash
$CFLAGS="-Wall -O2" ./configure
```

如果你正在使用 `tcsh`，请使用以下命令：

```bash
tcsh env CFLAGS="-Wall -O2" ./configure
```

# cp: 复制文件

```
cp[options] source-file destination-file
```

```
cp[options] source-file-list destination-directory
```

`cp` 工具用于复制一个或多个文件。它可以创建单个文件的副本（第一格式），也可以复制一个或多个目录（第二格式）。使用 `--recursive` 选项，`cp` 可以复制目录。

## 参数

`source-file` 是 `cp` 要复制的文件的路径。`destination-file` 是 `cp` 创建文件副本的目标路径。

`source-file-list` 是 `cp` 要复制的一个或多个文件路径名列表。`destination-directory` 是 `cp` 放置复制文件的目录。在此格式下，`cp` 会为每个复制的文件赋予与 `source-file` 相同的名称。

`--recursive` 选项允许 `cp` 从 `source-file-list` 递归地复制到 `destination-directory`。

## 选项

接受第 587 页描述的常用选项。

- `-archive`、`-a` 尝试尽可能保留 `source-file` 的所有属性。等同于 `-dpPR`。
- `-backup`、`-b` 如果复制文件会删除或覆盖现有文件，此选项将为将被覆盖的文件创建一个备份副本。该备份副本的名称与 `destination-file` 相同，但末尾添加了波浪线 (~)。当你同时使用 `--backup` 和 `--force` 时，当你尝试将文件覆盖自身时，`cp` 会创建一个备份副本。
- `-d` 复制符号链接，而不是链接所指向的文件。同时保留 `destination-file` 中与对应的 `source-file` 之间的硬链接。此选项等同于 `--no-dereference` 和 `--preserve-links`。
- `-force`、`f` 当 `destination-file` 存在且无法以写打开时，此选项会导致 `cp` 在复制 `source-file` 之前尝试删除 `destination-file`。当复制文件的用户没有访问 `destination-file` 的权限，但拥有包含 `destination-file` 目录的权限时，此选项非常有用。另参见 `--backup`。
- `-interactive`、`i` 当 `cp` 将覆盖文件时提示。如果输入带有 `y` 或 `Y` 的字符串，`cp` 继续执行。如果你输入其他内容，`cp` 将不复制该文件。
- `-dereference`、`L` 复制符号链接指向的文件。参见 `--no-dereference`。
- `-preserve`、`p` 创建一个与 `source-file` 的所有者、组、权限、访问日期和修改日期均相同的 `destination-file`。
- `-no-dereference`
- `-P` 复制符号链接，而不是链接所指向的文件。如果不使用 `-R`、`-r` 或 `--recursive` 选项，默认行为是解引用链接（复制指向的文件，而不是链接本身）。使用这些选项之一，`cp` 不会解引用符号链接（它复制链接本身，而不是链接指向的文件）。
- `-parents` 将相对路径复制到目录，并根据需要创建目录。（参见“示例”）。
- `-preserve=links` 在递归复制目录时，尝试保留 `destination-file` 中与对应的 `source-file` 之间的硬链接。
- `-`、`-recursive`、`-R` 递归复制包括普通文件的目录层次结构。隐含了 `--no-dereference` 选项。
- `-`、`-update`、`-u` 仅在 `destination-file` 不存在或其比 `source-file` 旧时复制。
- `-`、`-verbose`、`-v` 在 `cp` 复制每个文件时显示该文件名。

## 注意事项

如果在执行 `cp` 之前 `destination-file` 已存在，`cp` 将覆盖该文件，破坏其内容，但保留文件原有的所有者和组。

如果 `destination-file` 不存在，`cp` 使用 `source-file` 的访问权限。用户复制 `destination-file` 文件，该用户的组将成为与 `destination-file` 关联的组。

使用 `-p` 选项，`cp` 尝试设置所有者、组、权限、访问日期和修改日期以匹配文件。

与（第 702 页）不同，`cp` 创建的 `destination-file` 与其 `source-file` 是独立的。

## 示例

第一个命令在工作目录中为文件 `letter` 创建副本。副本的名称为 `letter.sav`。

```bash
$cp letter letter.sav
```

下一个命令将所有文件名以 `.c` 结尾的文件复制到 `archives` 目录（这是一个子目录）。每个复制的文件保留了其简单文件名，但具有新的绝对路径。由于使用了 `--preserve`，`archives` 中的文件具有与 `source-file` 相同的所有者、组、权限、访问日期和修改日期。

```bash
$cp --preserve *.c
```

下一个示例将 `/home/jenny` 中的 `memo` 复制到工作目录：

```bash
$cp /home/jenny/memo .
```

下一个示例使用 `--parents` 选项将文件 `memo/th/max` 复制到 `dir` 目录。`find` 工具显示了新创建的层次结构。

```bash
$cp --parents memo/th/max
```

# cpio: 归档工具

- `-reset-access-time`
    - `**-a**` 在复制源文件后重置它们的文件的访问时间，使其在复制后的访问时间与复制前相同。
    - `**-B (block)**` 将块大小设置为 5,120 字节，而不是默认的 512 字节。
- `-block-size=n`
    - 将用于输入和输出的块大小设置为 `n` 个 512 字节的块。
- `**-c (compatible)**` 以 ASCII 格式写入页头信息，以便其他系统上的旧版（不兼容的）`cpio` 实用程序读取该文件。此选项很少需要。
- `-make-directories`
    - `**-d**` 在复制文件时根据需要创建目录。例如，当您由 `find` 配合 `-depth` 选项生成的文件列表的归包中提取文件时，需要此选项。此选项只能与 `-extract` 和 `-pass-through` 选项配合使用。
- `-pattern-file=filename`
    - `**-Efilename**` 从 `filename` 读取模式，每行一个 `pattern`。您可以在命令行上指定额外的 `patterns`。
    - `**-nonmatching -f**` 反转从归包中提取文件时执行的测试含义。只有当文件不匹配任何 `patterns` 时，才会从归包中提取文件。
- `-file=archive`、`-F`
    - `archive` 使用 `archive` 作为归包文件的名称。在提取模式下，从 `archive` 读取而不是标准输入。在创建模式下，写入到标准输出。您可以使用此选项访问另一个系统上的设备；更多信息请参阅 `tar` 的 `--file` 选项（第 787 页）。
    - `-help` 显示选项列表。
    - `-link`、`-l` 在可能的情况下，链接文件而不是复制它们。
    - `-dereference`、`-L` 复制符号链接所指向的文件，而不是符号链接本身。
    - `-preserve-modification-time` 保留从归包中提取的文件的修改时间。如果没有此选项，提取文件将显示它们被提取的时间。有了此选项，新创建的文件将显示它们被复制到归包时的时间。
    - `-no-absolute-filenames` 在提取模式下，创建所有相对于工作目录的文件名——即使是使用绝对路径归档的文件也是如此。
    - `-rename`、`-r` 允许 `cpio` 在复制文件时重命名文件。当 `cpio` 提示您文件名时，您输入新名称。文件将以新名称复制。如果您按回车，`cpio` 将不会复制该文件。
    - `-list`、`-t` (目录列表) 显示归包的目录。此选项仅与 `--extract` 选项配合，尽管实际上没有从归包中提取任何文件。配合 `--verbose` 选项，它将以类似于 `ls -l` 的格式显示详细目录。
- `-unconditional`、`-u` 无论修改时间如何都覆盖现有文件。如果没有此选项，`cpio` 将不会用旧文件覆盖较晚修改的文件；它只会显示警告消息。
- `-verbose`、`-v` 在处理文件时列出文件。配合 `--list` 选项，它将以类似于 `ls -l` 的格式显示详细目录。

# 讨论

GNU `cpio` 版本 2.5 显示错误的截断 `inode` 错误消息；您可以安全地忽略这些。如果没有 `--unconditional` 选项，`cpio` 将不会用旧文件覆盖较晚修改的文件。

在创建归包时，可以使用普通文件名和目录名为输入。如果普通输入列表的名称在其父目录之前，归包中的顺序可能会导致可以避免的错误：当从归包中提取文件时，子文件在文件流中无处可去且不会被提取。

让文件在归包中出现在父目录之后并不总是解决方案。问题之一是在提取文件时使用了 `--preserve-modification-time` 选项。因为在目录内创建文件时，父目录的修改时间会变化。有了此选项，创建的文件将显示它们被复制到归包时的时间。

解决方案是让文件在归包中出现在父目录之前。使用 `--depth` 选项，`cpio` 在创建归包时确保所有文件都在父目录之前。在提取文件时使用 `--preserve-modification-time` 选项，因为父目录在创建归包时创建的修改时间会发生变化。

这种策略解决了另一个问题。在创建归包时使用 `--preserve-modification-time` 选项在提取文件时，父目录的修改时间会变化。使用 `--depth` 选项可以确保归包中的文件。`cpio` 在处理文件时列出文件。配合 `--list` 选项，它将以类似于 `ls -l` 的格式显示详细目录。

## 示例

您可以使用此选项来访问另一个系统上的设备；更多信息请参阅 `tar` 的 `--file` 选项（第 787 页）。

```bash
$cpio -idm /home/jenny/*
```

```bash
$pwd
/home/jenny
```

```bash
$cpio -idm /home/jenny/*
```

```bash
$pwd
/home/jenny
```

使用 `-v` 选项，`cpio` 写入。 目录的归包文件。

```bash
$cpio -idm /home/jenny/*
```

```bash
$pwd
/home/jenny
```

```bash
$cpio -idm /home/jenny/*
```

```bash
$pwd
/home/jenny
```
