
# 第三部分 系统管理
## 第 13 章 用户、组与登录

- 2. 从前面的输出中，你将看到许多设置。在大多数情况下，你只需要修改其中几项。注意输出中的内容，`erase`（删除）设置是未定义的（<undef>）。将其设置为为退格键（<Backspace>）工作。`CTRL+H` 是控制键和 H 键的组合。`CTRL+H` 是退格键的默认值。你可以使用 `stty` 命令告诉系统使用此键序列来执行退格功能。

在 shell 提示符下，输入 `stty ^H`：
```
$ stty ^H
```

- 3. 现在查看输入 `stty -a` 的结果：
```
$ stty -a
speed 9600 baud; line = 0;
rows = 0; columns = 0
min = 4; time = 0;
intr = ^C; quit; erase = ^_; = ^H; kill = ^U
of = ^B; = 0; eol2 <undef>; switch <undef>
stop = ^S; start = 0; dsup <undef>;nwerase = ^K; innext <undef>
parenb = parodd cs7; cstopb hupcl -clocad - loblk crts
ignbrnk intrk gnigar -parmrk -inpck istrip -inclr -igncr icrnl - iuclc
ixany ixony -imaxbel rtsoff - ctsxon - ctsen - noflish
isig ican iexten - xcase echo echo echoe -echon -echochl - echport -echoke -flushu -pendin
opost -olcl onlcr -onroc -onret -ofill -ofdel -topost
$
```
如你所见，退格键已设置。

- 4. 在上一个输出中，请注意另一个重要的 `stty` 值：`intr` 或中断键。按下中断键可以退出 UNIX 命令（通常是 Ctrl+C 或 Delete）。使用 `stty` 命令查询其值。在上一个示例中，`Ctrl+C` 就是中断键。

### 查看谁登录了系统

你现在准备好学习有关其他其他登录到系统的用户的命令了。今天早些时候，你可能会发现 `finger` 命令为每个当前登录的用户显示一行，如下所示：
dnt - finger:

| 登录名 | 姓名 | Tty | 空闲 | 登录时间 | 地位置 |
|---|---|---|---|---|---|
| beltran | Rene Beltran | *p0 | 4:44 | 9月20 15:39 | 10.1.1.101 |
| dhelp | Dbhelp System | *p20 | 7:42 | 9月20 12:53 | sm |
| ingrid | Ingrid Van Zangen | *p92 | 9:54 | 9月20 07:10 | iv |
| mori | Steve Moritsugi | *p1 | 1 | 9月20 08:35 | sm |

### who 命令提供了类似的信息：

```
$ who
```

| | | |
|---|---|---|
| Tim_Wilson | tty1 | 3月19 18:27 |
| Emily_Wilson | tty10 | 3月19 18:30 |
| oracle | tty2 | 3月19 15:27 |
| Taylor_Klausner | ttypd5 | 3月19 10:20 |
| Marissa_Klausner | ttypd1 | 3月18 06:00 |
| BPierce | tty7 | 3月19 19:17 |
| BWood | tty47 | 3月19 14:00 |
| CSArjent | tty10 | 3月19 11:27 |
| PSingleton | tty19 | 3月19 08:27 |
| Zach_Wilson | tty15 | 3月19 09:27 |
| Travis_Wilson | tty17 | 3月19 12:27 |
| JBerglund | tty19 | 3月19 08:27 |
| Rich_Blum | tty21 | 3月19 12:12 |
| Ed_Lewis | tty35 | 3月19 12:13 |
| Tony_Amico | console | 3月19 12:00 |

$
如从 `who` 的输出所示，系统上有多个用户。注意，某些用户是直接连接的（tty 终端 ID），而另一些是通过网络连接的（tty 终端 ID）。还要注意终端 ID `ttypd1` 和 `ttypd5` 与其他不同。这意味着这些用户正在以现代模式登录。

你还可以看到系统管理员之外还有人登录了系统控制台。这具有潜在危险，因为在某些系统中，通过登录系统控制台更容易获得特权访问。你可以使用这个简单的命令来查看谁登录了、他们是如何进入系统的以及何时登录的。

看看 `who` 命令的另一个用途。这次你使用该命令显示有关 UNIX 机器的信息。

在 shell 提示符下，输入 `who -b`：

```
$ who -b

system boot Oct 28 13:35
```

如你所见，退格键已设置。

### uptime 命令

另一个显示 UNIX 信息的命令是 `uptime`。

在 shell 提示符下，输入 `uptime`：

```
$ uptime

14:20:05 up 2:15, 1 user, load average: 0.01, 0.05, 0.00
```

输出告诉你系统运行的时间。这对于知道机器是否崩溃过很有帮助。

### w 命令

现在看看 `who` 命令的另一个用途。这次你使用该命令来显示有关 UNIX 机器的信息。

在 shell 提示符下，输入 `w`：

```
$ w

14:20:05 up 2:15, 1 user,

  0.00 0:00:.0, load average: 0.01, 0.05, 0.00
```

如你所见，退格键已设置。

# 第三部分
## 第 13 章

# su stevemor
mori 上次成功的实际登录：1999年9月20日周一 08:59:24 tty14
mori 上次失败的实际登录：1999年8月13日周五 17:28:00 tty1

```
TERM = (vt100)
$
```
