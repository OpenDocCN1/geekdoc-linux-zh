
`x11perf` `[-option1]` `[-option2 ..]`

表 6.1 列出了未指定测试的实用用选项。

| 选项 | 描述 |
| --- | --- |
| `-display host:display` | 连接到运行在 `host:display` 上的 X 服务器。 |
| `-repeat n` | 每个测试执行 `n` 次。默认值为 5。 |
| `-time s` | 每个测试执行 `s` 秒。默认值为 5 秒。 |
| `-all` | 执行所有测试。 |
| `-range test1[,test2]` | 执行从 `test1` 到 `test2`（包含在内）的所有测试。 |
| `-labels [test1,test2...]]` | 显示列出的每个测试的描述性标签。如果未指定测试，则显示所有标签。 |
| `-fg color` | 执行测试时使用前景色颜色 `color`。默认为黑色。 |
| `-bg color` | 执行测试时使用背景颜色 `color`。默认为白色。 |
| `-depth n` | 在测试会期间将颜色深度设置为每像素 `n` 位。默认值为当前设备的深度。 |

### 表 6.1 x11perf 非测试命令行选项

当每个测试完成时，结果将写入标准输出（`stdout`），因此你必须将它们重定向到文件进行保存。使用 `-all` 选项时要小心，因为运行超过 260 项测试可能需要很长时间。在之前描述的系统上，仅运行一次所有测试（`-repeat 1`）就花费了超过 35 分钟。`-labels` 选项显示每个测试的描述文本。列表 6.1 中的列显示了这些标签。当使用 `-range` 选项时，如果指定了 `test2`，测试范围将从 `test1` 开始到结束。

要查看测试列表及其执行顺序，请执行未修饰的 `x11perf` 命令，如列表 6.1 所示（输出为了可读性进行了修剪）：

### 列表 6.1 x11perf 测试简略列表

```
$ x11perf

usage: x11perf [-options ...]

where options include:

  -dot      Dot

  -rect1    1x1 rectangle

  -rect10   10x10 rectangle

  -rect100  100x100 rectangle

  -rect500  500x500 rectangle

  -move     Move

  -umove    Moved window

  -movree   Moved window

  -resize   Resize

  -uresize  Resize window

  -circulate Circulate

  -uculate
```

整个序列从 `-dot` 开始到 `-uculate` 结束。如果你对特定类型感兴趣，请考虑使用 `-range` 来选择子集。前几行标识了 `x11perf` 版本、服务器信息以及测试时间。

## 使用 x11perf

### 列表 6.2 来自 x11perf 的结果

```
x11perf performance program, version 1.5

XFree86 Project, Inc. on localhost:0

Fri Apr 27 22:37:27 2001

Sync time adjustment is 0.1980 msecs.

24000 reps @ 0.0215 msec ( 4660.0/sec): Move window via
    parent (4 kids)

24000 reps @ 0.0214 msec ( 4670.0/sec): Move window via
    parent (4 kids)

24000 reps @ 0.0214 msec ( 4670.0/sec): Move window via
    parent (4 kids)

24000 reps @ 0.0215 msec ( 4660.0/sec): Move window via
    parent (4 kids)

24000 reps @ 0.0227 msec ( 44100.0/sec): Move window via
    parent (4 kids)

1200000 trep @ 0.0217 msec ( 4610.0/sec): Move window via
    parent (4 kids)
```

接下来的五行显示了测试结果。每行列出了执行的总重复次数（`reps`），以及时间、每秒重复次数、测试的简要描述以及使用了多少对象。例如，在第五次通过中，总共 24000 次操作移动了 4 个子窗口。每次重复花费了 0.0227 毫秒，这相当于每秒 44100 次。最后一行显示了数据：总重复次数（1,200,000）、每次重复的平均速度（0.0217）以及平均速度（46,100）。

# 测量结果

