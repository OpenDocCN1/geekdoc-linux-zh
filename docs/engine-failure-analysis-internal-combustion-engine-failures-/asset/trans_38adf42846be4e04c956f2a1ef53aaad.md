
## 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -c, --complement | 补集 expression1 |
| -d, --delete | 删除 expression1 定义的字符 |
| -s, --squeeze-repeats | 将 expression1 定义的两个或更多连续字符替换为一个字符 |
| --help | 显示可用选项 |
| --version | 显示版本号 |

## 特殊字符

| 字符 | 描述 |
| :--- | :--- |
| \a | 响铃 |
| \b | 退格 |
| \f | 换页 |
| \n | 换行 |
| \r | 回车 |
| \t | 制表符 |
| \v | 垂直制表符 |
| \nnn | 八进制值为 nnn 的字符 |
| \\ | 字面反斜杠 |
| char1-char2 | 从八进制 char1 到八进制 char2 的字符范围 |

## 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| cat uppercase.txt \| tr '[A-Z]' '[a-z]' 或 cat uppercase.txt \| tr '[::upper:]' '[::lower:]' | 将文件 (uppercase.txt) 中的大写字母转换为小写字母。 |
| cat tabs.txt \| tr -d '\t' > notabs.txt | 从 tabs.txt 中移除制表符，并将输出写入 notabs.txt。 |

# troff

参见 **groff**。

# unexpand

`unexpand [ 选项 ] [ 文件名 ]`

将指定 *文件名* 中的空格转换为制表符，并写入标准输出（参见 *expand*）。你可以在空格分隔的列表或通过使用 shell 模式指定多个 *文件名*（参见 *第 4 章* 中的“Shell 模式”部分）。该实用程序在文本之前打印每个文件的名称。如果省略 *文件名*，该实用程序从标准输入接受输入。

## 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -a, --all | 转换所有空白，而不仅仅是初始空白 |
| --help | 显示可用选项 |
| -t *列表*, --tabs=*列表* | 使用逗号分隔的制表位列表 |
| -t *n*, --tabs=*n* | 将默认制表宽度设置为 *n* 个空格 |
| --version | 显示版本号 |

# uniq

`uniq [ 选项 ] [ 输入文件 [ 输出文件 ] ]`

从排序的输入文件中删除重复行并写入输出文件。

另见 *sort*。

## 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -c, --count | 在行前加上出现次数 |
| -d, --repeated | 打印重复行但不打印唯一行 |
| -f *n*, --skip-fields=*n* | 跳过前 *n* 个字段 |
| --help | 显示可用选项 |
| -i, --ignore-case | 忽略大小写 |
| -n | 跳过前 *n* 行 |
| +*n*, -s, --skip-chars=*n* | 跳过前 *n* 个字符 |
| -u, --unique | 仅打印唯一行而不打印重复行 |
| --version | 显示版本号 |
| -W *n*, --check-chars=*n* | 仅比较每行的前 *n* 个字符 |

## 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| uniq dupes.txt nodupes.txt | 从 `dupes.txt`（一个排序文件）中删除重复行并写入 `nodupes.txt`。 |

# unstr

`unstr [ 选项 ] [ *数据文件* ] [ *输出文件* ]`

通过将在数据文件中存储的字符串打印到输出文件，来反转 *strfile* 的工作。

*另见 fortune。*

# zcat

```
zcat filename
```

在屏幕上显示 *filename*（一个 *gzip* 压缩文件），而不解压缩文件。有关 *gzip* 的更多信息，请参见第 6 章。

另见 *zmore*。

## 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| zcat bibliography.gz \| less | 在屏幕上显示压缩文件 *bibliography.gz*，并将输出管道传输到 *less*。 |

# zcmp

```
zcmp [ 选项 ] filename1 [ filename2]
```

比较 *filename1* 和 *filename2*，这两个文件都是用 *gzip* 创建的压缩文件（参见第 6 章）。有关可用选项，请参见 *cmp*。

# zdiff

```
zdiff [ 选项 ] filename1 [ filename2]
```

比较 *filename1* 和 *filename2*，这两个文件都是用 *gzip* 创建的压缩文件（参见第 6 章）。有关可用选项，请参见 *diff*。

# zgrep

```
zgrep [ 选项 ] regexp filename
```

在指定的 *filename* 中搜索 *regexp*（一个扩展正则表达式），其中 *filename* 是用 *gzip* 创建的压缩文件（参见第 6 章）。你可以在空格分隔的列表或通过使用 shell 模式指定多个文件名（参见第 4 章中的“Shell 模式”部分）。有关可用选项，请参见 egrep。

