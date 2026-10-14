
$ cd test

**提示：** 如果你经常和硬核 Linux 爱好者混在一起并想融入他们，可以把切换到另一个目录称为 "cd'ing there"。■

如果你不知道当前正在工作的目录名称，这有点糟糕，但你可以使用 `pwd` 命令（进程工作目录）来提供该信息。`pwd` 命令会列出完整路径。

```bash
$ pwd
```

## 复制、移动、重命名和删除文件及目录

复制、移动和重命名文件是任何用户执行的最常见操作之一，无论使用命令行还是图形界面。要复制文件，你只需执行 `cp` 命令，后跟现有文件名和你想复制的新名。例如，要将名为 `file.txt` 的文件复制到 `new_file.txt`，你需要执行：

```bash
$ cp file.txt new_file.txt
```

通过指定源文件或目标文件的完整路径，`cp` 命令可以在文件系统的任何位置复制文件。例如：

```bash
$ cp /home/wvh/file.txt /tmp/new.file
```

接上之前的例子，如果我想将家目录下的 `file.txt` 复制到 `/tmp`，但保留与原始文件相同的名称，可以通过以下命令实现：

```bash
$ cp /home/wvh/file.txt /tmp/file.txt
```

### 注意

在指定 `cp` 命令的目标文件名称时要非常小心。如果已一个与你要复制的文件同名的文件，`cp` 命令将用你正在复制的文件的内容覆盖现有文件。如果你真的对此非常担心，请参阅本章中关于“定义和使用别名”的章节，了解如何永久设置一个安全的 `cp` 命令版本。■

# 第 11 章：使用命令行工具

例如，为了将名为 `include_test` 的目录内容复制到名为 `backup` 的新目录，我会执行以下命令：

```
$ cp -r include_test backup
```

命令完成后，新的 `backup` 目录将是 `include_test` 目录的副本。如果你来自密苏里州并且需要证明正确的操作正在执行，可以为 `cp` 命令添加 `-v`（详细）选项来列出复制命令的每个部分。该命令及其输出看起来如下：

```
$ cp -rv include_test backup
'include_test' -> 'backup'
'include_test/libxml2' -> 'backup/libxml2'
'include_test/libxml2/xlops' -> 'backup/libxml2/xlops'
'include_test/netdev' -> 'backup/netdev'
'include_test/netdev/devname.h' -> 'backup/devname.h'
'include_test/system' -> 'backup/system'
'include_test/system/libxml2' -> 'backup/system/libxml2'
'include_test/system/libxml2/xlops.h' -> 'backup/system/libxml2/xlops.h'
'include_test/system/netdev' -> 'backup/system/netdev'
'include_test/netdev/devname.h' -> 'backup/system/netdev/devname.h'
```

正如你所希望的那样，递归 `cp` 命令也会复制所有子目录及其包含的任何文件。

我之前提到过，在复制文件时将目录名称作为目标，会创建一个与原目标目录中文件同名的文件。在递归 `cp` 命令中指定目录名称作为目标时，情况也是如此。如果你尝试将一个目录复制到一个具有新名称且已存在的目录中，这在起初可能会令人困惑。在这种情况下，`cp` 会在目标目录下创建一个与你的原始目录同名的子目录。

在命令行中移动和重命名文件同样简单。Linux 系统实际上并没有提供 `rename` 命令 —— 在 Linux 系统上，`mv` 命令将现有文件和目录移动到新位置，并作为操作的一部分可选地对它们进行重命名。例如，要将 `file.txt` 重命名为新文件名 `newfile.txt`，你可以执行以下操作：

```
$ mv file.txt newfile.txt
```

`mv` 命令在指定完整路径以及指定目录作为要移动文件的位置方面，与 `cp` 命令遵循相同的约定。例如，以下命令将文件 `/home/wvh/file.txt` 移动到 `/tmp` 目录并将其重命名为 `newfile.txt`：

```
$ mv /home/wvh/file.txt /tmp/newfile.txt
```

### 第二部分：面向桌面用户的 Ubuntu

如果你想将文件移动到 `/tmp` 目录并保留其原始名称，可以执行以下命令：

```
$ mv /home/vwh/file.txt /tmp
```

与 `cp` 命令不同，`mv` 命令在移动或重命名目录时不需要任何特殊标志。例如，要将目录重命名为 `backup`，你可以执行以下操作：

```
$ mv test backup
```

与 `cp` 命令一样，如果 `backup` 目录已经存在，`mv` 命令会将 `test` 目录移动到 `backup` 目录中并保留其原始名称。`mv` 命令还提供了 `-v`（详细）选项来显示 `mv` 操作期间发生的情况，但在重命名目录时这可能非常令人有趣，正如下面的示例所示：

```
$ mv -v test backup
'test' -> 'backup'
```

在这种情况下，`mv` 操作只需要重命名目录。然而，由于 Linux 文件系统的创建方式，跨文件系统的磁盘分区移动目录需要 `mv` 命令对每个文件和子目录进行复制和删除，如下例：

```
$ mv -v include_test /tmp/backup
'include_test' -> '/tmp/backup'
'include_test/libxml2' -> '/tmp/backup/libxml2'
'include_test/libxml2/xlops.h' -> '/tmp/backup/libxml2/xlops.h'
'include_test/netdev' -> '/tmp/backup/netdev'
'include_test/netdev/devname.h' -> '/tmp/backup/devname.h'
'include_test/system' -> '/tmp/backup/system'
'include_test/system/libxml2' -> '/tmp/backup/system/libxml2'
'include_test/system/libxml2/xlops.h' -> '/tmp/backup/system/libxml2/xlops.h'
'include_test/system/netdev' -> '/tmp/backup/system/netdev'
'include_test/system/netdev/devname.h' -> '/tmp/backup/system/netdev/devname.h'
'include_test/new/new_file' -> '/tmp/backup/new/new_file'
removed 'include_test/libxml2'
removed directory: include_test/libxml2
removed 'include_test/netdev/devname.h'
removed directory: include_test/netdev
removed 'include_test/system/libxml2'
removed directory: include_test/system/libxml2
removed 'include_test/system/libxml2/xlops.h'
removed directory: include_test/system/libxml2
removed 'include_test/system/netdev'
removed directory: include_test/system/netdev
removed 'include_test/system/netdev/devname.h'
removed directory: include_test/system/netdev
removed 'include_test/new/new_file'
removed directory: include_test/new/new_file
```
