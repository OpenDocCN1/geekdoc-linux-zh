
# chmod 文件的访问模式（权限）

`chmod [options] who operator permission file-list` (符号模式)
`chmod [options] mode file-list` (绝对模式)
`chmod [options] --reference=rfile file-list` (引用模式)

该工具更改文件所有者、文件所属组和/或所有其他用户访问文件的方式。只有文件的所有者或超级用户（Superuser）可以更改文件的访问模式或权限。你可以以绝对的、符号或引用的方式指定新的访问模式。

参数指定了要以何种方式更改哪些模式。

## 符号模式

你可以通过用逗号分隔每组来指定多组符号模式（`who operator permission`）。

`chmod` 工具更改由 `who` 指定的用户类的访问权限。该用户类由表 V-4 列中指定的一个或多个字母指定。

| who | 用户类 | 含义 |
| --- | --- | --- |
| `u` | 用户 | 文件所有者 |
| `g` | 组 | 所有者所属的组 |
| `o` | 其他 | 所有其他用户 |
| `a` | 所有 | 可替代 `ugo` 使用 |

表 V-5 列出了符号模式操作符。

| operator | 含义 |
| --- | --- |
| `+` | 为指定的用户类添加权限 |
| `-` | 移除指定用户类的权限 |
| `=` | 设置指定用户类的权限——重置该用户类的所有其他权限 |

访问权限由表 V-6 中列出的一个或多个字母指定。

| 表 V-6 | 符号模式权限 |
| --- | --- |
| `permission` | 含义 |
| `r` | 设置读取权限 |
| `w` | 设置写入权限 |
| `x` | 设置执行权限 |
| `s` | 在执行文件时，将用户 ID（`user ID`）或组 ID（`group ID`）（取决于 `who` 参数）设置为文件所有者的对应 ID（更多信息请参阅第 94 页。） |
| `t` | 设置滞位位（只有超级用户可以设置滞位位，且只能配合 `u` 使用；见第 903 页。） |
| `X` | 如果是目录或其他用户类具有执行权限，则使其可执行 |
| `u` | 设置所有者的权限 |
| `g` | 设置组的权限 |
| `o` | 设置其他人的权限 |

## 绝对模式

你可以使用八进制数来指定访问模式。通过对表 V-7 中的相应值进行或运算来构造该数字。（示例参见表 V-8。）

| 表 V-7 | 绝对模式 |
| --- | --- |
| `mode` | 含义 |
| `4000` | 程序执行时设置用户 ID（第 94 页） |
| `2000` | 程序执行时设置组 ID（第 94 页） |
| `1000` | 滞位位（第 903 页） |
| `0400` | 所有者可以读取文件 |
| `0200` | 所有者可以写入文件 |
| `0100` | 所有者可以执行文件 |
| `0040` | 组可以读取文件 |
| `0020` | 组可以写入文件 |
| `0010` | 组可以执行文件 |
| `0004` | 其他人可以读取文件 |
| `0002` | 其他人可以写入文件 |
| `0001` | 其他人可以执行文件 |

## 表 V-8 列出了一些典型模式

| `mode` | 含义 |
| --- | --- |
| `077` | 所有者、其他人都可以读、写、执行 |
| `0755` | 所有者可以读、写、执行；组和其它可以读取和执行 |
| `0711` | 所有者可以读、写、执行；组和其它只能执行 |
| `0664` | 所有者和组可以读、写；其它可以读取 |
| `0660` | 所有者和组可以读、写；其它没有访问权限 |
| `0644` | 所有者可以读、写；组和其它可以读取 |
| `0600` | 所有者可以读、写；组和其它没有访问权限 |
| `0400` | 所有者可以读取；组和其它没有访问权限 |

# chown

更改文件的所有者和/或文件所属的组

- `chown [options] owner file-list`
- `chown [options] owner:group file-list`
- `chown [options] owner:file-list`
- `chown [options] :group file-list`
- `chown [options] --reference=rfile-list`

