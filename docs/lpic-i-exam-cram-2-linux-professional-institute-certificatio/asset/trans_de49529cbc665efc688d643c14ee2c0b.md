

## grep 使用示例

grep（全局正则表达式打印）使用以下语法执行命令：

`grep _options_ _pattern_ _file_`

**grep** 命令拥有许多有用的选项，包括：

-   **-c** — 此选项仅显示找到的匹配项的数量，不输出文件名或匹配内容。
-   **-c #** — 此选项在匹配字符串周围显示 X 行上下文。
-   **-h** — 此选项为每个匹配项打印文件名；当您想要随后编辑该文件时，此选项非常有用。
-   **-H** — 此选项抑制每个文件显示文件名。
-   **-i** — 此选项在不区分大小写的情况下搜索模式；显示所有匹配项。
-   **-l** — 此选项仅显示匹配文件的文件名；不显示匹配输出的行。
-   **-L** — 此选项显示没有字符串匹配的文件名。
-   **-w** — 此选项仅选择将字符串作为完整单词的行，而不是作为其他单词的一部分。
-   **-r** — 此选项读取并处理所有指定的目录，以及其中的所有文件。
-   **-x** — 此选项仅返回完全匹配的行；行中的每个字符都必须匹配。
-   **-v** — 此选项显示文件中不匹配字符串的所有行；这与默认行为完全相反。

### grep 使用示例

grep 可以使用文件和目录作为目标参数，或者接收 **stdout**（标准输出）进行解析。以下是一个使用 **grep** 解析输出的示例：

`who | grep ross`

此命令解析 **who** 命令的 **stdout**，查找名称 **ross**，如果找到则打印该行。

一个更复杂的 `grep` 使用示例是将其与另一个命令（如 `find`）结合使用：

```bash
find / -name readme -exec grep -iW kernel {} \;
```

上一条命令查找系统中所有名为 `readme` 的文件，然后对每个文件执行 `grep` 命令，不区分大小写地搜索完整单词 `kernel` 的任何实例。完整单词搜索会找到字符串 `kernel`，但不会找到 `kernels`。

使用 `grep` 命令选项查找字符串的一种创新用法是显示不匹配该字符串的行。例如，您可能希望定期检查 `/etc/passwd` 组中是否有未设置影子密码（shadowed password）的用户：

```bash
grep -v :x: /etc/passwd
```

输出：

```text
snuffy:$1$S0238jkr$wSwCT1u5Uh7v0EgxdftF1xkK1:501:501::/home/snuffy/:/bin/bash
```

看起来 `snuffy` 在 `/etc/passwd` 文件中有一个加密密码。因此，您应该运行 `pwconv` 命令来修复此问题，并让 `snuffy` 立即更改密码。

在课程中，我们通常花费相当多的时间在内核源代码中寻找示例。过了一段时间后，学生通常注意到我们查看的代码中某些词出现的频率，例如 *damn*、*beck* 和 *shooit*。我总是花时间向大家展示如何在代码中找到一些相当有趣且具有教育意义的术语，最终每个人都学到了很多关于 `grep` 的用法，也许还学会了使用其选项的几种新方法。

> 本节已尽力作为学习工具使用，让读者使用 `grep` 搜索某些术语，其中选择了对干扰最小的术语。使用 `grep` 及其选项的能力对考试至关重要。

![](img/49f4f38f3aec011238fa50f89e643db3_258_0.png)

要搜索内核源代码中的单词 `idiot`，请使用以下命令：

```bash
grep -iR idiot /usr/src/linux-2.4 | tail
```

这会生成以下输出：

```text
/usr/src/linux-2.4/Documentation/cdrom/sbpccmd: a complete idiot needs to
understand your hassle already with your first
/usr/src/linux-2.4/abi/srv4/xtl.c:    /* Idiot check... */
/usr/src/linux-2.4/drivers/media/video/marpli/dvb_filter.c:
    printk("NULL POINTER IDIOT(\n");
/usr/src/linux-2.4/drivers/net/3c59x.c: if (vp->cb_fn_base)
    /* The PCMCIA people are idiots.   */
/usr/src/linux-2.4/drivers/net/3c59x.c:
    if (vp->cb_fn_base)
    /* The PCMCIA people are idiots.   */
```

