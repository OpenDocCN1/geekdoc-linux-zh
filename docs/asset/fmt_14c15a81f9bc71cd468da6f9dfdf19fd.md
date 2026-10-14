
| | |
|---|---|
| Volatility Foundation Framework 2.4 ffffffff3a150 | suterusu 1892e |

`.note.gnu.build-id` `0xffffff3a000`
`.text` `0xffffff3a900`
`.text.unlikely` `0xffffff3afdc`
`.init.text` `0xffffff3a000`
`.exit.text` `0xffffff3a9dfc`
`.rodata` `0xffffff3a028`
`.rodata.strl.1` `0xffffff3a0050`
`.parinstructions` `0xffffff3a0ab0`
`.data` `0xffffff3a0100`
`.gnu.linkonce.this_module` `0xffffff3a15d0`
`.bss` `0xffffff3a1820`
`.symtab` `0xffffff3a0100`
`.strtab` `0xffffff3aae8`

在此调用中，`linux_lsmod`被指示识别`0xffffff3a15d0`处的段。恶意处理程序位于模块的`.text`段中，这是因为handler为`0xffffff39f5d7`，而`.text`段始于`0xffffff3e900`。在`.text`段和此地址之间没有映射其他段。这提供了额外的证据，说明通知器处理器指向该模块内部。

此时，你可以像本章早期部分那样使用`linux_moddump`从磁盘中提取模块。要找到函数名，从段所在的地址减去处理器的地址：

```
$ python

Python 2.7.3 (default, Jan 2 2013, 13:56:14)

[GCC 4.7.2] on linux2

>>> "%x" % (0xfffffffa3f5d7-0xffffff39e000)

'15d7'
```

接下来，你可以使用`readelf`在符号表中搜索计算偏移处的模块函数：

```
$ readelf -W suterusu.0xfffffffa39e000.1km | grep 15d7

28: 0000000000015d7 129 FUNC GLOBAL DEFAULT 2 notify
```

你现在知道函数`suterusu`被用作恶意处理器。你在源代码中也看到了这一点，但在没有分析的rootkit源代码的情况下，为了自动化识别标记，我们扩展了`linux_kernel_hidden_modules`插件。然后我们使用Volatility的`symbol_for_address`API找到对应的符号。补丁钩的名称为：

```
$ python vol.py --profile=LinuxDebian-3x64 -f sample.lime

linux_kernel_notifier
```

| | |
|---|---|
| Volatility Foundation Framework 2.4 Address 0xfffffffa3f5d7 | HOOKED:suterusu/notify |

插件在`HOOKED`字符串后为恶意钩子添加`<模块名>/<符号名>`。

# TTY 处理程序

要找到TTY处理程序，你必须首先知道如何在内存中找到TTY设备。了解TTY和PTS设备之间的区别也很，因为它们使用不同的处理程序并需要单独的验证和分析。TTY处理程序用于物理终端设备，例如，终端

# 740 第三部分：Linux 内存取证

物理机上的键盘登录，而PTS设备则用于SSH登录时实例化的模拟终端。

## 确定是否安装了恶意处理程序

取决于TTY处理器被挂钩的方式，一个设备或两个设备都可能同时被挂钩。这非常危险，因为rootkit程序的单一操作就可以挂钩系统上所有的TTY设备并立即监控所有的按键。

### 数据结构

`tty_struct`存储有关键盘通知器的信息。以下是它在64位Debian系统上的显示方式：

```
>>> dt("tty_struct")

'tty_struct (1280 bytes)

0x0 : magic ['int']

0x4 : kref ['kref']

0x8 : dev ['pointer', ['device']]

0x10 : driver ['pointer', ['tty_driver']]

0x18 : ops ['pointer', ['tty_operations']]

0x20 : index ['int']

0x28 : ldisc_mutex ['mutex']

0x48 : ldisc ['pointer', ['tty_ldisc']]

0x50 : termios_mutex ['mutex']

0x70 : ctrl_lock ['spinlock']

0x78 : termios ['pointer', ['ktermios']]

0x80 : termios_locked ['pointer', ['ktermios']]

0x88 : termios ['pointer', ['ktermios']]

0x90 : name ['String', ['length': 64]]

0xd0 : pgrp ['pointer', ['pid']]

0xd8 : session ['pointer', ['pid']]

0xe0 : flags ['unsigned long']

0xe8 : count ['int']

<snip>
```

### 关键点

关键点如下：

- **`dev`:** 指向设备结构的引用。
- **`ldisc`:** 指向TTY设备操作结构的引用，该结构接收输入并处理读/写操作。你必须检查这些方法以确保没有发生恶意的挂钩。
- **`name`:** 设备名称，例如`tty2`。
- **`session`:** 设备会话，可将设备与登录和进程关联。

# 内核模式 Rootkit

要挂钩TTY处理器，你可以执行以下步骤：

1. 定位TTY设备的文件指针结构。你通过将设备名称例如`/dev/tty1`传递给`file_open`函数来实现。
2. 使用`private_data`成员获取`tty_file_private`结构的引用，该结构进一步指向`tty_struct`。
3. 将`tty_struct->ldisc-ops->receive_buf`指针覆盖为你的日志函数的地址。

完成这些步骤后，你的函数就可以在按键通过设备时进行记录。为了检测这一点，`linux_check_tty`执行以下步骤：

1. 它遍历存储在`tty_drivers`全局变量中的TTY驱动程序列表。
2. 在每个`tty_driver`结构中，它访问`tty`成员，该成员持有驱动程序管理的TTY设备列表。
3. 对于列表中找到的每个TTY设备，都会验证`receive_buf`指针。在干净的系统中，它应该指向`n_tty_receive_buf`函数。

以下是在干净系统上运行Volatility插件的示例，该系统的TTY设备未被挂钩：

```
$ python vol.py -f centros.lime --profile=LinuxCentos64 linux_check_tty

Volatility Foundation Volatility Framework 2.4
```

| Name | Symbol |
| --- | --- |
| tty1 | 0xffffffffff831a0b0 n_tty_receive_buf |
| tty2 | 0xffffffffff831a0b0 n_tty_receive_buf |
| tty3 | 0xffffffffff831a0b0 n_tty_receive_buf |
| tty4 | 0xffffffffff831a0b0 n_tty_receive_buf |
| tty5 | 0xffffffffff831a0b0 n_tty_receive_buf |
| tty6 | 0xffffffffff831a0b0 n_tty_receive_buf |
```

在受感染的系统中，函数指向其他地方。在以下恶意软件示例的情况下，你可以挂钩一个隐藏模块：

```
$ python vol.py -f tty_hook.lime --profile=LinuxDebian-3_x64 linux_check_tty
Volatility Foundation Volatility Framework 2.4
```

| Name | Symbol |
| --- | --- |
| tty1 | 0xfffffffa04270116 HOOKED |
| tty2 | 0xfffffffa04270116 HOOKED |
| tty3 | 0xfffffffa04270116 HOOKED |
