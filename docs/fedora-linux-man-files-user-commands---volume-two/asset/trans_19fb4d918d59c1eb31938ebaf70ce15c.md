

查找 AppleSingle Macintosh 文件

- `—dave` 查找 Thursby Software Systems DAVE Macintosh 文件
- `—sfm` 查找 Microsoft 的 Services for Macintosh 文件（仅适用于 NT）（Alpha）
- `—osx-double` 查找 Mac OS X AppleDouble Macintosh 文件
- `—osx-hfs` 查找 Mac OS X HFS Macintosh 文件

## 字符集

**genoisimage** 以符合 POSIX 的方式处理文件名，将其视为 8 位字符的字符串。为了表示所有语言的所有编码，8 位字符并不足够。Unicode 或 ISO-10646 定义了字符编码，至少需要 21 位才能表示所有已知语言。它们可以用 *UTF-32*、*UTF-16* 或 *UTF-8* 编码来表示。UTF-32 使用纯粹的 32 位编码，但似乎并不常见。Microsoft 在 Win32 中使用 UTF-16，缺点是 16 位字符不符合 POSIX 文件系统接口。

现代 Unix 操作系统可能在文件名中使用 UTF-8 编码。每个 32 位字符由一个或多个 8 位字符表示。如果字符采用 *ISO-8859-1* 编码（用于中欧和北美），则与 UTF-32 或 UTF-16 编码的 Unicode 字符呈 1:1 映射。如果字符采用 *7-Bit ASCII* 编码（用于美国及其他字符集有限的国家），则与 UTF-32、UTF-16 或 UTF-8 编码的 Unicode 字符呈 1:1 映射。在 UTF-8 中无法表示为单个字节的字符代码（如果值 > 0x7F）会使用转义序列，映射为多个 8 位字符。

如果所有操作系统都使用 UTF-8，**genoisimage** 就不需要重新编码文件名中的字符。不幸的是，Apple 使用了完全不标准的编码，而 Microsoft 使用了与 POSIX 文件名接口不兼容的 Unicode 编码。

对于所有未采用 UTF-8 编码的操作系统，每个字节实际表示的字符取决于本地操作系统使用的*字符集*或*代码页*（Microsoft 使用的名称）——字符集中的字符将反映用户设定的区域或自然语言。

通常，字符代码 0x00-0x1f 是控制字符，代码 0x20-0x7f 是 7 位 ASCII 字符，而（在 PC 和 Mac 上）0x80-0xff 用于其他字符。

由于正在使用的字符/符号远多于 256 个，字符集仅代表其中的一小部分。因此，相同的字符代码在不同的字符集中可能代表不同的字符。所以，一个在例如中欧生成的文件名，在例如东欧的机器上查看时可能不会显示相同的字符。

使情况更复杂的是，不同的操作系统使用不同的字符集来对应区域或语言。例如，`é`（带尖音符的小写 e）的字符代码在 PC 上可能是 0x82，在 Macintosh 上可能是 0x8e，在西欧的 Unix 系统上可能是 0xe9，而在 Unicode 中则是 0x00e9。

只要并非所有操作系统和应用都使用相同的字符集作为文件名的基础，就有可能需要指定文件名使用哪个字符集，以及文件名在 CD 上应以哪个字符集显示。

有四个选项可用于指定你想使用的字符集：

- **-input-charset**
  定义你在主机上使用的本地字符集。任何发生的字符集转换都将使用此字符集作为起点。默认输入字符集在基于 MS-DOS 的系统上是 *cp437*，在所有其他系统上是 *iso8859-1*。如果给出了 **-J**，Joliet 目录中将使用输入字符集的 Unicode 等效字符。**-j-charset** 等同于 **-input-charset -J**。

- **-output-charset**
  定义 CD 上 Rock Ridge 名称使用的字符集。默认为输入字符集。

- **-input-hfs-charset**
  定义用于解码任何 Apple/Unix 文件格式中 HFS 文件名的 HFS 字符集。仅在与 **-mac-name** 一起使用时有用。有关更多信息，请参阅 **HFS MACINTOSH FILENAMES**（HFS Macintosh 文件名）。默认为 *cp10000*（Mac Roman）。

