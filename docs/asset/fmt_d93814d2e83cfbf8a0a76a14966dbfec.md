
`$cat filename.au>/dev/audio`

如需数百个 m-law 样本，请参阅 http://sunsite.unc.edu/pub/multimedia/sun-sounds。

## AIFF & AIFC

MIME 类型：
`audio/x-aiff` `aiff` `aiff` `aific`

音频交换文件格式 (`AIFF`) 允许以各种采样率存储单声道和多声道采样声音。由于它是一种交换格式，因此很容易转换为其他文件格式。它最广为人知的是一种保持原始录音原色的格式，通常用于不考虑存储空间的高端音频录音应用。该格式最初由 Apple 开发，主要由 Silicon Graphics 和 Macintosh 应用使用。

`AIFF` 文件可能很大。一分钟的 16 位立体声音频可能占用约 10 兆字节。由于原始 `AIFF` 格式不允许压缩音频数据，Apple 引入了 `AIFF-C`（或 `AIFC`）格式，该格式允许存储压缩和未压缩的音频数据。`AIFC` 支持高达 6:1 的压缩率，但是以牺牲文件信号质量为代价的。

大多数支持 `AIFF` 播放的应用程序也支持 `AIFC`。

由于 `AIFF` 支持多种采样率，某些网站选择提供大致等于标准 m-law 文件的 `AIFF` 文件，节省磁盘空间和网络带宽。这些文件通常标记为 1 通道、8 位、8kHz `AIFF` 文件。注意，当降采样时，`AIFF` 文件通常提供 8kHz 的采样率，而不是某些 m-law 文件的 8.013kHz 采样率。

## RIFF WAVE

MIME 类型：
`audio/x-wav` `wav`

这种由 Microsoft 和 IBM 赞助的专用格式资源交换文件格式波形音频 (`.wav`) 在 MS Windows v3.1 中引入，最常用于基于 Windows 的 PC。`WAVE` 文件支持多种编码方法，最常用的是 `ADPCM`（自适应差分码调制），所有 `WAVE` 文件都遵循丰富信息文件格式 (`RIFF`)。如果你觉得这些编码技术听起来很陌生，不要担心——在日常使用该格式时你不需要了解这些内容。

这种格式是微软比的 `AIFF` 格式，因为它支持单声道和多声道采样以及多种采样率。与 `AIFF` 类似，每分钟 44.1kHz 采样率的 16 位采样 `WAVE` 文件大约需要 10MB。因此，音频网站通常提供 8 位、8kHz、单通道版本。

> 提示 在 http://sunisite.unc.edu/pub/multimedia/pc-sounds 可以找到大型 `WAVE` 声音存档。

## MPEG

MIME 类型：
`audio/mpeg` `mp2`

国际标准组织视频专家小组负责当今互联网上常用的压缩标准之一。`MPEG` 解码器专为音频和视频压缩设计，已成为网络用户的喜爱。

## Creative Voice

MIME 类型：
`audio/x-voc` `voc`

Creative Voice (`.voc`) 是使用 Creative Lab Sound Blaster 和 Sound Blaster Pro 卡录制的专用声音文件格式。该格式仅支持最高 44.1kHz 的 8 位单声道音频文件以及22kHz 的立体声文件。

> 提示 Creative Labs 的主页位于 http://creaf.com/

## SND

扩展名 `.snd` 有些歧义。Sun/Next 声音文件在实际上是 m-law 文件时有时用 `.snd` 扩展识别。Macintosh 系统声音也有 `.snd` 扩展，某些 PC 声音也是如此。它们的采样率从 5.5kHz 到 22kHz 不等，11kHz 最流行。

Macintosh `.snd` 文件在 Mac 资源分叉的 Type 字段中被分配为 `SFIL`（声音文件）。这些文件可以由 `AFF/AIF` 样本和/或合成声音组成，这些声音可以利用 System 7 的声音硬件和软件。

## Raw PCM 数据

脉冲编码数据有时用 `.pcm` 扩展名识别，但有时完全没有扩展名。由于文件中没有提供头信息，你通常必须指定波形的采样率、分辨率和通道数。

## MIDI & MOD

网络并非所有的音频文件格式都只执行存储数字化音频单一的功能。在下一节中，我们将讨论两种独特的文件格式，如果你对电子音乐作曲感兴趣，可能会考虑使用它们。

## MIDI

MIME 类型：
```
audio/x-mid mid midi
```