# zfgrep

`zfgrep [ 选项 ] string filename`

在指定的 *filename* 中搜索指定的 *string*（一个由换行符分隔的一个或多个搜索词列表），其中 *filename* 是用 *gzip* 创建的压缩文件（参见第 6 章）。你可以在空格分隔的列表或通过使用 shell 模式指定多个文件名（参见第 4 章中的“Shell 模式”部分）。有关可用选项，请参见 fgrep。

# zgrep

`zgrep [ 选项 ] regexp filename`

在指定的 *filename* 中搜索 *regexp*（一个基本正则表达式），其中 *filename* 是用 *gzip* 创建的压缩文件（参见第 6 章）。你可以在空格分隔的列表或通过使用 shell 模式指定多个文件名（参见第 4 章中的“Shell 模式”部分）。有关可用选项，请参见 grep。

# zmore

`zmore filename`

显示 *filename*（一个用 *gzip* 或 *compress* 创建的压缩文件），而不解压缩文件。（有关 *gzip* 和 *compress* 的更多信息，请参见第 6 章。）你可以在空格分隔的列表或通过使用 shell 模式指定多个文件名（参见第 4 章中的“Shell 模式”部分）。如果省略 *filename*，该实用程序从标准输入接受输入。

## 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| = | 显示当前行号。 |
| . | 重复上一条命令。 |
| :q, :Q, q, Q | 退出。 |
| [ *n* ] regexp | 搜索 *regexp*（正则表达式）的第 *n* 次出现。默认情况下，*n* 为 1，因此搜索找到下一次出现。 |
| [ *n* ] Ctrl + D, [ *n* ] d | 显示 *n* 更多行。默认值为 11。 |
| ! command | 运行指定的 shell 命令。 |
| *n* | 显示 *n* 更多行。在输入数字后按下空格键。 |
| *nf* | 跳过 *n* 屏并打印一屏的行。 |
| *nn* | 搜索最后输入的正则表达式的第 *n* 次出现。 |
| *ns* | 跳过 *n* 行并打印一屏的行。 |
| s | 跳到下一个文件。 |

# 第 9 章

![](img/e85417bb52fc523c6fc7b3b77b124ecb_402_0.png)

处理声音和图形文件

本章涵盖了能够处理声音和图形文件的实用程序。这些实用程序可以制作 CD-ROM 音频轨道的磁盘录音，播放 MP3 和 MIDI 音频文件，将几乎所有类型的计算机图形文件转换为另一种图形格式，等等。

> 提示 本章讨论的一些命令在大多数 Linux 发行版中默认未安装。有关从互联网下载这些命令的信息，请参见简介。

# 概览

| 如何操作 | 参见此条目 | 示例 |
| :--- | :--- | :--- |
| 将图形文件从一种格式转换为另一种格式？ | **convert** | `convert jpeg image1.bmp image1.jpg` |
| 创建工作目录中所有图形文件的缩略图索引？ | **convert** | `convert \`vid:*\.jpg\` catalog.jpg` |
| 为刚刚刻录的 CD-ROM 创建印刷版珠宝盒标签？ | **cdlabelgen** | `cdlabelgen -c \`My Favorites\` -s \`2000\` -i \`Blues%Jazz%Rock%Alternative Rock%Techno%Industrial\` -e images/mp3.eps > cover.ps` |
| 播放音频 CD-ROM？ | **cdp** | `cdp` |
| 对音频 CD-ROM 上的所有音频轨道制作 WAV 录音？ | **cdparanoia** | `cdparanoia -B \`1\`` |
| 使用特效创建两个或更多图形文件的合成图像？ | **combine** | `combine -compose bumpmap image1.jpg image2.jpg combined.jpg` |
| 查看图形文件的详细信息？ | **identify** | `identify -verbose image1.jpg` |

## 声音和图形文件

本节详细介绍以下内容：

- 声音文件类型
- 图形文件类型

## 声音文件类型

下表列出了你通常在 Linux 系统上遇到的声音文件类型，按后缀（扩展名）组织。

### 常见声音文件格式

| 扩展名 | 描述 |
| :--- | :--- |
| .aiff | Apple/Silicon Graphics AIFF 声音 |
| .au | Sun/NeXT AU 声音 |
| .cdr | RAIW，CD-ROM 音频的无符号样本 |
| .cvs | 连续可变斜率调制，用于语音压缩 |
| .voc | Sound Blaster VOC 声音 |
| .wav | Microsoft WAV 声音 |
| .mp3 | MP3 压缩数字音频 |
| .mid .midi | MIDI 声音 |

