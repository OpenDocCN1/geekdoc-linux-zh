
| | | sort | 拓扑排序 | | |

### P

| 命令 | 描述 | 命令 | 描述 | 命令 | 描述 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| printf | 打印环境变量 | xargs | 构建参数列表执行工具 | | |

| printf | 打印字符串直到中断 | Y | | | |

| | | tar | 归档压缩工具 | | |

| | | test | 评估条件表达式 | | |

| | | time | 测量程序资源使用 | | |

# 使用终端

![](img/9eddebb0cf792a0bbe16478be74a68e1_83_0.png)

> 你知道吗……NASA 珍贵的超级计算集群 Pleiades 是由 Linux 驱动的？Pleiades 由 160 个机架（11,440 个节点）、245,536 个 CPU 核心、总计 93TB 的内存、184,320 个 NVIDIA CUDA 核心以及超过 6 英里的光纤缆组成。

NASA 的项目。NASA 高级超级计算部门使用 Pleiades 的项目包括：开普勒任务——寻找太阳外的类地球行星；CFD（计算流体力学）建模以帮助创建高效的太空发射系统；暗物质研究与模拟；地球洋流的可视化，为 ECCO（海洋环流和气候估计）项目构建数据。

其核心是一套复杂的 SUSE Linux Enterprise Server 配置，以及许多自定义开发包和其他独有的软件。

## 你知道吗……

NASA 运行在 Linux 上的超级计算机 Pleiades，目前位居全球最强第 11 位。

![](img/9eddebb0cf792a0bbe16478be74a68e1_84_0.png)

![](img/9eddebb0cf792a0bbe16478be74a68e1_84_1.png)

## 对 NASA 来说足够

www.bdmpublications.com 85

# Linux Python

> “Python 是一场关于程序员需要多少自由的实验。自由太多，没有人能读懂别人的代码；自由太少，表达力就会危险。”

—— Guido van Rossum（Python 语言开发者）

Python 是一门极佳的编程语言，它将易用性和强大的功能相结合，允许用户创建微型工具或处理性能密集型计算任务。

然而，Python 不仅仅是另一种编程语言。它背后有一个活力且活跃的社区，他们分享知识、代码、项目想法，以及未来版本的错误修复程序。

我们在书的这一部分使用了树莓派（Raspberry Pi），因为它基于 Linux 并且是可用最佳编程平台之一。树莓派的特性和功能使其成为完美的 Python 编程伙伴，让我们让我们开始吧。

- 为什么选择 Python？
- 如何在 Linux 中安装 Python
- 首次启动 Python
- 你的第一行代码
- 保存并执行你的代码
- 从终端执行代码
- 你知道吗……《太空入侵者》
- 数字与表达式
- 使用注释
- 变量操作
- 用户输入
- 创建函数
- 条件与循环
- Python 模块
- 你知道吗……调试

![](img/9eddebb0cf792a0bbe16478be74a68e1_86_0.png)

## 为什么选择 Python？

现代计算机有很多不同的编程语言可用，一些旧的 8 位和 16 位计算机也有一些语言可用。其中一些语言是为科学工作设计的，另一些是为移动平台等设计的。在所有语言中，你为什么选择 Python 呢？

## Python 之

自从最早的计算机出现，爱好者、用户和专业人士一直在刻苦工作，在过热的计算热量中劳作，创造出类似的东西。

这些编程先驱开辟了通往新领域的道路，通过战斗微小的战斗，让字母 'A' 能够在屏幕上滚动。对于习惯了超高定义图形和开放世界多人游戏的一代人来说，这听起来可能并不非常令人兴奋。然而，在四十年前它是光彩夺目的精彩。

无论你使用的是 Android 设备、iOS 设备、PC、Mac、Linux、智能电视、游戏机、MP3 播放器、内置 GPS 导航、机顶盒或其他数千种连接“智能”家电器，这一切都是编程。

自然地，这些基石为我们今天使用的每项技术奠定了基础。其中一些成为了软件公司的首席开发者，而另一些则将可用硬件推向了极限，并建立了不断积累财富的十亿英帝国。

所有上述数字设备都需要指令来告诉它们做什么，并允许与其交互。设备编程核心的指令可以使用多种编程语言构建。

你所使用的语言取决于情况、平台设备以及设备将如何与环境或交互。

![](img/9eddebb0cf792a0bbe16478be74a68e1_87_0.png)

```cpp
void SetCursor(p.y) {
    ctrl:SetFocus();
}

void Array::ChildFocus() {
    if(cursor == 0) {
        refreshCursor();
        ctrl:SetFocus();
    }
}

void Array::Draw(Rect w) {
    Size size = GetSize();
    rect(0,0,size.width,size.height);
    if(header.HasCursor()) {
        int xs = header.GetScroll();
        for (int j = 0; j < col.Count(); j++) {
            if (xs == 0) {
                xs += col.Width(j);
            }
        }
    }
    Color fc = Blend(SclBlue, Color);
    while (i < GetCount()) {
        if (rect.top > GetCursor()) {
            rect.top = GetLineY(i);
        }
        rect.bottom = GetLineY(i);
        int cw = header.TabWidth(j);
        if (i < 0) {
            rect.left = rect.left;
            rect.right = rect.right - (i == ColCount() - 1);
        }
    }
}
```

## 为什么选择 Python？

操作系统（如 Windows, macOS）通常是 C++ 和某些基于视觉的语言的组合。通常使用 C++ 并辅以如 HTML、Java 等大量可用语言。

Python 创建于二十多年前，已经演变成一门学习编程的理想语言。它对于爱好者、狂热者以及那些需要为硬件本身创建独特交互的人来说都是完美的。

更通用的编程被被用于创建程序、应用程序、他们想要的任何内容。它们被广泛应用于所有平台和几乎每个应用程序。有些变化比其他快，而 Python 就是其中一种通用语言。

Python 免费下载、安装，并适用于 Linux、Windows、macOS、FreeBSD、IBM 系列机器，它一直是世界上前五大编程语言之一，并持续领先于硬件和互联网的发展。

Python 被称为高级语言，因为它易于阅读。它非常适合初学者，因为它是易于学习的。