请注意，您得到了模式 *idiot* 的匹配项，既作为完整单词，也作为 *idiots* 等词的一部分。为了收紧限制，仅显示完整单词，请添加 -w 选项：

```bash
grep -iwr idiot /usr/src/linux-2.4 | tail
```

这会生成以下输出：

```text
/usr/src/linux-2.4/Documentation/cdrom/sbpcd:a complete idiot needs to
understand your hassle already with your first
/usr/src/linux-2.4/abi/svr4/xti.c: /* Idiot check... */
/usr/src/linux-2.4/drivers/media/video/margi/dvb_filter.c:
    printk("NULL POINTER IDIOT\n");
/usr/src/linux-2.4/drivers/net/aironet4500.h:/* darn idiot PCMCIA stuff
/usr/src/linux-2.4/drivers/scsi/ChangeLog: * scsi_ioctl.c:
    Make ioctl_probe function more idiot-proof. If
/usr/src/linux-2.4/fs/jffs/jffs_fm.c:
    the shore like an idiot... */
```

如您所见，输出不同——现在仅显示作为完整单词匹配模式的行。

### 使用正则表达式和 grep

除非使用正则表达式，否则使用 grep 查找特定的单词和短语可能很困难。*正则表达式* 具有搜索您并不确切知道的内容的能力，无论是通过部分字符串还是使用以下特殊字符：

-   **.** — 句点匹配任何单个字符，并强制该字符必须存在（a.v 是一个三个字母的正则表达式）。
-   **?** — 问号匹配可选项，并且仅匹配一次。
-   **\*** — 星号从零到多个字符进行匹配（a*v 找到 av、a2v 和 v，等等）。
-   **+** — 加号表示该项必须匹配一次，并且可以匹配多次。
-   **(n)** — 花括号内的数字表示该项将被匹配 n 次。
-   **(n,)** — 花括号内的数字后跟逗号字符，将匹配 *n* 次或更多次。
-   **(n,m)** — 由逗号分隔的花括号内数字对，将从 *n* 次匹配到 *m* 次。

这一切有什么用？尝试使用以下命令仅在源代码树中找到单词 *kernel*：

```bash
grep -rl Kernel /usr/src/linux-2.4 | wc -l
331
```

该命令找到 331 个包含至少一个 *kernel* 匹配项的文件。现在尝试使用此命令仅找到作为完整单词的 *Kernel*：

```bash
grep -rlw Kernel /usr/src/linux-2.4 | wc -l
322
```

现在再次尝试相同的命令，但修改它以便搜索 *Kernel*，但仅在其后跟一个句点时：

```bash
grep -rw Kernel. /usr/src/linux-2.4 | wc -l
44
```

现在，让我们搜索单词 *idiots* 作为搜索模式：

```bash
grep -rw idiots /usr/src/linux-2.4 | wc -l
2
```

再次运行命令，将上下文行数设置为三行，以查看正在注释什么：

```bash
grep -rw idiots /usr/src/linux-2.4
/usr/src/linux-2.4/drivers/net/3c59x.c: if (vp->cb_fn_base)
=/* The PCMCIA people are idiots. */
=/usr/src/linux-2.4/drivers/net/3c59x.c: if (vp->cb_fn_base)
=/usr/src/linux-2.4/drivers/net/3c59x.c: /* The PCMCIA people are idiots. */
=/usr/src/linux-2.4/net/ipv4/ip_gre.c: what the heck these idiots break standards established
```

![](img/49f4f38f3aec011238fa50f89e643db3_260_0.png)

> 在考试中，您需要熟悉如何使用正则表达式，特别是如何找到以特定字母开头和结尾但中间包含其他文本的字符串。

正则表达式生效的另一个例子是搜索特定的短语或单词，但不搜索另一个非常相似的词。

以下文件是 *watch.txt*，包含以下行：

```text
@1 The first sentence contains broad
@2 The second contains bring
```

