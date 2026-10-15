
你可以通过 `cpio` 实用工具基于数据的元数据（而非文件位置）进行备份。例如，假设你想为虚拟目录系统中由 `JKirk` 用户账户拥有的所有文件创建 `cpio` 归档。你可以使用 `find / -user JKirk` 命令并将其通过管道传入 `cpio` 实用工具来创建归档文件。这是一个便捷的功能。

你可以相当容易地查看存储在 `cpio` 归档中的文件。只需再次使用 `cpio` 命令，并使用其 `-itv` 选项和 `-I` 选项来指定归档文件，如列表 12.3 所示。

### 列表 12.3 使用 cpio 列出归档的内容

```bash
$ cpio -itvI Project4x.cpio
-rw-r--r--   1 Christin Christin   29900  Aug 19 17:37  Project42.txt
-rw-rw-r--   1 Christin Christin      0  Aug 19 18:07  Project43.txt
-rw-rw-p--   1 Christin Christin      0  Aug 19 18:07  Project44.txt
-rw-rw-p--   1 Christin Christin      0  Aug 19 18:07  Project45.txt
-rw-rw-p--   1 Christin Christin      0  Aug 19 18:07  Project46.txt
59 blocks
$
```

虽然代码清单 12.3 中未显示，但 `cpio` 实用工具会保留每个文件的绝对目录引用。因此，它常被用于创建系统镜像和完整备份。

要从归档中恢复文件，只需使用 `-i` 选项。但是，由于 `cpio` 会保留文件的绝对路径，如果你需要将文件恢复到另一个目录位置，这可能会比较棘手。为此，你需要使用 `--no-absolute-filenames` 选项，如代码清单 12.4 所示。

## 代码清单 12.4 使用 cpio 将文件恢复到不同的目录位置

```bash
$ ls -df Projects
  Projects/
$
$ mv Project4x.cpio Projects/
$
$ cd Projects
$ pwd
/home/Christine/Answers/Projects
$
$ ls Project4?.
  Project4x.cpio
$
$ cpio -iv --no-absolute-filenames -I Project4x.cpio
  Project42.txt
  Project43.txt
  Project44.txt
  Project45.txt
  Project46.txt
  59 blocks
$
$ ls Project4?.
  Project42.txt Project44.txt Project46.txt
  Project43.txt Project45.txt Project4x.cpio
$
```

在代码清单 12.4 中，`Project4x.cpio` 归档文件被移入一个已存在的子目录 `Projects`。通过 `--no-absolute-filenames` 选项剥离归档文件中的绝对路径名称，你可以将文件恢复到新的目录位置。如果你想将文件恢复到原始位置，只需省略该选项，并使用代码清单 12.4 中所示的其他 `cpio` 开关即可。

# 使用 tar 进行归档

`tar` 实用工具的名称代表“磁带归档器”（tape archiver），常用于创建数据备份。与 `cp` 类似，使用 `tar` 命令时，选定的文件会被复制并存储在一个单一文件中。这个文件被称为 `tar` 归档文件。如果该归档文件使用数据压缩工具进行压缩，则生成的压缩归档文件被称为 `tarball`。

`tar` 程序有几个有用的选项。表 12.2 描述了常用于创建数据备份的选项。

**表 12.2** `tar` 命令中常用于创建 tarball 的选项

| 短选项 | 长选项 | 描述 |
| :--- | :--- | :--- |
| `-c` | `--create` | 创建一个 `tar` 归档文件。备份可以是完整备份或增量备份，具体取决于所选的其他选项。 |
| `-u` | `--update` | 将文件追加到现有的 `tar` 归档文件中，但仅复制自原始归档文件创建以来被修改的那些文件。 |
| `-g` | `--listed-incremental` | 基于提供的文件中存储的元数据创建增量或完整归档。 |
| `-z` | `--gzip` | 使用 `gzip` 将 `tar` 归档文件压缩为 `tarball`。 |
| `-j` | `--bzip2` | 使用 `bzip2` 将 `tar` 归档文件压缩为 `tarball`。 |
| `-J` | `--xz` | 使用 `xz` 将 `tar` 归档文件压缩为 `tarball`。 |
| `-v` | `--verbose` | 在处理每个文件时显示该文件的名称。 |

要使用 `tar` 实用工具创建归档，你需要在选项和命令中添加一些参数。代码清单 12.5 展示了创建 `tar` 归档的示例。

## 代码清单 12.5 使用 tar 创建归档文件

```bash
$ ls Project4?.
Project42.txt Project43.txt Project44.txt
Project45.txt Project46.txt
$
$ tar -cvf Project4x.tar Project42.txt
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
$
```

在代码清单 12.5 中，使用了三个选项。`-c` 选项创建 `tar` 归档。`-v` 选项显示文件在放入归档文件时的文件名。最后，`-f` 选项指定归档文件名，即 `Project4x.tar`。虽然并非强制要求，但在 `tar` 归档文件上使用 `.tar` 扩展名被视为良好的规范。命令的最后一个参数指定要复制到此归档中的文件。