`chown` 工具用于更改文件的所有者和/或文件所属的组。只有 `root` 用户可以更改所有者，而属于新组的所有者可以更改文件所属的组。

## Arguments

`owner` 是新所有者的用户名或数字用户 ID（`UID`）。`file-list` 是想要更改所有权和/或组关联的路径列表。`group` 是文件所关联的新组的组名或数字 ID。表 V-9 显示了你可以指定新所有者和/或组的方法。

| Argument | 含义 |
| --- | --- |
| `owner` | `file-list` 的新所有者；不更改组 |
| `owner:group` | `file-list` 的新所有者和新组关联 |
| `owner:` | `file-list` 的新所有者；组关联更改为新所有者的登录组 |
| `:group` | `file-list` 关联的新组；不更改所有者 |

## Options

接受第 587 页描述的常用选项。

- `--dereference -c` 为每个更改了所有权/组的文件显示一条消息。更改符号链接所指向的文件的所有权/组，而不是符号链接本身。默认值是 `--no-dereference`。
- `--quiet` 或 `--silent` 防止 `chown` 在无法更改文件所有权/组时显示错误信息。
- `--no-dereference` 更改符号链接的所有权/组，而不是链接指向的文件（默认值）。
- `--recursive -R` 当你在 `file-list` 中包含目录时，此选项将遍历目录层级，为遇到的所有文件设置指定的所有权/组。将 `file-list` 中文件的所有权和组关联更改为 `rfile` 的所有权和组。
- `--verbose -v` 为每个文件显示消息，说明所有权/组是被保留了还是更改了。

## Notes

`chown` 工具在更改文件所有者时会清除 `setuid` 和 `setgid` 位。

## Examples

以下命令更改 `manuals` 目录下 `chapter1` 文件的所有者，以及 `Alex` 的所有者。新所有者是 `Jenny`：

```bash
# chown jenny manuals/chapter1
```

以下命令将 `/home/alex/literature` 目录及其所有子目录下所有文件的所有者改为 `Alex`，并将 `Alex` 的登录组设置为文件的关联组：

```bash
# chown --recursive alex: /home/alex/literature
```

下一个命令将 `literature` 中文件的所有权更改为 `alex`，并将这些文件的关联组改为 `pubs`：

```bash
# chown alex:pubs /home/alex/literature/*
```

最后一个示例将 `manuals` 中文件的组关联更改为 `pubs`，而不更改其所有权。执行此命令的文件所有者必须属于 `pubs` 组。

```bash
$ chown :pubs manuals/*
```

# cmp

比较两个文件

`cmp [options] file1 [file2 [skip1 [skip2]]]`

`cmp` 工具按字节比较两个文件之间的差异。如果文件相同，`cmp` 将保持静默输出。如果文件不同，`cmp` 会显示第一个不同字节的字节数和行号。

## Arguments

`file1` 和 `file2` 是 `cmp` 比较的文件路径名。如果省略 `file2`，`cmp` 将使用标准输入。在 `file1` 或 `file2` 中使用句字符 (`-`) 会导致 `cmp` 从标准输入读取而非该文件。

`skip1` 和 `skip2` 是十进制数字，表示在开始比较之前在每个文件中跳过的字节数。

## Options

- `--print-bytes -b` 显示更多信息，文件名、字节数和行号，以及第一个不同字节的八进制和 ASCII 值。
- `--ignore-initial=n -i` 在开始比较之前跳过文件中的前 `n` 个字节。
- `--verbose -l`（小写 `"l"`）不再在第一个字节的字节处停止，而是继续比较两个文件并同时显示位置和值。
- `--quiet` 或 `--silent` 当文件相同时抑制输出。它无法更改文件的所有权/组。（注：原文此处描述可能混入了 chown 内容，按原文保留）

## Notes

`cmp` 工具在更改文件所有者时会清除 `setuid` 和 `setgid` 位。（注：原文此处描述可能混入了 chown 内容，按原文保留）

