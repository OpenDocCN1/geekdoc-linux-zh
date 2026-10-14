
# 两个文件之间的差异

当你有两个文件的版本时，了解两个文件之间的差异可能有用。例如，在升级 RPM 时，你的旧配置文件留在原地，新版本的配置文件创建为 `.rpm`。这时，你可以使用 `diff` 命令发现你的配置和新配置之间的差异，以便合并两者。例如：

```
$ diff /etc/apache2/httpd.conf /etc/apache2/httpd.conf.rpm
```

你可以将 `diff` 的输出改为所谓的统一格式（unified format）。统一格式对人类更容易读。它在每个报告的更改块前后添加行，并使用 `+` 和 `-` 显示文件之间的差异。以下命令集创建一个包含数字序列（1-7）的文件 `f1.txt`，创建一个使用 `sed` 修改了其中一个更改的文件 `f2.txt`，并使用 `diff` 命令比较两个文件：

```
$ seq 1 7 > f1.txt              将数字序列发送到 f1.txt
$ cat f1.txt                        显示 f1.txt 的内容
1
2
3
4
5
6
7
$ sed '4/8/' f1.txt > f2.txt      将 4 改为 8 并发送到 f2.txt
$ diff f1.txt f2.txt              显示文件中第 4 行已更改
4
8
$ diff -u f1.txt f2.txt          显示 diff 的统一输出
```

```
--- f1.txt 2007-09-07 18:26:06.000000
+++ f2.txt 2007-09-07 18:26:09.000000
@@ -1,7 +1,7 @@
1
2
3
-4
+8
5
6
7
```

`diff -u` 输出显示了修改日期和时间等信息。`diff` 命令可以为你提供另一种视角。`diff` 命令可以交互式地合并两个文件的输出，如下所示：

```
$ diff f1.txt f2.txt
1
2
3
4
5
6
7
```

`diff` 主题的另一个变体是 `vimdiff`，它并排打开两个文件并用颜色列出差异。同样，`gdiff` 也打开两个文件。

`diff -u` 的输出可以交给 `patch` 命令。`patch` 命令接收旧文件和 diff 文件作为输入并输出补丁后的文件。按照上面的示例，我们使用两个文件之间的 `diff` 命令生成补丁，然后将补丁应用到第一个文件：

```
$ diff -u f1.txt f2.txt > patchfile.txt
$ patch f1.txt < patchfile.txt      补丁文件 f1.txt
$ cat f1.txt
1
2
3
4
8
```

有很多 OSS 开发者（包括内核开发者）分发他们的代码补丁。`patch` 和 `diff` 命令也可以在整个目录树上运行。然而，这种用法超出了本书的范围。

# 使用 awk 和 cut 处理列

另一个巨大的文本处理工具是 `awk` 命令。`awk` 命令是一门完整的编程语言。虽然使用 `awk` 命令可以做更多，但以下示例向你展示了与提取文本列的一些技巧：

```
$ ps aux | awk '{print $1,$11}'
$ ps aux | awk '/francois/ {print $11}'
$ ps aux | awk '{print $11}'      同上
```

默认情况下，`awk` 命令假设列之间的分隔符是空格。你可以通过 `-F` 选项指定不同的分隔符：

```
$ awk -F: '{print $1,$5}' /etc/passwd 使用冒号分隔符打印列
```

你可以使用 `cut` 命令获得类似的结果。与之前的 `awk` 示例一样，我们指定冒号作为列分隔符来处理 `/etc/passwd` 文件：

```
$ cut -d:- -f1,5 /etc/passwd 使用冒号分隔符打印列
```

`cut` 命令也可以用于字段范围。以下命令列出 `/etc/passwd` 的 1 到 5 列：

```
$ cut -d:- -f1-5 /etc/passwd 显示第 1 到 5 列
```

与其使用连字符（-）表示数字范围，你可以可以使用它来打印从特定列数及以上的所有列。以下命令显示 `/etc/passwd` 中从第 5 列开始的所有列：

```
$ cut -d:- -f5- /etc/passwd 显示第 5 列及之后的列
```

# 第5章：文本处理