- **-output-hfs-charset**
  定义用于从当前使用的输入字符集创建 HFS 文件名的 HFS 字符集。在大多数情况下，这将来自通过 **-input-charset** 给出的字符集。默认为输入 HFS 字符集。

**genisoimage** 中内置了许多字符集。要获取列表，请使用 **-input-charset help**。此列表不包括从当前区域设置派生的字符集（如果 **genisoimage** 是用 *iconv* 支持构建的）。

对于任何字符集选项，可以通过提供文件名作为参数来从文件读取额外的字符集。仅当给定的文件名不匹配任何一个内置字符集时，才会读取该文件。

字符集文件的格式与可从 . 获取的映射文件相同。格式如下：

第 1 列是输入字节代码（十六进制，形式为 0xXX）
第 2 列是 Unicode（十六进制，形式为 0xXXXX）
行的其余部分被忽略。

任何空白行、不符合上述格式（即没有两列或更多列）的行或注释行（以 *#* 字符开头）将被忽略且无警告。任何缺失的输入代码都映射到 Unicode 字符 0x0000。

请注意，虽然支持 UTF-8，但其他 Unicode 编码（如 UCS-2/UTF-16 和 UCS-4/UTF-32）不受支持，因为 POSIX 操作系统无法原生处理它们。

可以通过在任何字符集选项中关键字 *default* 作为参数来定义 1:1 的字符集映射。这是旧版本 **mkisofs** 的行为。

从输入文件名生成的 ISO9660 文件名不会从输入字符集进行转换。ISO9660 字符集是 ASCII 字符的一个非常有限的子集，因此任何转换都是徒劳的。

任何 **genisoimage** 无法转换的字符都将被 `_` 字符替换。

## HFS 创建者/类型

Macintosh 文件有两个相关属性，定义了哪个应用程序创建了该文件（CREATOR）以及文件包含什么数据（TYPE）。两者都是（恰好）4 个字母的字符串。通常，这允许 Macintosh 用户双击文件并启动正确的应用程序等。可以使用类似 ResEdit（或类似工具）在 Macintosh 上查找特定文件的 CREATOR 和 TYPE。

CREATOR 和 TYPE 信息存储在各种 Apple/Unix 编码文件中。对于其他文件，可以使用映射文件（使用 -map）和/或文件的魔术数（通常是前几个字节中的签名）（使用 -magic）来基于文件名扩展名确定 CREATOR 和 TYPE。如果给出了这两个选项，它们在命令行上的顺序很重要。如果先给出 -map，则在魔术数匹配之前会尝试文件名扩展名匹配。然而，如果先给出 -magic，则在文件名扩展名匹配之前会尝试魔术数匹配。

如果没有使用映射或魔术文件，或者未找到匹配项，可以通过使用 .genisoimagerc 文件中的条目或使用 -hfs-creator 和/或 -hfs-type 来设置所有常规文件的默认 CREATOR 和 TYPE，否则默认的 CREATOR 和 TYPE 是 Unix 和 TEXT。

映射文件的格式与 aufl 使用的文件格式相同。此文件有五个列，分别是扩展名、文件转换、CREATOR、TYPE 和注释。以 `#` 字符开头的行是注释行，将被忽略。一个示例文件如下：

```
# Example filename mapping file
#

# EXT XLate CREATOR TYPE  Comment
.tif   Raw 8BIM  TIFF   Photoshop TIFF image
.hqx   Ascii BnHq  TEXT   BinHex file
.doc   Raw MSWD  WDBN   Word file
.mov   Raw TVOD  MooV   QuickTime Movie
*      Ascii txt   TEXT   Text file
```

其中：

- 第一列 EXT 定义要映射的 Unix 文件名扩展名。任何不匹配的默认文件名扩展名的映射都由 `*` 字符定义。

- Xlate 列定义了 Unix 和 Macintosh 文件之间的文本转换类型。genisoimage 会忽略它，但保留它是为了与 (1) 兼容。虽然 genisoimage 不会更改文件内容，但如果二进制文件的 TYPE 被设置为 TEXT，它可能在 Macintosh 上被错误读取。因此，更好的默认 TYPE 选择可能是 `???`？

- CREATOR 和 TYPE 关键字必须是 4 个字符长，并用单引号括起来
