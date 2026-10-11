
`mcopy` 命令用于在 Unix 和 MS-DOS 文件之间进行复制。它使用以下语法：

```
mcopy [-tnvmoOsSfRA] sourcefile targetfile
```

```
mcopy [-tnvmoOsSfRA] sourcefile [ sourcefiles... ] - targetdirectory
```

```
mcopy [-tnvm] MSDOSsourcefile
```

`Mcopy` 将指定的文件复制到目标文件中，或将多个文件复制到指定的目录中。源和目标可以是 MS-DOS 文件或 Unix 文件。

在 MS-DOS 文件上使用驱动器字母标识（例如 `'a:'`）决定了传输的方向。缺少驱动器标识意味着路径从当前目录开始的 Unix 文件。如果指定了源驱动器字母但没有附带文件名（例如 `mcopy a:: .`），则从该驱动器复制所有文件。

如果只提供一个单独的 MS-DOS 源参数（例如 `"mcopy a:\foo.exe"`），则假设目标目录为当前目录 `'.'`。文件名为 `'-'` 表示标准输入或标准输出，具体取决于其在命令行上的位置。

`Mcopy` 接受以下命令行选项：

- `q` 在复制多个文件时，一旦某个复制失败（例如由于目标磁盘存储空间不足）即退出。
- `t` 文本文件传输。`Mcopy` 将传入的回车/换行符转换为换行符。
- `n` 覆盖 Unix 文件时不确认。`Mcopy` 在覆盖现有 Unix 文件时不会警告用户。若要关闭 DOS 文件的确认，请使用 `-o`。
- `m` 保留文件修改时间。如果目标文件已存在，且 `-n` 选项未生效，`mcopy` 会询问是否覆盖该文件或重命名新文件（'名称冲突'）以获取更多详细信息。

### 缺陷

与 MS-DOS 不同，MS-DOS 中的 `'+'` 运算符（追加）不受支持。但是，你可以使用 `mtype` 产生相同的效果：

```
mtype a:file1 a:file2 a:file3 >unixfile
mtype a:file1 a:file2 a:file3 | mcopy - a:msdosfile
```

### MDEL

`mdel` 命令用于删除 MS-DOS 文件。其语法为：

```
mdel [-v] msdosfile [msdosfiles ... ]
```

`Mdel` 删除 MS-DOS 文件系统上的文件。

`Mdel` 在删除只读文件之前会请求验证。

### MDELTREE

`mdeltree` 命令用于删除 MS-DOS 文件。其语法为：

```
mdeltree [-v] msdosdirectory [msdosdirectories...]
```

`Mdeltree` 从 MS-DOS 文件系统上移除目录及其包含的所有文件和子目录。如果要删除的目录不存在，则会发生错误。

### MDIR

`mdir` 命令用于显示 MS-DOS 目录。其语法为：

```
mdir [-w] msdosdirectory
mdir [-f] [-w] [-a] msdosfile [msdosfiles...]
```

`Mdir` 显示 MS-DOS 目录的内容。

`Mdir` 支持以下命令行选项：

- `-w` 宽输出。使用此选项时，`mdir` 会在页面上横向打印文件名，而不显示文件大小或创建日期。
- `-a` 同时列出隐藏文件。
- `-f` 快速。不尝试查找可用空间。在较大的磁盘上，查找可用空间量需要花费一些不可忽略的时间，因为必须读取并扫描整个 FAT。`-f` 标志跳过了这一步。在 FAT32 文件系统中不需要此标志，因为它们显式存储大小。

如果路径的某个组件不是目录，则会发生错误。

### MFORMAT

`mformat` 命令用于在已进行低级格式化的磁盘上添加 MS-DOS 文件系统。其语法为：

```
mformat [-t cylinders] [-h heads] [-s sectors] [-l volume_label]
[-F] [-1 fsVersion] [-S sizetode] [-2 sectors_on_track_0]
[-M software_sector_size] [-a] [-X] [-C] [-H hidden_sectors]
[+- root_sectors] drive:
```

`Mformat` 向已经由 Unix 低级格式化的磁盘添加最小的 MS-DOS 文件系统（引导扇区、FAT 和根目录）。

支持以下选项：（如果此 `mtools` 副本在编译时未包含 `USE_2M` 选项，则 `S`、`2`、`1` 和 `M` 选项可能不存在。）

