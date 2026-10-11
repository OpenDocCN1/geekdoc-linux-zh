
$ Terminal

`$root@boball:~# pico -w /usr/bin/fax`

```
```

### 配置你的调制调器

滚动到 `DEV=` 条目并输入传真调制调器的设备名称。例如，如果你的调制调器在 COM2 上，使用 `ttyS1`。使用 `linda` 命令配置 `/dev/modem` 符号链接，该条目应该是 `DEV=modem`。

### 选择调制调器类别

`fax` 命令支持三种传真协议：Class 1、Class 2 和 Class 2.0。通过删除对应类别前面的井号 (`#`) 为你的调制调器选择正确的类别。例如，如果你的传真调制调器支持 Class 2 协议，删除 `CLASS2=` 的井号。检查你的调制调器文档以查看支持哪些传真协议。确保只选择了一个协议，其他协议前面都有井号。

```
$ Terminal

$root@boball:~# linda /dev/modem

# 传真脚本的名称，efax 以及完整的路径

# 如果必要的话。

# /usr/bin/efax

# /etc/efax.conf

# 传真调制调器连接的设备，例如，对于

# COM2 上的外部调制调器使用 ttyS1。例如，如果

# 你的调制调器连接到内置串口，使用 ttyS1。因此，使用 dev-modem 或 dev-tty1。

DEV=modem

# 要使用的调制调器命令类型。取消其中之一的
```

```
$ Terminal

$root@boball:~# linda /dev/modem

# 要使用的调制调器命令类型。根据你的调制调器

# 取消以下行中其中一行的注释。

CLASS=2

# 你的国际格式格式的电话号码，最多 20 个字符。

# 例如，+1-555-5555，以及字符集。

# 你在页眉上应显示的名称

NAME=Fax from +1-555-5555
```

### 输入你的传真号码

滚动并在 `FROM=` 条目中输入你的传真号码。（替换已有的号码）。例如，如果你的号码是 1-703-123-1234，按此格式输入项目，不带连字符：`FROM=*1 703 123 1234`。

![](img/c48ad0dbc61332ca39f773da7141f4e1_118_0.png)

### 输入你的名称并保存

滚动并在 `NAME=` 条目中输入你的名称。（替换现有的名称）。例如，如果你的名字是 Joseph Piccolo，输入如下：`NAME=Joseph Piccolo`。然后按 `Ctrl+X`，按 `Y` 保存文件。

![](img/c48ad0dbc61332ca39f773da7141f4e1_118_1.png)

### 查看传真测试

使用 `fax` 命令的 `test` 选项测试你的设置。在终端命令行输入 `fax test`，然后输入 `type` 读取。完成后，按 `Q` 退出。

![](img/c48ad0dbc61332ca39f773da7141f4e1_118_2.png)

### 不同的文档大小

传真时，更改 `fax` 脚本中的 `PAGE=` 条目以使用不同的纸张尺寸（如 `legal`）。

### 其他选项

你可以在 `fax` 脚本中设置其他选项，例如用于打印传真的默认命令或查看传真的默认程序。OpenLinux 包含了如果你使用 `fax` 脚本所需的所有程序。

### 故障排除

设置传真时阅读 `efax` 页面提示（使用命令行作为 `efax`）。你也会通过 `fax` 脚本找到技巧。

![](img/c48ad0dbc61332ca39f773da7141f4e1_118_3.png)

## 如何使用 OpenLinux 传真

### 发送文本文件

此任务显示了如何使用 `fax` 命令发送、接收和打印传真文件。要查看传真，必须先启动 X11 会话。为了打印传真，打印机必须配置为适用于 Linux。设置打印机请查看“打印文本和图形”，并遵循“安装打印机”任务步骤。发送文本传真，使用 `fax` 命令及其 `send` 和 `-l`（小写 L）选项，后跟传真号码和文本文件的名称。例如，要将 `document.txt` 发送到 820-742，输入 `fax -l 820742 document.txt` 并按回车。`-l` 是低分辨率，传输更安全、更快。

```bash
$ fax document.txt

mydocument.txt: 11/27/98 13:27 1998 efax 16 Ed Cases

fax: 02: opened /dev/ttyS0

fax: 07: session 9600bps 8.5"B-rt44

fax: 12: dialing 820742

fax: 17: connected 820742 9300 bps (1 703 123 121)

fax: 27: sent 24-064 lines, 19380-bytes

fax: 32: header (11/27/98 13:26) Coastal Development (1 703 123 121)

fax: 37: sent -l document.txt

fax: 42: sent 24-064 lines, 19370+bytes

fax: 47: sent 24-064 lines, 19710+ bytes, S 9048 bytes

fax: 52: closed
```

### 发送 PostScript 文件

通过传真发送 PostScript 图形，使用 `fax` 命令及其 `send` 和 `-l` 选项，后跟传真号码和 PostScript 图形的名称。例如，将 `graphic.ps` 发送到 820-742，输入 `fax send -l 820742 tiger.ps` 并按回车。

### 设置接收传真

等待接收传真，在命令行使用 `fax` 命令的 `wait` 选项并按回车。`fax` 命令等待传入的传真。

```bash
$ fax tiger.ps -l 820-742

tiger.ps: 11/27/98 12:24 1998 efax 16 Ed Cases

fax: 02: opened /dev/ttyS0

fax: 07: session 9600bps 8.5"B-rt44

fax: 12: dialing 820742

fax: 17: connected 820742 9300 bps (1 703 123 121)

fax: 27: sent 24-064 lines, 19380-bytes

fax: 32: header (11/27/98 13:26) Coastal Development (1 703 123 121)

fax: 37: sent -l tiger.ps

fax: 42: sent 24-064 lines, 19370+bytes

fax: 47: sent 24-064 lines, 19710+ bytes, S 9048 bytes

fax: 52: closed
```
