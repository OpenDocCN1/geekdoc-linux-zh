
在介绍命令行工具、选项和参数的章节中，使用了标准的 Linux `ls` 命令作为示例。列出文件和目录是你从 shell 中想要执行的最常见操作之一（或者至少，你会发现自己一直在这样做）。然而，如上一节所述，你的 Ubuntu 系统提供了数百个命令。我无法在这里介绍所有的命令，因为那意味着 Wiley 需要给这本书书装上轮子，但确实有一些你想要从 shell 中执行的常用任务。本节重点介绍了你可能想要从命令行执行的一些最常见任务，并最后讨论了如果你不知道相应命令行工具的晦涩名称，该如何确定应该使用哪些命令。

# 在 Linux 文件系统中移动

就像使用图形界面时一样，如果你从命令行进行工作，你也会希望以某种逻辑方式组织文件和目录。一旦组织好这些内容，你就需要使用 `cd`（切换目录）命令，它的作用正如你所预期。在 Linux 中，`cd` 命令将你的当前工作目录更改为你作为参数提供的的目录。例如，要进入名为 `test` 的目录，你只需执行以下命令：

```
$ cd test
```

如果你在硬核 Linux 分支中穿梭并想要融入其中，请参考如何使用 `cd` 切换到另一个目录。

如果你不知道当前工作目录的名称，这有点可怕，但你可以使用 `pwd`（进程工作目录）来获取该信息。`pwd` 命令列出当前（在本例中为你的 shell）运行的完整路径，如下所示：

```
$pwd
/vwh/test
```

你可以通过指定完整路径作为 `cd` 命令的参数切换到 Linux 系统上的任何目录，如下所示：

```
$ cd /usr/local
$ pwd
/usr/local
```

正如你看到的，我的 shell 运行在 `/usr/local`，我执行的其他命令都将在该目录下执行。为了方便起见，`cd` 命令会自动切换到你的主目录，这很可能是你大多数文件和目录最初所在地。

# 使用命令行工具

无论你是克隆一个现有文件作为起点，还是重新组织你的文件和目录以便于查找，在命令行中执行复制和移动文件及目录与在图形用户界面（GUI）中一样简单，区别在于你必须输入而不是指向并点击。在许多情况下，Linux 命令行工具提供的数以万计的选项比通用命令能带给你多得多的控制力。

延续 Linux/Unix “为什么要比需要的输入多余的字母？”的传统，Linux 命令 `cp` 用于复制文件和目录，是从我的家目录开始介绍的。要复制一个文件，你只需执行 `cp` 命令，后面跟着现有文件的文件名和你想要的新文件名。例如，要将名为 `file.txt` 的文件复制到新的 `new_file.txt`，你将执行以下命令：

```
$ cp file.txt new_file.txt
```

在指定 `cp` 命令的目标文件名称时要小心。如果已经存在一个与要复制的文件同名的文件，`cp` 命令将用你正在复制的文件的内容覆盖现有文件。如果你对这一点感到担心，请参阅本章后面关于“定义与别名”的章节，了解如何正确设置安全版本的 `cp` 命令。

通过指定源文件或目标文件的完整路径，`cp` 命令可以复制文件系统中任何你拥有权限创建文件的任何位置的文件。例如，要将家目录下的 `file.txt` 复制到 `/tmp` 目录（每个人都可以创建文件的地方）下的目标 `new_file.txt`，无论我当前正在哪个文件或目录中工作，都可以执行该命令：

```
$ cp /home/whf/file.txt /tmp/file.txt
```

你也可以通过指定 `cp` 操作的目标名称，使用 `cp` 命令复制到不同的目录。继续使用上一个的例子，如果我想将家目录下的 `file.txt` 复制到 `/tmp`，但让复制的文件保留与原文件相同的名称，可以使用以下命令：

```
$ cp /home/whf/file.txt /tmp
```

此命令在复制文件时不需要任何特殊选项。然而，你可以通过指定 `-r`（递归）选项来使用 `cp` 命令复制目录。例如，要将名为 `include_test` 的目录的内容复制到名为 `backup` 的新目录，我将执行以下命令：

