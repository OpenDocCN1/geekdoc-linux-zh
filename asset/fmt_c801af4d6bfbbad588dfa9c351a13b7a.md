
| `%b` | 文件大小。 |
| `%d` | 目录。 |
| `%e` | 文件扩展名。 |
| `%f` | 文件名。 |
| `%h` | 高度。 |
| `%m` | Magick。 |
| `%p` | 页码。 |
| `%s` | 场景编号。 |
| `%t` | 文件名顶部。 |
| `%w` | 宽度。 |
| `%x` | X 分辨率。 |
| `%y` | Y 分辨率。 |
| `\n` | 换行符。 |
| `\r` | 回车符。 |
| `--compress type` | 设置图像压缩类型。可选值有：BZip、Fax、Group4、JPEG、LZW、RunlengthEncoded、None、Zip。 |
| `--contrast`，`+contrast` | 增强 (`--contrast`) 或降低 (`+contrast`) 图像对比度。 |
| `--crop 宽 x 高` | 在指定的宽度和高度处裁剪图像。 |
| `--cycle n` | 按指定量（*n*）移动图像颜色映射。 |
| `--density <宽>x<高>` | 设置图像的垂直和水平分辨率（像素）。 |
| `--density 宽 x 高` | 将图像的垂直和水平分辨率设置为指定的宽度和高度（像素）。 |
| `--depth value` | 设置图像的颜色深度（8 或 16）。 |
| `--despeckle` | 减少图像中的斑点。 |
| `-dispose type` | 使用指定类型的 GIF 处置。可选值有：<br>0 无处置。<br>1 帧之间不处置。<br>2 用背景色覆盖帧。<br>3 用前一帧覆盖。 |
| `-draw string` | 用一个或多个图元为图像添加注释。图元包括以下项：circle、color、ellipse、fillCircle、fillEllipse、fillPolygon、fillRectangle、image、line、matte、point、polygon、rectangle 和 text。 |
| `-font 字体` | 设置普通文本的字体。 |
| `-frame 宽 × 高 + 外部斜边宽度 + 内部斜边宽度` | 使用带有指定宽度、高度、外部斜边宽度和内部斜边宽度的装饰性边框。 |
| `-gamma n` | 使用指定级别（*n*）的伽马校正，其中 *n* 是从 0.8 到 2.3 的级别。 |
| `-geometry 宽 × 高 [ % | ! | +− × 偏移量 | +− − y 偏移量 ]` | 按指定的最大宽度和高度创建图像，同时保持原始图像的宽高比。附加 `%`（百分号）可按百分比调整宽度和高度。要强制使用指定的尺寸，请附加 `!`（感叹号）。 |
| `-gravity type` | 设置图像引力朝向的方向。可选值有：NorthWest、North、NorthEast、West、Center、East、SouthWest、South 和 SouthEast。 |
| `-interlace type` | 设置交织方案类型。可选值有：None、Line、Plane 或 Partition。 |
| `-label string` | 使用 *string* 作为标签。 |
| `-matte` | 如果图像具有 matte 通道信息，则存储该信息。 |

#### 选项（续）

| 使用此选项 | 以执行此操作 |
| :--- | :--- |
| `--mode type` | 设置蒙太奇类型。选项包括 Frame、Unframe（默认）或 Concatenate。 |
| `-monochrome` | 将图像转换为黑白。 |
| `-page width x height [ % \ ! ]` | 设置图像画布的像素宽度和高度。追加百分号以按百分比调整宽度和高度。追加感叹号以强制使用确切尺寸。Postscript 页面的可选尺寸如下： |

| 页面尺寸 | 宽度 | 高度 |
| :--- | :--- | :--- |
| 11x17 | 792 | 1224 |
| A0 | 2380 | 3368 |
| A1 | 1684 | 2380 |
| A2 | 1190 | 1684 |
| A3 | 842 | 1190 |
| A4 | 595 | 842 |
| A4Small | 595 | 842 |
| A5 | 421 | 595 |
| A6 | 297 | 421 |
| A7 | 210 | 297 |
| A8 | 148 | 210 |
| A9 | 105 | 148 |
| A10 | 74 | 105 |
| ArchA | 648 | 864 |
| ArchB | 864 | 1296 |
| ArchC | 1296 | 1728 |
| ArchD | 1728 | 2592 |
| ArchE | 2592 | 3456 |
| B0 | 2836 | 4008 |
| B1 | 2004 | 2836 |
| B2 | 1418 | 2004 |
| B3 | 1002 | 1418 |
| B4 | 709 | 1002 |
| B5 | 501 | 709 |
| C0 | 2600 | 3677 |
| C1 | 1837 | 2600 |
| C2 | 1298 | 1837 |
| C3 | 918 | 1298 |
| C4 | 649 | 918 |
| C5 | 459 | 649 |
| C6 | 323 | 459 |
| Fisa | 612 | 936 |
| Fise | 612 | 936 |
| HalfLetter | 396 | 612 |
| Ledger | 1224 | 792 |
| Legal | 612 | 1008 |
| Letter | 612 | 792 |
| LetterSmall | 612 | 792 |

##### 选项

- `-pen color`
  - 设置字体颜色或不透明颜色。
- `-pointsize point`
  - 为 PostScript 字体使用指定的磅值（point）。
- `-quality value`
  - 设置 JPEG、MIFF 或 PNG 的压缩级别。
- `-rotate degrees < | >`
  - 向左（<）或向右（>）旋转图像指定的度数。
- `-scene n`
  - 指定图像场景编号 n。
- `-shadow`
  - 在磁贴下方添加阴影以模拟深度。
- `-sharpen factor`
  - 按指定系数（0.0–99.9%）锐化图像。
- `-size width x height`
  - 当无法自动获取时，设置图像的宽度和高度。
- `-texture filename`
  - 使用指定文件名中找到的纹理作为图像背景。
- `-tile width x height`
  - 设置合成图像中磁贴的宽度和高度。
- `-transparency color`
  - 使指定颜色透明。
- `-treedepth 0 | 1`
  - 将树深度设置为 0 或 1。
- `-verbose`
  - 显示所有消息。

#### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `montage image1.jpg image2.jpg` | 创建包含 `image1.jpg` 和 `image2.jpg` 的蒙太奇。 |

#### mpg123

`mpg123 [ option | filename | URL ]`

在默认音频设备上播放由 *filename* 或 *URL*（网络地址）指定的 MP3 音频文件。对于 *filename*，您可以指定由空格分隔的文件列表、shell 模式（参见第 4 章中的“Shell Patterns”部分）或 URL。要停止播放当前文件并跳至下一个，请按下 `Ctrl + C`。要停止播放并退出，请快速连续按下两次 `Ctrl + C`。要播放 WAV、AU 和其他采样声音，请参阅 `play`。要播放 MIDI 声音，请参阅 `playmidi`。

##### 选项

| 使用此选项 | 以执行此操作 |
| :--- | :--- |
| `-t`, `-test` | 测试模式（无音频输出）。 |
| `@ filename`, `-list filename` | 从指定的 filename 获取输入，该 filename 可以是文件名、shell 模式（参见第 4 章中的“Shell Patterns”部分）或 URL。 |
| `-0`, `-single0`, `-1`, `-single1` | 仅播放左声道（0）或右声道（1）。仅适用于 MPEG 流。 |
| `-2`, `-2to1`, `-4`, `-4to1` | 按指定系数降低采样率。 |
| `--8bit` | 强制 8 位输出。 |
