
`mpartition -p drive`
`mpartition -r drive`
`mpartition -I [-B BootSector] drive`
`mpartition -a drive`
`mpartition -d drive`
`mpartition -c [-s sectors] [-h heads] [-t cylinders] [-v [-T type] [-b begin] [-l length] [-f]`

# mpartition

## 名称
`mpartition` - 对 MSDOS 硬盘进行分区

## 描述
`mpartition` 命令用于创建 MS-DOS 文件系统作为分区。这旨在用于非 Linux 系统，即无法使用 `fdisk` 且无法访问 SCSI 设备的系统。此命令仅在设置了分区变量的驱动上工作。

`mpartition -p drive`
`mpartition -r drive`
`mpartition -I [-B BootSector] drive`
`mpartition -a drive`
`mpartition -d drive`
`mpartition -c [-s sectors] [-h heads] [-t cylinders] [-v [-T type] [-b begin] [-l length] [-f]`

`Mpartition` 支持以下操作：

- `p` 打印用于重建驱动器分区的命令。如果驱动未定义分区或检测到不一致，则不打印。如果设置了详细模式 `-v`，则打印当前分区表。
- `r` 移除 `drive` 描述的分区。
- `I` 初始化分区表并移除所有分区。
- `c` 创建 `drive` 描述的分区。
- `a` “激活”分区，即使其可启动。一次时间只能有一个分区是可启动。
- `d` “取消激活”分区，即使其不可可启动。

如果没有给出任何操作，则打印当前设置。

对于分区创建，有可用选项：

- `sectors` 分区每个磁道的扇区数（这也是整个驱动器每个磁道的扇区数）。
- `heads` 分区的磁头数（这也是整个驱动器的磁头数）。默认情况下，几何信息（扇区数和磁头数）从相邻的分区表条目得出，或从尺寸推测。
- `cylinders` 分区的柱面数（不是整个驱动器的柱面数）。
- `begin` 分区的起始偏移，以扇区表示。如果没有给出 `begin`，`mpartition` 让分区从磁盘开始处（分区 1）或紧接上一个分区的结束开始。
- `length` 分区的尺寸（长度），以扇区表示。如果没有给出 `end`，`mpartition` 根据扇区数、磁头数和柱面数计算尺寸。如果没有给出这些，它将考虑磁盘大小和起始位置，赋予分区最大的可能尺寸。

## 作者
Marcel Mol <>（当前维护者）。
Mark P. Hahn（原作者）

## EOF 警告
此帮助页由 mtools 的 texinfo 文档自动生成，可能不完全准确或完整。详情请参见此帮助页末尾。

# mren

## 名称
`mren` - 重命名现有的 MSDOS 文件

## NOTEOFWARNING
本手册页根据 mtools 的 texinfo 文档自动生成，可能并不完全准确或完整。详情请参阅本页末尾。

## 描述
`mren` 命令用于重命名或移动现有的 MS-DOS 文件或子目录。

其语法如下：

```
mren [-voSsRA] sourcefile targetfile
```

`Mren` 用于重命名 MS-DOS 文件系统上的现有文件。

在详细模式下，如果提供的名称无效，`Mren` 将显示新的文件名。

如果使用第一种语法（仅一个源文件），且目标名称不包含任何斜杠或冒号，则文件（或子目录）将在原目录中重命名，而不是像 `mmove` 那样移动到当前的 `mcd` 目录。与 MS-DOS 版本的 REN 不同，`mren` 可用于重命名目录。

## SEEALSO
Mtools 的 texinfo 文档

## VIEWINGTHEXTIDOC
本手册页根据 mtools 的 texinfo 文档自动生成。然而，此过程只是近似的，某些项目（如交叉引用、脚注和索引）在翻译过程中丢失了。事实上，这些项目在手册页格式中没有合适的表示。此外，info 中使用的所有信息都没有翻译成手册页版本。因此，我强烈建议您使用原始 texinfo 文档。请参阅本页末尾查看 texinfo 文档的说明。

- 要从 texinfo 文档生成可打印副本，请运行以下命令：`./configure; make dvi; dvips mtools.dvi`
- 要生成 html 副本，运行：`./configure; make html`

可以在 ∞ 处找到预制的 html 版本。
- 要生成 info 副本（可以使用 emacs 的 info 模式浏览），运行：`./configure; make info`

texinfo 文档在打印或作为 html 显示时看起来最美观。事实上，在 info 版本中，由于 info 使用的引用约定，某些示例难以阅读。

# msgattrib

## 名称
`msgattrib` - 消息目录上的属性匹配和操作

