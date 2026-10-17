
如果你参考第 198 页上的“遥控命令编码协议”，你会注意到这些计时值比理想波形所示的噪声更大。第一个脉冲约为 2500 毫秒，对应于头部。其他脉冲约为 1300 或 650 毫秒，分别对应 1 和 0。间隙约为 500 毫秒，但较大的初始值对应于按键之间的时间。`lired` 守护进程的任务是拒绝不对应有效波形的脉冲，并正确解释有效的脉冲。完成对 `mode2` 的实验后，按下 `CTRL-C` 终止该工具。

此时，我们已经确定 `lirc_serial` 设备驱动程序就是 `lired` 守护进程。在下一节中，我们将提供配置 `lired` 守护进程的说明，它将使用该设备驱动程序的输出。

如果你想编写一个直接使用 `lirc_serial` 设备驱动输出的程序，`mode2` 工具的源代码提供了如何访问 `/dev/lirc` 设备文件的示例。该源代码可以在 http://www.lirc.org 获取，也包含在本书附 CD `/usr/src/packages/` 目录下的 `lirc-0.8.1.tar.bz` 压缩包中。

# 第 12 章

## 配置 lirc 守护进程

LIRC 软件包中最智能的部分是 `lirc` 守护进程。这部分分析来自 `/dev/lirc` 设备文件的带噪声计时值，并产生一系列易于下游 LIRC 工具或用户应用程序解析的命令。

为了让 `lirc` 守护进程解释来自 `/dev/lirc` 的计时数据，它必须理解遥控协议。配置文件 `/etc/lirc.conf` 捕获了这些协议信息。以下是 Laddie 设备使用的 `lirc.conf` 文件，为了节省空间删除了注释和部分条目。

```
begin remote

name        SONY-TV

bits        12

flags       SPACE_ENC

eps         30

aeps        100

header      2457 525

one         1269 520

zero        650 520

gap         26076

toggle_bit  0

begin codes

POWER       0xA90

ENTER       0xD10

VOL-        0xC90

VOL+        0x490

CH-         0xB90

CH+         0x090

end codes

end remote
```

使用 LIRC 时不需要理解此文件中的条目，我们会在这里做一些注释，以防你想手动编辑文件。`name` 可以是任何描述遥控器的字符串。`bits` 字段是数据位总数（在本例中为命令代码位加地址位）。`eps` 和 `aeps` 字段代表相对和绝对误差容差（在本例中为 30% 和 100 微秒）。`header`、`one` 和 `zero` 字段代表脉冲计时（微秒）和数据位。重复命令之间有约 26,000 微秒的间隙（`gap`），且 `toggle_bit` 反映了重复命令的实际计时，可能与协议标准有所不同。`codes` 是各种命令的实际数据序列。对于适用于其他遥控器的额外字段，你可以在 WinLIRC 网页 http://winlirc.sourceforge.net/technicaldetails.html 查看详情。

如果你有一个使用你所示协议的遥控器，你应该能够在不更新 `/etc/lirc.conf` 文件的情况下控制 Laddie 设备。（再次，我们使用的是 RCA RCU410 通用遥控器，设置为索尼电视，代码为 002）。LIRC 网站也提供了许多遥控器的配置文件，但使用 LIRC 的 `record` 工具可以轻松从头生成这些文件。`record` 工具通过监控 `/dev/lirc` 的输出并提示用户输入遥控内容来创建配置文件。

现在为你的遥控器创建一个配置文件。正如我们在测试 `lirc_serial` 设备驱动时提到的，`mode2` 工具的源代码提供了如何访问 `/dev/lirc` 设备文件的示例。

该程序位于 CD 中的 `/Code/src/examples/socket_cat.c`。请使用以下命令编译并运行该程序：

```
laddie:## cd /Code/src/examples/socket_cat

laddie:## make

laddie:# ./socket_cat /dev/lircd
```

然后在你的遥控器上按下几个按钮。你应该能看到类似下面的输出。

```
0000000000c90 00 VOL- /etc/lircd.conf

0000000000d90 00 VOL+ /etc/lircd.conf

0000000000b90 00 CH- /etc/lircd.conf

0000000000b90 00 CH+ /etc/lircd.conf

0000000000a90 00 POWER /etc/lircd.conf

0000000000a90 01 POWER /etc/lircd.conf

0000000000a90 02 POWER /etc/lircd.conf
```
