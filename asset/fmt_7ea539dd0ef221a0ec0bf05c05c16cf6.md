
## setterm

```
setterm [ -foreground
black|red|green|yellow|blue|magenta|cyan|white|default ]
```

```
setterm [ -background
black|red|green|yellow|blue|magenta|cyan|white|default ]
```

```
setterm [ -ulcolor
black|grey|red|green|yellow|blue|magenta|cyan|white ]
```

```
setterm [ -ulcolor bright
red|green|yellow|blue|magenta|cyan|white ]
```

```
setterm [ -hbcolor
black|grey|red|green|yellow|blue|magenta|cyan|white ]
```

```
setterm [ -hbcolor bright
red|green|yellow|blue|magenta|cyan|white ]
```

```
setterm [ -inversescreen [on|off] ]
```

```
setterm [ -bold [on|off] ]
```

```
setterm [ -half-bright [on|off] ]
```

### 终端与键盘

```
setterm [ -blink [on|off] ]
```

```
setterm [ -reverse [on|off] ]
```

```
setterm [ -underline [on|off] ]
```

```
setterm [ -store ]
```

```
setterm [ -clear [ all|rest ] ]
```

```
setterm [ -tabs [tab1 tab2 tab3 ... ] ] where tabn = 1-160
```

```
setterm [ -clrtabs [ tab1 tab2 tab3 ... ] where (tabn = 1-160)
```

```
setterm [ -regtabs [ 1-60 ] ]
```

```
setterm [ -blank [ 0-60 ] ]
```

```
setterm [ -powersave [ on|vsync|hsync|powerdown|off ] ]
```

```
setterm [ -powerdown [ 0-60 ] ]
```

```
setterm [ -dump [ 1-NR_CONS ] ]
```

```
setterm [ -append [ 1-NR_CONS ] ]
```

```
setterm [ -file dumpfilename ]
```

### 命令

```
setterm [ -standout [ attr ]
```

```
setterm [ -blength [ 0-2000 ]
```

```
setterm [ -bfreq freqnumber ]
```

此命令向标准输出显示一个字符串，用于设置指定的终端功能。大多数选项都是自俗易懂的。

示例：将你的终端键盘类型设置为 Olivetti：

`setterm -keyboard olivetti`

- `--term` 用于覆盖 `TERM` 环境变量。
- `--reset` 显示终端重置字符串。
- `--initialize` 显示当前的终端初始化字符串。
- `--default` 将显示选项重置为默认值。
- `--store` 将当前显示选项存储为默认值。

### stty [SETTING]...

# stty [OPTION]

如果不带任何选项调用 `stty`，`stty` 将显示波特率、行规律控制数和行设置，这些设置与 "`stty sane`" 不同。如果带有选项调用，它将显示或设置一个或多个指定的值。

示例：如果你真的搞乱了 `stty` 值，并想让一切回到合理的配置：

`stty sane`

| 控制键 | stty 名称 | 功能 |
|---|---|---|
| `<Ctrl>-` | | quit | ^C 的更具激情的版本。 |
| `<Ctrl>?, <Del>` | erase | 删除上一个字符。 |

![](img/3ac9b27762bf6b1e48d880d6f0f96f8b_150_0.png)

122 终端与键盘

```
<Ctrl>-C   intr       停止运行的程序。
<Ctrl>-D   eof       发送输入结束信号。
<Ctrl>-Q               重启输出到屏幕。
<Ctrl>-S   stop      停止输出到屏幕。
<Ctrl>-U   kill      清除命令行。
<Ctrl>-Z   susp      挂起执行中的命令。
```

```
-a, --all    以人类可读的格式显示所有当前设置。
-g, --save    以参数格式显示所有当前设置，另一个可以恢复当前设置的 stty 命令。
```

### 控制设置

```
parenb    告诉 stty 在输出中生成奇偶位并在输入中期望奇偶位。可以取反。
parodd    告诉 stty 设置奇偶校验（即使取反也是如此）。
cs5, cs6, cs7, cs8 告诉 stty 将字符大小设置为 5、6 或 8 字节。
hup, hupcl    告诉 stty 在最后一个终端关闭时发送挂断电话信号。可以取反。
stopb    告诉 stty 每个字符使用两个停止位（如果取反则使用一个）。
creat     告诉 stty 允许接收输入。
clocal    告诉 stty 禁用调制解调器控制。
crcts 告诉 stty 启用 RTS/CTS 流控制。
```

### 输入设置

```
ignbrk 告诉 stty 忽略中断字符。
brkint 告诉 stty 让中断导致中断信号。
ignpar 告诉 stty 忽略带有奇偶性错误的字符。
parodd 告诉 stty 设置奇奇偶校验（即使取反也是如此）。
creat 告诉 stty 允许接收输入。
clocal 告诉 stty 禁用调制解调器控制。
crcts 告诉 stty 启用 RTS/CTS 流控制。
```

`parenb` 告诉 `stty` 在输出中生成奇偶位并在输入中期望奇偶位。可以取反。

`parodd` 告诉 `stty` 设置奇偶偶校验。

`cs5, cs6, cs7, cs8` 告诉 `stty` 将字符大小设置为 5、6 或 8 字节。

`hup, hupcl` 告诉 `stty` 在最后一个终端关闭时发送挂断电话信号。

`stopb` 告诉 `stty` 每个字符使用两个停止位。

`creat` 告诉 `stty` 允许接收输入。

`clocal` 告诉 `stty` 禁用调制解调器控制。

`crcts` 告诉 `stty` 启用 RTS/CTS 流控制。

### 特殊字符

特殊字符的默认值取决于系统。它们使用“名称 值”的语法进行设置，其中值可以用光帽符号表示（例如，`^C`）、字面值，也可以是整数（十六进制前加 0x）。

| intr | 中断信号。 |
| :--- | --- |
| quit | 退出信号。 |
| erase | 删除上输入的最后一个字符。 |
| kill | 删除当前行。 |
| eof | 终止输入，又名文件结束（EOF）。 |
| eol | 行结束。 |
| eol2 | 另一种行结束字符。 |
| swtch | 切换到不同的 shell 层。 |
| start | 在停止后重启输出。 |
| stop | 停止输出。 |
| susp | 发送终端停止信号。 |
| dsusp | 在刷新输入后发送终端停止信号。 |
| rprnt | 重新绘制当前行。 |
| werase | 删除上输入的最后一个单词。 |
| Inext | 字面量输入下一个输入的字符，即使它是特殊字符。 |

### 特殊设置

**`min N`** 指定在时间超时前满足读取的最小字符数，到那时将设置 "`-icanon`"

**`time N`** 指定当设置了 "`-icanon`" 时，如果未读取到最小字符数，则指定超时前的秒数（十分之一）。

**`ispeed N`** 指定输入速度为 N。

**`ospeed N`** 指定输出速度为 N。

**`rows N`** 定义给 tty 内核驱动的行数。

**`cols N, columns N`** 定义传递 tty 内核驱动的列数。

**`size`** 显示内核认为终端拥有的行数和列数。

**`line N`** 指定要使用的行规律。

**`speed`** 打印终端速度。