在实现可能的增强后，你将想要查看它是否有效。`x11perf` 让这项任务变得简单。首先，使用相同的测试重试，并将输出保存到文件中。接下来，使用 `x11perf` 比较结果。好消息是 `x11perf` 比 `x11perf` 简单得多。它的语法如下：

```
x11perf [-r -ro] [-l label_file] file1 file2 [...]
```

在这里，`file1` 和 `file2` 存储了第一次和第二次测试的结果。你也可以指定额外的文件。`-r` 表示输出应包含一列，显示第二次及后续测试相对于第一次测试的性能。`-l label_file` 限制了用于比较的所选测试（使用 `x11perf -labels` 来确定要使用的正确标签）。`file1` 必须统计重试中所有测试的结果，否则程序将失败。列表 6.3 描述了一个典型的 `x11perf` 会话。

## 列表 6.3 x11perf 的输出

```
$ x11perf -r movree.1 movree.2

1: movree.1

2: movree.2
```

| 1 | 2 | 操作 |
|---|---|---|
| 46100.0 | 43100.0 ( 0.93 ) | 通过父级移动窗口（4个子窗口） |
| 105000.0 | 92300.0 ( 0.88 ) | 通过父级移动窗口（16个子窗口） |
| 94700.0 | 123000.0 ( 1.30 ) | 通过父级移动窗口（25个子窗口） |
| 112000.0 | 174000.0 ( 1.55 ) | 通过父级移动窗口（50个子窗口） |
| 115000.0 | 180000.0 ( 1.57 ) | 通过父级移动窗口（75个子窗口） |
| 104000.0 | 184000.0 ( 1.77 ) | 通过父级移动窗口（100个子窗口） |
| 121000.0 | 185000.0 ( 1.53 ) | 通过父级移动窗口（200个子窗口） |

前两列显示了正在比较的测试结果。因为示例使用了 `-r`，第三列以百分比表示第二次测试相对于第一次的性能。最后一列显示了执行的测试。这个示例通常表明，某些因素恶化了服务器在这一特定测试中的性能，因为重试中的两个测试都变慢了。

## 为本地使用调优 X 服务器

本节提供了若干改进本地 X 服务器性能的建议——即对于运行与其客户端运行在同一台机器上的服务器。

# X 窗口性能
第 6 章

### 提示
为了在测试和调优服务器时节省时间，如果你的系统启动到运行级别 5（即 X 登录窗口），请将默认运行级别改为 3（文本登录）。然后使用 `startx` 脚本（或你系统上的等效脚本）启动服务器。

## 提高服务器的优先级

通常情况下，X 服务器是 Linux 系统上最消耗 CPU 的进程之一。然而，很少有 Linux 厂商或 Linux 用户利用提高服务器相对于其他进程优先级的能力。结果是，X 服务器的运行优先级与简单的文本编辑器相同。在许多情况下，仅需提高 X 服务器的优先级就能消除性能缓慢的问题。家用电脑、办公工作站以及主要用于访问互联网的计算机通常对这种简单的方法反应良好。

提高 X 服务器的优先级会赋予它一个较低的 `nice` 值。进程的 `nice` 值是内核用于修改其相对于其他进程分配 CPU 时间比例的数字。`Nice` 值的范围从 -20 到 20。进程的 `nice` 值越低，它对其他进程就越不“友好”——也就是说，内核中断它给其他进程分配 CPU 时间次数就越少。默认值为 0，意味着内核不会根据 `nice` 值修改进程的优先级。因此，假设有两个进程 A 和 B，它们都以 0 的默认 `nice` 值运行，那么将 A 的 `nice` 值改为 -20 将会赋予它比 B 更高的优先级。将 B 的优先级改为 20 则会使它的优先级低于 A。

### 注意
Linux 内核用于进程调的算法和启发式方法比这里解释的要复杂得多。尽管如此，出于本章的目的，这个简单的解释就足够了。

