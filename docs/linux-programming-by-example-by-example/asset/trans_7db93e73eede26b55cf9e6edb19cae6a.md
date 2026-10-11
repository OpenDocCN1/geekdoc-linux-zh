

```cpp
set_field_userptr(fields[1], NULL);

fields[2] = new_field(1, 12, 2, 1, 0, 0);
set_field_buffer(fields[2], 0, "Last Name : ");
set_field_opts(fields[2], field_opts(fields[2]) & ~O_ACTIVE);

fields[3] = new_field(1, 20, 2, 14, 0, 0);
set_field_userptr(fields[3], NULL);

fields[4] = NULL;

/* create and post the form */
form = new_form(fields);
post_form(form);
refresh();

/* start the command loop */
form_driver(form, REQ_OVL_MODE);
while(toupper(ch = getch()) != KEY_F(10)) {
    if(ch == KEY_UP || ch == KEY_PPAGE)
        form_driver(form, REQ_PREV_FIELD);
    else if(ch == '\n' || ch == KEY_DOWN || ch == KEY_NPAGE)
        form_driver(form, REQ_NEXT_FIELD);
    else if(ch == KEY_BACKSPACE)
        form_driver(form, REQ_DEL_PREV);
    else if(isprint(ch))
        form_driver(form, ch);
    else
        form_driver(form, E_UNKNOWN_COMMAND);
}

unpost_form(form);
free_form(form);
for(i = 0; i < 5; i++)
    free_field(fields[i]);

keypad(stdscr, FALSE);
nocbreak();

app_exit();
exit(EXIT_FAILURE);
}
```

在学习代码中的具体内容之前，请先查看图 12.7，该图展示了该程序的运行效果。不过，如果你编译并运行该程序，会对它的工作原理有更直观的感受。使用下箭头键或 Page Down 键移动到下一个字段，使用上箭头键或 Page Up 键移动到上一个字段，按 F10 键退出。要填写字段，只需输入内容并按 Enter 键即可。

![](img/be588b36b489136ce784030a08a1d3d4_313_0.png)

## 输出

![](img/be588b36b489136ce784030a08a1d3d4_313_1.png)

图 12.7：使用 ncurses 表单库构建的数据输入屏幕。

ncurses 的初始化包括设置 *cbreak* 模式，以便内核允许大部分击键操作直接传递给应用程序而不经过处理。下一个代码块创建了五个字段、两个标签和两个文本输入字段，以及一个 `NULL` 字段来终止字段向量。`fields` 向量是 `post_form` 的参数，该函数创建表单并在调用 `refresh` 后将其显示在屏幕上。

在进入处理所有用户输入的 *while* 循环之前，`form_driver` 为输入字符设置了覆盖模式。除非用户按下 F10，否则应用程序会处理所有输入。按下上箭头键或 Page Up 键（解释为 `KEY_UP` 或 `KEY_PPAGE`）将映射为移动到上一个字段的请求（`REQ_PREV_FIELD`）。类似地，下箭头键和 Page Down 键映射为 `REQ_NEXT_FIELD` 事件请求。该程序还通过将其映射到 `REQ_DEL_PREV` 启用了退格键，该键用于删除前一个字符。按下 F10 时，程序会进行清理并终止。

## 下一步是什么？

在本章中，你完成了对 ncurses 一些高级功能的入门介绍。下一章，“音频 API：OSS/Free”，将继续带你了解 Linux 编程接口的其余部分。

# 13— 音频 API：OSS/Free

直到不久之前，声卡还只能作为附加设备在 PC 购买后安装。如今，即使是所谓的“商务 PC”也在主板上配备了某种形式的最低限度音频硬件。本章将教你声卡编程的基础知识。它简要概述了声卡技术，然后开始讨论 Linux 的音频 API。本章讨论的主题如下：

- 描述音频硬件
- 音频硬件编程的一般准则
- 操纵混音器设备
- 编程 MIDI 硬件
- 编写音频播放程序
- 介绍高级音频功能

## 发声原理

声卡不是单一的硬件设备。相反，它们由几个组件组成。尽管制造商之间，甚至同一制造商的声卡之间都存在相当大的差异，但大多数声卡都拥有 MIDI 接口、数字语音设备、混音器设备和合成器。Linux 对这些设备的支持是通过 /dev 文件系统下的条目启用的：

