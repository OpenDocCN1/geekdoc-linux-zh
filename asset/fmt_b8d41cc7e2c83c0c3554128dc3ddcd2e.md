
# 使用 MS-DOS 媒体

## mdel — 删除 MS-DOS 文件

`mdel [-v] dos_files`

| 选项或参数 | 功能 |
| --- | --- |
| `-v` | 详细模式 |
| `dos_files` | 要删除的文件名。 |

## mdir — 显示 MS-DOS 目录

`mdir` 等同于 MS-DOS 的 `dir` 命令。`-w` 选项等同于 `dir` 命令的 `/w` 切换位开关。

```
mdir [-w] dos_dir
mdir [-a] [-f] [-w] dos_files
```

| 选项或参数 | 功能 |
| --- | --- |
| `-a` | 在列表中包含隐藏文件。 |
| `-f` | 快速输出 — 不包含空间计数。 |
| `-w` | 宽屏输出 — 列出文件名，不包含大小或日期信息。 |
| `dos_dir` | 要列出内容的目录名称。 |
| `dos_file` | MS-DOS 文件名（可能使用通配符表示）。 |

## mininfo — 打印 MS-DOS 文件系统参数

`mininfo` 显示 MS-DOS 文件系统引导扇区的字段内容。

```
mininfo [-v] drive
```

| 选项或参数 | 功能 |
| --- | --- |
| `-v` | 包含引导扇区的十六进制转储。 |
| `drive` | 要访问的设备标识符（`a:`、`b:` 等）。 |

## mmd — 创建新目录

`mmd` 命令在 MS-DOS 磁盘上创建一个或多个目录。

```
mmd dos_dirs
```

| 参数 | 功能 |
| --- | --- |
| `dos_dirs` | 要创建的目录名称或跟随冒号的驱动器和目录名称。 |

## mtype — 显示文件内容

`mtype` 命令在屏幕上显示文件内容。它还具有在显示过程中进行一些细微转换的选项。

```
mtype [-s] [-t] dos_files
```

| 选项或参数 | 功能 |
| --- | --- |
| `-s` | 去除数据中的高位。 |
| `-t` | 将回车/换行转换为换行符。 |
| `dos_files` | 要显示的文件名。 |

`copy` 不允许你像其 MS-DOS 等效命令那样追加文件。要追加文件，请使用 `mtype` 并将其输出重定向到文件。例如，将第一张软盘上的 `two.nd` 追加到 `first.st` 的末尾并将结果放入 `both.files` 中，请输入 `mtype a:first.st a:two.nd > both.files`。

## xcopy — 将一个目录复制到另一个目录

`xcopy` 通过复制所有文件和子目录，在另一个位置复制目录下的文件层次结构。

```
xcopy source_dir target_dir
```

| 参数 | 功能 |
| --- | --- |
| `source_dir` | 要复制的文件目录。 |
| `target_dir` | 复制目标。如果 `target_dir` 不存在，`xcopy` 将创建它并将文件直接复制其中。 |

## 更多 Mtools 命令

以下命令也包含在 Mtools 工具包中。

| 命令 | 功能 |
| --- | --- |
| `mattrib` | 设置/清除属性位。 |
| `mbad` | 扫描坏块。 |
| `mdeltree` | 删除目录树。 |
| `mformat` | 格式化 MS-DOS 磁盘。 |
| `minfo` | 显示 MS-DOS 文件系统引导扇区的字段内容。 |
| `mkmanifest` | 创建一个 LINUX shell 脚本，以消除 MS-DOS 转换为 8.3 文件名时的混乱问题。 |
| `mlabel` | 添加卷标签。 |

## 挂载 MS-DOS 媒体和分区

| 命令 | 功能 |
| --- | --- |
| `mmount` | 挂载 MS-DOS 文件系统。 |
| `mmove` | 重命名 MS-DOS 文件或目录。 |
| `mpartition` | 创建 MS-DOS 分区。 |
| `mrd` | 移除 MS-DOS 子目录。 |
| `mren` | 重命名 MS-DOS 文件或目录。 |
| `mtoolstest` | 测试 Mtools 配置。 |

## 使用 Linux 内置支持挂载 MS-DOS 文件系统

与其使用 Mtools，你也可以使用 Linux 内置的对 MS-DOS 文件系统的支持。你可以像挂载任何其他文件系统一样挂载 MS-DOS 文件系统，然后将其视为 Linux 文件层次结构的一部分。

## 挂载硬盘分区

如果你在 Linux 计算机上有一个 MS-DOS 文件系统，你可以保留它。只需遵循以下步骤：

1. 以 root 身份登录。
2. 使用 `mkdir` 创建挂载点目录。
3. 编辑 `/etc/fstab` 并为相应的设备和挂载点添加挂载行。参见下表获取该行字段的示例。
4. 保存更新后的 `/etc/fstab`。
5. 输入 `mount -a` 强制重新读取 `/etc/fstab`。

| 字段 | 功能 |
| --- | --- |
| `Device` | 分区的设备名称。 |
| `Mount point` | 要挂载文件系统的目录名称。 |
| `Filesystem type` | 要使用的文件系统类型。MS-DOS 分区使用 `msdos`。 |
| `Options` | 挂载方式。使用默认值是安全的。 |
| `Dump frequency` | 如果不想让此分区包含在标准备份（dump）中，则使用 `0`。 |
| `fsck order` | 使用 `0`。 |

## 使用 Mac 媒体

例如，如果你的第一个硬盘上的第二个分区 (`/dev/hda2`) 是 MS-DOS 文件系统，你可以保留它。只需像挂载任何其他文件系统一样挂载 MS-DOS 文件系统，然后将其视为 Linux 文件层次结构的一部分。
