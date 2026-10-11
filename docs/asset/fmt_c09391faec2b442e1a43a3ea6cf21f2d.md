
假设我已从软盘将这些文件复制到另一个 Unix 系统，现在我希望文件恢复其原始名称。如果文件“manifest”（上述捕获的输出）已随这些文件一起发送，它可以用于转换文件名。

## 错误

`mkmanifest` 生成的短名称遵循旧惯例（来自 `mtools-2.0.7`），而不是来自 Windows 95 和 `mtools-3.0` 的惯例。

## MINFO

`minfo` 命令打印 Dos 文件系统的参数，如扇区数、磁头和柱面。它还打印一条 `mformat` 命令行，可用于在另一个介质上创建类似的 Dos 文件系统。然而，这不适用于 2m 或 Xdf 介质，也不适用于 Dos 1.0 文件系统的 `minfo drive`。

`Mlabel` 支持以下选项：

- `v` 除了其他信息外，打印引导扇区的十六进制转储

## MLABEL

`mlabel` 命令向磁盘添加卷标。其语法为：

```
mlabel [-vcs] drive:[new_label]
```

`Mlabel` 显示当前卷标（如果存在）。如果未提供 `new_label`，且未设置 `c` 或 `s` 选项，它会提示用户输入新的卷标。若要删除现有的卷标，请在提示符处按回车键。

会采取合理措施以创建有效的 MS-DOS 卷标。如果指定的标签无效，`mlabel` 将更改标签（如果设置了详细模式，还会显示新标签）。`mlabel` 成功时返回 0，失败时返回 1。

`mlabel` 支持以下选项：

- `c` 清除现有标签，不提示用户。
- `s` 显示现有标签，不提示用户。

### MMD

`mmd` 命令用于创建 MS-DOS 子目录。其语法为：

```
mmd [ -voOsSrRA ] msdosdirectory [ msdosdirectories... ]
```

`mmd` 在 MS-DOS 文件系统上创建新目录。如果目录已存在，则会发生错误。

### MMOUNT

`mmount` 命令用于挂载 MS-DOS 磁盘。它仅在 Linux 上可用，因为只有当操作系统内核允许您配置磁盘几何参数时，它才有用。其语法为：

```
mmount msdosdrive [ mountargs ]
```

`mmount` 读取 MS-DOS 磁盘的引导扇区，配置驱动器几何参数，最后通过向 `mount` 传递 `mountargs` 来挂载它。如果未指定挂载参数，则使用设备名称。如果磁盘写保护，则自动以只读方式挂载。

### MMOVE

`mmove` 命令用于移动或重命名现有的 MS-DOS 文件或子目录。其语法为：

```
mmove [ -voOsSrRA ] sourcefile targetfile
mmove [ -voOsSrRA ] sourcefile [ sourcefiles... ] targetdirectory
```

`mmove` 移动或重命名现有的 MS-DOS 文件或子目录。与 MS-DOS 版本的 `MOVE` 不同，`mmove` 能够移动子目录。

### MPARTITION

`mpartition` 命令用于将 Linux MS-DOS 文件系统创建为分区。这旨在用于非 Linux 系统，即 fdisk 和对 SCSI 设备的易访问性不可用的系统。此命令仅适用于设置了分区变量的驱动器。其语法为：

```
mpartition -p drive
mpartition -r drive
mpartition -I drive
mpartition -a drive
mpartition -d drive
mpartition -c [-s sectors] [-h heads] [-t cylinders] [-v [-T type]] [-b begin] [-l length] [-f]
```

`Mpartition` 支持以下操作：

- `p` 打印用于重建该驱动器分区的命令行。如果未定义该驱动器的分区，或检测到不一致，则不打印任何内容。如果同时设置了 verbose (`-v`)，则打印当前的分区表。
- `r` 删除由 `drive` 描述的分区。
- `I` 初始化分区表，并删除所有分区。
- `c` 创建由 `drive` 描述的分区。
- `a` “激活” 分区，即使其可引导。一次只能有一个分区可引导。
- `d` “停用” 分区，即使其不可引导。

如果未指定任何操作，则打印当前设置。

对于分区创建，可使用以下选项：

