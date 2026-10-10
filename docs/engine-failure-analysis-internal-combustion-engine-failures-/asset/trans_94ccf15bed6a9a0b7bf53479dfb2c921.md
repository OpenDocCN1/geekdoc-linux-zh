
## 选项

| 使用此选项 | 用于执行此操作 |
| --- | --- |
| –b, –backup | 在删除源文件之前，为其制作一个备份副本。 |
| –f, –force | 删除已存在的目标文件，且不提示确认。 |
| –help | 显示可用的选项。 |
| –i, –interactive | 在覆盖已存在的目标文件之前进行提示。 |
| –S extension, –suffix=extension | 使用指定的扩展名代替默认附加到文件名的备份后缀 ~。 |
| –u, –update | 仅当源文件（而非目录）比目标文件更新时，才创建副本。 |
| –v, –verbose | 显示解释该命令正在执行的操作的消息。 |
| –version | 显示版本号。 |
| –V type, –version-control=type | 指定要使用的备份后缀类型。可用的类型有： |
| - **t, numbered** | 编号备份。 |
| - **nil, existing** | 如果存在编号备份，则使用编号。 |
| - **never, simple** | 始终使用 ~。 |
| - **none, off** | 从不制作备份。 |
| –x, –one-file-system | 仅在当前文件系统上执行操作。 |

## 示例

| 此命令 | 执行以下操作 |
| --- | --- |
| `mv –ivb essay1.doc` essay1.bak | 将源文件 (**essay1.doc**) 重命名为 essay1.bak。 |
| `mv –ivb essay1.doc /home/suzanne/backup/` | 将源文件 (**essay1.doc**) 移动到 /home/suzanne/backup。 |
| `mv -ivb essay1.doc /home/suzanne/backup/essay1.bak` | 将源文件 (**essay1.doc**) 移动到 `/home/suzanne/backup` 并将其重命名为 **essay1.bak**。 |
| `mv -ivb *.doc /home/suzanne/backup` | 将当前目录下所有 **.doc** 扩展名的文件移动到 `/home/suzanne/backup` 目录。 |
| `mv -iub *.doc /home/suzanne/backup` | 将当前目录下所有 **.doc** 扩展名的文件移动到 `/home/suzanne/backup` 目录，但仅当源文件比目标文件更新或目标文件不存在时才执行。 |

# rm

```
rm [ option ] [ file ]
```

删除指定的文件。当您复制多个文件时，可以使用 shell 模式来指定文件（参见第 4 章“Shell 模式”部分）。当与 `-R` 选项一起使用时，递归删除目录内容（删除当前目录及其所有相关子目录中的文件）。

## 选项

| 使用此选项 | 用于执行此操作 |
| --- | --- |
| `-d, --directory` | 即使目录非空也解除链接。需要超级用户权限。 |
| `-f, --force` | 忽略不存在的文件，并且不进行提示。 |
| `--help` | 显示可用的选项。 |
| `-i, --interactive` | 在覆盖已存在的目标文件之前进行提示。 |
| `-r, -R, --recursive` | 删除当前目录及其所有相关子目录的内容。 |
| `--v`, `--verbose` | 显示解释该命令正在执行的操作的消息。 |
| `--version` | 显示版本号。 |

## 示例

| 此命令 | 执行以下操作 |
| --- | --- |
| `rm -iv essay1.doc` | 删除 **essay1.doc**。 |
| `rm -iv *.doc` | 删除当前目录中所有 `.doc` 扩展名的文件。 |
| `rm -iv *` | 删除当前目录中的所有文件。 |
| `rm -R /home/suzanne/junk` | 删除指定目录及其所有相关子目录，包括这些目录中包含的任何文件。 |

# rmdir

`rmdir [ option ] directory`

删除指定的目录，但仅限于该目录为空的情况。若要删除包含文件的目录，请参阅 *rm*。

## 选项

