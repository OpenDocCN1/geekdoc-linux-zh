
然后才能开始与麦克风交互。`PyAudio`的工作方式类似于处理文件，因此对于大多数程序员来说应该很熟悉。你通过语句 `p = pyaudio.PyAudio()` 开始创建一个新的 `PyAudio` 对象。然后你可以使用函数 `p.open(...)` 打开一个输入流，它有几个参数。你可以设置录音的数据格式；在示例代码中我们使用了 `format=pyaudio.paInt16`。你可以设置采样率（赫兹）。例如，我们使用的是 `rate=44100`，这是标准的 44.1KHz 采样率。你还需要说明录音使用的缓冲区大小 – 我们使用了 `frames_per_buffer=1024`。由于我们要录音，你需要使用 `input=True`。最后一个参数是选择要录制的声道数，在这种情况下我们将使用 `channels=2`。流打开后，你可以开始从中读取。你需要使用创建流时使用的相同块大小来读取音频数据 – 它看起来像 `stream.read(1024)`。然后你可以简单地循环读取直到完成。然后有两个命令用于关闭输入流。你需要调用 `stream.stop_stream()` 然后 `stream.close()`。如果你完全做完了，你可以现在调用 `p.terminate()` 来关闭到树莓派上音频设备的连接。

下一步是能够发送音频输出，以便贾维斯也可以与你交谈。为此你可以使用 `PyAudio`，所以我们不需要查看另一个 Python 模块。为了简单起见，假设你有一个想要播放的 WAVE 文件。你可以使用 `wave` Python 模块来加载它。同样，你将创建一个 `PyAudio` 对象并打开一个流。参数 `output` 应设置为 `true`。格式、声道数和速率都是从存储在 WAVE 文件中的音频数据中得出的信息。要实际听到

# 创建你自己的数字助手

#### 完整代码列表

```python
# You need to import the pyaudio module
import pyaudio

# First, we will listen
# We need to set some parameters
# Buffer chunk size in bytes
CHUNK = 1024
# The audio format
FORMAT = pyaudio.paInt16
# The number of channels to record on
CHANNELS = 2
# The sample rate, 44.1KHz
RATE = 44100
# The number of seconds to record for
RECORD_SECS = 5

# Next, we create a PyAudio object
p = pyaudio.PyAudio()

# We need a stream to record from
stream = p.open(format=FORMAT, channels=CHANNELS,
    rate=RATE, input=True, frames_per_buffer=CHUNK)

# We can now record into a temporary buffer
frames = []
for i in range(0, int(RATE / CHUNK * RECORD_SECS)):
    data = stream.read(CHUNK)
    frames.append(data)

# We can now shut everything down
stream.stop_stream()
stream.close()
p.terminate()

# If we want to play a wave file, we will need the wave module
import wave

# We can open it, give it a filename
wf = wave.open("filename.wav", "rb")

# We need a new PyAudio object
p = pyaudio.PyAudio()

# We will open a stream, using the settings from the wave file
stream = p.open(format=p.get_format_from_width(wf.getsampwidth()),
    channels=wf.getnchannels(), rate=wf.getframerate(),
    output=True)

# We can now read from the file and play it out
data = wf.readframes(CHUNK)
while data != b'':
    stream.write(data)
    data = wf.readframes(CHUNK)

# Don't forget to shut everything down again
stream.stop_stream()
stream.close()
p.terminate()
```

对于音频，你只需循环遍历，每次从 WAVE 文件中读取一块数据，并立即写入 `PyAudio` 流。完成后，你可以像上面那样停止流并关闭它。

在上述两种情况下，当你调用这些函数时，它们会阻塞，直到它们完成。如果你希望在录制音频或输出音频时仍能进行其他处理，有哪些选项？存在非阻塞版本，它们接受一个名为 `stream_callback` 的回调函数作为额外参数。这个回调函数接受四个参数，分别命名为 `in_data`、`frame_count`、`time_info` 和 `status`。如果 `input` 为 true，则 `in_data` 参数将包含录制的音频。回调函数需要返回一个包含 `out_data` 和 `flag` 的元组。如果调用函数 `open` 时 `output` 为 true，则 `out_data` 包含要输出的数据。如果输入为 true，则 `out_data` 应等于 `None`。flag 可以是 `paContinue`、`paComplete` 或 `paAbort` 中的任意一个，含义显而易见。需要注意的是，当你希望使用回调函数时，不能调用 `read` 或 `write` 函数。一旦流打开，你只需调用函数 `stream.start_stream()`。这会启动一个单独的线程来处理此流处理。你可以使用 `stream.is_active()` 来检查当前状态。一旦流处理完成，你可以调用 `stream.stop_stream()` 来停止次要线程。

既然我们已经介绍了如何从树莓派获取和输出音频信息，你可以开始将这种功能添加到你的下一个项目中。在下一步中，我们将看看如何使用语音识别模块将这些音频信息转换为计算机可用的形式。我们还将探讨使用 TTS 模块将文本转换为音频输出的不同方法。

# 数字助手，第 2 部分：语音识别

在这个第二部分中，学习如何解码你的音频数据，并弄清楚周围的人正在发出什么指令。

## 转接任务

你可以将音频数据处理转交给 Google，通过 HTTP 直接访问 API，将你的音频数据发布到适当的 URL。首先安装 Python 模块 `SpeechRecognition`：

```bash
$ pip install SpeechRecognition
```

现在创建一个 `Recognizer` 对象的实例。一个名为 `WaveFile` 的 Helper 对象将获取音频文件并准备供 Google API 使用。然后使用 `record()` 函数处理它，并将处理后的音频交给函数 `recognize()`。当它返回时，你将得到可能的文本对的列表，以及每个可能文本解码的置信百分比。请注意，此模块使用非官方 API 密钥，因此对于超过小规模个人测试的任何用途，你应该申请自己的 API 密钥。

![](img/a1548a579bd09ff29b2b92de3f565e63_77_0.png)

之前我们看了如何使用树莓派监听周围的世界。这是构建我们自己的 J.A.R.V.I.S 系统的第一步，该系统因《钢铁侠》电影而闻名。下一步是尝试理解我们刚才听到的内容。通常，这被称为语音识别，它是一个非常大且活跃的研究领域。每个主要的移动操作系统都有应用程序试图利用这种人类交互模式。还有几个不同的 Python 模块可以实现这种语音到文本（STT）转换步骤。在第二篇文章中，我们将看看如何使用 `Pocket Sphinx` 来承担所有繁重的工作。`Sphinx` 由卡内基梅隆大学开发，并在 BSD 许可证下授权，因此你可以自由添加特定任务所需的任何额外功能。由于该领域的活跃性，花时间跟踪所有更新和性能改进是非常值得的。

虽然你可以下载所有这些模块的源代码并从零开始构建，但我们假设你使用的是基于 Debian 的发行版，如 Raspbian。对于这些发行版，你只需使用：

```bash
$ sudo apt-get install python-pocketsphinx
```
