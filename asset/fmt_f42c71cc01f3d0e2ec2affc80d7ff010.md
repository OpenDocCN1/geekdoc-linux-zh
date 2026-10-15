
`bash` 命令 `export` 将指定的 shell 变量声明环境变量。这意味着变量在所有调用的命令和子 shell 中都是可用的。可以选择也可以为变量赋值。如果调用命令时不带参数，将显示所有环境变量。

- `-n`
将环境变量变回普通 shell 变量。因此，该命令的效果与不带选项使用时完全相反。

```bash
exportfs [options]
```

`exportfs -a` 命令向运行的 NFS 服务器报告 NFS 配置文件 `/etc/exports` 的更改。因此，必须执行该命令才能使 `/etc/exports` 中的更改生效。

```bash
expr expression
expr string : pattern
```

`expr` 以算术方式评估指定的表达式，或对字符字符串执行模式比较。指定的变量、数字和操作符之间必须有空格！所有允许的操作符的短描述可以在 `expr` 的 `man` 命令中找到。注意，shell 中的许多操作符必须使用 `\` 字符保护以免被立即评估。

如果你使用 `bash` 作为 shell，你也可以在其中不使用 `expr` 进行计算：可以通过 `$[expression]` 在那里指定算术表达式。`grep` 中描述的通配符可以使用于模式。通常，模式必须放在单引号中，以防止 shell 评估特殊字符。

### 示例

第一个 `expr` 命令执行简单的计算。第二个命令返回对应模式表达式的最大字符数。第三个命令从字符字符串中提取模式的括号部分。

```bash
user$ expr 3 + 7 \* 19
136
user$ expr abcdefghi : 'a.*'
```

```bash
user$ expr abc_efg_hij : '.*\(*\)__*'
efg
```

### `fail2ban-client [options] command`

`Fail2ban` 是一个安全程序，用于监控登录并在多次错误登录后封锁相关 IP 地址一段时间。如果安装了 `Fail2ban`，可以通过 `fail2ban-client` 检查和更改其功能。

- `get parameter`
导入配置参数。

- `reload [jailname]`
重新加载整个配置或某个 jail 的配置。在 `Fail2ban` 中，jail 是一个被监控的程序。

- `set [jailname] value`
更改通用参数或 jail 的参数。

- `start/stop [jailname]`
完全启动或停止 `Fail2ban` 或仅停止一个 jail。

- `status [jailname]`
显示活动 jail 的列表或 jail 的详细信息。

`fail2ban-client` 在仅带 `-d` 选项运行时输出当前配置，这对于排查混乱的文件非常有用。以下命令显示计算机上有四个活动 jail。SSH 服务器的 jail 已经封锁了 1418 个地址。目前封锁了 3 个。

```bash
root# fail2ban-client status
Status
Number of jail: 4
Jail list: docet, postfix, sshd, sshd-ddos
```

```bash
root# fail2ban-client status sshd
Status for the jail: sshd
Filter
  Currently failed: 4
  Total failed: 11362
Journal matches: _SYSTEMD_UNIT=sshd.service _COMM=sshd
Actions
  Currently banned: 3
  Total banned: 1418
  Banned IP list: 58.218.nnn.nnn 58.242.nnn.nnn 180.76.nnn.nnn
```

可以使用 `fail2ban-client set` 解封误封的 IP 地址（在这里对 ssh jail 这样做）：

```bash
root# fail2ban-client set sshd unbanip 1.2.3.4
```

### `fc-list [pattern]`

`fc-list` 列出所有匹配可选搜索模式的字体。可以使用 `| sort` 进行排序。

### `fdisk [options] [device]`

`fdisk` 是一个过时的硬盘分区程序。它只能处理具有 MBR 分区表的磁盘！由于这个原因，你应该熟悉 `parted`，它兼容主引导记录 `MBR` 和更现代的 GUID 分区表 `GPT`。

### `ffmpeg [inopts] [-i infile] [outopts] outfile`

来自同名包的 `ffmpeg` 命令将视频文件从一种格式转换为另一种。在指定选项时，注意这些选项仅适用于下一个视频文件。因此，选项的顺序对于命令的正确功能至关重要。除非进行不同的设置，否则对结果文件使用与源文件相同的编码器和设置。

除了列出的选项外，还有无数其他。选项的理想设置本身就是门科学。如果你不想处理这些，建议使用一个用于视频录制的图形化用户界面，例如 `HandBrake`。

- `-acodec/-vcodec`
指定的音频或视频编码器。`ffmpeg -codecs` 提供了可用编码器的列表。

- `-b n`
指定的位比特率，单位为比特/秒（默认为 200 kBit/s）。

- `-f format`
使用指定的格式。

- `-formats`
列出支持的格式、编码器、过滤器等。

- `-r n`
指定的帧率（默认为每秒 25 帧）。

- `-s size`
以 `wxh` 格式指定的帧大小（例如 `800x600`）。或者，你可以指定一个预定义的字符字符串（例如 `vga` 或 `hd720`；请参见 `man ffmpeg`）。

- `-ss position`
从指定的时间开始转换。时间可以用秒数或 `hh:mm:ss[.xxx]` 格式指定。

- `-t duration`
仅转换指定的时间段（而不是整个文件）。时间段的指定方式与 `-ss` 选项相同。

- `-target type`
指定的目标文件格式（例如 `vcd`、`dvd` 等）。

- `-vpre quality`
为指定的编码器选择具有预定义选项（预设）的文件（例如 `default`、`medium`、`max` 或 `fast`）。可选择的预设文件通常位于 `/usr/share/ffmpeg` 目录。

- `-y`
覆盖现有文件。

#### 示例

以下命令创建一个 DVD 分辨率的电影文件：

```bash
user$ ffmpeg -i in.avi -target pal-dvd -y out.avi
```

第二个示例将 OGV 电影文件转换为 YouTube 兼容的 MPEG 文件：

```bash
user$ ffmpeg -i in.ogv -vcodec libx264 -vpre medium -acodec copy -y out.mp4
```

### `fg [process]`

`bash` 命令 `fg` 让之前使用 `Ctrl+Z` 中断的任务在前台继续运行。如果没有指定进程，`fg` 适用于上一个被中断的进程或上一个在后台启动的任务。否则，必须通过进程名称或 `bash` 内部作业号（不是 PID）来指定进程。

除了 `fg process`，还允许使用缩写 `%process`。

### `fgconsole [--next-available]`

`fgconsole` 输出当前活动控制台编号。使用 `--next-available` 选项，该命令将确定第一个空闲（未使用）控制台编号。要更改活动控制台，可以使用 `chvt` 命令。

### `file [options] file`

`file` 尝试确定指定文件的类型。结果是 `file` 返回一个包含文件名和文件类型的字符字符串。`file` 不评估文件名或其标识符，而是评估文件内容！

- `-z`
尝试识别压缩文件的数据类型。

#### 示例

正如文件名所示 `name.jpg` 包含一个 JPEG 位图文件：

```bash
user$ file name.jpg
name.jpg: JPEG image data, JFIF standard 1.02
```
