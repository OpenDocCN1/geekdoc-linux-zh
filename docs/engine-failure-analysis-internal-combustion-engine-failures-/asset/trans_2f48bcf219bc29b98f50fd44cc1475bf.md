

## 选项（续）

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-p, percentage` -- `set-pitch percentage` | 按指定百分比改变音调。 |
| `-P n, -set-overlap n` | 设置用于抖动的校正重叠扇区数 (n)。 |
| `-q, -quiet` | 隐藏消息。 |
| `-R, -dump-rates` | 显示可能的转储速率。 |
| `-r n, -rate n` | 将采样率设置为每秒 n 个样本。 |
| `-s, -stereo` | 以立体声录制。 |
| `-S n, -speed-select n` | 将 CD-ROM 设置为速度 n。 |
| `-T, -deemphasize` | 消除输入样本中的预加重效果。 |
| `-t start track[ +end track ], -track start track[ +end track ]` | 指定起始曲目，以及可选的结束曲目。 |
| `-v n, -verbose-level n` | 设置详细程度，从 0（隐藏消息）到 63（最大）。 |
| `-V, -verbose-SCSI` | 启用控制台中的 SCSI 命令日志记录。 |
| `-w, -wait` | 在录制前等待信号。 |
| `-x, -max` | 设置最高 CD-ROM 质量。 |

## 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `cdda2wav -I generic_scsi -D0,4,0 -t1+5` | 读取指定 SCSI CD-ROM 驱动器（总线 0，ID 4，LUN 0）上的曲目 1 到 5，并将 WAV 文件写入工作目录。 |

## cdlabelgen

`cdlabelgen -c title -s subtitle [ option ]`

创建用于打印 CD-ROM 宝石盒前面板和托盘卡的 PostScript 文件。此实用程序需要 Perl 5.003 或更高版本。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-c string` | 使用指定的字符串设置 CD-ROM 的分类。 |
| `-b` | 抑制托盘卡上铭牌的打印，以便为超过 192 项直至 256 项留出空间。 |
| `-t template` | 指定要使用的模板。 |
| `-D` | 抑制日期打印。 |
| `-d \| string` | 将日期设置为今天，或使用指定的字符串。 |
| `-a filename` | 使用指定的文件名（.eps 文件）在封面上打印。 |
| `-E filename` | 使用指定的文件名（.eps 文件）在托盘卡上打印。 |
| `-f filename` | 使用 *filename* 作为项目名称的来源。 |
| `-h` | 显示可用选项。 |
| `-l list` | 在 CD 的托盘卡上打印项目列表。该列表应由以百分比 (%) 分隔符分隔的项目组成。 |
| `-o filename` | 打印到指定的文件名。 |
| `-S n` | 将封面图形文件缩放到比例 *n*。 |
| `-s string` | 指定 CD-ROM 的子类别。 |
| `-T n` | 将托盘卡图形文件缩放到比例 *n*。 |
| `-w` | 启用托盘卡上打印项目的自动换行。 |

### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `cdlabelgen -c 'My Favorites' -s '2000' -l 'Blues%Jazz%Rock%Alternative Rock%Techno%Industrial' -e images/mp3.eps > cover.ps` | 创建一个名为 `cover.ps` 的文件，其中包含 `cdlabelgen` 的指定输出。 |

## cdp

```
cdp [ option ] [ play track ]
```