## 摘要
```
msgattrib [OPTION] [INPUTFILE]
```

## 描述
根据属性过滤翻译目录的消息，并操作这些属性。

长选项的强制性参数对于短选项也是强制的。

### 输入文件位置
```
INPUTFILE
input PO=DIRECTORY
-D, --directory=DIRECTORY 用于搜索输入文件的目录列表
```
如果没有给出输入文件或其为 `-`，则读取标准输入。

### 输出文件位置
```
-o, --output-file=FILE
将输出写入指定的文件
```
如果未指定输出文件或其为 `-`，则将结果写入标准输出。

### 消息选择
- `-translated` 保留已翻译的消息，移除未翻译的消息
- `--untranslated` 保留未翻译的消息，移除已翻译的消息
- `--no-fuzzy` 移除标记为‘fuzzy’（模糊/部分匹配）的消息
- `--only-fuzzy` 保留标记为‘fuzzy’的消息
- `--no-obsolete` 移除过时的 #~ 消息
- `--only-obsolete` 保留过时的 #~ 消息

### 属性操作
- `-set-fuzzy` 将所有消息设为‘fuzzy’
- `--clear-fuzzy` 将所有消息设为非‘fuzzy’
- `--set-obsolete` 将所有消息设为过时
- `--clear-obsolete` 将所有消息设为非过时
- `--previous` 在设置‘fuzzy’时，保留已翻译消息的之前的 msgid
- `--clear-previous` 从所有消息中移除“previous msgid”
- `--empty` 在移除‘fuzzy’时，同时将 msgstr 设为空
- `--only-file=FILE.po` 仅操作 FILE.po 中列出的条目
- `--ignore-file=FILE.po` 仅操作未列在 FILE.po 中的条目
- `--fuzzy` —only-fuzzy 和 --clear-fuzzy 的同义词
- `--obsolete` —only-obsolete 和 --clear-obsolete 的同义词

### 输入文件语法
- `-P, —properties-input` 输入文件采用 Java .properties 语法（注意：可能是 .properties）
- `--stringtable-input` 输入文件采用 NeXtStep/GNUstep .strings 语法

### 输出细节
- `--color` 始终使用颜色和其他文本属性
- `--color=WHEN` 如果满足 WHEN，则使用颜色和其他文本属性。WHEN 可以是。
- `-style=WHEN` 如果满足 WHEN，则使用颜色和其他文本属性。WHEN 可以是。

显示此帮助信息并退出
- `-V, --version` 输出版本信息并退出

由 Bruno Haible 编写。

## 报告缺陷
将缺陷报告至 <>。

## 版权
Copyright © 2001-2010 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <> 这是一个免费软件：你可以自由地更改和重新分发。在法律允许范围内，不提供任何保证。

## 另参
**msgcat** 的完整文档作为 Texinfo 手册维护。如果你的站点上正确安装了 **info** 和 **msgcat** 程序，则运行命令

```
info msgcat
```

应该允许你访问完整的手册。

# MSGCMP

## 名称
`msgcmp` - 比较消息目录和模板

## 概要
```
msgcmp [OPTION] def.po ref.pot
```

## 描述
比较两个 Uniform 风格的 .po 文件，以检查两者是否包含相同组的 msgid 字符串。`def.po` 文件是带有翻译的现有 PO 文件。`ref.pot` 文件是最后创建的 PO 文件，或 PO 模板文件（通常由 xgettext 创建）。这对于检查你是否翻译了程序中的每条消息非常有用。如果找不到精确匹配，将使用模糊匹配来产生更好的诊断结果。

长选项的强制性参数对于短选项也是强制性的。

### 输入文件位置
- `def.po` 翻译
- `ref.pot` 对源文件的引用
- `-D,--directory=DIRECTORY` 将 DIRECTORY 添加到输入搜索列表中

### 操作修饰
- `-m,--multi-domain` 对 def.po 中的每个域应用 ref.pot
- `-N,--no-fuzzy-matching` 不使用模糊匹配
- `--use-fuzzy` 考虑模糊条目
- `--use-untranslated` 考虑未翻译条目

### 输入文件语法
- `-P,--properties-input` 输入文件采用 Java .properties 语法
- `--stringtable-input` 输入文件采用 NeXtstep/GNUstep .strings 语法

### 信息性输出
- `-h,--help` 显示此帮助信息并退出
- `-V,--version` 输出版本信息并退出

由 Peter Miller 编写。

## 报告缺陷
将缺陷报告至 <>。

