
# **表 6-8**

**dd 的常用选项**

| 选项 | 用途 |
| :--- | :--- |
| `if=FILE` | 指定源位置，替代标准输入。这是输入文件。 |
| `of=FILE` | 指定目标位置，替代标准输出。这是输出文件。 |
| `ibs=BYTES` | 指定每次读取的 *BYTES* 数量。 |
| `obs=BYTES` | 指定每次写入的 *BYTES* 数量。 |
| `bs=BYTES` | 指定每次读写 *BYTES* 的数量。 |
| `cbs=BYTES` | 指定每次转换 *BYTES* 的数量。 |
| `skip=BLOCKS` | 指定在复制之前跳过输入文件中的 *BLOCKS* 数量。 |
| `seek=BLOCKS` | 指定在写入之前跳过输出文件中的 *BLOCKS* 数量。 |
| `count=BLOCKS` | 指定从输入文件复制的 *BLOCKS* 数量，而不是复制整个文件。 |

`dd` 命令可用于多种特殊任务。例如，假设您当前使用的系统同时运行 Windows NT 和 Windows 98。第一个分区包含 Windows 98 系统文件，并格式化为 FAT。第二个分区包含 Windows NT 系统文件，并格式化为 NTFS。第三个分区格式化为 FAT，包含两个操作系统共享的数据。该驱动器还包含 3GB 的空间，您希望将其用于 Linux。由于这台计算机被您的年幼子女使用，您更希望使用他们熟悉的 NT 引导加载程序。这可以通过将 Linux 引导扇区连同 LILO 安装到不会覆盖主引导记录的位置来实现；在这种情况下，您将 Linux 引导分区安装到 `/dev/hda5`。在 Linux 中，挂载 Windows 98 系统分区，以便您可以向其写入数据。然后运行以下命令：

```
# /bin/dd if=/dev/hda5 bs=512 count=1 of=/mnt/win_c/bootsek.lin
```

这将在 Windows 98 系统分区上创建一个名为 `bootsek.lin` 的文件。该文件将作为一个大小为 512 字节的块进行写入。然后您需要启动 NT 或 Windows 98，并编辑 `boot.ini` 文件以包含以下行：

```
c:\bootsek.lin="Linux"
```

这将为 Linux 在 NT 引导加载程序中增加一行。当在启动时选中此行时，系统随后将启动到 LILO 引导加载程序。每当在 Linux 系统上运行 `lilo` 命令时，都需要重写 `bootsek.lin` 文件。

在这个例子中，`dd` 命令用于从 Linux 引导分区复制文件到另一个格式化为 FAT 文件系统的分区。当将文件从 ASCII 转换为 EBCDIC（扩展二进制编码十进制交换码，由 IBM 使用，例如在使用磁带备份系统时）时，此命令也很有用。

## 移动文件

手动移动文件是可能的，方法是将其复制到新位置并删除原始文件。但是，Linux 包含一个用于移动文件的命令，该命令可以自动执行这些任务。`mv` 命令（*move* 的缩写）允许您在 Linux 系统上移动和重命名文件。此命令的工作方式与本章前面介绍的 `cp` 命令非常相似，使用相同的命令语法。`mv` 命令使用的选项略有不同，并在表 6-9 中进行了说明。

### 表 6-9

**mv 的常用选项**

| 选项 | 用途 |
| :----- | :--- |
| `-f`   | 无提示地删除现有文件。 |
| `-i`   | 在覆盖文件前提示用户。 |
| `-u`   | 指定不移动具有相同或较新修改时间的文件到目标位置。 |
| `-v`   | 在移动时详细打印文件名。 |

在以下示例中，所有匹配以 `file` 开头的模式的文件名都被详细地移动到 `myfiles` 目录中。

```bash
# mv -v file* myfiles
fileaa -> myfiles/fileaa
fileab -> myfiles/fileab
fileac -> myfiles/fileac
filead -> myfiles/filead
fileae -> myfiles/fileae
filespace -> myfiles/filespace
```

在第二个示例中，目录 `myfiles` 被重命名为 `files`。

```bash
# mv myfiles files
```

## 删除文件

处理文件和目录时经常需要的另一个任务是删除它们。`rm` 命令（*remove* 的缩写）用于在 Linux 系统上删除文件和目录。`rm` 命令使用以下语法：

```
rm *options* *FILE*
```