要使用特定的 `nice` 值启动 X 服务器，请使用 `nice` 命令。要调整运行中的服务器的 `nice` 值，请使用 `renice` 命令。普通用户可以降低自己进程的优先级，但只有 root 用户可以更改其他用户的进程或增加进程的优先级。

`nice` 命令的语法如下：

```
nice *[option] [command arguments]*
```

在这里，`command` 和 `arguments` 分别指定要运行的程序及其所需的任何选项。`option` 可以是 `-value` 或 `-n value`，其中 `value` 是你想要的 `nice` 值。如果未指定 `option`，则会启动程序并将其 `nice` 值增加 10。例如，要以 -5 的 `nice` 值启动 X 服务器，以下命令任选其一均可行：

```
# nice -5 /usr/X
# nice -n -5 /usr/X
```

## 性能监控技术
第三部分

在 24bpp 分率下，1280 × 1024 的内存需求如下：

`(1280 × 1024 × 3) / 1024 = 3840KB`

幸运的是，你通常可以用图像清晰度换取色彩丰富度，反之亦然。通过实验和测试可以为你的情况确定最佳组合。

> 提示
> 要将千字节（KB）转换为兆字节（MB），请将千字节值除以 1024。例如，3840KB 等于 3.75MB。即 3840 / 1024 = 3.75。

列表 6.4 中的 `x11perfcomp` 输出说明了更丰富的位深（8、16 和 24bpp）在相同显示分辨率下对服务器性能的影响。

## 列表 6.4 相同分辨率下的位深对比

- 1: 8bit
- 2: 16bit
- 3: 32bit

| 1 | 2 | 3 | 操作 |
|---|---|---|---|
| 4500.0 | 46300.0 | 41100.0 | 填充 10x10 64边形（凸） |
| 13900.0 | 10600.0 | 2530.0 | 填充 100x10 64边形（凸） |
| 33200.0 | 33400.0 | 31600.0 | 填充 10x10 64边形（复杂） |
| 13500.0 | 10600.0 | 2530.0 | 填充 100x10 64边形（复杂） |

这四项测试测量了服务器在 1280 × 1024 像素的恒定显示分辨率以及逐渐增加的 8、16 和 24bpp 位深下，绘制 10 × 10 像素或 100 × 100 像素的64边边形的性能。尽管结果并非完全统一（特别是在 16bpp 位深下），但总体趋势显示性能结果较低，特别是当从 16bpp 变为 24bpp 时。

## 禁用未使用的模块和服务器扩展

如果你不使用 X 模块或服务器扩展，请不要加载它。这将加快服务器的启动速度并减少服务器的内存占用。大多数 Linux 供应商提供的默认配置可能并不理想。要查看服务器加载了哪些模块和扩展，请查找配置文件中的 `Module` 指令部分。列表 6.5 显示了一个示例部分。

## X Window性能

## 第6章

## 列表 6.5 Module 部分指定要加载的 X 模块和扩展

```
Section "Module"
  Load "GLcore"
  Load "dbe"
  Load "extmod"
  Load "fbdevhw"
  Load "dri"
  Load "glx"
EndSection
```

这些模块提供的功能如下列表所示：

- `GLCore`—提供基础 3D 渲染能力
- `dbe`—启用对双缓冲的支持
- `extmod`—加载各种 X 服务器扩展
- `fbdevhw`—为服务器访问硬件帧缓冲区设备提供支持
- `dri`—实现直接渲染基础设施（Direct Rendering Infrastructure），一种直接将 3D 数据发送到显卡硬件的方法
- `glx`—实现核心 3D 渲染到 X11 窗口系统的接口

如果你不需要 3D 渲染能力，可以使用哈希符号 (`#`) 注释加载这些模块的行来禁用 `GLCore` 和 `glx` 模块，或者从配置文件中删除这些行。这样做将为其他用户释放服务器启动时间和内存。

