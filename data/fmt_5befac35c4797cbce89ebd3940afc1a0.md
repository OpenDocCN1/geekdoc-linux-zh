
缩小了一半！但我在压缩的波形中丢失任何数据了吗？我戴上耳机，快速输入`shnp *.shn`，立刻感到放心；`shorten`如其广告所述：没有丢失任何数据！正如你所见，`shorten`提供了真正出色的压缩率，而且它对非商业使用免费，这非常棒。请注意，`shorten`也支持有损音频压缩，如果需要的话；请查看`shorten`的手册页以获取更多信息。

## SoundTracker 模块

SoundTracker 模块是一种在 Amiga 电脑时代流行的音乐文件格式。作为电子游戏存储音乐的主要方法，SoundTracker 模块及其衍生格式（如 `3XD`、`MED` 和许多其他格式）在互联网上广泛可用。针对控制台和 `X` 窗口系统都有许多可用的模块播放器。

模块与许多音乐文件的不同之处在于，它们同时存储乐谱和数字声音采样。模块播放器以不同的频率播放这些采样，以模拟乐器的不同音符（一种原始的波表合成形式）。最终效果出人意料地好。模块是一种极其灵活的音乐格式。它们让程序员和音乐家对作品的最终结果拥有绝对的控制权，因为实际的声音采样在模块文件中被逐字传输。与此形成对比的是 `MIDI` 文件，在 `MIDI` 文件中，音乐家只提供乐谱，并依赖声卡 `ROM` 提供听起来不错的乐器进行播放。所以你可能知道，`MIDI` 乐器的质量因声卡而异，而模块在几乎所有现代声硬件上听起来几乎完全相同。

### libmikmod

为了帮助你理解模块播放器，我们将下载一个名为`libmikmod`的全功能模块和声音播放器库，并用`C`编写一个简单的模块播放器。然后我们将编译它并使用它来播放我们从互联网下载的各种SoundTracker 模块。找到`libmikmod`的最佳方法是访问 `http://freshmeat.net` 并搜索“`libmikmod`”。按照正确的链接下载`libmikmod`后，现在你准备编译它。输入以下内容：

```bash
cd /tmp
tar xzvf /location/of/file/libmikmod-3.1.7.tar.gz
cd libmikmod-3.1.7
./configure
```

如果你正在使用`ALSA`，请改为输入`./configure --enable-alsa`。这会告诉`libmikmod`直接使用`ALSA`，而不是通过`OSS`兼容性模块。在此步骤之后，源代码树准备好进行编译，因此输入

```bash
make
```

现在，以`root`用户身份输入

```bash
make install
ldconfig
```

## 测试 libmikmod

`libmikmod`现在将自动安装，并且通过`ldconfig`更新你的库依赖信息，以便程序可以找到`libmikmod`。现在，为一个特殊的`C`编程项目创建一个目录——我们要创建一个简单的模块播放器。列表 29.3 几乎是`libmikmod`信息文档中示例程序的逐字复制：我们唯一添加的是将模块指定为命令行参数的功能。虽然代码行数并不多，但得益于`libmikmod`的强大功能，它完成了工作。

**列表 29.3** `libmikmod` 示例模块播放器

```c
/* MikMod Sound Library example program: a simple module player */
/* A tiny modification by Daniel Robbins, 7/6/99 */
#include <unistd.h>
#include <mikmod.h>

main(int argc, char **argv)
{
  MODULE *module;

  /* Register all the drivers */
  MikMod_RegisterAllDrivers();

  /* Register all the module loaders */
  MikMod_RegisterAllLoaders();

  /* Initialize the library */
  md_mode=DMODE_SOFT_MUSIC;

  if(MikMod_Init("")
  {
    fprintf(stderr,"Could not initialize sound, reason:%s\n",
    MikMod_strerror(MikMod_errno));
    return;
  }
  /* load module */
  module = Player_Load(argv[1],64,0);
  if (module)
  {
    /* start module */
    Player_Start(module);
    while(Player_Active()
    {
      /* we're playing */
      usleep(10000);
      MikMod_Update();
    }
    Player_Stop();
    Player_Free(module);
  }
  else
    fprintf(stderr,"Could not load module, reason: %s\n",
    MikMod_strerror(MikMod_errno));
  /* give up */
  MikMod_Exit();
}
```

输入上述程序并将其保存为`mkplay.c`后，可以通过输入以下命令进行编译：

