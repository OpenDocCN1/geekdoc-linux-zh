
```bash
#!/bin/bash

gnuplot -persist <<ENDOFTHISDOC &
  set terminal wx
  set y2label 'Gold'
  set y2label 'Silver'
  set xlabel 'Trading days'
  set y2tics autoref
  plot 'datasource.txt' using 1:2 axes x2y2 with lines
  'datasource.txt' using 1:3 axes x2y2 with lines
  ENDOFTHISDOC
```

我们通过使用 `xlabel` 和 `ylabel` 命令开始，为轴分配文本描述。接下来，将 `y2tics` 属性设置为 `autofreq`：这指示 `gnuplot` 使用其内部逻辑找到最佳步长值。此外，它还覆盖了默认设置：如果任由 `gnuplot` 自行处理，它将在图表的第一个轴上显示刻度。

至此，是时候最后一次运行我们的独立示例了。下图展示了您可以预期的结果。

## 将文件移除！

只要 shell 脚本是交互式运行，显示图表就是有趣的——如果您的脚本是离线的，创建可以通过电子邮件或 `SCP` 传输分发的文件会更有趣。

这可以通过重定向 `gnuplot` 的终端实例来实现，使其将信息输出到文件而不是显示在帧缓冲器上的窗口。让我们通过修改之前的金属图表程序来做到这一点——一个为简洁起见省略状态变量代码的愉快精简版本看起来像这样：

以下是这段数据，数字可能会因环境而异：

```
root@amihan-thinkpad:~/Desktop/Deadstuff/2016Nov/April$ bash# cat_pingstore.dat
cof
50.7
50.3
204
53.5
50.4
51.0
50.9
57.8
50.0
53.0
```

```bash
#!/bin/bash

gnuplot <<ENDOFTHISDOC &
set terminal png
set output 'goldchart.png'
 plot 'datasource.txt' using 1:2 axes x1y1 ... 
ENDOFTHISDOC
```

这次调用 `gnuplot` 的方式与常规做法不同，因为它首先将终端设置为 `png`，从而指示程序将绘图输出到 `PNG` 文件。随后使用 `set output` 来指定要生成的文件名，之后即可发出其他命令。运行后，包含该 shell 脚本的文件将生成一个图形文件。然后，可以使用任意首选的文件传输命令将其转发至最终目的地。

## 不同的数据

现在，既然你在运行时已将单独的 `.pub` 文件加载到 `gnuplot` 中，我们便可以改变程序的行为，以输出主 shell 脚本在执行过程中收集的数据。一个好的例子就是绘制显示到服务器 `ping` 时延的图表——假设网络连接始终稳定，我们可以认为发送 10 个数据包大约需要 10 秒。这使得 `ping` 成为本教程最终绘图应用的理想候选对象——展示连接可靠性随时间变化的历史趋势为你的数据增添了额外的含义。

遗憾的是，`ping` 的输出无法直接用于绘图：`gnuplot` 期望的是均匀的数值，且不太可能直接解析其输出。管道可以解决这个问题——`awk` 工具允许你轻松提取文本中的特定部分。例如，以下行代码将提取相关列：

```bash
ping -c 10 www.google.fr | awk -F '[ ]' '(print $[NF-1])' > pingstore.dat
```

运行后，对于本文作者而言，文件 `pingstore.dat` 中将包含该产品的 `man` 手册页中的时间。但对于普通用户来说，本文讨论的操作说明已经足够使用了。

幸运的是，这个问题可以通过 `grep` 解决。按所示方式调用时，该程序将限制其输出为纯数字数据：

```bash
ping -c 10 www.google.fr | awk -F '[ ]' '(print $[NF-1])' | grep -E “[0-9]” > pingstore.dat
```

至此，还剩一个问题需要解决，即对数据文件内容进行绘图：

```bash
#!/bin/bash

ping -c 10 www.google.fr | awk -F '[ ]' '(print $[NF-1])' | grep -E “[0-9]” > pingstore.dat

gnuplot -persist <<ENDOFTHISDOC &
plot ‘pingstore.dat’ with lines
ENDOFTHISDOC
```

