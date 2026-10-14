

执行此操作的软件是 MP3 编码器。这与其说是录制过程，不如说是转换过程：将现有音频转换为 MPEG 音频格式。遗憾的是，MP3 编码算法已获得专利，所有使用该算法的软件都必须支付许可费。这一限制意味着，未经许可编写 MP3 编码软件程序是违法的。这也是 MP3 如今逐渐失去人气、被 Ogg Vorbis 音频格式取代的主要原因。与许多计算趋势一样，这一趋势的早期采用者来自 Linux 世界。

## 23.3.2 编码 Ogg 文件

```
Oggenc
DEB: vorbis-tools
RPM: vorbis-tools
WWW: http://www.vorbis.com/
```

使用 `oggenc` 编码 Ogg Vorbis 音频文件。它接受一个音频文件作为参数，并写入一个具有相同基本文件名和 `.ogg` 扩展名的新文件。若要指定不同的文件名，请将所需名称作为 `-o` 选项的参数提供。

⇒ 要从 WAV 文件 `interview.wav` 制作 Ogg Vorbis 文件，请输入：
$ oggenc interview.wav [RET]

此命令会创建一个新文件 `interview.ogg`。

## 23.3.3 将 Ogg 转换为其他格式

要将 Ogg Vorbis 音频文件转换为其他格式，请使用 `ogg123` 并通过 `-d` 选项指定“wav”驱动程序。你作为参数提供给此命令的 Ogg Vorbis 文件将被写入当前目录下名为 `output.wav` 的 WAV 格式文件。

⇒ 要将 Ogg Vorbis 文件 `bobhopehour.ogg` 转换为 WAV 格式，请输入：
$ ogg123 -d wav bobhopehour.ogg [RET]

此命令会在当前目录中写入一个新文件 `output.wav`。通过将输出文件名作为 `-o` 选项的参数来指定输出文件。

⇒ 要将 Ogg Vorbis 文件 `bobhopehour.ogg` 转换为 WAV 格式，并写入名为 `hope1.wav` 的文件，请输入：
$ ogg123 -d wav -o hope1.wav bobhopehour.ogg [RET]

注意：WAV 输出可以使用传统方法进一步转换为其他格式（例如，参见前面的方法）。

如果你想在转换的同时收听文件，可以通过为你所使用的音频系统驱动程序添加额外的 `-d` 选项来实现。

## 23.4 使用其他声音编辑器

Linux 中的声音软件发展迅速，纸质书籍不可能跟上其步伐；你可以通过查看 Dave Phillips 的“Linux 声音与 MIDI 软件”来了解最新进展。该资源提供了最全面、最新的 Linux 相关声音软件列表（参见附录 D [进一步阅读的参考资料]，第 731 页）。

与文本编辑器一样，声音编辑器也种类繁多，从简单的编辑器到高级环境应有尽有。下表列出了一些最流行的编辑器。

### Audacity
带有频谱图显示的音频编辑器。以其速度著称。
DEB: audacity
RPM: audacity
WWW: http://audacity.sourceforge.net/

### Brahms
适用于 KDE 的图形化音乐编辑器，其功能包括乐谱和钢琴卷帘记谱。
DEB: brahms
RPM: brahms
WWW: http://brahms.sourceforge.net/

### DAP
用于编辑声音文件的图形化工具。
RPM: dap
WWW: http://www.cee.hw.ac.uk/~richardk/

### Festival
语音合成系统，可读取英语（英式和美式）、西班牙语和威尔士语的纯文本输入，并将语音输出为声音。
DEB: festival
RPM: festival
WWW: http://www.cstr.ed.ac.uk/projects/festival/

### Freebirth
音序器、低音合成器和采样播放器。
DEB: freebirth
RPM: freebirth
WWW: http://www.hitsquad.com/smm/programs/Freebirth/

### GLAME
被描述为“音频界的 GIMP”的音频编辑器。GLAME 是“GNU/Linux Audio Mechanics”的首字母缩写。
DEB: glame
RPM: glame
WWW: http://glame.sourceforge.net/

### Pure Data
用于实时音频编程的强大系统。
DEB: pd
WWW: http://www-crca.ucsd.edu/~msp/software.html

### Rosegarden
MIDI 音序器、音乐记谱（乐谱）编辑器和音乐作曲编辑器。
DEB: rosegarden
RPM: rosegarden
WWW: http://www.rosegardenmusic.com/

### Tapiir
受老式磁带延迟效果启发的图形化实时音频效果处理器。
DEB: tapiir
WWW: http://www.iua.upf.es/~mdeboer/projects/tapiir/

### XWave
一个简单的声音编辑器，可执行你在 WAV 文件编辑器中预期的基本功能。
DEB: xwave
WWW: http://www.ibiblio.org/pub/linux/apps/sound/editors/

