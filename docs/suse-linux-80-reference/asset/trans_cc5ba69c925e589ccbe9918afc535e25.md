

- 它考虑队列中打印作业的顺序。
- 它监视队列和打印机的状态，并在请求时提供相关信息。
- 它监听 515 端口，以接受（或拒绝）来自远程计算机的本地队列打印作业。
- 它将队列上的打印作业转发到远程机器的打印机假脱机程序。

有关 LPRng 假脱机程序的详细信息可以在 LPRng HOWTO 文件：`/usr/share/doc/packages/lprng/LPRng-HOWTO.html`、`printcap` 的手册页（man printcap）以及 `lpd` 的手册页（man lpd）中找到。

## 打印机假脱机程序的管理工具

对打印队列进行许多操作需要 root 权限。管理工具在*基础*手册的*管理打印系统的命令*一节以及 LPRng HOWTO 文件：`/usr/share/doc/packages/lprng/LPRng-HOWTO.html#LPRNGCLIENTS` 中有概述。因此，下面我们仅对这部分信息进行总结。

**lpq -Pqueue** 显示指定队列中的打印作业。如果 `all` 作为 LPRng 假脱机程序队列给出，则将显示所有队列中的所有打印作业。`lpq -l -Pqueue` 显示更广泛的信息，`lpq -L -Pqueue` 输出详细的状态报告，有助于故障排除。更多信息请参阅*显示远程队列的状态*。另请参阅 `lpq` 的手册页（man lpq）以及 LPRng HOWTO 中的文件：`/usr/share/doc/packages/lprng/LPRng-HOWTO.html#LPQ`。

**lprm -Pqueue jobnumber** 从指定队列中删除具有给定作业编号的打印作业。只有 root 可以删除其他用户发送的作业。root 可以通过输入命令 `lprm -Pall all` 删除 LPRng 假脱机程序中所有队列中的所有打印作业。

更多信息请参阅下一页的*生成打印作业*一节、`lprm` 的手册页（man lprm）、文件：`/usr/share/doc/packages/lprng/LPRng-HOWTO.html#LPRM` 以及第 193 页的*可能存在的问题*。

**lpc** 控制打印队列：可以按名称指定队列，也可以指定所有队列。下面列出的大多数 lpc 命令只能由 root 执行。最重要的选项有：

- `help` — 提供选项的简要概述
- `status queue` — 发出状态报告
- `disable queue` — 阻止新作业进入队列
- `enable queue` — 打开队列以接收新作业
- `stop queue` — 停止队列中作业的打印。不过，当前正在打印的作业将完成。
- `start queue` — 恢复队列中作业的打印
- `down queue` — 相当于 disable 和 stop 一起使用
- `up queue` — 与 enable 和 start 一起使用效果相同
- `abort queue` — 与 down 相同，不同之处在于当前正在打印的作业会立即停止。作业保留在队列中，使用 up 重新启动队列后可以继续处理。

在命令行中直接将这些命令传递给 `lpc`（例如 `lpc status`），或者不带参数运行 `lpc`，这样就会启动具有自己提示符 `lpc>` 的对话模式，等待输入 `lpc` 命令。使用 `quit` 或 `exit` 结束此对话。

更多信息可以在 `lpc` 的手册页（man lpc）、文件：`/usr/share/doc/packages/lprng/LPRng-HOWTO.html#LPRM` 以及*基础*手册的“显示和管理队列”一节中找到。

> **注意**
>
> 即使在打印过程中关闭计算机然后重新启动 Linux，打印作业仍会保留在队列中。出现问题的打印作业应使用上面显示的命令从队列中删除。

## 生成打印作业

`lpr` 命令在*基础*手册的“生成打印作业”一节以及 LPRng HOWTO 文件：`/usr/share/doc/packages/lprng/LPRng-HOWTO.html#LPR` 中有所描述，因此下面我们仅提供一些补充信息。

### 为本地队列生成打印作业

典型的打印命令是 `lpr -Pqueue file`。

如果省略 `-Pqueue` 选项，则默认值取自 PRINTER 环境变量。这也适用于 `lpq` 和 `lprm` 命令 — 请参阅 `lpr` 的手册页（man lpr）、`lpq` 的手册页（man lpq）和 `lprm` 的手册页（man lprm）。环境变量 PRINTER 在您登录时自动设置，可以使用命令 `echo $PRINTER` 检查，并使用 `export PRINTER=queue` 将其重置为另一个队列。

### 为远程队列生成打印作业

LPRng 假脱机程序也可以通过 `lpr` 命令访问远程队列，例如 `lpr -Pqueue@printserver file`。将 `printserver` 替换为打印服务器的名称或 IP 地址，将 `queue` 替换为打印服务器上的队列名称。当然，这还需要打印服务器配置为允许您在其队列上打印。有关更多信息，请参阅下文*在 TCP/IP 网络中打印*一节中的项目*连接到打印服务器并在打印服务器上过滤的打印机*。