```
$ cp -r include_test backup
```

执行命令后，新的 `backup` 目录将是 `include_test` 目录的精确副本。如果你来自密苏里并需要确保正确的事情发生，你可以为 `cp` 命令添加 `-v`（详细）选项，以列出复制命令的每个部分。此命令及其输出将如下所示：

```
$ cp -rv include_test backup
'Include_test' -> 'backup'
'Include_test/libxml2' -> 'backup/libxml2'
'Include_test/libxml2/xmlops.h' -> 'backup/libxml2/xmlops.h'
'Include_test/devdev' -> 'backup/devdev'
'Include_test/devdev/devname.h' -> 'backup/devdev/devname.h'
'include_test/system' -> 'backup/system'
'include_test/system/libxml12' -> 'backup/system/libxml12'
'include_test/system/libxml12/xmlops.h' -> \
  'backup/system/xmlops.h'
'include_test/system/netdev' -> 'backup/system/netdev'
'include_test/system/netdev/devname.h' -> \
  'backup/system/netdev/devname.h'
```

正如你所希望的，递归 `cp` 命令还会递归地复制所有子目录以及任何文件（当复制一个文件时包含的文件，它会在目标位置创建一个与原文件同名的文件）。

我之前提到过指定目录名称作为原始目标。当为递归 `cp` 命令指定目录名称时也是如此。如果你尝试将一个目录复制为一个新名称，且已经存在一个同名的目录，这最初可能会令人困惑。在这种情况下，`cp` 命令会将与你的原始目录同名的目录作为目标的子目录。

从命令行移动和删除文件非常简单。Linux 系统实际上并没有提供单独的命令——在 Linux 系统上，`mv` 命令将文件和目录都移动到新位置，并可选地作为移动操作的一部分重命名它们。例如，要将 `file.txt` 重命名为新的 `myfile.txt`，你将执行以下操作：

```
$ mv file.txt newfile.txt
```

`mv` 命令在指定完整路径以及指定要移动文件的目标位置的目录名称方面，与 `cp` 命令遵循相同的约定。例如，以下命令将文件 `/home/vwh/file.txt` 移动到 `/tmp` 目录并将其重命名为 `file.txt`：

```
$ mv /home/vwh/file.txt /tmp/newfile.txt
```

如果你想将文件移动到 `/tmp` 目录并保留其原始名称，可以执行以下操作：

```
$ mv /home/vwh/file.txt /tmp
```

与 `cp` 命令不同，`mv` 命令在移动或重命名目录时不需要任何特殊标志。要将 `test` 目录重命名为 `backup`，你需要执行以下操作：

```
$ mv test backup
```

与 `cp` 命令一样，如果 `backup` 目录已经存在，`mv` 命令会将 `test` 目录移动到 `backup` 目录中并保留其原始名称。`mv` 命令提供了 `-v`（详细）选项来显示 `mv` 操作期间发生了什么，这在重命名目录时是相当有趣的，你可以从以下示例中看到：

```
$ mv -v test backup
'test' -> 'backup'
```

在这种情况下，`mv` 操作只需要重命名目录。然而，由于 Linux 文件系统的创建方式，跨越位于不同硬盘分区的的文件系统移动目录需要每个文件和目录首先由 `mv` 命令创建并被删除，如下例所示：

```
$ mv v include_test /tmp/backup
'include_test' -> '/tmp/backup'
'include_test/libxml2' -> '/tmp/backup/libxml2'
'include_test/libxml2/xmlops.h' -> '/tmp/backup/libxml2/xmlops.h'
'include_test/netdev' -> '/tmp/backup/netdev'
```

正如你所看到的，这很多内容与 `cp` 命令非常相似。在这个示例中，我首先使用 `cp` 命令演示我的当前目录（`.`）和目标目录（`/tmp`）位于不同的文件系统。你可以从 `mv` 命令的详细输出中看到差异。
