

## 图 1. 运行改进后的脚本的结果

```bash
if [ ! -z "$(file -b $name|grep 'image data')" ]
then
    figuresize $name
    if [ ! -z "$height" ]; then
        echo "<a href=$name><img src=$name border=0"
        echo " alt=$name height=$size"
        echo " align="absmiddle" />"
        echo "$name ($height x $width)</a>"
    else
        echo "<a href=$name><img src=$name border=0"
        echo " alt=$name height=$size"
        echo " align="absmiddle" />"
        echo "$name</a>"
    fi
fi
else
    echo "<a href=$name>$name</a><br />"
fi
echo "<hr />"
done
```

运行这个改进后的脚本的结果（其中图片可点击，条目之间有水平线等）如**图 1**所示。

![](img/526fd434dcfcf1b461b94c24ea170f36_30_1.png)

## 栏目

### 玩转 Shell

现在，让我们看看如何让脚本变得更智能：

```bash
if [ ! -z "$height" ] ; then
  if [ $height -gt $width ] ; then
    dimensionLabel="height"
  else
    dimensionLabel="width"
  fi
```

你能看出我在此处做了什么吗？这让我们能够判断图形的两个维度中哪一个是较大的，然后将 dimensionLabel 设置为那个特定的维度。以下是结果：

```bash
echo "<img src=$name $dimensionLabel=$size />"
```

其中我将 size 设置为我们想要的缩略图尺寸——在我们的示例脚本中为 75。

我还将添加几个计数器，以便在最后总结显示的图片数量与显示的总文件数量。只是因为这，呃，很有趣，对吧？以下是循环的最新版本，正如你可能预期的那样，随着它变得更加复杂，它也变得更为繁琐：

```bash
for name in *
do
if [ ! -z "$(file -b $name|grep "image data")" ]
then
  imgcount=$(( $imgcount + 1 ))
  figuresize $name
  if [ ! -z "$height" ] ; then
    if [ $height -gt $width ] ; then
      dimensionLabel="height"
    else
      dimensionLabel="width"
    fi
    echo "<a href=$name><img src=$name border=0"
    echo " alt=$name $dimensionLabel=$size"
    echo " align="absmiddle" /></a>"
  else
    echo "<a href=$name><img src=$name border=0"
    echo " alt=$name height=$size"
    echo " align="absmiddle" /></a>"
    echo "$name</a>"
  fi
else
  echo "<a href=$name>$name</a><br />"
fi
echo "<hr />"
totcount=$(( $totcount + 1 ))
done
```

![](img/526fd434dcfcf1b461b94c24ea170f36_31_0.png)

**图 2. 更美观的输出**

```bash
echo "<p>Displayed $imgcount images out of $totcount entries total.</p>"
```

最终结果（希望这样会更美观）如**图 2**所示。

既然我们可以在脚本中规范化这些缩略图（至少对于非 JPEG 图像，由于 file 命令的限制），接下来我们要研究的是如何以多张图片并排、网格或表格的形式显示结果，而不是像我们现在看到的那样每行一张图片。这要复杂一些，因为它涉及到又一个计数器，但当你等待下一期的《Linux Journal》时，你可能应该补习一下基本的 HTML 表格标签，因为我们将使用这些标签。然后，最后，我们将切换到 ImageMagick 替代 file，这样我们可以获取所有图像文件的尺寸，而不仅仅是 Gif 和 PNG 文件。

> Dave Taylor 是拥有 26 年 UNIX 经验的资深人士，The Elm 邮件系统的创造者，最近也是畅销书《Coached Shell Scripts》和《Teach Yourself Unix in 24 Hours》（在他撰写的 16 本技术书籍中）的作者。他的主要网站是 www.intuitive.com，他还在 AskDaveTaylor.com 上提供技术支持。

## **ABERDEEN STONEHAVEN X318**

## **ABERDEEN STONEHAVEN X526**

## **ABERDEEN STONEHAVEN X633**

### ABERDEEN STONEHAVEN X318

- 3U 12TB 双核就绪存储服务器
- 最多两个双核 AMD Opteron™ 2000 系列处理器
- 最多 16 个 750GB (12TB) 热插拔 SATA 硬盘
- 内部 SATA 2.5" 硬盘位用于操作系统驱动
- 800+ MB/sec 持续数据吞吐量 RAID 控制器
- 最多 32GB 667/533Mhz ECC 注册 DDR2 SDRAM
- nVIDIA nForce Pro 芯片组，支持 64 位
- 650W 冗余热插拔电源
- 5 年保修

起始价 **$4,259**

### ABERDEEN STONEHAVEN X526

- 5U 18TB 双核就绪存储服务器
- 最多两个双核 AMD Opteron™ 2000 系列处理器
- 最多 24 个 750GB (18TB) 热插拔 SATA 硬盘
- 两个内部 SATA 硬盘位用于镜像操作系统驱动
- 800+ MB/sec 持续数据吞吐量 RAID 控制器
- 最多 32GB 667/533Mhz ECC 注册 DDR2 SDRAM
- nVIDIA nForce Pro 芯片组，支持 64 位
- 950W 三重冗余热插拔电源
- 5 年保修

起始价 **$5,679**

### ABERDEEN STONEHAVEN X633

- 6U 24TB 双核就绪存储服务器
- 最多两个双核 AMD Opteron™ 2000 系列处理器
- 最多 32 个 750GB (24TB) 热插拔 SATA 硬盘
- 两个后置热插拔 SATA 硬盘位用于镜像操作系统驱动
- 800+ MB/sec 持续数据吞吐量 RAID 控制器
- 最多 32GB 667/533Mhz ECC 注册 DDR2 SDRAM
- nVIDIA nForce Pro 芯片组，支持 64 位
- 1550W 冗余热插拔电源
- 5 年保修

