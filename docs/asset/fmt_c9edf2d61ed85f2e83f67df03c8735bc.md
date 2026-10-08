
有什么帮助理解这个吗？

顺颂商祺。

标签c (上一个问题), exploit (上一个问题) (下一个问题)

*(注：提供的 OCR 文本从 47 页开始有很多重复/乱码。我将根据提供的段落提供一个清理后的版本。)*

## Q: 动态 Java 插桩 (dynamic instrumentation)?

标签: dynamic-analysis (上一个题) (下一个题), java (上一个题) (下一个题), android (上一个题) (下一个题)

这并不是严格意义上的“逆向工程”，它主要与动态插桩有关。
就像 `strace` 允许你查看进程的系统调用，或者使用 `ftrace` 查看函数调用一样，Java 是否有类似的工具？

我感兴趣的是一个运行在 `javaVM` 中的 `.jar` 文件。
是否有任何方法可以对应用程序产生的所有 Java API 调用进行插桩或追踪？
也就是说，不需要对 `.jar` 内容进行任何静态分析，也不需要对 `.jar` 内容进行任何修改（例如添加钩子 `hooks`）。理想情况下，有一种解决方案可以提取或追踪例如被修改过的 `javaVM` 的行为。

这在 Android 上同样适用——如果环境/系统正常，是否有方法可以在不修改 APK 文件的情况下，追踪应用程序的所有 Android 框架 API 调用（或其他本质的 Dalvik VM 函数）？
在我的理想中，分析师在运行**未修改**的应用程序（jar 或 .apk）时会得到如下输出：

| 时间戳 | 事件 | 参数 |
| :--- | :--- | :--- |
| timestamp1 | java.security.Random.getSeed() called. | (Number) |
| timestamp2 | java.security.X509Certificate.checkValidity() called. | (null) |
| timestamp3 | java.sql.Connection.prepareStatement() called. | ("SELECT * FROM X WHERE w = ") |

标签: dynamic-analysis (上一个题) (下一个题), java (上一个题) (下一个题), android (上一个题) (下一个题)

用户: javasec

perror 回答

## Oracle Java 虚拟机

可以通过 Java 平台调试器架构 (`JPDA`) 实现 Java 程序的执行追踪。该框架允许你对 JVM 内的执行进行完全控制（无需修改原始代码）。请参考此教程以深入了解该框架。

如果你想自己实现它，应该使用 `MethodEntry` 接口并拦截任何方法调用。
但，如果你很懒（就像我一样），最好使用已有的项目，例如 `InTrace`（另见 InTrace 项目的相关项目页面）。

## Android Java Dalvik 虚拟机

可以通过 Dalvik 调试监控服务器 (`DDMS`) 和完整的 Android 调试框架实现 Android Java 程序的追踪。

已经存在可以追踪程序执行的工具，例如 `Traceview` 和 `dmtracedump` 工具。最后，关于 Dalvik JVM 有一些提示。

ange 回答

你可以使用代理（agent）对 Java 进行插桩，它会操作已加载文件的字节码（建议使用 `ASM` 进行字节码操作）。

你可能想使用 Eclipse 的 Bytecode Outline 插件来调试执行执行。。

这是一个关于该主题的优秀教程。

mathew-hall 回答

`AspectJ` 可以通过加载时织入 (`load-time weaving`) 在 JVM 上实现此功能。它是基于 `Asm` 构建的，因为它提供了更多抽象（不涉及字节码）。追踪方法调用非常简单：首先定义一个过滤器来匹配你感兴趣的“切入点 (pointcuts)”，然后指定你想执行的动作（“建议 (advice)”）。

不过语法有点别扭：

```
// Skip code block
package aspects;

import java.util.logging.Level;

import java.util.logging.Logger;

import org.aspectj.lang.Signature;

aspect Trace {

    pointcut traceMethods() { (execution(* ..)) && cflow(within(Trace))); }

    before(traceMethods()) {

        Signature sig = thisJoinPointStaticPart.getSignature();

        String line="\+thisJoinPointStaticPart.getSourceLocation().getLine();

        String sourceName = thisJoinPointStaticPart.getSourceLocation().getWithinType().getCanonicalName();

        Logger.getLogger("Tracing").log(

            Level.INFO,

            "Call from "

            + sourceName

            " line "

            + line

            " to "

            + sig.getDeclaringTypeName() + "." + sig.getName()

        );

    }

}
```

