
其中 `scsibus` 是 SCSI 总线的编号（主总线为 0），`target` 是 SCSI 目标 ID（通常为 1 到 6 之间的数字），`lun` 是其 LUN 编号（几乎总是 0）。

使用 `speed` 参数设置写入数据的速度系数：输入 `speed=2` 指定双倍速度，或输入 `speed=4` 指定四倍速度。

使用 `-dummy` 选项在关闭驱动器激光的情况下运行，因此不会进行实际刻录；这在你首次使用 CD-R 驱动器时很有用，并且

> ² 你也可以使用此工具配合 CD-RW 驱动器并写入 CD-RW 光盘。

需要测试你的配置以确保设置正确。另一个有用的选项是 `-v`，它提供更详细的输出信息。

将要刻录的音频文件名作为 `-audio` 选项的参数给出，按其应出现在光盘上的顺序排列。文件以 CD-DA CD 音频格式写入，并且应包含 16 位立体声，每秒 44,100 个采样（`.cdr` 或 `x.cdda` 文件满足此标准）。

### 使用方法

- 要将文件 `symphony.cdr` 刻录到主 SCSI 总线上目标 ID 为 2 的 CD-R 驱动器中的光盘，输入：

```
$ cdrecord dev=0,2,0 -audio symphony.cdr [RET]
```

- 要以双倍速度将当前目录中以 `.cdr` 扩展名结尾的所有文件刻录到主 SCSI 总线上目标 ID 为 2 的 CD-R 驱动器中，并给出详细输出，输入：

```
$ cdrecord dev=0,2,0 speed=2 -v -audio *.cdr [RET]
```

- 要对文件 `symphony.cdr` 在主 SCSI 总线上目标 ID 为 6（LUN 1）的 CD-R 驱动器中进行测试刻录，输入：

```
$ cdrecord dev=0,6,1 -dummy -audio symphony.cdr [RET]
```

当你为文件使用通配符时，如上面的第二个示例，shell 会按字母顺序展开文件。要按特定顺序写入一组音轨而不指定所有名称作为参数，请重命名它们，使其名称以对应你想要写入顺序的数字开头（参见 Recipe 5.5 [Moving Files and Directories]，第 144 页）。

例如，如果你有三个文件 `morning-song.cdr`、`midday-song.cdr` 和 `evening-song.cdr`，并且你想按该顺序写入它们，请将文件重命名为 `01-morning-song.cdr`、`02-midday-song.cdr` 和 `03-evening-song.cdr`。否则，如果你将它们指定为 `*.cdr`，shell 会对其名称进行排序，因此它们将被刻录到 CD-R 的顺序为 `evening-song.cdr`、`midday-song.cdr` 和 `morning-song.cdr`——这与预期完全相反！

要写入包含数据和音频音轨的光盘，首先指定数据音轨的文件（它应包含采用 ISO 9660 或 Rock Ridge 格式的文件系统映像），然后使用 `-audio` 选项跟上要使用的音频音轨的名称。 resulting CD-R 既可作为数据 CD 挂载，也可在音频 CD 播放器上播放（光盘上的第一音轨，即数据音轨，在播放音频时将被跳过）。

### 数据与音频混合刻录示例

要将数据轨道的 `band-info` 以及当前目录下所有扩展名为 `.cdda` 的音频轨道刻录到主 SCSI 总线上的目标 ID 为 2 的 CD-R 驱动器，请键入：

```
$ cdrecord dev=0,2,0 band-info -audio *.cdda [RET]
```

**NOTES**：刻录音频 CD 时，应尽可能减少正在运行的进程。如果 `cdrecord` 即使短暂地暂停以让系统调度其他进程，CD-R 可能会被毁坏！因此，在 CD-R 刻录过程中，建议避免在控制台之间切换——或在运行 X 时在窗口之间切换。

## 22.4 使用其他音频光盘工具

下表列出了一些可用于音频光盘的其他工具和应用程序。

- `Ccdcd` 从命令行播放 CD。

  DEB: `cccd`

  RPM: `cccd`

  WWW: http://cccd.undergrid.net/

- `Cdinfo` 显示有关音频 CD 的信息。

  WWW: http://bytesex.org/misc.html

- `CDlabelgen` 为光盘生成标签和正面插页卡。

  DEB: `cdlabelgen`

  RPM: `cdlabelgen`

  WWW: http://tinyurl.com/3bty3

