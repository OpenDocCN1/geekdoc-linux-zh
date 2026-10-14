

包含打印机名称定义；你将其中一个作为 lpr 命令的 -P 选项提供。也就是说，要将作业发送到此打印机，你可能会使用

```bash
$ lpr -Pst800 file
```

其中 file 是一个 PostScript 文件；在该示例中，你可以使用 lp、PostScript 和 ps 作为 st800 的替代项。/etc/printcap 中的每个条目对应一台打印机；上面的示例涉及一台 Epson Stylus Color 800 打印机。

## PROBLEM 50

**Symptoms:** lpd 对一台打印机行为异常（作业丢失、过滤不正确、完全失败等）。条目的一部分被忽略。

**Problem:** /etc/printcap 文件中缺少冒号或反斜杠。

**Fixes:** 冒号必须开始和结束 printcap 条目中的所有行（第一行除外，第一行不应有前导冒号），并且条目中除最后一行外的所有行都必须以反斜杠结尾。以下条目是错误的，因为它缺少反斜杠和前导冒号：

```text
lp|PostScript|ps|st800|My Printer:
lp=/dev/lp0:sd=/var/spool/lpd/st800:
...
of=/usr/local/lib/filters/psof:
```

以下条目是正确的——反斜杠和冒号已加下划线：

```text
lp|PostScript|ps|st800|My Printer:\
:lp=/dev/lp0:sd=/var/spool/lpd/st800:\
...
:of=/usr/local/lib/filters/psof:
```

## A Typical Remote Printer Entry with lpd or LPRng

远程打印机是指 Linux 不对其进行排队的打印机。当 lpd 为远程打印机接收到作业时，它只是将作业传递给另一台机器。以下典型的远程打印机条目适用于 lpd 或 LPRng：

```text
remote|Printer on another Desk:\
:lp=:sd=/var/spool/lpd/lj:\
:mx#0:rm=mikado.example.com:rp=lp:
```

接收打印作业的远程主机是 mikado.example.com，而该主机上的打印机名称是 lp（通常在远程主机的 /etc/printcap 中定义）。

## Common /etc/printcap Components

以下是一些常见的 /etc/printcap 参数：

### :sd=/some_directory:

 spool 目录：文件在等待打印时进入此队列。此目录必须存在，并且打印守护进程（通常以用户 daemon 运行）必须能够写入它。我们第一个 printcap 示例的 spool 目录为 /var/spool/lpd/st800。

### PROBLEM 51

**Symptom:** 打印作业导致错误或直接消失。

**Problem:** Spool 目录不存在或 lpd 无法写入它。

**Fix:** 如果你在 /etc/printcap 中指定了 `:sd=dirname:`，请确保该目录存在，并且 lpd，通常以 daemon 运行，可以写入它。在打印机经常增减的大型网络中，此目录可能会造成很大的麻烦——你可以使用第 5.5 节中描述的 printcap 生成系统自动创建它们。对于小型网络和打印服务器，简单的 `# chown -R daemon.daemon dirname` 通常可以解决大多数这些问题。

### :lf=/some_directory/file:

日志文件：这通常是打印机 spool 目录中的一个名为 log 的文件。打印守护进程必须能够写入它。

### :af=/some_directory/file:

记账文件：如果你的打印机支持，你可以用此文件跟踪打印机使用情况。

### PROBLEM 52

**Symptom:** 打印机记账似乎不起作用。

**Problem:** 记账文件无法写入。

**Fix:** 与 spool 目录一样，daemon 必须能够写入 printcap 中 `af=file` 指定的文件。

### :if=/some_directory/file:

打印（输入）过滤器：这是所有作业在送往打印机之前必须通过的通用过滤器。除了将任何纯文本转换为 PostScript 外，此过滤器还为打印准备设备，并且在许多情况下实际上将输出发送到设备（例如，如果它是网络打印机）。如果打印机不直接支持 PostScript，此过滤器会将 PostScript 转换为打印机的本机格式。

### :of=/some_directory/file:

输出过滤器：此过滤器在打印作业处理后运行。输出过滤器对于清理或其他作业间任务很有用，例如创建横幅页。

### :mx#0:

这设置最大文件大小。设置为 0（与本示例相同）时，文件大小没有限制。由于 PostScript 文件大小与作业的物理大小关系不大，因此将其保持在 0 以外是没有意义的。

### :sh:

抑制页眉页：打印系统默认打印页眉页（也称为横幅或分流页），用于标识用户和作业名称。此标志关闭页眉页，这对于大多数现代应用程序来说是完全合适的。

### :rm=some_host: 和 :rp=some_printer:

这些表示远程打印机名称和主机。这些选项告诉 lpd 打印机未本地连接，并且应将作业发送到 some_host 在 some_printer 上打印。（LPRng 提供了一个更简洁的替代方案——见下文 LPRng Enhancements。）

相关手册页：printcap (5)、lpd (8)、lpq (1)、lpr (1)