使用 `ajc -outxml -outjar aspects.jar Trace.java` 编译。

使用织入器运行 `FooClass`，执行：

`java -javaagent:aspectjweaver.jar -cp aspects:${target_name} FooClass`

标签: dynamic-analysis (上一个题) (下一个题), java (上一个题) (下一个题), android (上一个题) (下一个题)

## Q: 什么是 MSR 追踪？

**标签:** dynamic-analysis (上一个题) (下一个题)

我正在读一篇关于 MSR 追踪的旧帖子，但我不懂它是什么。
**标签:** dynamic-analysis (上一个题) (下一个题)
用户: javasec

perror 回答

`MSR`（模型特定寄存器）是 x86 处理器中的寄存器，可用于调试、性能监控等。在追踪上下文中，它通常指的是诸如分支追踪存储 (`BTS`) 或最后分支记录 (`LBR`)，这些功能允许硬件以最小的开销记录执行流。

有几种方法可以使用它：

1. **BTS (Branch Trace Store):** 一项将处理器跳转的每一个分支记录到内存缓冲区中的功能。它可以非常详细，但开销较高且会迅速填满缓冲区。
2. **LBR (Last Branch Record):** 一项记录处理器跳转的最后 N 个分支的功能。它的开销非常低，但只提供最近分支的有限历史。

通常，MSR 追踪用于性能分析，并通过查看事件发生“之前”的执行路径来识别性能瓶颈或崩溃。

User: perror

回答由 brendan-dolan-gavitt

`PANDA` 开发人员。我实际上测试过，你想要的大多数功能 QEMU 的原生 gdbstub 都支持。如果你在使用 QEMU 时使用了 `-s -S` 选项，它将监听端口 `1234` 以待传入连接，并提供你所需的功能：

- 使用 `si` 命令进行单步执行
- 使用 `info reg` 和（例如）`set $edi = 0x40c8c39` 获取/设置寄存器
- 使用 `x` 命令读取内存内容
- 使用 `set (*char) 0x1a5f2c0 = 0xd9` 修改内存
- 使用（例如）`break *0x826e2671` 设置断点

因此通过 gdb 脚本，我认为你应该能够通过原生 gdb 和 QEMU 获得你想要的能力。

所有这些都已使用 Windows 7 32位虚拟机和使用 `target remote :1234` 命令的 gdb 完成测试。

标签：dynamic-analysis (上一个问题) (下一个问题)

# Q：在动态分析期间使用 SSA（单赋值静态赋值）

标签：dynamic-analysis (上一个问题)

我读过可以使用 `PIN` 或 `Valgrind` 等工具进行动态插桩。然而，`Valgrind` 提供中间表示并将二进制文件转换为 SSA，这使得执行二进制分析更加方便。有没有人能解释一下为什么使用 SSA 形式会更方便？为什么在没有中间表示的情况下使用 `PIN` 进行动态分析很困难？

谢谢。

标签：dynamic-analysis (上一个问题)

User: user1004985

回答由 yaspr

回答这个问题需要的空间比提供的多得多。我更倾向于向你推荐你可以找到的最佳资源，以便深入理解对 SSA 的需求。

首先，从维基百科开始，熟悉 SSA 的基本结构和构建块（Phi 函数等）。然后，阅读这篇发表于 1991 年的参考文章，它比维基百科的文章复杂一些。

如果你想要一个更详细的尽管不完整的文档，请阅读这本书。它涵盖了用于构造/破坏以及分析的广泛算法。

如果你想要一个长且详细的回答，请告诉我，我可以写一个正式的。

标签：dynamic-analysis (上一个问题)

# 文件格式

跳转到问题，

Wiki 由用户 [aperson]() 创建

**文件格式**仅仅是数据编码的方式。你通常可以通过文件扩展名识别它们；例如，扩展名为 `.html` 的文件可能是一个 HTML 文档，而扩展名为 `.gif` 的文件可能是一个 GIF 图像文件。