## 版权
Copyright © 1995-1998, 2000-2010 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <> 这是一个免费软件：你可以自由地更改和重新分发。在法律允许范围内，不提供任何保证。

## 另参
**msgcmp** 的完整文档作为 Texinfo 手册维护。如果你的站点上正确安装了 **info** 和 **msgcmp** 程序，则运行命令

```
info msgcmp
```

应该允许你访问完整的手册。

# MSGCOMM

## 名称
`msgcomm` - 匹配两个消息目录

## 概要
```
msgcomm [OPTION] [INPUTFILE]...
```

## 描述
找到两个或多个指定 PO 文件中共有的消息。通过使用 `--more-than` 选项，可以在打印消息之前请求更高的共性。相反，可以使用 `--less-than` 选项在打印消息之前指定较低的共性（例如 `--less-than=2` 将仅打印唯一消息）。翻译、注释和提取的注释将被保留，但仅来自定义它们的第一个 PO 文件。所有 PO 文件的位置将累加。长选项的强制性参数对于短选项也是强制性的。

### 输入文件位置
- `INPUTFILE ...` 输入文件
- `-f,--files-from=FILE` 从 FILE 获取输入文件列表
- `-D,--directory=DIRECTORY` 将 DIRECTORY 添加到输入搜索列表中

如果输入文件为 `-`，则读取标准输入。

### 输出文件位置
- `-o,--output-file=FILE` 将输出写入指定的文件

如果没有指定输出文件或文件为 `-`，则将结果写入标准输出。

### 消息选择
- `-<, --less-than=NUMBER` 打印定义少于此数量的消息，未设置则默认为无限
- `-> --more-than=NUMBER` 打印定义大于此数量的消息，未设置则默认为 1
- `-u,--unique` `--less-than=2` 的简写，请求仅打印唯一消息

### 输入文件语法
- `-P, --properties-input` 输入文件采用 Java .properties 语法
- `--stringtable-input` 输入文件采用 NeXT/GNUstep .strings 语法

### 输出细节
- `-color` 始终使用颜色和其他文本属性
- `-color=WHEN` 如果满足 WHEN 则使用颜色和其他文本属性。WHEN 可以是 ‘always’‘never’‘auto’或 ‘html’。
- `-style=STYLEFILE` 为 —color 指定 CSS 样式规则
- `-e, —no-escape` 在输出中使用 C 转义字符（默认）
- `-E, —escape` 在输出中使用 C 转义字符，不使用扩展字符
- `-force-po`
- `-i, --indent`
- `-no-location`
- `-n, --add-location`
- `-strict Uniform 输出`
- `-n`
- `-output`
- `-p, --properties-input` 输入文件采用 Java .properties 语法
- `-stringtable-input` 输入文件采用 NeXT/GNUstep .strings 语法

### 信息性输出
- `-h, --help` 显示此帮助信息并退出
- `-V, --version` 输出版本信息并退出

## 作者
由 Bruno Haible 编写。

## 报告 Bug
将 Bug 报告至 <>。

## 版权
Copyright © 2001-2010 Free Software Foundation, Inc. 许可证 GPLv3+: GNU GPL 3 版或更高版本 <> 这是一个免费软件：你可以自由地更改和重新发行它。在法律允许范围内，不提供任何担保。

## 另请
**msgconv** 的完整文档作为 Texinfo 手册维护。如果 **info** 和 **msgconv** 程序在你的站点上正确安装，可以使用命令

```
info msgconv
```

应该可以让你访问完整的手册。

# MSGEN

## 名称
`msgen` - 创建英语消息目录

## 概要概要
```
msgen [OPTION] INPUTFILE
```

## 描述
创建一个英语翻译目录。输入文件是最后创建的英文 PO 文件，或 PO 模板文件（通常由 xgettext 创建）。未翻译的条目将被分配与 msid 相同的翻译。

长选项的强制性参数对于短选项也是强制性的。

### 输入文件位置
- `INPUTFILE` 输入 PO 或 POT 文件
- `-D,--directory` 将 DIRECTORY 添加到输入文件搜索列表中

如果输入文件为 `-`，则读取标准输入。

### 输出文件位置
- `-o,--output-file=FILE` 将输出写入指定的文件

如果未指定输出文件或其为 `-`，则结果被写入到标准输出。

### 输入文件语法
- `-P,--properties-input` 输入文件采用 Java .properties 语法
- `--stringtable-input` 输入文件采用 NeXTstep/GNUstep .strings 语法

### 输出详情
- `--lang=CATALOGNAME` 设置头部条目中的 'Language' 字段