起始价 **$7,139**

> “终极 Linux 服务器... 对我们的基准测试来说太快了... 我们毫不犹豫地推荐 Aberdeen 系列的服务器。”  
> *《Linux Journal》—Aberdeen Stonehaven A261T*

> “非常适合视频服务或其他存储密集型任务”  
> *《PC Magazine》—Aberdeen X26XS*

> “Aberdeen 超越了 HP ... 得分显著更高 ... AberNAS 128 拥有出色的功能”  
> *《Network Computing》—Aberdeen AberNAS 128*

> “强大的性能 ... 令人震惊 ... 大开眼界 ... 迄今为止最高的 WebBench 分数”  
> *《PC Magazine》—Aberdeen Stonehaven A261S*

AMD、AMD Arrow 标志、AMD Opteron 以及它们的组合是 Advanced Micro Devices, Inc. 的商标。条款和条件请参见 www.aberdeencinc.com/legal/terms.htm (01/19/07)

**888-297-7409**
**www.aberdeencinc.com/linux**

## 语言——有些已消亡，有些仍活着

**JON "MADDOG" HALL**

### 编程不仅仅是 Java。

“maddog，”那声我熟悉的呼唤响起。那是我的一个年轻朋友 Eduardo 的声音。“你为什么把你的船命名为 Agape？是因为这艘船很宽敞吗？”我停下手里的活儿，不再打磨我的小帆船，转而面向我的年轻朋友。“不，这个词不是英语，而是拉丁语。它的意思并不是为了与一种常用于酿酒的小水果押韵，而是为了表达最高形式的爱。”Eduardo 看了我一会儿，说：“我不知道你会说除英语以外的语言。”“大部分情况下，我不会，”我回答。“我在几十年前的小学学习过拉丁语和法语，但当我意识到掌握多种语言的价值时，大部分那些训练已经溜走了。然而，学过拉丁语和法语确实有时会派上用场，因为我有时会发现那些被遗忘的训练有助于理解外语和我们母语英语中的新词。现在，我研究的语言主要是计算机语言。”“这是另一回事，”Eduardo 说。“当你真正需要的只有 Java 时，为什么会有这么多语言？”我放下打磨块，靠在 Agape 船上，仔细思考了一会儿。

FORTRAN 是我学会的第一种计算机语言。那是 1969 年，我通过阅读一本名为《使用 FORTRAN 对 IBM 1130 进行编程》的书来学习 FORTRAN，并在一个拥有 4,000 字主存、一个卡片阅读器/穿孔机的 IBM 1130 计算机系统上进行实践。该系统还有一个链式打印机（你最好别知道那是什么）和一个笔式绘图仪。注意，这种语言的名字是 FORTRAN，全是大写字母。那是我们当时书写的样子，因为它代表 FORmula TRANslator（公式翻译器），就像 COBOL 代表 Common Business Oriented Language（面向通用业务的语言）一样。FORTRAN 是面向工程师和科学家的，而 COBOL 是面向商务人士的。这两种语言都相当出色地完成了它们的工作。

因为我是工程专业的学生，也是 Western Electric Corporation（贝尔系统的成员）的合作实习生，所以我学习了 FORTRAN。在某个时间点，营销人员决定人们不喜欢名字中使用全大写字母，于是这种语言被称为 Fortran。多年来，FORTRAN（始于 1950 年代初）变成了 FORTRAN II，FORTRAN III，FORTRAN IV，然后开始使用与其更新年份相关的名称。如今，正在为 Fortran 2008 的定义做工作。Fortran 是一个很好的例子，说明一种语言（不仅仅是名字）如何改变以适应时代的需求。

从 Drexel Institute of Technology（现为 Drexel 大学）的合作实习期返回后，我开始寻找更多被称为计算机的设备。我在电气工程学院的计算机实验室里发现了多台 Digital PDP-8 小型计算机。尽管这些系统有一种类似于 FORTRAN 的小型语言，称为 Focal，但 Drexel 大学的 PDP-8 小型计算机大多是用汇编和/或机器语言编程的，也就是机器使用的 0 和 1。

我得到了一些关于如何用机器语言为 PDP-8 编程的书，并自学了如何使用计算机最基础的语言进行编程。幸运的是，PDP-8 的机器语言非常简单，只有八条基本指令和一个充当“累加器”的主寄存器。每条指令的长度都相同，并且符合 12 位的字长，因此 PDP-8 简单但繁琐。PDP-8 不能做减法（更不用说乘法或除法了），因此你必须加上减数的二补数来进行减法。

处理器的前面板上有开关和指示灯，通过拨动这些开关，你可以直接将程序输入到系统内存中。更重要的是，你可以每次执行一条机器语言指令来单步执行你的程序，在机器的累加器和程序计数器（也由控制台上的指示灯表示）上查看每条指令的结果。

当然，大多数人不会通过开关输入整个程序；他们使用 ASR-33 Teletype 将汇编语言的源代码输入到编辑器中，将源代码打印到纸带上，将该纸带输入到汇编器中，最终得到一条包含要输入到计算机中的 1 和 0 的目标级纸带。

程序的一次周转至少通常需要 45 分钟。将编辑器（纸带）读入需要五分钟。接下来，你输入你的程序，进行几次编辑，并将你的程序穿孔到新的纸带上。然后，你读入三遍汇编器（15 分钟的纸带读取时间），读入你的源代码程序（假设你的纸带没有撕裂），并穿孔输出包含你程序的二进制（纸）带。

最后，你将二进制纸带读入计算机内存，看着程序很可能覆盖了实际内存中的它自己和其他所有内容，然后你重新开始整个过程