```bash
> gcc mkplay.c -o mkplay -lmikmod
```

这将生成一个名为`mkplay`的二进制文件，可用于播放SoundTracker 和类似SoundTracker 的模块。只需在命令行中按以下方式指定它们：

```bash
> mkplay mymodule.mod
```

我建议你将这个新的二进制文件复制到`/usr/local/bin`，以便将其加入你的路径中，从而可以从任何目录访问。现在，在我们尝试运行程序之前，我们必须找到一些SoundTracker 模块。最简单的办法是前往`http://www.yahoo.com` 搜索“`mod files`”或浏览到 娱乐 > 音乐 > 计算机生成 > `mod` 类别。你创建的新播放器可以处理`.mod`、`.s3m`和`.xm`文件以及其他文件。下载一些文件，听一听，看看你的感受。模块的一个良好来源是位于`http://ftp.wustl.edu/~aminet/dirs/tmoe_mods.html` 的`AmiNet` 模块归档库。这些文件大多是`lha`压缩的——幸运的是，`Caldera OpenLinux` 拥有一个`lha`解压缩程序。下载归档文件后，输入以下内容：

```bash
> lha x myfile.lha -o Medited
mymodule.mod
```

现在你可以使用你的播放器播放该模块：

```bash
> mkplay mymodule.mod
```

SoundTracker 模块提供了一种简单且易于分发的方法，用于分发可以在各种硬件上播放的歌曲。模块的优势在于它们自带乐器。我们将研究`MIDI`，这是一种独立于乐器并用于专业应用以及越来越多基于`PC`应用的标准。

## MIDI 简介

`MIDI`是`Musical Instrument Digital Interface`（乐器数字接口）的缩写，最初设计于`1982`年，旨在为音乐合成器提供互操作和共享音乐信息标准方式。自那时起，`MIDI`在`PC`领域变得非常流行。许多声卡内置了`MIDI`端口，许多声卡还在其本身集成了先进的`MIDI`合成器。但在我们深入`MIDI`的细节之前，将`MIDI`与数字化音频以及SoundTracker 模块进行比较是一个好主意。

与数字化音频相比，`MIDI`文件小得多。由于`MIDI`文件仅包含`MIDI`合成器播放特定乐谱所需的指令，而不包含数字化声音数据本身，这使得`MIDI`文件在当今标准下显得极其微小，一首五分钟歌曲通常仅为`50KB`。与此形成对比的是，典型的`CD`质量歌曲为`50MB`，`MPEG 1 Layer 3`编码的歌曲为`5MB`，你可以看到`MIDI`文件实际上是多么小。

然而，这种小尺寸带来了一些局限性。因为`MIDI`文件仅包含合成器在特定时间演奏特定乐器的指令，作曲家对最终音乐质量的控制相对较少。毕竟，不同的合成器和声卡使用不同的合成技术来模拟现场乐器，这些乐器不仅在声音质量和特性上差异巨大，相对音量也可能不同。这可能导致一种情况：一个`MIDI`文件在使用某款声卡的`MIDI`合成引擎播放时听起来很棒，但在另一款声卡上听起来很糟糕（或明显更差）。尽管声卡`MIDI`波形表合成器的现代进步已大大改善了整体音质，但两台合成器绝不等同的事实将永远存在。因此，虽然`MIDI`允许在多种电子音乐设备上进行音乐回放，但它也严重限制了音乐家对音乐最终“声音”的控制。他或她完全不知道完成的乐曲是在相当于电子三角钢琴的设备上播放，还是像木琴（`kazoo`）这样的廉价乐器。

使用`MIDI`的另一个更明显的限制在于，它是一种专门设计用来表示器乐音乐的格式。无法使用`MIDI`准确传输人声或复杂且独特的音效。使用`MIDI`有点像为极其先进的自动钢琴作曲。实际上，`MIDI`合成器就是这种东西。

考虑到这一点，`MIDI`是几种特定用途的理想音乐格式。它是器乐作曲和回放的理想选择，特别是当音乐可能需要稍后编辑时。数字化音乐，如`MPEG 1 Layer 3`和`CD`音频，并不处于可以轻松更改的格式中。在处理`MIDI`文件时，一段音乐可以很容易地逐音符进行修改。它是可塑的，而数字音频则不是。`MIDI`的另一个理想用途是多媒体项目（如游戏）中器乐音乐的播放。对于背景音乐，`MIDI`提供了一种理想的作曲方式，其音乐几乎可以在任何类型的声音硬件上听到。当然，如果你是一名专业音乐家，`MIDI`是你想要处理的内容。它是电子乐器所说的语言，而你的计算机（配合适当的声音硬件）也能说这种语言。

