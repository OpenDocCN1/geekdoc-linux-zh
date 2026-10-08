
标签: `packers` (`Prev Q`), `upx` (`Prev Q`) (`Next Q`)

# 反汇编器 (Disassemblers)

## 问题

Q: 递归遍历 (`Recursive Traversal`) 中使用的算法是什么？

标签: `disassemblers` (`Prev Q`)

反汇编二进制代码是一个困难的话题，但目前工具中似乎只有两种（幼稚的）算法被广泛使用。

- 线性扫描 (`Linear Sweep`)：基础算法，获取所有标记为代码的节，并通过按顺序读取后续指令来对其反汇编。
- 递归遍历 (`Recursive Traversal`)：通过记录调用（`call`）何时发生以及何处发生来改进线性扫描，并在遇到 `ret` 时返回上一次调用。

然而，对这些算法的描述非常模糊。在现实工具中，谁能提供这些算法更真实的描述？

标签: `disassemblers` (`Prev Q`)

用户: `perror`

`perror` 的回答

反汇编二进制代码是一个困难的话题，但目前工具中似乎只有两种（幼稚的）算法被广泛使用。

- 线性扫描：基础算法，获取所有标记为代码的节，并通过按顺序读取后续指令来对其反汇编。
- 递归遍历：通过记录调用（`call`）何时发生以及何处发生来改进线性扫描，并在遇到 `ret` 时返回上一次调用。

然而，对这些算法的描述非常模糊。在现实工具中，谁能提供这些算法更真实的描述？

标签: `winapi` (`Prev Q`)

# 壳器 (Packers)

## 问题

Q: 如何防止对 UPX 加壳的可执行文件执行 `upx -d` 操作？

标签: `packers` (`Prev Q`) `upx` (`Prev Q`) (`Next Q`)

我最近读了 Ange 发的一封推文，其中提到了一种在调用 `-d`（解压缩）选项时，可以欺骗 UPX 的技术。

我想知道它是如何工作的，以及通过什么技术可以防止 UPX 加壳的可执行文件通过 `upx -d` 被解压（如果在 Linux 和 Windows 上都可行的话）。

标签: `packers` (`Prev Q`), `upx` (`Prev Q`) (`Next Q`)

用户: `perror`

`ange` 的回答

UPX 不会检查解壳存根（unpacking stub）的完整性，它只是盲目地从存储的信息中恢复数据，而不是从实际执行中恢复。

由于 UPX 是开源且有文档的（带注释的 IDB），很容易修改它并执行一些操作（如反调试、补丁、解密、跳转到真实入口点……），这些操作在执行 `upx -d` 时会丢失。

这种 UPX 破解手段在恶意软件中并不罕见。

`blabb` 的回答

欺骗 `-d` 可能非常简单，只需一个字节，这里有一个小示例。

打包 MS-Windows 标准的 `calc.exe`，用十六编辑一个字节，结果得到一个无法通过 `upx -d` 解包的可执行文件（这并没有损坏 exe，exe 可以运行并可以手动解包）。只有使用 `-d` 选项才会生效。

- 1. 创建一个新文件夹 `foolpx`：

```
foolux:\-md foolpx
```

- 2. 复制 `calc.exe`：`copy c:\WINDOWS\system32\calc.exe foolpx\updexcalc.exe`

```
重命名的 calc.exe

已复制 1 个文件。
```

- 3. 打包重命名的 `calc.exe`：

```
foolux:\.upx .foolpx\updexcalc.exe

Ultimate Packer for Executables

Copyright (C) 1996 - 2011

UPX 3.08w Markus Obermer, Laszlo Molnar & Jan Reiser      Dec 12th 2011
```

| 文件大小 | 比例 | 格式 | 名称 |
| --- | --- | --- | --- |
| 114688 | 56832 | 49.55% | win32/pe | updexcalc.exe |

已打包 1 个文件。

- 4. 创建一个已打包的 `calc.exe` 副本，用于十六编辑和文件比较。差异在于 PE 头部中名为 `upx0` 且链到 `BPX0` 的节中有 1 个字节的差异：

```
foolpix:\\foolpix\updexcalc.exe .\foolpix\modupxdexcalc.exe

已复制 1 个文件。

foolpix:\fc .\foolpix\updexcalc.exe .\foolpix\modupxdexcalc.exe

正在比较文件 .FOOLUPX\updexcalc.exe .FOOLUPX\MODUPDEXCALC.EXE

00001EB: 55 42
```

