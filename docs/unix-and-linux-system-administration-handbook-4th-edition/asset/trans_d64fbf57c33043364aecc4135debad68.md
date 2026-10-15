
## 31.10 STTY：设置终端选项

stty 使你可以直接更改和查询终端驱动程序的各种设置。选项数不胜数，但大多数都可以放心忽略。stty 使用的驱动程序选项名称通常与 termios 手册页相同，但偶尔会有出入。

普通终端比较合适的一组选项是：

```
solaris$ stty intr ^C kill ^U erase ^H -tabs
```

这里的 `-tabs` 会防止终端驱动程序利用终端内置的制表机制，这是一个实用的做法，因为许多模拟器对制表符的处理并不聪明。其余选项分别将中断、删除行和擦除字符设置为 <Control-C>、<Control-U> 和 <Control-H>（退格键）。

你也可以使用 stty 来查看终端驱动程序的当前模式，而不只是设置它们。不带参数的 stty 产生的输出如下：

```
solaris$ stty
speed 38400 baud;
erase = ^H; eol = M-^?; eol2 = M-^?; swtch = <undef>;
ixonany
tab3
```

若要获得更详细的状态报告，请使用 `-a` 选项：

```
solaris$ stty -a
speed 38400 baud; rows 24; columns 80;
intr = ^C; quit = ^\; erase = ^H; kill = ^U; eof = ^D; eol = M-^?; eol2 = M-^?;
swtch = <undef>; start = ^Q; stop = ^S; susp = ^Z; dsusp = ^Y; rprnt = ^R;
werase = ^W; lnext = ^V; flush = ^O;
-parenb -parodd cs8 hupcl -cstopb cread -clocal -crtscts
-ignbrk brkint -inpck -imaxbel -iutf8 -ignpar -parmrk -inpck -istrip -inlcr -igncr icrnl ixon -ixoff
-iuclc ixany imaxbel
opost -olcuc -ocrnl onlcr -onocr -onlret -ofill -ofdel nl0 cr0 tab3 bs0 vt0 ff0
isig icanon iexten echo echoe echok -echonl -noflsh -xcase -tostop -echoprt
echoctl echoke
```

输出的格式类似，但列出了更多信息。如果你近来编写过终端驱动程序，应该凭直觉就能明白这些输出的含义。

stty 操作的是其标准输入的文件描述符，因此你可以使用 shell 的输入重定向字符（<）来设置和查询当前终端之外的其他终端的模式。要更改他人终端的模式，你必须以超级用户身份操作。

## 31.11 TSET：自动设置选项

tset 会将终端驱动程序初始化为适合给定终端类型的模式。类型可以在命令行中指定；如果省略类型，tset 将使用 TERM 环境变量的值。

**tset** 支持一种语法，可将 TERM 环境变量的某些值映射为其他值。如果你经常通过调制解调器或数据交换机登录，并希望终端驱动程序针对你在连接另一端实际使用的终端进行正确配置，而不是使用诸如“dialup”这样通用而无用的类型，那么这个功能就很有用。

例如，假设你在家里使用 **xterm**，而你拨入的系统被配置为认为调制解调器的终端类型是“dialup”。把命令

```
tset -m dialup:xterm
```

放到你的 **.login** 或 **.profile** 文件中，这样无论何时拨入，终端驱动程序都会为 **xterm** 进行合适的设置。

遗憾的是，**tset** 命令并不像它表面上表现得那么简单。要让 **tset** 在设置终端模式之外还调整环境变量，你需要类似下面几行内容：

```
set noglob
eval `tset -s -Q -m dialup:xterm`
unset noglob
```

这套命令组合会抑制 **tset** 通常打印的消息（**-Q** 参数），并要求改为输出用于设置环境的 shell 命令（**-s** 参数）。**tset** 打印出的 shell 命令由反引号捕获，并通过内置命令 **eval** 作为输入送入 shell，从而使其效果与用户亲自输入这些命令一样。

**set noglob** 会阻止 shell 展开 **tset** 输出中可能包含的 * 和 ? 等元字符。**sh/ksh** 用户不需要这条命令（也不需要用于撤销它的 **unset noglob**），因为这些 shell 通常不会展开反引号内的特殊字符。无论你使用哪种 shell，**tset** 命令本身都一样；**tset** 会查看环境变量 SHELL，以决定输出哪种风格的命令。

## 31.12 解除终端卡死

有些程序（例如 vi）在运行时会大幅更改终端驱动程序的状态。这种干预通常对用户不可见，因为程序退出或被挂起时会恢复终端状态。但是，程序有可能崩溃或被终止，而没有执行这一清理步骤。发生这种情况时，终端可能会表现得非常奇怪：它可能无法正确处理换行符、回显键入的字符，或无法正常执行命令。

另一种常见的搞乱终端的方式，是意外地对二进制文件运行 **cat** 或 **more**。大多数二进制文件都含有各种 8 位字符，这必定会把一些不太健壮的模拟器“送入外太空”。