在逆向工程中，`file-format` 标签用于关于确定给定文件格式的问题，以及关于逆向工程某些文件格式的问题。

来自 [Wikipedia]()

**文件格式**是用于对信息进行编码以存储在计算机中的标准方法。文件格式规定了如何使用位在数字存储介质中编码信息。文件格式可以是专有的或免费的，可以是未发布的或开放的。

某些文件格式是为了非常特定类型的数据设计的：例如，PNG 文件使用无损数据压缩存储位图图像。然而，其他文件格式是为了存储多种类型的数据设计的：Ogg 格式可以作为不同类型多媒体的容器，包括音频和视频的任何组合，或者不带文本（如字幕）以及元数据。文本文件包含各种字符编码方案之一。某些文件格式，如 HTML、可缩放矢量图形和计算机软件源代码，是用允许它们用于特定目的的句法定义的文本文件。

# 常见问题

- [在哪里可以找到关于文件格式的信息？]
- [文件格式逆向工程的自动化工具？]()
- [如何逆向工程专有数据文件格式（例如 Smartboard Notebook）？]()

## 问题

# Q：如何逆向工程专有数据文件格式（例如 Smartboard Notebook）？

标签：dynamic-analysis (上一个问题) (下一个问题)

逆向工程专有数据文件格式（如 Smartboard Notebook）的方法是：首先，使用十六进制编辑器查看文件头部（魔数/Magic Bytes）。许多格式在文件开头有特定的字节来标识类型。如果文件是压缩的，尝试使用解压工具查看其内容。如果它是加密的，则可能需要找到密钥。通过分析该软件如何读取这些文件也可以推断其结构。

如果你想通过手动方法，你需要将文件的子集与已知的签名或模式进行匹配。这对于可能被压缩的文件格式尤其适用，因为数据模式的规律性会降低。因此，你需要在文件中找到一种模式，通常称为签名（signature）或指纹（fingerprint）。大多数文件的头部或尾部都有魔数（magic numbers），方便程序检查它们要加载的是什么类型的文件。关于知名的文件签名，有一些不错的资源：

- * Garry Kessler 的文件签名列表
- * 维基百科上的文件签名列表
- 文件签名数据库

由 0xc00000221 回答

Peter 的建议一如既往地优秀。我想补充几点：

- * 如果你有可以使用该格式程序的访问权限，你始终可以通过逆向工程来寻找有关该格式的细节，甚至获取它正在寻找的签名（例如，假设它包含某些样本但是一个专有且不为人知的格式）
    * 这可能提供有关访问该格式的库的线索，从而提供有关格式的线索（想想 IDA FLIRT/FLAIR）
- * 使用 VLC 的其他媒体播放器也是查找细节的好方法（ctrl+J 和 ctrl+I）。也就是说，你只需尝试打开它，看看播放器能给你提供什么媒体信息。良好的播放器不会强制你在打开之前保留特定的文件扩展名。但要警惕潜在的漏洞（即在沙箱环境中操作）

由 nneaneo 回答

除了其他回答中的几个建议外，这里是一些针对音频的特定建议：

- * 如果你大致知道音频的播放时长，计算音频文件的近似比特率。这会告诉你它是否经过了压缩，压缩率可以大致告诉你你正在处理的是什么。例如，4kbps~32kbps 是语音编码器的指示，64~256kbps 是压缩音频（MP3/OGG Vorbis），512~3072kbps 是无损编码器，显著的高则意味着未压缩或弱压缩（例如 ADPCM, PCM）音频。反之，你可能会推测出它包含的内容（语音、音乐、音效等）。
- 如果你怀疑它是弱压缩的，可以尝试在你喜爱的音频编辑器（如 Audacity）中将文件作为 PCM 流打开并听听。如果它经过任何形式的压缩，可能会有大量的噪声，但如果某些格式（如 ADPCM）是恒定比特率，在这种情况下仍然可以使用。我过去曾用这种策略来分析我收到的某个（仍未知）音频样本的口语内容。事实上，这种策略可以利用人类的模式识别能力揭示加密不良、未压缩文件的内容。