- 5. 使用 `-d` 选项解压文件。其中一个会被解包，另一个将不会解包：

```
foolpix:\>upx -d .\foolpix\modupxdcalc.exe

Ultimate Packer for executables

Copyright (C) 1996-2011

UPX 3.0 Markus Obermer, Laslo Molnar & John Reiser Dec 12th 2011
```

| 文件大小 | 比例 | 格式 | 名称 |
| --- | --- | --- | --- |
upx: \\Foolpix\modupxdcalc.exe: CantUnPackException: file is modified/hacked/protected; ta

未解包 0 个文件。

```
foolpix:\>upx -d .\foolpix\updexcalc.exe

Ultimate Packer for executables

Copyright (C) 1996-2011

UPX 3.0 Markus Obermer, Laslo Molnar & John Reiser Dec 12th 2011
```

| 文件大小 | 比例 | 格式 | 名称 |
| --- | --- | --- | --- |
| 114688 | 56832 | 49.55% | win32/pe | updexcalc.exe |

已解包 1 个文件。

```
foolpix:\>
```

标签: `packers` (`Prev Q`), `upx` (`Prev Q`) (`Next Q`)

# 反汇编器 (Disassemblers)

## 问题

Q: 递归遍历 (`Recursive Traversal`) 中使用的算法是什么？

标签: `disassemblers` (`Prev Q`)

反汇编二进制代码是一个困难的话题，但目前工具中似乎只有两种（幼稚的）算法被广泛使用。

- 线性扫描 (`Linear Sweep`)：基础算法，获取所有标记为代码的节，并通过按顺序读取后续指令来对其反汇编。
- 递归遍历 (`Recursive Traversal`)：通过记录调用（`call`）何时发生以及何处发生来改进线性扫描，并在遇到 `ret` 时返回上一次调用。

然而，对这些算法的描述非常模糊。在现实工具中，谁能提供这些算法更真实的描述？

标签: `disassemblers` (`Prev Q`)

用户: `perror`

`perror` 的回答

反汇编二进制代码是一个困难的话题，但目前工具中似乎只有两种（幼稚的）算法被广泛使用。

- 线性扫描：基础算法，获取所有标记为代码的节，并通过按顺序读取后续指令来对其反汇编。
- 递归遍历：通过记录调用（`call`）何时发生以及何处发生来改进线性扫描，并在遇到 `ret` 时返回上一次调用。

# 嵌入

## 问题

Q: 如何获取网页上嵌入的原始音频/视频文件的位置？

标签：`embedded` (上一个问题)

有些网站像 The Free Dictionary 以及许多其他翻译和发音服务，在你听的单词旁边提供一个小图标，可以听到它的发音。

我该如何找到网页上嵌入的音频/视频文件的来源？我该从哪里开始？

标签：`embedded` (上一个问题)

用户：`howard-r0ark`

回答来自 `samuraii`

当你创建一个网站并嵌入图像、视频、音频、`javascript` 或其他外部资源时，你也会通过自己的 URL 来指定它们的位置。

例如，你在服务器上拥有如下目录结构，它解析为以下可访问的 URL（假设你的网站是 `www.example.com`）：

```
|-- /index.html             -> www.example.com/index.html

|-- /images/               -> www.example.com/images/

|   |-- banner.png          -> www.example.com/images/banner.png

|   |-- favicon.png          -> www.example.com/icons/

|-- /audio/                -> www.example.com/audio/

|   |-- intro.mp3             -> www.example.com/audio/intro.mp3

|   |-- voice.flac            -> www.example.com/audio/voice.flac
```

当你访问 `index.html` 时，浏览器会查找所有其他嵌入的 URL 并从服务器获取。你可以使用 Firefox 或 Chrome 开发者控制台等工具来捕捉请求。这些请求中应该有一个是媒体文件的 URL。

如果你有一个 HTML `<embed>` 标签（或 `<img>` 标签），媒体的 URL 是通过 `src` 属性指定的，你也可以使用 Firefox 或 Chrome 开发者控制台等工具对其进行检查。你可以在页面的任何地方右键点击“检查元素”并检查 HTML。

```
<embed src="audio/intro.mp3"> -> www.example.com/audio/intro.mp3
```