## Examples

以下示例调用 `comm` 时没有带任何选项，因此它会显示三列。第一列列出仅于文件 `c` 的行，第二列列出仅于文件 `d` 的行，第三列列出 `c` 和 `d` 中都存在的行：

```bash
$ comm c d

bbbbb

ccccc

ddddd

eeeee

fffffff

g99999

hhhhh
```

下一个示例展示了使用选项防止 `comm` 显示第 1 和第 2 列。结果是第 3 列，即文件 `c` 和 `d` 共同行的列表：

```bash
$ comm -12 c d

ddddd

eeeee
```

## configure

自动对源码配置

### `.configure` 选项

`configure` 脚本是 GNU 配置和构建系统的一部分。为自己的产品提供源代码的软件开发者面临着一个问题：如何让相对初级的用户能够在各种机器架构、操作系统和系统软件上轻松地构建并安装软件包。为了实现这一目标，许多软件开发者在其源代码中附带了一个名为 `configure` 的 shell 脚本。

当你运行 `configure` 时，它会确定本地系统的功能。`configure` 收集的数据将用于生成 `Makefile`，然后通过 `make`（第 715 页）使用这些 `Makefile` 构建可执行文件和库。你可以通过指定命令行选项和环境变量来调整 `configure` 的行为。

### 选项

- `-disable-feature` 工作方式 `--enable-feature` 相同，但它禁用了对该功能的支持。
- `--enable-feature` 将 `feature` 替换为正在配置的软件可以支持的功能名称。例如，使用命令 `configure --enable-zsh-mem` 对 Z Shell 源码进行配置，会将源码配置为使用 `zsh` 提供的特殊内存分配程序，而不是使用系统内存分配程序。检查软件发行版附带的 `README` 文件以查看 `feature` 的可用选择。
- `--help` 显示 `configure` 的所有可用选项的详细列表。此列表的内容取决于正在配置的软件发行版。
- `--prefix=directory` 默认情况下，`configure` 构建的 `Makefile` 会将软件安装在 `/usr/local` 目录（当你执行 `make install` 命令时）。若要安装到不同的目录，请将 `directory` 替换为想要安装软件的目录路径。
- `--with-package` 将 `package` 替换为可以包含在正在配置的软件中的可选包名称。例如，如果你使用命令 `configure --with-dll` 为 Windows 模拟器 `wine` 源码进行配置，则源码将被配置为构建用于 Windows 模拟的共享库。检查软件发行版附带的 `README` 文件以查看 `package` 的可用选择。此外，`configure --help` 通常也会显示 `package` 的可用选择。

## 讨论

GNU 配置和构建系统允许软件开发者分发软件，这些软件可以自配置以便在各种系统上构建。该系统构建一个名为 `configure` 的 shell 脚本，为在本地系统中构建和安装软件发行版做好准备。`configure` 脚本搜索本地系统以寻找软件发行版的各种依赖项，并构建相应的 `Makefile`。一旦运行了 `configure`，你就可以使用 `make` 命令构建软件，并使用 `make install` 安装软件。

`configure` 脚本确定使用哪种 C 编译器（通常是 `gcc`）并指定一组传递给该编译器的标志。你可以设置环境变量 `CC` 和 `CFLAGS` 以用你自己的选择来覆盖这些值。（参见“示例”部分。）

## 注意事项

每个使用 GNU 自动配置工具的包都提供自己的自定义 `configure` 副本，由软件开发者使用 GNU `autoconf` 工具创建。请阅读你正在安装的包附带的 `README` 和 `INSTALL` 文件，获取有关可用选项的详细信息。

`configure` 脚本是自包含的，可以在各种系统上正确运行。你不需要特殊的系统资源来使用 `configure`。

## 示例

调用 `configure` 的简单方法是 `cd` 到要配置的软件发行版的根目录，然后运行以下命令：

```bash
$ ./configure
```