当列由不等的空格分隔时（例如 `ps` 命令的输出），我们倾向于使用 `awk` 命令。当处理由逗号（）或冒号（；）分隔的文件时（例如 `/etc/password` 文件），我们倾向于使用 `cut` 命令。

## 将文本文件转换为不同格式

Unix 世界文本文件使用的行符（`\n`）与 DOS/Windows 世界使用的行符（`\r\n`）不同。你可以使用 `od` 命令查看文件中这些特殊字符：

```
$ od -c -t x1 myfile.txt
```

因此，为了确保文件从一个环境复制到另一个环境时能够正常显示，必须进行转换。以下是一些示例：

- `unix2dos` < `myfile.txt` > `mydosfile.txt`
- `cat` `mydosfile.txt` | `dos2unix` > `unixfile.txt`

上述 `unix2dos` 示例将 Linux 或 Unix 纯文本文件（`unixfile.txt`）转换为 DOS 或 Windows 文本文件（`mydfile.txt`）。`dos2unix` 示例演示了将 DOS/Windows 文件转换为 Linux/Unix 文件的可能性。你需要安装 `unix2dos` 包来获取这些命令。

## 总结

Linux 和 Unix 系统传统上使用纯文本文件进行系统配置、文档、命令输出以及许多形式的信息存储。因此，创建了许多命令来搜索、编辑和其他处理纯文本文件。即使在今天拥有 GUI 界面的情况下，处理纯文本文件的能力对于成为 Linux 高手至关重要。

本章探索了 Linux 中处理纯文本文件的一些常用命令。这些命令包括文本编辑器（如 `vi`、`nano` 和 `joe`），以及可以编辑流式数据的命令（如 `sed` 和 `awk` 命令）。还有用于排序排序（`sort`）、计数文本（`wc`）和翻译字符（`tr`）的命令。

# 第6章：多媒体操作

如果你只需要播放歌曲或将图像或音频文件转换为不同的格式，无需使用 GUI 工具。处理多媒体文件（音频或图像）有很多命令，如果你发现需要批量处理多媒体文件，这些命令非常快速高效；将你转换单个文件的命令添加到脚本中，即可对许多文件重复该过程。

本章侧重于通过 shell 处理音频和数字图像文件的工具。

## 处理音频

Linux 系统提供了许多可以处理数十种音频格式文件的命令。可以使用 `oggplay`、`mpgplay` 和 `play` 等命令来听音频文件。还有从 CD 刻录歌曲并对其进行高效编码的命令。甚至有命令让你将音频流到任何网络以听你的播放列表。

本章内容：
- 使用 `play`、`oggplay` 和 `mpgplay` 播放音乐
- 使用 `alsamixer` 调整音频
- 使用 `cd` 刻录音乐
- 使用 `ogg`、`lame` 编码音乐
- 使用 `icecast` 流传输音乐
- 使用 `sox` 转换音频文件
- 使用 `convert` 数字图像

## 播放音乐

根据你想播放的音频格式，Linux 有多种命令行播放器。`play` 命令（基于后文介绍的 `sox` 功能）可以自由播放音频文件。使用 `oggplay` 播放流行的开源格式，包括 Ogg Vorbis (FLAC) 和 Speex 文件。通过第三方仓库提供的 `mpgplay` 播放器在播放 MP3 音乐方面非常流行。

使用 YaST 安装 `sox` 包。输入 `play -h` 查看用于 `play` 的音频格式和效果：

```
$ play -h
```

```
支持的文件格式：：aif aiffs alsa au cdda cdr cvdat dms fscm hcm maud nist null ossdsp raw sb sl ndt sou tw u4 um vorbis vox wav
```

```
支持的效果：：all band chorus deither echo equalizer fade flanger highpass lowpass mixer noisered pan polyphase repeat resample reverb silence speed stretch synth treble tremolo trim
```

以下是使用这些命令播放文件的示例：

```
$ play inconceivable.wav 播放 WAV 文件（可能从 CD 刻录）
$ play *.wav 播放目录中的 WAV 文件（默认数量为全部）
$ play hi.au AU 文件，调低音量（可以降低失真）
```