### 通用 MIDI 系统

通用`MIDI`系统（`GM`）旨在解决各种`MIDI`设备之间存在的一个有趣问题——为特定乐曲选择正确的乐器。以一个在特定`MIDI`系统上创作的`MIDI`乐谱为例。当在另一制造商的`MIDI`系统上回放时，选择到错误乐器并不罕见。这是因为，在`MIDI`文件中，乐器是通过数字选择的，而制造商并没有一套标准数字来映射到不同硬件上的相同乐器。因此，例如，即使乐谱是用长笛创作的，它在另一制造商的合成器上可能会回放为钢琴。为了解决这个问题，`GM`规范定义了从数字到乐器类型的标准映射，因此长笛永远是长笛，钢琴永远是钢琴。这解决了`MIDI`文件互换的问题，并消除了用户端可能需要对`MIDI`文件进行任何调整才能正确播放的需求。记住通用`MIDI`——你会经常听到它。如果你遇到一个使用错误乐器回放的`MIDI`文件，你也会知道发生了什么。

### MIDI 乐器——FM 与波形表合成

我们已经涵盖了`MIDI`的基础知识，但尚未深入查看合成阶段——`MIDI`合成器究竟如何通过扬声器回放数字乐器波形？我们将涵盖两种技术：`FM`合成和波形表合成。

`FM`合成，见于较旧的声卡中，是一种描述音乐乐器的相对简单的方法。主要适用于表示合成声音，`FM`合成乐器在声卡`ROM`中占据的存储空间相对较少。`FM`合成的主要缺点在于，难以准确模拟真实乐器的声音。`FM`合成因其“合成器”（`synthy`）般的声音而易于识别。

另一方面，波形表合成可以充分表示真实乐器，并且是现代声卡和合成器首选的乐器格式。在其最基本的形式中，波形表由特定乐器的样本组成，然后可以以不同的音高回放以模拟特定乐器的不同音符。然而，当前的波形表技术比这复杂得多。这种复杂性使得使用相对有限的内存就能实现极高品质的结果。当然，波形表声音占用的存储空间比`FM`大得多，`MIDI`爱好者和专业人士配备具有`32MB`或更多专用板载`RAM`用于存储波形表样本的声卡并不罕见。现代波形表合成使用了音高偏移、插值和特殊数据压缩等技术，将合成声音的极限推向新高度。

### 软件 MIDI 合成

传统上，`MIDI`回放是通过使用声卡上内置的硬件合成器、可选的从板，或插入声卡`MIDI`端口的外部`MIDI`盒来实现的。最近，`MIDI`合成出现了一种新的可能性：软件合成。与现代机器上，这项任务可以完全在软件中执行，而不是依赖专用声音硬件将`MIDI`数据转换为数字音频数据。软件合成引擎通常使用波形表乐器将`MIDI`文件渲染为数字位流，然后通过声卡的数字音频输出设备进行播放。虽然你可能会想知道为什么在专用`MIDI`硬件触手可及的情况下还有人想要这样做，但有很多充分理由。首先，并非所有人都拥有提供`MIDI`回放的声卡。其次，虽然许多声卡提供`16`位声音和`MIDI`回放，但`MIDI`硬件可能使用`FM`合成，其在音质方面无法与现代波形表合成相提并论。此外，在现代`Pentium II`级别机器上，软件合成所需的`CPU`时间几乎可以忽略不计，使其成为一个具有吸引力且灵活的选项，如果你的声卡没有任何类型的`MIDI`支持，这也是必需的。

你甚至可能已经在`Microsoft Windows`下使用了基于软件的合成引擎而不自知。声卡制造商的一种常见做法是设计一个具备在硬件中播放`32`个同时乐器的能力的声卡，然后宣传该声卡能够同时播放`64`个乐器！其方式

要实现这种技巧，需设计驱动程序，使得当同时使用的乐器数量超过`32`个时，提供软件合成。通常，`Windows`声卡驱动程序提供选项来开启或关闭这些额外的声部。

### SoftOSS

