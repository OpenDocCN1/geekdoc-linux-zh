
## 第 5 步：配置 vgetty 监听电话

`vgetty` 守护进程用于监听电话线上的入站电话。以下描述详细说明了如何配置此项目包含的特殊补丁 `vgetty`：

1. 以 root 用户身份登录。
2. 查看 `/dev/modem` 指向设备是 `/dev/tty0` 或 `/dev/tty1`（你懂的）。
3. 打开 `etc/mgetty-sendfax/voice.conf`（使用任何文本编辑器），检查其中的值。我们期望大多数情况下默认值是有效的：

```
voice_devices modem
rings 3
call_program /usr/local/vocp/bin/vocp
```

4. 如果需要，通过以下命令停止进程：

```
# kill -9 mgetty
```

5. 如果进程正在运行，通过以下命令检查状态：

```
# ps -ef | grep mgetty
```

6. 为了测试调制解调器，重新启动进程。
7. 在电话接听前默认的响铃数是 3。我将这个值改成了 2，当我测试了几次电话。
8. 打开 `/etc/inittab`（以 root 身份），检查结尾是否出现以下行：

```
ttyS0:2:off:modem:/usr/sbin/mgetty -F /dev/tty0 9600 -L /dev/modem -p /usr/local/vocp/bin/vocp
```

9. 从电话拨打调制解调器并按照说明操作。

## 第 6 步：配置调制解调器

要配置录音，你需要识别调制解调器、更改采样率并尝试一些消息。在开始之前，确保扬声器已连接。接下来，脚本将测试每种调制解调器：

1. 以 root 用户身份登录。
2. 从终端窗口运行 `vgetty-test` 脚本：

```
# /usr/local/vocp/bin/vgetty-test.pl
```

3. 提示时输入调制解调器设备（`/dev/modem`）：

```
Enter modem device (/dev/modem): [/dev/modem]
```

4. 选择声音输出的地方：

```
Select output for vm command. Possible values are: 2 3 4 5 6 [2]: 6
```

5. 脚本开始测试每个类型：

```
Running vm play for Digi 4 - hit ^C (Ctrl-C) once to abort
Could you hear the sound test file? [n]
```

6. 如果你没有听到声音测试文件，输入 `n`，它将继续测试其他调制解调器类型。如果你清晰地听到了，输入 `y`。
7. 当你最终找到工作的调制解调器设置时（并按 `y`），`VOCP` 会更改配置文件以使用你的设置。它还会转换所有消息文件以使用正确的压缩。脚本退出时会显示将消息转换为正确的调制解调器类型和压缩率时所使用的设置。例如：

```
ltdconfig Rockwell 4 7200:
```

## 第 10 章 — 设置数字接线员

8. 为了确保消息翻译正确，请进入消息目录并播放消息。操作方法如下：

```
# cd /var/spool/voice/messages
# vm play -s -v english.rmd
```

语音消息应该通过调制解调器的内部扬声器或连接到调制解调器的外部扬声器播放。然后你应该能看到调制解调器重置（正如我们之前的几个步骤中跟踪日志文件所示）。对于你的解调器，你可能需要使用 `-e`（用于外部扬声器）而不是 `-s`（用于内部扬声器）来设置输出设备。

9. 接下来，测试调制解调器是否能够读取并播放录制的消息。拨打调制解调器连接的电话线路（使用你的手机或家中电话）。你会听到欢迎消息（`root.rmd`），然后是选择不同留言方式的选项列表。如果你听到了消息，请挂断并继续第 7 步：设置通用压缩和电子邮件设置。

10. 如果你在让语音消息音量大到拨入调制解调器的人听清时遇到困难（正如我们之前做的那样），你可以运行 `ltdrmaxvolume` 命令。该命令尝试为你调制解调器确定的选项增加 `/var/spool/voice/messages` 目录及其子目录下所有文件的音量。如果你愿意，可以自己插入这些值（从你之前的步骤中看到的输出）。对于 ampleample：

```
# ltdrmaxvol Rockwell 4 7200
```

## 第 7 步：设置通用压缩和电子邮件设置

`VOCP` 配置文件 (`/etc/vocp/vocp.conf`) 包含了进行录音和管理消息分发的基本设置。你需要在文件中设置的最重要选项包括：

- 调制解调器和压缩 — 设置你正在使用的特定解调器如何处理压缩的选项
- 电子邮件通知 — 确定如何通过电子邮件发送录制的电话消息的选项

在该文件中还有许多其他可以考虑更改的选项。我在本步骤的最后列出了其中一些。打开 `/etc/vocp/vocp.conf` 文件（以 root 身份，使用任何文本编辑器）。然后开始检查以下章节：

- 语音箱树 — `boxconfig` 选项设置语音箱树的位置。默认情况下，其位置为 `/etc/vocp/boxes.conf`，如下，这不需要更改。（你将在稍后的步骤中编辑 `boxes.conf` 文件来设置你的语音信箱。）

```
boxconfig
/etc/vocp/voice.conf
```

原始调制解调器数据格式 (rmd) — 正确获取这些设置非常重要。在之前的解调器声明期间，`rmdformat` 和 `rmdcompression` 选项已自动更改为 `Rockwell` 和 `4`，适用于使用的 `MultiTech MT5600ZDXV`。如果你有不同的解调器，可以使用 `pvformat -L` 查看其他格式和压缩方式。`rmample` 被设置为 `7200`。

接几个选项应使用默认值。确保 `VOCP` 命令位于 `/usr/local/bin` 中（如 `pvftooldir` 所示）。`pause` 选项设置等待用户输入的秒数（3秒）。`max_errors` 值设置了用户在断开连接之前可以在信箱中进行多少无效操作（默认为 2）。

| `rmdformat` | 4 |
| :--- | :--- |
| `rmdcompression` | |
| `rmdample` | 7200 |
| `pvftooldir` | `/usr/local/bin` |
| `pause` | 3 |
| `max_errors` | 2 |

- 电子邮件通知 — 在这里你设置是否将音频电话消息随电子邮件通知发送。你还设置了你希望如何压缩消息（`Ogg` 或 `MP3`）。

将 `email_attach_message` 设置为 `1` 会导致实际音频消息附带在电话消息到达的电子邮件通知中。如果你只想收到通知，请将其设置为 `0`；稍后从 Linux 播放消息。我将其从 `1` 改为 `1` 以附带音频消息。

默认情况下，消息使用 `Ogg` 压缩（`message_in_email_format.ogg`）并在稍后播放。你可以将其设置为 `mp3`。

当 `VOCP` 编码录制的电话消息时，它使用 `/usr/local/bin` 目录中的脚本。对于 `Ogg`，它运行 `pvftoolg`；对于 `MP3`，它运行 `pvftomp3`。这些脚本分别执行 `ogg` 和 `m3` 命令。

随后的其他选项是 `sendmail` 程序向你发送电子邮件。`email_subject` 将寻机箱和电子邮件箱的主题设置为 "VOCP VoiceMail"，而 `email_from_address` 设置发送到 `vocp@localhost.local` 的消息中的 `From:` 字段。你可能至少想更改 `email_from_address`。你可以将 `email_subject` 改为类似 "Jones Family Voice"的内容。

| `email_attach_message` | 1 |
| :--- | :--- |
| `message_in_email_format` | `ogg` |
| `programs` | `email /usr/sbin/sendmail` |
| `email_subject` | "VOCP VoiceMail" |
| `email_from_address` | `vocp@localhost.local` |

![](img/93c80330322e65d5105a6014afe2d807.png)