- 检查文件中的元数据块——字符串、在编辑器中快速检查文件的第一个和最后一个块，或者直接搜索你可能看到的字符串。

标签：file-format (上一个问题) (下一个问题)

## Q: 在哪里可以找到关于文件格式的信息？

标签：file-format (上一个问题) (下一个问题)

假设有“某个”文件（可能是可执行文件，可能是数据或其他），并且我想要运行或编辑它。如果我用文本编辑器打开这个文件，其格式是不可读的。示例包括：Java 类、Windows 可执行文件、SQLite 数据库、DLL 等……

如果我们可以信任扩展名，我就知道文件格式。

是否有某个网站或数据库包含大量关于低加密或二进制文件格式的信息？信息应该包括：

- 文件的用途
- 文件布局和结构
- 最终可以读取或执行该文件的程序

我并不是在寻找识别文件格式的方法。我已经知道文件格式，但需要关于该格式的信息。当格式被使用时，它的结构是什么？

标签：file-format (上一个问题) (下一个问题)

用户：camil-staps

由 nneonne 回答

我是 Hachoir 项目的开发者，项目旨在描述任何文件的格式。目前它拥有许多已知格式的解析器，包括 Java 类、Windows 可执行文件、MP3 文件等。在开发新的解析器时，必须找到关于格式的信息。没有单一来源可以描述每种格式，通常第一步是搜索<格式名称>，并在官方网站查找文档。如果没有官方网站，你仍然可以从那里获取 90% 的格式文档。对于常见格式，像 Oracle 和 Microsoft 这样的大公司为了互操作性目的，提供了 PE (EXE/DLL)、XLS、PPT 等格式的文档，你可以浏览 MSDN。对于多媒体格式，维基百科是一个很好的资源。它们也涵盖了一些游戏格式。对于不常见的格式，如果通过 Google 无法获得规格，我的方法通常是找到一个理解该文件的开源程序，并定位他们的文件规格源——这可能也会提供有关访问该格式的库的线索，从而提供有关格式的线索（想想 IDA FLIRT/FLAIR）。

- 使用 VLC 的媒体播放器也是查找细节的好方法（ctrl+J 和 ctrl+I）。也就是说，你只需尝试打开它，看看播放器能给你提供什么媒体信息。良好的播放器不会强制你在打开之前保留特定的文件扩展名。但要警惕潜在的漏洞（即在沙箱环境中操作）

- 如果你有可以使用该格式程序的访问权限，你始终可以通过逆向工程来寻找有关该格式的细节，甚至获取它正在寻找的签名（例如，假设它包含某些样本但是一个专有且不为人知的格式）

- * 如果你大致知道音频的播放时长，计算音频文件的近似比特率。这会告诉你它是否经过了压缩，压缩率可以大致告诉你你正在处理的是什么。例如，4kbps~32kbps 是语音编码器的指示，64~256kbps 是压缩音频（MP3/OGG Vorbis），512~3072kbps 是无损编码器，显著的高则意味着未压缩或弱压缩（例如 ADPCM, PCM）音频。反之，你可能会推测出它包含的内容（语音、音乐、音效等）。

- 如果你怀疑它是弱压缩的，可以尝试在你喜爱的音频编辑器（如 Audacity）中将文件作为 PCM 流打开并听听。如果它经过任何形式的压缩，可能会有大量的噪声，但如果某些格式（如 ADPCM）是恒定比特率，在这种情况下仍然可以使用。我过去曾用这种策略来分析我收到的某个（仍未知）音频样本的口语内容。事实上，这种策略可以利用人类的模式识别能力揭示加密不良、未压缩文件的内容。

（注：原文后半存在大量重复段落，已根据要求去重处理，仅保留核心逻辑翻译）

```python
data = "\xff\xff\x04\x05\x04test\x02A\x04\x03\x04\x05\x00\x00\x05\x05test\x02\x03\x05test"

position = 0

print ""

position += 1

DecodeData(position)

print "\xff - ?"

print ""

position += 1

DecodeData(position)

print "\x05 - ?"

print ""

position += 1

size_in_bytes = DecodeData(position)

position += 1

Readword(position, size_in_bytes)

print ""

position += 1
```