在命令名前加上 `./` 是为了确保你运行的是随软件提供的 `configure` 脚本。由于 `--recursive` 选项的影响，`configure` 默认会处理链接。

如果你正在使用 `bash`，请使用以下命令：

```bash
$ CFLAGS="-Wall" ./configure
```

如果你正在使用 `csh`，请使用以下命令：

```csh
$ set CFLAGS=-Wall;configure
```

如果你正在使用 `sh`，请使用以下命令：

```sh
$ set CFLAGS="-Wall"; ./configure
```

## cp

复制文件

```bash
cp [options] source-file [destination-file]

cp [options] source-file ... destination-file
```

`cp` 工具复制文件或目录。`cp` 复制文件或目录。带有 `--recursive` 选项，`cp` 可以复制目录。

### 参数

`source-file` 是 `cp` 复制的文件路径。`destination-file` 是 `cp` 放置副本的路径。

`source-file ...` 是 `cp` 复制的多个文件。`destination-directory` 是 `cp` 放置文件的目录。

### 选项

接受第 587 页描述的常用选项。

- `-archive -a` 尽可能保留 `source-file` 的属性。同 `-dP`。
- `--backup` 如果复制覆盖现有文件，此选项将为文件创建备份。备份文件的名称与文件名相同，但带有波浪号 (`~`)。
- `-d` 复制符号链接而不是其指向的文件。在存在对应文件时，对 `cp` 会保留硬链接。
- `--interactive -i` 当 `cp` 将覆盖文件时提示你。如果你回答 `y` 或 `Y`，`cp` 将继续。如果你输入其他任何内容，`cp` 将不复制文件。
- `--force` 当 `destination-file` 存在且无法打开时，此选项会导致 `cp` 在复制前删除它。
- `--dereference -L` 复制链接指向的文件。参见 `--no-dereference`。
- `--preserve -p` 创建与 `source-file` 相同的所有者、组、权限、访问日期和修改日的 `destination-file`。
- `--no-dereference -P` 复制符号链接而不是其指向的文件。如果不使用 `-R`、`-r` 或 `--recursive`，默认行为是引用（复制指向的文件）。使用这些选项之一，`cp` 不会引用（它复制链接）。
- `--parents` 将相对路径复制到目录，根据需要创建目录。（参见“示例”。）
- `--preserve=links` 在递归复制目录时，对对应文件保留硬链接。
- `--recursive -R` 或 `-r` 递归复制普通文件和目录层次。隐含了 `--no-dereference` 选项。
- `--update -u` 仅当 `destination-file` 不存在或比 `source-file` 更旧时复制。
- `--verbose -v` 在 `cp` 复制每个文件时显示其名称。

### 注意事项

如果在执行 `cp` 之前 `destination-file` 已存在，`cp` 将覆盖该文件，破坏内容但保留访问权限、所有者和组。

如果 `destination-file` 不存在，`cp` 使用 `source-file` 的访问权限。复制文件的用户成为 `destination-file` 的所有者，用户的组成为与 `destination-file` 相关的组。

使用 `-p` 选项，`cp` 尝试设置所有者、组、权限、访问日期和修改日期与 `source-file` 匹配。此选项等同于 `--preserve`。

与第 702 页不同，`cp` 创建的 `destination-file` 与 `source-file` 是独立的。

### 示例

第一个命令在工作目录下创建文件 `letter` 的副本。副本名为 `letter.sav`。

```bash
$ cp letter letter.sav
```

下一个命令将所有以 `.c` 结尾的文件复制到 `archives` 目录（它是工作目录的子目录）。每个复制的文件保留其文件名，但具有新的绝对路径。由于 `--preserve` 选项，归档中复制的文件的所有者、组、权限、访问日期和修改日期将与源文件相同。

```bash
$ cp --preserve *c archives
```

下一个示例将 `memo` 从 `/home/jenny` 复制到工作目录：

```bash
$ cp /home/jenny/memo
```