`/dev/mixer`, `/dev/dsp`, `/dev/audio`, `/dev/sequencer` 和 `/dev/midi`。

## 音频硬件

MIDI（*Musical Instrument Digital Interface*，乐器数字接口）接口是连接外部设备（特别是合成器，但也包括灯光设备和其他舞台道具）到计算机的端口。混音器是一个控制设备，用于控制输入和输出的音量水平，并切换可用的输入设备，例如麦克风和 CD。数字语音设备用于录制和播放数字化语音数据。它们通常根据用于录制和编码采样的 *codecs*（编解码器）或算法来命名。

合成器设备用于播放音乐并产生各种各样的声音和音效。通常，合成器分为两类。一类基于 Yamaha OPL2 和 OPL3 芯片，这些芯片在大多数声卡上很常见。第二类是波表合成器——它们通过存储在声卡芯片中录制的乐器采样来产生声音。在这两种类型中，波表合成器能产生丰富得多的、更逼真的声音。

## 音频设备

Linux 的 /dev 文件系统包含与可用音频硬件大致一一对应的设备文件。所有设备都以数字 *N*（通常为 0、1 或 2）结尾，设备名称通过符号链接指向它们。例如，在我的系统中，`/dev/mixer` 是指向 `/dev/mixer0` 的符号链接。本章的其余部分都指代符号链接，除非有必要指代特定的设备文件。

`/dev/mixer` 是混音器硬件的接口，而 `/dev/dsp` 和 `/dev/audio` 是数字语音设备的主要接口。这两者之间的唯一区别在于 `/dev/audio` 默认使用 µLaw（µ 是希腊字母 *mu*，发音为 "mew"）编码，该编码使用 8 位表示 12 或 16 位样本，而 `/dev/dsp` 使用 8 位无符号线性编码。`/dev/sequencer` 是用于电子音乐和游戏发出的声音的设备。它是声卡上合成器芯片的接口，也可以用于访问外部 MIDI 设备和波表。最后，`/dev/midi` 用于低级 MIDI 输出。

## 音频编程准则

以下准则摘自 OSS 程序员指南，该指南由 Linux 音频 API 的原作者 Hamu Savolainen 编写。可以在万维网 http://www.4front-tech.com/gguide/intro.html 上找到完整文档。

首先，音频 API 旨在使针对其编写的应用程序能够在不同的操作系统和音频硬件之间移植。为此，该 API 依赖于在 `<sys/soundcard.h>` 中定义的宏。尽管实现会随着音频驱动的发展而变化，但宏将保持一致。此外，不要编写使用编号设备的应用程序代码。相反，请使用上一节“音频设备”中描述的符号链接。用户可能拥有多个音频设备或有其他原因使用不同的设备编号，但符号链接始终指向用户想要用于特定目的的设备。

避免“功能狂热”，即给你的应用程序加上许多与其主要目的次要的花哨功能的过程。例如，如果你在写一个 CD 播放器，它不需要录音功能。类似地，不要假设每个人都在使用最新的高科技声卡。相反，请编写最低公分母，即 Sound Blaster，并添加检测和使用高级或高端功能的代码（参见“高级音频编程”部分，了解如何做到这一点）。

## 使用音频 API

要使用音频 API，请在源代码中包含 `<sys/soundcard.h>`。不需要特殊的链接器命令，但当然，你必须有一张工作正常的声卡。在详细讨论音频 API 之前，你必须了解 `ioctl` 调用，即输入/输出控制，它用于通过文件描述符操纵字符设备。其原型在 `<ioctl.h>` 中声明，如下所示：

```c
int ioctl(int fd, int request, ...);
```

`ioctl` 控制打开在文件描述符 `fd` 上的设备，并执行 `request` 中包含的命令。第三个参数约定为 `char *argp`，通常携带大小参数。`ioctl` 是一个针对不适合 Linux 流 I/O 模型的通用命令。`ioctl` 请求（通常称为 `ioctls`）的部分列表可以在 `ioctl_list(2)` 手册页中找到，但它已经过时了。

混音器的 `ioctl` 分为三类：音量控制、输入源和查询函数。查询能力特别重要。例如，有些声卡没有混音器，或者它们没有主
