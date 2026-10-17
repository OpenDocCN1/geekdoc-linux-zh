
```cpp
{
    _where->writePinLow(PIND7);
}
```

```cpp
int main(void)
{
    mmapGpio rpiGpio;
    //Set outputs
    rpiGpio.setPinDir(PINA0,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PINA1,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PINA2,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PINA3,mmapGpio::OUTPUT);
    //TURN OFF ASAP!
    rpiGpio.setPinDir(PINCS0,mmapGpio::OUTPUT);
    rpiGpio.writePinHigh(PINCS0);
    //TURN ON ASAP!
    rpiGpio.setPinDir(PINCS1,mmapGpio::OUTPUT);
    rpiGpio.writePinHigh(PINCS1);
    rpiGpio.setPinDir(PIND0,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PIND1,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PIND2,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PIND3,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PIND4,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PIND5,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PIND6,mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PIND7,mmapGpio::OUTPUT);

    unsigned char dataStore[2][16];

    for(int j=0;j<2;j++)
    {
        for(int k=0;k<16;k++)
        {
            dataStore[j][k]=64;
        }
    }

    int blockCounter=0;
    int rowCounter=0;
    while(1)
    {
        blockCounter++;
        if(blockCounter==16)
        {
            if(rowCounter==0)
            {
                blockCounter=0;
                rowCounter=1;
            }
            else
            {
                blockCounter=0;
                rowCounter=0;
            }
        }

        safelySetRow(rowCounter, &rpiGpio);
        setAddress(blockCounter, &rpiGpio);
        setData(dataStore[rowCounter][blockCounter], &rpiGpio);
        usleep(50);
    }
    return 0;
}
```

## 数字助手，第二部分：语音识别

在这第二期文章中，学习如何解码你的音频，并弄清楚周围的人正在发出什么指令。

![](img/c9d26cf718256f071c3af699b9670538_71_0.png)

**乔伊·伯纳德 (Joey Bernard)**

作为一个真正的文艺复兴人，他将在制作家具、帮助研究人员解决科学计算问题以及编写 Android 应用之间分配他的时间。

### 任务卸载

你可以将音频数据处理卸载给 Google，通过 HTTP 直接访问 API，将你的音频数据发布到适当的 URL。首先安装 Python 模块 `SpeechRecognition`：

- `pip install SpeechRecognition`

现在创建一个 `Recognizer` 对象的实例。一个名为 `WAVFile` 的辅助对象将获取音频文件并准备它供 Google API 使用。然后使用 `record()` 函数处理它，并将处理后的音频传递给要识别的函数。当它返回时，你将获得一个可能的文本列表，以及每个可能文本的置信度百分比。

**右方** CMUSphinx 用于跨平台、开源项目，如智能学习助手 ILA

在上一期中，我们探讨了如何让我们的树莓派聆听周围的世界。这是构建我们自己的 JARVIS 系统版本的第一步，该系统因 `钢铁侠` 电影而闻名。下一步是尝试理解我们刚才听到的内容。通常，这被称为语音识别，它是一个非常庞大且活跃的研究领域。每个主要的移动操作系统都有应用程序试图利用这种人类交互模式。也有几个不同的 Python 模块可用，可以进行这种语音到文本 (STT) 的转换。在这第二篇文章中，我们将查看使用 Pocket Sphinx 来承担繁重的工作。Sphinx 由卡内基梅隆大学开发，并采用 BSD 许可证授权，因此你可以自由添加特定任务所需的任何此类功能。鉴于该领域的活跃程度，花费时间跟踪所有更新和性能改进是非常值得的。

```bash
sudo apt-get install python-pocketsphinx
```

```bash
sudo apt-get install pocketsphinx-hmm-wsj pocketsphinx-lm-wsj
```

...以获取引擎所需的所有文件。你还需要音频模型文件和语言模型文件才能以你选择的语言进行转换。要获取英文所需的文件，你可以安装包：

如果你需要处理其他语言，可能需要走出常规包管理系统。然后你就可以直接开始编写和使用代码了。要开始使用这些模块，你需要通过以下方式导入 `pocketsphinx` 和 `sphinxbase`：

```python
import pocketsphinx as ps
import sphinxbase
```

虽然我们可以在网上下载所有这些模块的源代码并从头构建它们，但我们要假设你使用的是基于 Debian 的发行版，如 Raspbian。对于这些发行版，你可以简单地使用：

这些模块实际上是围绕处理将声音转换为文本的实际计算工作的 C 代码的 Python 封装。最基础的工作流程包括从 `pocketsphinx` 模块实例化一个 `Decoder` 对象。`Decoder` 对象接受多个输入参数来定义它允许使用的语言文件。这些包括 `"hmm"`、`"lm"` 和 `"dict"`。如果你使用上述用于处理英文的包，那么你需要的文件将位于目录 `/usr/share/pocketsphinx/model/hmm/wsj` 和 `/usr/share/pocketsphinx/model/lm/wsj` 中。如果你没有设置这些参数，那么它会尝试使用合理的默认值，这对于英文语音通常工作得非常好。这个新创建的 `Decoder` 对象现在可以被赋予带有待处理数据的 WAV 文件。如果你还记得上一期，我们将录制的语音保存为 WAV 文件。为了以正确的格式记录此音频，你需要编辑上一期的代码并确保你以单声道（例如使用一个声道）录制，并以 16kHz 和 16 位样本进行录制。为了正确读取它，你可以使用一个文件对象，并以读权限将其加载为二进制文件。WAV 文件在文件开头有一小部分头部数据，你需要跳过去。这是通过使用 `seek` 函数跳过前 44 个字节来完成的。现在文件指针位于正确的位置，你可以将文件对象传递给 `Decoder` 对象的 `decode_raw()` 函数。然后它会离开并进行一系列的数据处理，试图弄清楚说了什么。要获取结果，你需要使用 `get_hypid` 函数调用。从这个函数中你会得到一个包含三个元素的列表：一个包含对说话文本最佳猜测的字符串，一个包含话语 ID 的字符串，以及一个包含此猜测得分的数字。

## Python 栏目