有几个选项可以与 `rm` 命令一起使用。最常用的选项在表 6-10 中显示。

### 表 6-10

**rm 的常用选项**

| 选项 | 用途 |
| :--- | :--- |
| -d | 由超级用户（superuser）使用。无论目录是否为空都将其删除。 |
| -f | 无提示地处理文件名，即使它们不存在。 |
| -i | 在删除文件时提示用户。 |
| -r | 递归删除目录内容。 |
| -v | 详细删除文件。 |

在以下示例中，`pwd` 中所有以 `nn` 开头的文件都被删除。

```
# rm nn*
```

第二个命令详细地删除位于 `files` 目录中的所有文件，连同该目录本身。

```
# rm -frv files
removing files/fileaa
removing files/fileab
removing files/fileac
removing files/filead
removing files/fileae
removing files/filespace
removing the directory itself: files
```

## 创建目录

至此，我们已经涵盖了文件的创建和删除以及目录的删除。现在我们将查看 `mkdir` 命令（*make directory* 的缩写），它用于创建目录。这是一个非常基本的命令，一次只能创建一个目录层。当与 `-p` 选项一起使用时，还可以根据需要创建父目录。为了创建目录 `/home/angle/ourfiles`、`/home/angle/ourfiles/myfiles`、`/home/angle/ourfiles/yourfiles`，可以使用以下命令。

```bash
# mkdir /home/angle/ourfiles /home/angle/ourfiles/myfiles /home/angle/ourfiles/yourfiles
```

在上述命令中，首先创建目录 `/home/angle/ourfiles`。然后该命令在 `ourfiles` 目录内创建 `myfiles` 和 `yourfiles` 目录。

## 理解文件系统层次结构

![](img/96d9ccd181675a8ae8b6a1146c919d2b_279_0.png)

- **查找系统文件并将文件放置在正确位置。** 理解文件系统层次结构标准，了解标准文件位置，了解各种系统目录的用途，查找命令和文件。涉及使用以下命令：`find`、`locate`、`which`、`updatedb`。涉及编辑以下文件：`/etc/updatedb.conf`

Linux 文件系统遵循树状结构。根目录（`/`）包含主要目录。位于根目录下的每个目录都可以像分支一样包含其他目录。熟悉处理 Linux 时的几个关键目录非常重要。在本节中，我们将检查其中的许多目录。

### 标准文件位置

以下是 Linux 系统上的一些标准文件位置。

- `/etc`—包含系统中使用的许多脚本和配置文件。
- `/etc/skel`—包含要复制到每个用户主目录的文件。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_279_1.png)

第 10 章将更详细地介绍 `/etc/skel` 文件。

- `/usr`—包含许多存储用户和超级用户账户使用的应用程序和源文件的子目录。其中一些包括以下内容：
  - `/usr/bin`—包含用户使用的可执行文件。这应包含在用户的路径语句中。
  - `/usr/sbin`—包含超级用户使用的可执行文件。
  - `/usr/local` — 包含不属于 Linux 操作系统部分的应用程序。
  - `/usr/local/bin` — 包含初始操作系统安装后安装的软件。这也应在用户的路径中。
  - `/usr/local/sbin` — 包含初始操作系统安装后安装的管理软件。
  - `/var/log` — 包含日志文件。
  - `/var/spool` — 包含邮件和打印文件。
  - `/bin` — 包含系统启动期间使用的二进制文件。
  - `/sbin` — 包含超级用户使用的管理二进制文件。

## 系统目录

以下是 Linux 系统中具有特定用途的一些系统目录：

- `/` — 系统根目录。
- `/root` — 超级用户的主目录。
- `/home` — 包含用户的主目录。
- `/boot` — 包含引导加载程序使用的文件，包括内核。
- `/dev` — 包含外围访问文件。
- `/proc` — 包含系统信息的虚拟目录。

# 定位文件

**目标**
2.4 设备，Linux 文件系统，文件系统层次结构标准

- 查找系统文件并将文件放置在正确位置。理解文件系统层次结构标准，了解标准文件位置，了解各种系统目录的用途，查找命令和文件。涉及使用以下命令：`find`、`locate`、`which`、`updatedb`。涉及编辑以下文件：`/etc/updatedb.conf`

在 Linux 系统上，您将需要的另一项功能是定位文件。幸运的是，Linux 提供了几种查找文件的方法。`find`、`locate`、`which` 和 `whereis` 命令在此任务中都很有用。