| 使用此选项 | 用于执行此操作 |
| --- | --- |
| `--ignore-fail-on-non-empty` | 即使一个或多个指定的目录包含文件，也继续处理 |
| `-p`, `--parents` | 如果当前的命令使关联的父目录变空，则删除这些父目录 |
| `--verbose` | 显示有关每个被处理的目录的消息 |
| `--help` | 显示可用的选项 |

## 示例

| 此命令 | 执行以下操作 |
| --- | --- |
| `rmdir /home/suzanne/junk` | 如果指定的目录为空，则将其删除。 |

# safedlete

**safedlete [ option ] file**

将指定的文件删除到 safedlete 目录，并在永久删除之前保留指定时间段。您可以使用 shell 模式来指定文件名（参见第 4 章“Shell 模式”部分）。您可以使用 alias（参见第 3 章），以便使用 safedlete 而不是 rm。若要恢复已删除的文件，请使用 undelete。如果您的 Linux 发行版中没有包含此实用程序，您可以从 `http://metalab.unc.edu/pub/Linux/utils/shell/` 获取源代码。

另请参阅 undelete。

## 选项

| 使用此选项 | 用于执行此操作 |
| --- | --- |
| `-i, -interactive` | 在删除文件之前提示用户 |
| `-v, -verbose` | 在删除每个文件之前打印其名称 |
| `-f, -force` | 忽略不存在的文件，并且不提示用户 |
| `-r, -R, -recursive` | 删除当前目录及其所有相关子目录中的所有文件 |
| `--help` | 显示命令选项 |
| `--version` | 显示命令版本 |

## 示例

| 此命令 | 执行以下操作 |
| --- | --- |
| `safedlete my-doctoral-thesis.doc` | 删除指定的文件 (`my-doctoral-thesis.doc`)。 |
| **safedelete -R \*** | 删除当前目录及其所有相关子目录中的所有文件。 |

# stat

```
stat *file*
```

显示关于指定文件的所有可用信息，包括大小、已分配的 512K 块数、文件类型、权限（数值模式和符号模式）、所有者、特殊权限（设置用户 ID 和设置组 ID）、inode 号、链接数、最后访问时间、最后修改时间以及最后状态改变时间。

# symlinks

```
symlinks [ options ] *directory*
```

显示指定目录中或工作目录中（如果未指定目录）的符号链接信息。此实用程序可以确定以下链接特性：

- **相对链接**: 这种类型的符号链接通过相对路径名表示，例如 `../books/backup`。
- **悬空链接**: 这种类型的链接不再有目标。
- **绝对链接**: 这种类型的符号链接通过绝对路径名表示，例如 `/home/suzanne/books/backup`。
- **混乱链接**: 链接信息中包含不必要的斜杠或点。
- **冗长链接**: 包含通向目标的不必要迂回路径。
- **Other_fs**: 这些链接现在位于目标最初所在文件系统之外的文件系统中。

## 选项

| 使用此选项 | 用于执行此操作 |
| --- | --- |
| -c | 将绝对路径名转换为相对路径名 |
| -d | 删除悬空链接 |
| -r | 检查工作目录及其所有相关子目录内的符号链接 |
| -s | 缩短冗长的链接 |
| -v | 显示所有符号链接，包括默认不显示的相对链接 |

# touch

```
touch [ option ] filename
```

如果未使用选项，则更改指定文件名的最后访问时间或修改时间为当前时间。您可以使用选项指定其他时间。您可以使用 shell 模式指定两个或更多文件（参见第 4 章“Shell 模式”部分）。如果指定的文件名不存在，此命令将创建该文件。当您使用 `-t` 选项更改日期和时间时，请使用格式 *mmdhhhhmm*[yy]。例如，*0521073002* 对应于 2002 年 5 月 21 日 7:30 AM。当您使用 `-d` 选项更改日期和时间时，可以使用本章前面“日期和时间表达式”部分中列出的任何有效日期和时间格式。

## 选项

| 使用此选项 | 用于执行此操作 |
| --- | --- |
| -a, --time=atime, | 更改访问时间，但不更改其他时间。 |
| -m, --time=mtime, |  |
| --time=use |  |
| -c, -no-create | 不创建任何文件。 |