如果您正在寻找软件`MIDI`合成，`SoftOSS`是一种可行的方案。`SoftOSS`作为`Open Sound System`（`OSS`）的驱动程序实现，提供了一个完全基于软件的合成器，对于兼容`OSS`的应用程序而言，其表现就像一个硬件设备。这意味着它提供了与标准`Linux` `MIDI`程序完全兼容的优势。目前，`SoftOSS`占用的`CPU`资源比`Timidity`少，但音质略逊一筹。

### Kmidi

`Kmidi`是一个基于`KDE`的应用程序，包含在`Caldera OpenLinux`中。它具有使用软件合成回放`MIDI`文件的功能；不幸的是，`Caldera`附带版本的该程序是`beta`版，略显不稳定。我建议您使用`Kmidi`的“大哥”`TiMidity++`来回放`MIDI`文件。

### TiMidity++

`TiMidity++`是一个优秀的`MIDI`软件合成引擎，完全模拟了`Gravis UltraSound`系列波形声卡，从而提供了真正惊人的音质。它可以从`http://www.goioce.co.jp/member/mo/timidity`获取。尽管`TiMidity++`在运行前需要一些配置，但最终的效果绝对值得付出这些努力。

`TiMidity`安装的第一步是从`TiMidity`网站下载源代码，编译软件，并安装编译后的应用程序。安装过程大致如下：

```bash
> cd /tmp
> tar xzvf TiMidity++-2.1.0.tar.gz
> cd TiMidity++-2.1.0
> ./configure --enable-nruses
```

（配置将开始）

```bash
> make
```

（编译将开始）

完成后，只需以`root`身份输入`make install`。软件将安装到`/usr/local`，并且我们将准备好进入配置过程的下一阶段——安装补丁文件。

## 为 TiMidity++ 和 OSS 安装补丁文件

安装补丁文件是一个繁琐且耗时的过程，但我会帮助你以最少麻烦的方式完成它。你要做的第一件事是访问`Eric A. Welsh`的`TiMidity`补丁网站，地址为`http://www.stardate.bc.ca/~guspatches.htm`。`Eric`在其页面上提供了一个高质量、可自由分发的补丁集。虽然体积较大，但下载和安装绝对是值得的。安装过程的第一步是下载`unar`二进制文件。我们将使用此程序来解压补丁文件归档。点击他页面顶部的`UNRAR`链接并下载`rarlinux.sfx`归档文件。将其移动到一个独立的临时目录中，然后输入

```bash
> ./rarlinux.sfx
```

该可执行归档文件现在将解压到当前目录。现在，以`root`身份将`rar`和`unar`复制到`/usr/local/bin`。我们现在准备好开始下载和安装补丁文件了。下载`eawpats`补丁集的所有部分，以及完整的`drumsfx`补丁集。这些文件将以`.rar`、`.r00`、`.r01`等结尾。下载完这些文件后，请下载任何可用的更新文件。我们现在准备好安装这些补丁了！`TiMidity++`安装完成后，只需以`root`身份执行以下操作：

```bash
> cd /usr/local/timidity
> unar e /path/to/rar/files/eawpats5.rar
> unar e /path/to/rar/files/drumsf4.rar
> unar e /path/to/rar/files/eawp5up1.rar
```

你使用的文件名可能略有不同，但它们将与上述文件名类似并以`.rar`结尾。解压完成后，我们`TiMidity`的最后一步是编辑`/usr/local/lib/timidity/timidity.cfg`文件，该文件应包含以下未注释的行：

```bash
dir /usr/local/lib/timidity
source gravis.cfg
source gsdrums.cfg
source gsxfx.cfg
source xgmap2.cfg
```

完成后，`TiMidity++`应该就准备就绪可以使用了。加载声音驱动程序并适当设置音量后，以下命令应该能播放音乐：

```bash
> timidity myfile.mid
```

为了获得更令人印象深刻的声音，请尝试以下命令行，它增加了混响、合唱效果、对声音样本进行抗混叠处理、增加`256`声部复音功能，并提高输出的采样频率：

```bash
> timidity -a -s65000 -EFchorus=1 -EFreverb=1,63 -p 256 -D 10 myfile.mid
```

要让`SoftOSS`使用`EAW`补丁集，只需在`shell`中输入以下命令，将`GUSPATCHDIR`环境变量设置为`/usr/local/lib/timidity`：

```bash
export GUSPATCHDIR=/usr/local/lib/timidity
```
