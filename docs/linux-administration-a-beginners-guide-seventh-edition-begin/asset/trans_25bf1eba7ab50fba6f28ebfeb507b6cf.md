

呼出电话，限制另一组仅能进行内部通话。通常，拨号计划（dialplan）如下：

```
[general]
--> 此处放置某些设置
```

```
[globals]
-->在这里定义一些全局变量
```

```
[context_name_1]
--> 分机 1, 优先级 1, 应用
--> 分机 1, 优先级 2, 应用
```

```
--> 分机 helpdesk, 优先级 1, 应用
...
```

```
include => context_name_1

--> 分机 999, 优先级 1, 应用
--> 分机 999, 优先级 1, 应用
```

这些设置的解释如下：

[general]

- **static=yes | no** 控制 Asterisk 在添加或删除扩展时是否重写 **extension.conf** 文件。如果设置 **static=no**，你可以通过 CLI 命令保存拨号计划。
- **protect=yes | no** 此选项如果设置为 no，则允许通过 CLI 命令从命令行重写拨号计划。
- **autofload=yes | no** 如果此选项设置为 yes，Asterisk 在完成其任务后将挂断电话。如果没有设置，*强烈建议*将此选项设置为 yes。

## Linux 管理：入门指南

[globals]:

可选部分，可在此上下文中指定你自己的变量。注意，全局变量不区分大小写，因此 $[MYVAR] 和 $(MYVAR) 是相同的。通用格式：`variable_name => variable_value`

[context_name]:

上下文标题。这是为每个设备或通道配置的默认上下文。对于每一个迁入的连接，Asterisk 都会查找该设备定义的上下文，并执行在该节标题下定义的指令集。每个上下文由一个或多个扩展（extensions）组成。扩展“数字”可以由数字、字母或两者共同组成；它仅仅是 Asterisk 在拨打该扩展分号时将执行的一组特定操作。通过上下文的帮助，我们可以组织拨号计划。

```
include => context
```

你可以将一个上下文中的扩展包含到另一个上下文中。Asterisk 始终会尝试在当前上下文中查找匹配的扩展，只有当当前上下文中没有匹配项时，才会遵循 include 语句进入新的上下文。

## 模块：modules.conf

所有在 Asterisk 系统启动时默认加载的模块（例如各种应用程序、解码器和通道）均在 modules.conf 文件中配置。这是 Asterisk 加载器配置文件，在其中可以配置从目录 (/usr/lib64/asterisk/modules/ ) 加载或不加载的所有模块。虽然 modules.conf 文件不是强制要求的，但没有它，Asterisk 系统无法提供任何功能。

如果你在 modules.conf 文件中定义了 autoload=yes，Asterisk 将在目录 (/usr/lib64/asterisk/modules/) 中搜索所有模块并在启动时加载它们。

未加载的模块会消耗大量资源，不会对你的系统性能产生负面影响；但是，最佳实践是仅加载你计划在系统中使用的模块。

## 语音协议 (VoIP)

在连接到 Asterisk 控制台时，module show 命令会检查你 Asterisk 系统中加载的模块。注意，你的控制台输出可能与以下列表不同：

```
CLI> module show
Module              Description             Count Status Level
chan_sip.so         Session Initiation Protocol (SIP)  0 Running core
codec_ulaw.so        Mu-Law/Decoder           0 Running core
...
format_g72.so                               0 Running core
res_rtp_asterisk.so  Asterisk RTP Stack       0 Running core
res_xmpmf.so         Asterisk Interface      0 Running core
```

对于我们的第一个 PBX 实例，我们将接受 modules.conf 文件中的默认配置指令。让我们查看一个示例 modules.conf 文件以理解其内部结构。