### 显示远程队列的状态

使用以下命令查询远程队列：

```
newbie@earth:  > lpq -Pqueue@printserver
newbie@earth:  > lpq -l -Pqueue@printserver
newbie@earth:  > lpq -L -Pqueue@printserver
```

此状态查询可能很有帮助，尤其是在您无法通过远程队列打印时。请参阅下文*在 TCP/IP 网络中打印*一节中的项目*验证远程 lpd*。

### 删除远程队列中的打印作业

通过输入以下命令，可以删除远程队列中所有自己生成的打印作业：

```
newbie@earth:  > lprm -Pqueue@printserver jobnumber
newbie@earth:  > lprm -Pqueue@printserver all
```

root 对远程队列没有任何访问权限。

## 打印过滤器

lpdfilter（软件包 lpdfilter）用作打印过滤器。打印过滤器的基本操作方法在*基础*手册的*打印作业流程*一节中有所描述。下面将详细描述打印作业流程。要准确分析打印过滤器，请浏览打印过滤器脚本（尤其是 `/usr/lib/lpdfilter/bin/if`）。您还可以按照第 215 页的*打印过滤器故障排除*一节中的说明进行操作。

1. 打印过滤器（`/usr/lib/lpdfilter/bin/if`）定义从假脱机程序直接传递给它的选项，或者从打印作业的“控制文件”以及相应队列的 `/etc/printcap` 和 `/etc/lpdfilter/queue/conf` 文件中读取选项（路径名中的 queue 应替换为实际队列名称）。

2. 它定义要打印的数据类型。脚本 `/usr/lib/lpdfilter/bin/guess` 使用 file 命令来确定数据类型。命令的输出根据 `/etc/lpdfilter/types` 文件中的规范定义要打印的数据类型。
    - 如果是 ascii 队列，则强制打印过滤器将要打印的数据视为 ASCII 文本。
    - 如果不是 ascii 队列，打印过滤器将尝试检测要打印的数据类型。

3. 根据要打印的数据类型和队列，数据随后会被转换为打印机特定信息：
    - 如果是原始队列，数据通常直接转发到打印机（或另一个队列）。但是，根据 `/etc/lpdfilter/queue/conf` 中的设置，也可能使用 recode 进行转换。如果是绝对原始队列——没有 lpdfilter——您必须删除相应队列的 `/etc/printcap` 中的行 `:if=/usr/lib/lpdfilter/bin/if:\`。
    - 如果不是原始队列：
        - (a) 如果打印数据不是 PostScript，则首先使用 `/usr/lib/lpdfilter/filter/type2ps` 将其转换为 PostScript（将 type 替换为打印数据的实际类型）。特别是，ASCII 文本通过 `/usr/lib/lpdfilter/filter/ascii2ps` 使用程序 `a2ps` 转换为 PostScript，具体取决于为队列配置的国家特定编码，因此简单的文本也可以打印国家特定的特殊字符。有关更多信息，请参阅 a2ps 的手册页（`man a2ps`）。
        - (b) 如果需要，可以再次重新格式化 PostScript 数据，只要在 `/etc/lpdfilter/queue/pre` 中有相应的脚本（将此处 queue 替换为实际队列名称）。
        - (c) 如有必要，PostScript 数据随后会转换为另一种打印机语言。
            - 如果连接了 PostScript 打印机，PostScript 数据将直接发送到打印机（或另一个队列）。此外，可以激活 `/usr/lib/lpdfilter/global/functions` 中定义的 bash 函数“duplex”和“tray”，以使用 PostScript 命令启用双面打印或纸盒选择——前提是 PostScript 打印机能够相应地处理这些命令。
            - 如果未连接 PostScript 打印机，将使用针对您的特定打印机型号的 Ghostscript 驱动程序生成打印机特定数据，然后可以将其发送到打印机或另一个队列。Ghostscript 命令的参数直接存储在 `/etc/printcap` 文件的 `cm` 行中，或者存储在 `/etc/lpdfilter/queue/app` 文件中（将此处 queue 替换为实际队列名称）。如果在 `/etc/lpdfilter/queue/post` 中有适当的脚本（将此处 queue 替换为实际队列名称），则可以重新格式化 Ghostscript 输出。
        - (d) 打印机特定数据将被发送到打印机（或另一个队列）。同时，如果在 `/etc/lpdfilter/queue/conf` 中指定了打印机特定的控制序列，则可以在打印机特定数据之前和之后发送这些控制序列。

### 配置打印过滤器

打印过滤器通常在设置打印系统时通过 YaST2 配置，如*基础*手册中“YaST2、打印机”一章所述。