> 你也可以使用旧式的 `tar` 命令选项。对于这种风格，你需要去掉 `tar` 选项开头的单个短横线。例如，`-c` 变为 `c`。请记住，旧式的 `tar` 命令附加选项之间不能有空间。因此，`tar cvf` 是有效的，但 `tar c v f` 是无效的。

如果你正在备份大量文件或大数据量，使用压缩工具是个好主意。通过在你的 `tar` 命令选项中添加一个额外的开关即可轻松实现。代码清单 12.6 展示了一个使用 `gzip` 压缩创建 `tarball` 的示例。

## 代码清单 12.6 使用 tar 创建 tarball

```bash
$ tar -zcvf Project4x.tar.gz Project4?.
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
$
$ ls Project4x.tar.gz
Project4x.tar.gz
$
```

请注意代码清单 12.6 中 `tarball` 的文件名具有 `.tar.gz` 文件扩展名。使用 `.tar` 扩展名并添加一个指示所用压缩方法的标识符被视为良好的规范。但是，如果需要，你可以将其简化为 `.tgz`。

这个命令有一个有用的变体，可以同时创建完整备份和增量备份。一个简单的示例有助于解释这个概念。创建完整备份的过程如代码清单 12.7 所示。

## 代码清单 12.7 使用 tar 创建完整备份

```bash
$ tar -g FullArchive.snar -Jcvf Project42.txz Project42.txt Project43.txt Project44.txt Project45.txt Project46.txt
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
$
$ ls FullArchive.snar Project42.txz
FullArchive.snar Project42.txz
$
```

请注意代码清单 12.7 中的 `-g` 选项。`-g` 选项创建一个称为快照文件的文件，即 `FullArchive.snar`。`.snar` 文件扩展名表示该文件是 `tarball` 快照文件。快照文件包含与 `tar` 命令配合使用以创建完整和增量备份的元数据。快照文件包含文件时间戳，因此 `tar` 实用工具可以确定自上次备份以来文件是否已被修改。快照文件还用于识别新文件或确定自上次备份以来是否有文件被删除。

前面的示例创建了指定文件的完整备份以及元数据快照文件 `FullArchive.snar`。现在，相同的快照文件将被用于帮助确定是否有任何文件已被修改、是新的或已被删除，以创建增量备份，如代码清单 12.8 所示。

## 代码清单 12.8 使用 tar 创建增量备份

```bash
$ echo "Answer to everything" >> Project42.txt
$
$ tar -g FullArchive.snar -Jcvf Project42_Inc.txz Project4?.txt
Project42.txt
$
$ ls Project42_Inc.txz
Project42_Inc.txz
$
```

在代码清单 12.8 中，文件 `Project42.txt` 已被修改。同样，`tar` 命令使用 `-g` 选项并指向之前创建的 `FullArchive.snar` 快照文件。这次，`FullArchive.snar` 中的元数据显示 `tar` 命令知道 `Project42.txt` 文件自上次备份以来已被修改。因此，新的 `tarball` 仅包含 `Project42.txt` 文件，这实际上是一个增量备份。你可以根据需要继续使用该快照文件创建额外的增量备份。

> `tar` 命令以“级别”来查看完整备份和增量备份。完整备份是包含所有指定文件的备份，被视为 0 级备份。完整备份后的第一个 `tar` 增量备份被视为 1 级备份。第二个 `tar` 增量备份被视为 2 级备份，以此类推。

每次创建数据备份时，验证它们是一个良好的实践。表 12.3 提供了一些用于查看和验证数据备份的 `tar` 命令选项。

**表 12.3** `tar` 命令中常用的归档验证选项

| 短选项 | 长选项 | 描述 |
| :--- | :--- | :--- |
| `-d` | `--compare` / `--diff` | 将 `tar` 归档文件的成员与外部文件进行比较，并列出差异。 |
| `-t` | `--list` | 显示 `tar` 归档文件的内容。 |
| `-W` | `--verify` | 在处理每个文件时对其进行验证。此选项不能与压缩选项一起使用。 |

备份验证可以采取多种形式。你可以使用 `tar` 命令的 `-v` 选项来确保期望的文件（有时称为成员）包含在你的备份中，以便在文件被包含在归档文件中时观察文件列表。你也可以在备份完成后验证期望的文件是否包含在备份中。使用 `-t` 选项列出 `tarball` 或归档文件的内容。示例如代码清单 12.9 所示。

## 代码清单 12.9 使用 tar 列出 tarball 的内容

```bash
$ tar -tf Project4x.tar.gz
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
$
```

你可以通过将归档文件中的文件与当前文件进行比较来验证归档文件中的文件。完成此任务的选项是 `-d` 选项。示例如代码清单 12.10 所示。

## 代码清单 12.10 使用 tar 比较 tarball 成员与外部文件

```bash
$ tar -df Project4x.tar.gz
Project42.txt: Mod time differs
Project42.txt: Size differs
$
```

另一个良好的实践是在 `tar` 归档创建后立即自动验证备份。这很容易通过附加 `-W` 选项来实现，如清单 12.11 所示。