- `-t` 柱面数。
- `-h` 磁头（面）数。
- `-s` 每轨道扇区数。如果给出了 `2m` 选项，则为通用轨道（即非 0 头 0 轨道）上的 512 字节扇区等价数量。如果没有给出 `2m` 选项，则为每轨道的物理扇区数（可能大于 512 字节）。
- `-l` 可选的卷标。
- `-S` 大小代码。扇区大小为 `2^(sizecode + 7)`。
- `-2` 2m 格式。此选项的参数描述了 0 轨道 0 头上的扇区数。此选项推荐用于比正常大的扇区。
- `-1` 不使用 2m 格式，即使磁盘的当前几何形状是 2m 几何形状。
- `-M` 软件扇区大小。此参数描述了 MS-DOS 文件系统使用的扇区大小（以字节为单位）。默认情况下，它是物理扇区大小。
- `-a` 如果给出此选项，将生成 Atari 风格的序列号。Ataris 将它们的序列号存储在 OEM 标签中。
- `-X` 将磁盘格式化为 XDF 磁盘。更多详情请参见 `"XDF"` 章节。磁盘必须首先使用 `fdtutils` 包中包含的 `xdfcopy` 工具进行低级格式化。
- `-C` 创建磁盘镜像文件，以在其上安装 MS-DOS 文件系统。显然，这对于软盘和硬盘分区等物理设备来说是无用的。
- `-H` 隐藏扇区数。此参数对于格式化未对齐轨道边界（即第一个轨道的第一个磁头不属于该分区，而是包含分区表）的硬盘分区很有用。在这种情况下，隐藏扇区数通常等于每柱面的扇区数。这未经测试。
- `-n` 序列号

| 选项 | 描述 |
| :-- | :--- |
| F | 将分区格式化为 FAT32（实验性）。 |
| I | 在格式化 FAT32 驱动器时设置 `fsVersion` id。为了查明此信息，请在现有的 FAT32 驱动器上运行 `minfo`，并将其告知我，以便我能在未来版本的 `mttools` 中包含正确的值。 |
| c | 设置簇的大小（以扇区为单位）。如果该簇尺寸会生成一个相对于其位数来说过大的 FAT，`mtools` 会自动增加簇尺寸，直到 FAT 足够小为止。 |
| r | 设置根目录的大小（以扇区为单位）。仅适用于 12 位和 16 位 FAT。 |

若要将以非默认密度格式化软盘，您必须提供（至少）那些与默认值不同的命令行参数。

`Mformat` 成功时返回 `0`，失败时返回 `1`。

它不会向 Fat 记录坏块信息，请使用 `mkmanifest` 来处理该功能。

### MKMANIFEST

`mkmanifest` 命令用于创建一个 shell 脚本（打包列表），以恢复 Unix 文件名。其语法如下：

```
mkmanifest [files]
```

`Mkmanifest` 创建一个 shell 脚本，用于辅助恢复被 MS-DOS 文件名限制破坏的 Unix 文件名。MS-DOS 文件名限制为 8 个字符的名称、3 个字符的扩展名、仅大写、无设备名称，且无非法字符。

`mkmanifest` 程序与 `pcomm`、`arc` 和 `mtools` 中用于将完美的 Unix 文件名修改以符合 MS-DOS 限制的方法相兼容。仅当读取该软盘的目标系统无法处理 `vfat` 长文件名时，此命令才有用。

### 示例

您想要将以下 Unix 文件复制到 MS-DOS 软盘（使用 `mcopy` 命令）。

- `very_long_name`
- `2.many.dots`
- `illegal:`
- `good.c`
- `prn.dev`
- `Capital`

`Mcopy` 将名称转换为：

- `very_1on`
- `2xmany.dot`
- `illegal`
- `good.c`
- `xprn.dev`
- `capital`

该命令

```
mkmanifest very_long_name 2.many.dots illegal: good.c prn.dev Capital > manifest
```

将产生以下内容：

- `mv very_1on very_long_name`
- `mv 2xmany.dot 2.many.dots`
- `mv illegal: illegal:`
- `mv xprn.dev prn.dev`
- `mv capital Capital`

请注意，`good.c` 无需转换，因此它未出现在输出中。