- `Cdp` 在终端中播放音频 CD；它包含命令行和全屏控制台模式。

  RPM: `cdp`

  WWW: http://cdp.sourceforge.net/

- `Groovy CD Player` 播放音频 CD，配有圆润的“groovy”显示数字面板，瞬间吸引那些怀念 70 年代流行文化的用户。

  DEB: `groovycd`

- `Player`

  控制台 CD 播放器，可以读取 WorkMan 或 CDDB 数据库并输出 PostScript CD 音频封面。

  WWW: http://bytesex.org/misc.html

- `WorkBone`

  在终端中播放音频 CD，并允许你在曲目播放时向前或向后跳过曲目。

  DEB: `workbone`

  WWW: http://tinyurl.com/2ul7j

- `WorkMan`

  在 X 中播放音频 CD，具有图形界面，模仿物理 CD 播放器的前面板。

  DEB: `workman`

  RPM: `workman`

  WWW: http://tinyurl.com/26eof

- `XCDRoast`

  `cdrecord` 工具的图形前端，用于在 X 中使用。

  DEB: `xcdroast`

  RPM: `xcdroast`

  WWW: http://www.xcdroast.org/

## 23. 编辑声音文件

存在各种各样的工具和应用程序来编辑声音文件。本章描述了一些此类工具，并给出剪切和粘贴声音文件、应用效果和滤镜以及在格式之间转换声音文件的方法。

### 23.1 操作声音文件中的选区

`Snd`

DEB: `snd`

RPM: `snd`

WWW: http://www-ccrma.stanford.edu/software/snd/

`Snd` 是 X 的声音文件编辑环境，其目标是让声音如同 Emacs 之于文本。（它也使用 Emacs 风格的键绑定。）

你可以在 `/usr/doc/snd` 目录中找到它的完整手册；本节解释如何使用 `Snd` 来处理声音文件中的选区。

要打开 `Snd` 中的声音文件，将要打开的文件名作为参数传递给 `snd`。

要打开声音文件 `mixdown.wav`，请键入：

```
$ snd mixdown.wav RET
```

![](img/be7f02611e5cefde1a18c788fede22f7_520_0.png)

图 23-1. `Snd` 中加载了文件。

此命令以 `mixdown.wav` 这一 WAV 文件启动 `Snd`，如图 23-1 所示。

在 `Snd` 中选择声音文件的一部分与在 Emacs 中选择文本类似；你可以通过在鼠标上左键单击并拖动跨越区域来标记 `Snd` 中声音文件或录音的一部分。你拖过的区域会被着色并称为选区。一旦你选择了声音的一部分，你选择的任何效果都将作用于该选区。你还可以将正在编辑的声音的选区剪切并粘贴到其他声音缓冲区中。

`xwave` 工具（以及许多其他工具，很可能）具有类似的功能和能力（参见食谱 23.4 [使用其他声音编辑器]，第 496 页）。

#### 23.1.1 剪切声音文件的一部分

要在 `Snd` 中编辑的声音文件中剪切出一部分，首先通过左键单击并拖动来选择该部分，然后从 `Edit` 菜单中选择 `Cut`，有点像裁剪图像文件。

#### 23.1.2 将选区粘贴到声音文件中

在 `Snd` 中将剪切的声音选区粘贴到不同的声音缓冲区中，方法是打开新缓冲区，在目标缓冲区中左键单击，然后从 `Edit` 菜单中选择 `Paste`。你的最近选区将被粘贴到你在声音缓冲区中单击的位置。

#### 23.1.3 将声音文件混合在一起

要在 `Snd` 中将不同的音频文件作为多轨混合在一起，从 `File` 菜单中选择 `Mix` 并指定用作各个音轨的文件。

### 23.2 应用声音效果

`SOund eXchange`

DEB: `sox`

RPM: `sox`

WWW: http://sox.sourceforge.net/

“Sound eXchange” 工具 `sox` 是一个声音样本转换器。它读取声音作为文件或标准输入，并将声音输出到文件或标准输出，同时在两者之间进行转换。你可以使用 `sox` 将声音文件从一种格式转换为另一种格式，或对声音应用特殊效果。本节描述了你可以用 `sox` 对声音文件应用的一些特殊效果。

应用效果时，原文件永远不会被更改。你必须指定输出文件，或使用连字符（`-`）来表示标准输出。将输出格式指定为 `-t` 选项的参数。你只能用每个 `sox` 命令应用一种效果；因此，要给声音文件同时添加回声和混响，你就需要发出两个 `sox` 命令。