启动音频 CD-ROM 的交互式文本模式播放器。要使用此实用程序，必须将 CD-ROM 设备配置为可通过 `/dev/cdrom` 访问。如有必要，请切换到 `/dev` 并创建一个指向实际 CD-ROM 设备的符号链接（参见第 5 章中的 `ln -s`）。要使用此实用程序，请按下 NumLock 键，并使用数字小键盘命令（参见本节中的命令表）控制音频 CD-ROM。通过添加 `play` 后跟一个曲目编号（整数），可以立即开始播放。该实用程序将从指定曲目开始播放。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-h` | 显示可用选项。 |
| `-l` | 在开始之前等待初始化。 |
| `-n` | 抑制自动播放模式。 |

### 命令

| 使用此命令 | 执行此操作 |
| :--- | :--- |
| `9` | 播放。 |
| `0` | 退出而不停止播放。 |
| `1` | 在当前曲目内后退。 |
| `2` | 退出并停止播放。 |
| `3` | 在当前曲目内前进。 |
| `4` | 转到上一曲目。 |
| `5` | 再次播放。 |
| `6` | 转到下一曲目。 |
| `7` | 停止播放。 |
| `8` | 暂停或恢复播放。 |
| `c` | 编辑 CD-ROM 名称。按 Enter 键恢复菜单。 |
| `Enter` | 编辑当前曲目的名称。 |
| `Right arrow (→)` | 转到下一个项目。 |
| `Left arrow (←)` | 转到上一个项目。 |
| `Up arrow (↑)` | 暂停。 |
| `Down arrow (↓)` | 退出。 |

### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `cdp` | 打开交互式 CD-ROM 音频播放器。 |
| `cdp play 5` | 打开交互式 CD-ROM 音频播放器并开始在曲目 5 上播放。 |

## cdparanoia

`cdparanoia [option] span [filename]`

从音频 CD-ROM 读取音频轨道，并将数据写入 WAV、AIFF、AIFF-C 或 RAW 格式文件。如果未指定文件名，该实用程序将在工作目录中写入自动命名的文件。默认情况下，程序以立体声采样 CD-ROM 音频，采样率为每秒 44,100 个周期。对于 *span*，使用 *begin* [hh:mm:ss:sectors]-*end* [hh:mm:ss:sectors] 格式指定轨道，其中 *begin* 和 *end* 是曲目编号，hh:mm:ss:sectors 对应于轨道计时（hh:mm:ss）和扇区。要录制整个光盘，指定 *span* 为 1-（1 后跟连字符）。

另请参阅 *cdda2wav*。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-a, --output-aifc` | 以非压缩的 Apple AIFFC 格式输出数据。 |
| `-B, --batch` | 在轨道边界处拆分多个轨道的输出。 |
| `-C, --force-cdrom-big-endian` | 将 CD-ROM 驱动器视为大端设备。 |
| `-c, --force-cdrom-little-endian` | 将 CD-ROM 驱动器视为小端设备。 |
| `-d device, --force-cdrom-device device` | 从指定设备读取，而不是从遇到的第一个驱动器读取。 |
| `-e, --stderr-progress` | 强制将进度信息输出到 stderr。 |
| `-f, --output-aiff` | 以 Apple AIFF 格式输出数据。 |
| `-g device, --force-generic-device device` | 与 -d 一起使用以指定设备。 |
| `-h, --help` | 显示可用选项。 |
| `-n, --force-default-sectors n` | 强制接口后端每次读取 n 个扇区进行原子读取。 |
| `-p, --output-raw` | 以 RAW 格式输出无头数据，为主机字节顺序的交错采样 16 位 PCM 数据。 |
| `-Q, --query` | 检测 CD-ROM 驱动器并报告信息。 |
| `-q, --quiet` | 隐藏程序消息。 |
| `-R, --output-raw-big-endian` | 以 RAW 格式输出无头数据，为大端（MSB 优先）字节顺序的交错采样 16 位 PCM 数据。 |
| `-r, --output-raw-little-endian` | 以 RAW 格式输出无头数据，为小端（LSB 优先）字节顺序的交错采样 16 位 PCM 数据。 |
| `-S n, -force-read-speed n` | 使用速度 *n* 读取 CD-ROM 驱动器。 |
| `-s, -search-for-drive` | 强制搜索 CD-ROM 驱动器。 |
| `-v, -verbose` | 显示所有消息。 |
| `-V, -version` | 显示版本号。 |
| `-W, -disable-scratch-repair` | 禁用划痕补偿。 |
| `-w, -output-wav` | 以 WAV 格式输出数据。 |
| `-X, -disable-scratch-detection` | 在验证期间禁用划痕补偿。 |
| `-Y, -disable-extra-paranoia` | 禁用读内数据验证。 |
| `-Z, -disable-paranoia` | 禁用数据验证和纠错功能。 |

### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `cdparanoia -B "1-"` | 从曲目 1 开始，将整张 CD-ROM 音频光盘制作为 WAV 文件。将每个曲目放入其自己的磁盘文件中。 |
| `cdparanoia -B "-4"` | 将曲目 1 到 4 制作为 WAV 文件（-4 表示实用程序应从 CD-ROM 开始处启动）。将每个曲目放入其自己的磁盘文件中。 |
| `cdparanoia -B "5-8"` | 将曲目 5 到 8 制作为 WAV 文件。将每个曲目放入其自己的磁盘文件中。 |

## combine

`combine [ option ] source image1 source image2 [ mask ] combined image`

将两个或多个图形文件（由 *source image1*、*source image2* 指定）合并为一个合成图像（*combined image*）。可以指定多种组合类型并添加特殊效果。使用 *-compose* 选项指定组合效果。要创建包含两个或更多独立图块的合成图像，请参阅 *montage*。此实用程序是 ImageMagick 软件包的一部分，可在 http://www.imagemagick.org 下载。

另请参阅 *convert*、*identify*、*mogrify*。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `-blend percentage` | 按指定百分比混合两个图像。 |
| `-colors n` | 在图像中使用 n 种颜色。 |
| `-colorspace type` | 指定颜色空间类型。有效值为 GRAY、OHTA、RGB、Transparent、XYZ、YCbCr、YIQ、YPbPr、YUV 或 CMYK。默认为 RGB。 |
| `-comment "string"` | 使用指定字符串注释图像。务必用双引号包围字符串。 |
| `-compose type` | 指定组合类型。有效值为： |
| | - **add**：图像数据之和加上溢出回绕。 |
| | - **atop**：源图像 2 遮挡源图像 1，但合成图像被修剪为源图像 1 的大小。 |
| | - **bumpmap**：源图像 1 由相同图像着色。 |
| | - **difference**：源图像 2 减去源图像 1 的结果。 |
| | - **in**：源图像 2 遮挡源图像 1。 |
| | - **minus**：源图像 2 减去源图像 1。 |