- `s sectors` 分区每磁道扇区数（这也是整个驱动器每磁道扇区数）。
- `h heads` 分区的磁头数（这也是整个驱动器的磁头数）。默认情况下，几何信息（扇区数和磁头数）是从相邻的分区表条目中得出的，或是根据大小猜测的。
- `t cylinders` 分区的柱面数（不是整个驱动器的柱面数）。
- `b begin` 分区的起始偏移量，以扇区为单位。如果未提供 `begin`，`mpartition` 将让分区从磁盘开始处（分区编号 1）或前一个分区结束处立即开始。
- `l length` 分区的大小（长度），以扇区为单位。如果未提供 `end`，`mpartition` 会根据扇区数、磁头数和柱面数计算出大小。如果这些也未提供，它会考虑磁盘大小和下一个分区的起始位置，给予分区尽可能大的尺寸。

以下选项适用于所有修改分区表的操作：

- `f` 通常，在将任何更改写回分区之前，`mpartition` 会执行某些一致性检查，例如检查重叠和分区的适当对齐。如果这些检查中的任何一个失败，分区表将不会被更改。`-f` 允许您覆盖这些安全措施。

以下选项适用于所有操作：

- `v` 与 `-p` 一起使用时，打印当前的分区表（无更改操作），或修改后的分区表。
- `vv` 如果详细标志给出两次，`mpartition` 将在从设备读取分区表和向设备写入分区表时打印分区表的十六进制转储。

## MRD

`mrD` 命令用于删除 MS-DOS 子目录。其语法为：

```
mrd [-v] msdosdirectory [msdosdirectories...]
```

`MrD` 从 MS-DOS 文件系统中删除目录。如果目录不存在或非空，则会发生错误。

## MREN

`mren` 命令用于重命名或移动现有的 MSDOS 文件或子目录。其语法为：

```
mren [-voOsSrRA] sourcefile targetfile
```

`Mren` 重命名 MS-DOS 文件系统上的现有文件。

在详细模式下，`mren` 会显示新文件名，如果提供的名称无效。

如果使用第一种语法（只有一个 `sourcefile`），且目标名称不包含任何斜杠或冒号，则文件（或子目录）将在同一目录中重命名，而不是像使用 `mmove` 时那样移动到当前 `mcd` 目录。与 MS-DOS 版本的 `REN` 不同，`mren` 可用于重命名目录。

## MTOOLSTEST

`mtoolltest` 命令用于测试 mtools 配置文件。调用时，只需输入 `mtoolltest`，无需任何参数。`Mtoolltest` 读取 mtools 配置文件，并将累计配置打印到 `stdout`（标准输出）。该输出本身可作为配置文件使用（不过你可能希望移除冗余条款）。你可以使用此程序将旧式配置文件转换为新式配置文件。

## MTYPE

`mtype` 命令用于显示 MS-DOS 文件的内容。其语法如下：

```
mtype [-ts] msdosfile [msdosfiles...]
```

`Mtype` 在屏幕上显示指定的 MS-DOS 文件。

除了标准选项外，`Mtype` 还支持以下命令行选项：

- `t`: 文本文件查看模式。`Mtype` 将输入的换行回车符（CR/LF）转换为换行符（LF）。
- `s`: `Mtype` 从数据中去除最高位。

可以使用 `mcd` 命令来建立设备和当前工作目录（相对于 MS-DOS），否则默认为 `A:/`。`Mtype` 在成功时返回 0，完全失败时返回 1，部分失败时返回 2。与 MS-DOS 版本的 `TYPE` 不同，`mtype` 允许使用多个参数。

## MZIP

`mzip` 命令用于在 Solaris 或 HP-UX 上发出 ZIP 磁盘专用命令。其语法如下：

```
mzip [-eprwx]
```

`Mzip` 支持以下命令行选项：

- `e`: 弹出磁盘。
- `f`: 强制弹出，即使磁盘已挂载。
- `r`: 写入保护磁盘。
- `w`: 解除写入保护。
- `p`: 密码写入保护。
- `x`: 密码保护。
- `q`: 查询状态。

若要移除密码，请将其设置为无密码模式之一 `-r` 或 `-w`，`mzip` 随后会提示输入密码并解锁磁盘。如果你忘记了密码，可以通过低级格式化磁盘来清除密码（使用你的 SCSI 适配器的 BIOS 设置）。随驱动器附带的 ZipTools 磁盘也受密码保护。一旦安装了 ZipTools，该密码会自动移除。

## XCOPY

`xcopy` 脚本用于将一个目录递归复制到另一个目录。其语法如下：

```
xcopy sourcedirectory targetdirectory
```