### 清单 12.11 使用 tar 自动验证备份的文件

```console
$ tar -Wcvf ProjectVerify.tar Project4?.txt
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
Verify Project42.txt
Verify Project43.txt
Verify Project44.txt
Verify Project45.txt
Verify Project46.txt
$
```

如果您使用压缩来创建 `tar` 包，则不能使用 `-W` 选项。但是，您可以先创建并验证归档文件，然后在单独的步骤中对其进行压缩。您还可以在从 `tar` 归档文件中提取文件时使用 `-W` 选项。这对于立即验证从归档恢复的文件非常方便。

表 12.4 列出了一些您可以使用 `tar` 实用程序从 `tar` 归档文件或 `tar` 包中恢复数据的选项。请注意，用于创建备份的某些选项，例如 `-g` 和 `-W`，也可以在恢复数据时使用。

### 表 12.4 tar 命令常用的文件恢复选项

| 短选项 | 长选项 | 描述 |
| :--- | :--- | :--- |
| `-x` | `--extract` | 从 `tar` 包或归档文件中提取文件，并将其放置在当前工作目录中 |
| | `--get` | |
| `-z` | `--gunzip` | 使用 `gunzip` 解压缩 `tar` 包中的文件 |
| `-j` | `--bunzip2` | 使用 `bunzip2` 解压缩 `tar` 包中的文件 |
| `-J` | `--unxz` | 使用 `unxz` 解压缩 `tar` 包中的文件 |

使用 `tar` 实用程序从归档文件或 `tar` 包中提取文件相当简单。清单 12.12 展示了一个从先前创建的 `tar` 包中提取文件的示例。

### 清单 12.12 使用 tar 从 tar 包中提取文件

```
$ mkdir Extract
$
$ mv Project4x.tar.gz Extract/
$
$ cd Extract
$
$ tar -zxvf Project4x.tar.gz
Project42.txt
Project43.txt
Project44.txt
Project45.txt
Project46.txt
$
$ ls
Project42.txt Project44.txt Project46.txt
Project43.txt Project45.txt Project4x.tar.gz
$
```

在清单 12.12 中，创建了一个新的子目录 `Extract`。将清单 12.6 中创建的 `tar` 包移动到新子目录中，然后从 `tar` 包中恢复文件。如果您将此清单中使用的 `tar` 命令与清单 12.6 中使用的命令进行比较，您会注意到这里用 `-o` 选项取代了清单 12.6 中使用的 `-c` 选项。另外，请注意在清单 12.12 中，文件提取后并未移除 `tar` 包，因此您可以根据需要反复使用它。

![](img/c0a399aca0d18f8822d714ad0a173123_442_0.png)

> `tar` 命令还有许多其他功能，例如使用 `tar` 备份参数和/或创建备份和恢复 shell 脚本的能力。请访问 GNU tar 网站 `www.gnu.org/software/tar/manual`，以了解更多关于这个流行的命令行备份工具的信息。

由于 `tar` 实用程序是磁带归档器，如果您愿意，还可以将 `tar` 包或归档文件放置在磁带上。在挂载并正确定位磁带后，只需在 `tar` 命令中用 SCSI 磁带设备文件名（如 `/dev/st0` 或 `/dev/nst0`）替换归档或 `tar` 包文件名即可。

## 使用 dd 进行复制

`dd` 实用程序允许您备份磁盘上的几乎所有内容，包括一些较旧的 Linux 发行版仍在使用旧的主引导记录（MBR）分区。它主要用于创建整个硬盘或分区的低级副本。它常用于数字取证中创建系统镜像、复制损坏的磁盘以及擦除分区。

该命令本身相当简单。`dd` 实用程序的基本语法结构如下：

```
dd  if=input-device of=output-device [OPERANDS]
```

`output-device` 是整个驱动器或分区。`input-device` 也是如此。请确保为 `out` 选择正确的设备，为 `in` 选择正确的设备；否则，您可能会无意中擦除数据。

除了 `of` 和 `if` 之外，还有几个其他参数（称为操作数）可以帮助进行 `dd` 操作。常用选项在表 12.5 中进行了描述。

### 表 12.5 dd 命令常用的操作数

| 操作数 | 描述 |
| :--- | :--- |
| `bs=BYTES` | 设置一次读取和写入的最大块大小（`BYTES` 的数量）。默认值为 512 字节。 |
| `count=N` | 设置要复制的输入块数量（`N`）。 |
| `status=LEVEL` | 设置显示到 `STDERR` 的信息量（`LEVEL`）。 |

`status=LEVEL` 操作数需要稍作解释。`LEVEL` 可以设置为以下值之一：

- `none` 仅显示错误消息。
- `noxfer` 不显示最终传输统计信息。
- `progress` 显示定期传输统计信息。

通常通过示例来理解 `dd` 实用程序更容易。清单 12.13 展示了一个将一个完整磁盘逐位复制到另一个磁盘的简化示例。

### 清单 12.13 使用 dd 复制整个磁盘