好消息是，XFree86 使用了动态模块加载方案，其原理类似于 Linux 内核。模块即使提供基本功能也是按需加载的。坏消息是，许多模块也内置在服务器中。然而，某些模块仅在启动时使用会被卸载。要识别内置模块，请查看服务器日志文件中类似的条目：

- `(II) Initializing built-in extension MIT-SHM`
- `(II) Initializing built-in extension XInputExtension`
- `(II) Initializing built-in extension XTEST`

XFree86 日志记录了启动加载的模块。要确定服务器启动时加载了哪些模块，请查找日志文件中类似以下的条目：

- `(II) LoadModule: "bitmap"`
- `(II) Loading /usr/X11/lib/modules/fonts/libbitmap.map`
- `(II) Module bitmap="The XFree86 Project"`
  compiled for 4.0.3, module version = 1.0.0
  Module class: XFree86 Font Renderer
  ABI class: XFree86 Font Renderer, version 0.2

在无情禁用某个特定模块之前，请确保服务器会自动卸载它。例如，`scanci` 模块在启动期间会被卸载。查找类似下方的条目：

- `(II) UnloadModule: "scanci"`
- `(II) Unloading /usr/X11/lib/modules/fonts/libscanci.map`

## 使用特定芯片选项

使用特定芯片的配置选项可以提高服务器性能。例如，某些选项针对特定硬件，应谨慎使用。

## 性能监控技术
第三部分

- `xset fp+ fontpath1,fontpath2...`—将 `fontpathN` 添加到服务器当前字体路径的末尾
- `xset fp rehash`—指示服务器根据当前的字体路径重新读取其字体数据库

在更改了运行中的 X 服务器的字体路径后，你必须强制服务器重建其内存中的字体数据库，否则更改将不会生效。要做到这一点，你需要执行命令 `xset fp rehash`。紧接着运行 `xset q` 以确认结果。列表 6.6 展示了如何使用 `xset` 删除字体路径。输出已经过修剪，以节省空间并减少杂乱。

## 列表 6.6 使用 xset 删除字体路径

```
$ xset q

...

Font Path:
/usr/X11R6/lib/X11/fonts/local/
/usr/X11R6/lib/X11/fonts/misc/
/usr/X11R6/lib/X11/fonts/75dpi/:unscaled,
/usr/X11R6/lib/X11/fonts/100dpi/:unscaled,
/usr/X11R6/lib/X11/fonts/CID/
/usr/X11R6/lib/X11/fonts/75dpi/,

/usr/X11R6/lib/X11/fonts/100dpi/

$ xset -fp /usr/X11R6/lib/X11/fonts/local/

$ xset fp rehash

$ xset q
```

Font Path:
/usr/X11R6/lib/X11/fonts/misc/
/usr/X11R6/lib/X11/fonts/75dpi/:unscaled,
/usr/X11R6/lib/X11/fonts/100dpi/:unscaled,
/usr/X11R6/lib/X11/fonts/CID/
/usr/X11R6/lib/X11/fonts/75dpi/,

/usr/X11R6/lib/X11/fonts/100dpi/
```

第一个 `xset` 命令显示了现有的字体路径。第二个 `xset` 命令 `-fp` 从服务器的字体路径中移除 `/usr/X11R6/lib/X11/fonts/local/`。注意，`xset` 需要结尾的 `/` 来正确指定目录路径。如果缺少该斜杠，`xset` 会发出警告，提示字体路径未更改。在使用 `rehash` 选项刷新服务器字体数据库后，最后的 `xset` 调用显示 `/usr/X11R6/lib/X11/fonts/local` 不再是 X 服务器字体路径的一部分。

# X 窗口性能 第 6 章

和通常一样，在更改了加载的字体集后，务必测试服务器的性能并评估结果。在这种情况下，应该进行的测试应包括 `x11perf` 的字符绘制测试，或者至少是其中的某些子集。可以使用命令 `x11perf-range text xfigfonttext` 调用完整的测试。

## 使用字体服务器
