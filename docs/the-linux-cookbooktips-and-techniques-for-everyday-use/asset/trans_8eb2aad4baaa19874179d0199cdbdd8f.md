

```
$ sox old.wav new.wav phaser 1 .5 4 .5 1 -s RET
```

- 要为文件 `old.wav` 添加相位“呼吸”效果并将输出写入 `new.wav`，请输入：

```
$ sox old.wav new.wav phaser .5 .5 .5 .9 .5 -t RET
```

> 注意：使用大于 .5 的衰减可能会导致反馈。

## 24.2.7 为声音文件添加合唱效果

要为声音文件添加合唱效果，请使用 `chorus`。其选项为音量的“输入增益”和“输出增益”、以毫秒为单位的延迟和衰减、以赫兹为单位的速度，以及以毫秒为单位的合唱深度。指定 `-s` 或 `-t` 用于正弦或三角调制。

- 要为文件 `old.wav` 添加 100 毫秒的合唱效果并将输出写入 `new.wav`，请输入：

```
$ sox old.wav new.wav chorus 1 .5 100 1 1 -t RET
```

- 要为文件 `old.wav` 添加深沉、“外星人般声音”的合唱效果并将输出写入 `new.wav`，请输入：

```
$ sox old.wav new.wav chorus 1 .5 100 1 5 9 -t RET
```

## 24.2.8 为声音文件添加 Vibro-Champ 效果

`vibro` 效果模仿 Fender Vibro-Champ 放大器的效果。将速度以赫兹为单位作为选项给出，最大为 30，并指定 0 到 1 之间的可选深度值，默认为 .5。

- 要为文件 `old.wav` 添加微妙的 Vibro-Champ 效果并将输出写入 `new.wav`，请输入：

```
$ sox old.wav new.wav vibro 1 RET
```

- 要为文件 `old.wav` 添加最大化的 Vibro-Champ 效果并将输出写入 `new.wav`，请输入：

```
$ sox old.wav new.wav vibro 30 1 RET
```

## 24.2.9 反转声音文件

使用 `reverse` 效果来反转声音文件中的声音。

- 要反转文件 `old.wav` 中的声音并将输出写入 `new.wav`，请输入：

```
$ sox old.wav new.wav reverse RET
```

## 24.3 转换声音文件

@sf(Debian): `sox`
@sf(WWW): http://home.sprynet.com/~cbagwell/sox.html
使用 sox 进行大多数声音文件转换。将输入文件名称和要写入的输出文件名称作为参数给出；使用指定输出文件声音格式的文件名扩展名（参见章节 声音文件格式）。

- 要将文件 `new.wav` 转换为音频 CD 格式文件，请输入：

```
$ sox new.wav new.cdr RET
```

此命令写入一个新文件 `new.cdr`，采用音频 CD 格式；原始文件 `new.wav` 不会被更改。

有时您可能需要指定其他选项，例如对于原始音频文件，其中采样率和其他属性必须指定。

- 要将当前目录中的所有原始音频文件转换为音频 CD 格式文件，请输入：

```
$ for i in *.raw RET
{ RET
sox -s -w -c2 -r 44100 $i -x $i.cdr RET
} RET
```

此命令将所有 `.raw` 文件写入名称相同但扩展名为 `.cdr` 的新文件。然后您可以使用 `cdrecord` 用 `.cdr` 文件刻录音频 CD（参见章节 刻录音频 CD-R）。

要将文件转换为特定格式而不使用标准扩展名，请使用 `-t` 选项指定要写入的格式。

- 要将文件 `new.wav` 转换为音频 CD 格式并将输出写入名为 `cd-single` 的文件，请输入：

```
$ sox new.wav -t cdr cd-single RET
```

### 24.3.1 制作 MP3 文件
编码 MP3 文件。

### 24.3.2 将 MP3 转换为其他格式
将 MP3 文件转换为其他格式。

## 24.3.1 制作 MP3 文件

@sf (WWW): http://www.sulaco.org/mp3/

从原始音频或 WAV 格式音频文件制作 MP3 文件的过程称为“编码” MP3 文件；执行此操作的程序是 MP3 编码器。这与其说是录制过程，不如说是一种转换过程：现有音频被转换为 MP3 文件。 （要从自己的录音制作 MP3 文件，请将录音制作成 CD 质量的 WAV 文件，然后再进行转换。）

不幸的是，编码 MP3 的算法是专利化的，所有使用它的软件都必须支付许可费——包括自由软件。这一限制使得人们难以创建自由软件 MP3 编码器，这也是一些自由软件和开源团体倡导开发高质量压缩音频格式以取代 MP3 的原因。一种变通方法以 LAME 的形式出现，“LAME Ain't an MP3 Encoder”。LAME 不是 MP3 编码器，而是一个自由软件补丁文件（参见章节 使用差异报告修补文件），旨在与专利持有者分发的示例源代码一起使用。

这意味着您可以分别下载两者并将它们组合起来，得到一个名为 `not lame` 的工作 MP3 编码器，也许是目前 Linux 上最快的编码器（是的，编码 MP3 是一个缓慢的过程）。当您访问 http://www.sulaco.org/mp3/ 上的 LAME 项目时，您会找到一个链接，可以从澳大利亚的一个站点下载预组装的 `not lame` 二进制文件，在那里专利法不适用。