我们的最后一个示例比较特殊，因为它只是向 `gnuplot` 提供 `pingstore.dat` 文件并指示其使用线条进行绘制操作。`gnuplot` 的内部算法将为 `X` 轴生成一个数值序列，从而确保图表看起来美观。

关于 `Gnuplot` 已经写过一整本书了——经常做图表的人绝对应该花点时间阅读该产品的 `man` 手册页。然而，对于普通用户而言，本文讨论的操作说明已经绰绰有余。

至此，我们穿越 shell 脚本领域的旅程也就此结束。尽管我们涵盖了大量内容，但这远非关于 shell 脚本所能讲述的全部内容。如果你发现自己反复执行某种任务，你肯定应该考虑寻找一个 shell 脚本来处理它——得益于 `UNIX` 管理者的开放性和乐于分享的特质，简单的 `Google` 搜索很可能会带来超出你狂野想象的结果。

## 教程

# 漏洞利用

## 在受控环境中分析、调整并运行漏洞利用

直接运行现成的漏洞利用程序是一项冒险的业务：它可能导致系统完全崩溃。

![](img/1f330653f83dcf0397f7d224ce8bbc16_36_0.png)

Toni Castillo Girona 拥有软件工程学士学位，并作为信息通信技术（ICT）研究支持专家在西班牙加泰罗尼亚地区的一所公立大学工作。他定期在他的博客 `disabaues.upc.es` 上撰写关于 `GNU/Linux` 的文章。

![](img/1f330653f83dcf0397f7d224ce8bbc16_37_0.png)

*上方图示：通过执行基于 `tprobe` 的漏洞利用程序，我们可以重写 `/usr/bin/passwd` 并获得 `root shell`*

近期出现了许多危险的安全漏洞，其中大多数可以通过执行不同的概念验证（PoC）脚本进行利用。其中一些甚至配有引人注目的名字（例如 `DirtyCOW`）。有时这些 `PoC` 可以直接运行，但有时则不能。因此，如果某个 `PoC` 没有产生预期结果，并不意味着它没有以某种方式影响系统。如果你执行了漏洞利用程序但它不起作用，可能是因为特定的系统不受影响，或者该 `PoC` 需要调整。最坏的情况是：漏洞利用程序损坏了系统。这就是为什么你需要分析漏洞利用程序的实际运作方式，理解其基于的漏洞，并在受控环境中（例如虚拟机）执行它。本教程将通过对最新出现的三个漏洞（截至撰写时）——`CVE-2016-5195`、`CVE-2016-663` 和 `CVE-2016-8664` 进行操作，并提供 `shellcode` 的简要逐步指南，从而为你提供对漏洞利用程序的总体理解。漏洞利用程序用各种编程语言编写：`C`、`Perl`、`Python`、`Ruby`... 甚至 `Bash`。分析特定的漏洞利用程序，然后使用你喜欢的语言重新编码它以证明你理解了其功能，是一个好主意。

`shellcode`（在某些时间点并通过不同技术）被传递到存在漏洞的应用程序。你可以从头编写 `shellcode`，也可以使用 `msfvenom`（`Metasploit` 框架中的一个工具）来生成。`WebSecurity Dojo` 架构是 `x86`，因此让我们生成一个将生成新 `shell` 的 `ELF32` 二进制文件。在你的 `Kali Linux` 终端中输入以下内容：

```bash
msfvenom -p linux/x86/exec -a x86 chmod=/bin/bash PrependSetuid=True -f elf > myshell1
```

试一试：将文件复制到你的 `WebSecurity Dojo` 虚拟机：

```bash
scp myshell1 dojo@YOUR_DOJO_IP:
```

在 `WebSecurity Dojo` 内部，你需要输入这些命令来获取所有者权限，并最终在 `myshell1` 上设置执行位和粘滞位。

```bash
sudo chown root:root myshell1
sudo chmod 4755 myshell1
```

以用户 `dojo` 身份执行它，你将获得一个新的 `root shell`。

```
./myshell1
bash-4.2#
```

## 将 shellcode 转换为 C 字符缓冲区（十六进制操作码）
