
`knum linseg 40,p3/7,60,p3/7,46,p3/7,54,p3/7,24,p3/7,58,p3/7,48,p3/7,80`

`kvel linseg 20,p2,39,p2/33`

`kran pcauchy 23` ; 调用一个名为柯西分布的特定随机函数

`kdur = int(kran)+46`

`kpause = frac(kran)`

`kchan, knum, kvel, kdur, kpause`

`moscil`

`edin`

`edin`

`knum` 和 `kvel` 是结果（以及控制或 k-rate 信号），`linseg` 是一个创建包络（修改函数）的操作码，而 `P3` 是传递给或从 sc 文件的事件持续时间。`P3/7` 表示包络的每个段长度等于事件持续时间除以七。

因此在上面的示例中，`knum` 语句创建了一个包络函数，其分段以 `p3/7` 的速率在指定的 MIDI 音符编号之间提供线性移动。

## 控制更改消息

接下来的两个乐器控制发送到我的外部合成器和 MIDI 控制调音器的 MIDI 程序更改（Program Change）消息（关于 MIDI 的更多信息请见第 6 章）。

```
instr 11

kchan = 0

kprog = 2.

kmin = 1.

kmax = 128.

outoutpc kchan, kprog, kmin, kmax

endin

instr 100

kchan = 8

kprog = 6.

kmin = 1.

kmax = 128.

outpc kchan, kprog, kmin, kmax

endin
```

这是该乐器的 sc 文件：

```
;;; MIDI OUT opcodes

;;; mussle.sco

t 0 60 ; 速度指示

i1 1.0 1.0 ; 不同的 p3 持续会被拉伸

ni1 2.0 7.0

i1 9.0 18.0 ii1 18.0 17.0 ; 由 knum 指定的音符

iii1 0.0 1 ii100 0 1

e
```

编译这些文件的命令行是：

```
csound -Q0 -n -dm6 mussle.orc mussle.sco
```

其中 `-Q0` 选择第一个 MIDI 设备，`-n` 抑制写入磁盘（为了性能）。如果有快速的 CPU 和硬盘，你可以结合各种 I/O 选项。我测试了实时音频 MIDI 输出：它可以运行，但在 Pentium 16 上速度缓慢。

## Csound 辅助工具

Csound 拥有丰富的辅助应用程序，其中一些包含在源码树中。源码包包括 `score`（用于创建和操作 Csound 源的库）、`sndinfo`（显示所选音频文件的信息）以及一组为 Csound 合成操作码提供数据的强大分析工具。除了源码包自带的，Csound 还有许多其他强大实用的工具：分析数据编辑器、score 处理环境和鼓机都是免费提供的。`Cecilia`、`HPComposer` 和 `Silence` 是三个大型 Csound 辅助工具；`Midi2CS` 和 `hydraj` 是较小的助手。我们先讨论后者。

## Midi2CS

作者：Ruedier Borrman  
版本：0.95 / 2  
网站：http://~snafu.de/~rubo/midi2cs  
FTP 站点：n/a  
维护：是  
可用性：仅限二进制  
版权：作者所有  
摘要：将你喜爱的 MIDI 文件转换为 Csound 的方便工具

Ruedier Borrman 的 `Midi2CS` 使用 Csound 作为渲染引擎将标准 MIDI 文件转换为 WAV 文件。`MIDI2CS` 可以使用用户的样本（AIFF 或 WAV 格式）或用户定义的 Csound 乐器。通过此功能，`MIDI2CS` 可以以 MIDI 排序器无法实现的方式调度。`MIDI2CS` 带有独特的循环功能，使其适合创建 Techno 和其他舞曲；然而，该程序可以创建几乎任何类型的音乐。如果你感兴趣，请查看 Ruedier 网站上关于 `Midi2CS` 的优秀教程。`MIDI2CS` 仅以二进制形式提供给 Linux，因此设置程序非常简单。在 `/home` 或 `/usr/local` 创建一个新的 `Midi2CS` 目录，从上述网站下载最新包。`Midi2CS` 封装为 gzipped 二进制文件，因此在使用之前运行 `gunzip midi2cs.gz`。在使用之前，你可能需要通过 `chmod a+x midi2cs` 设置文件权限。权限正确后，`Midi2CS` 即可运行。

### 软件声音合成

将 MIDI 文件渲染为 WAV 是三步骤程序。运行不带参数的 `midi2cs` 创建项目文件 `midi2cs.pro`。编辑此项目文件让 `midi2cs` 知道处理哪个 MIDI 文件，给输出的 `.orc` 和 `.sco` 文件命名，以及使用哪些 Csound 乐器渲染 MIDI 文件。再次运行 `midi2cs`（不带参数）创建你的 Csound `.orc/.sco` 文件。图 9-1 显示了这一步的结果：

![](img/43a9671cef617c9c7a18f7a6904433f1_209_0.png)

第二阶段 `MIDI2CS`

最后一步运行 `csound` 将新的 `.orc` 和 `.sco` 文件编译为 WAV 格式文件：

```
csound -W -o ppanner.wav ppanner.orc ppanner.sco
```

该示例将编译图 9-1 中列出的 `ppanner`（Pink Panther）`.orc` 和 `.sco` 文件。你可以通过编写包含以下一行的脚本文件（命名为 `cs.scr`）来自动化最后一步：

```
csound -W -o $1 $1
```
