
## 特性

- Spice 客户机代理为 Spice Linux 客户机添加以下特性：
- 客户机鼠标模式（客户机无需捕获鼠标，无鼠标延迟）
- 根据客户机窗口数量及其分辨率，自动调整 X11 会话的虚拟显示器数量及其分辨率
- 支持在活动的 X11 会话与客户机之间复制和粘贴（文本和图像），此功能同时支持主要选择区和剪贴板
- 支持从客户机向代理传输文件

## 选项

- `-h`
  打印所有命令行选项的简短描述
- `-d`
  记录调试阶段（使用两次可获取更多信息）
- `-f`
  将 uinput 设备视为虚假设备；不进行 ioctl 操作。这与 Xspice 结合使用时非常有用。
- `-o`
  守护程序在处理完单个会话后退出。
- `-s port`
  设置 virtio 串行端口（默认值：/dev/virtio-ports/com.redhat.spice.0）
- `-u device`
  设置输入设备（默认值：/dev/uinput）
- `-x`
  不将程序转为守护进程
- `-X`
  禁用会话信息的使用，**spice-vdagentd** 需要知道哪个 **spice-vdagent** 位于当前活动的 X11 会话中。**spice-vdagentd** 使用 console kit 或 systemd-login（编译时选项）来实现此功能；-X 选项禁用了此功能，如果无法获取会话信息，则只允许存在一个 **spice-vdagent**

## 文件

Sys-V 初始化脚本或 systemd 单元解析以下文件：

`/etc/sysconfig/spice-vdagentd`

可以通过在该文件中设置 *SPICE_VDAGENTD_EXTRA_ARGS* 变量来向 **spice-vdagentd** 传递默认命令行选项

## 另请参阅

(1)

## 版权

版权所有 2010-2013 Red Hat, Inc. 许可证 GPLv3+：GNU GPL 第 3 版或更高版本 <>。

这是自由软件：您可以自由修改和重新分发它。在法律允许的范围内，没有任何担保。

## SPKAC

### 名称

spkac - SPKAC 打印和生成工具

### 概要

`openssl spkac [-in 文件名] [-out 文件名] [-key 密钥文件] [-passin 参数] [-challenge 字符串] [-pubkey] [-spkac spkac文件] [-spksect 节] [-noout] [-verify] [-engine 标识符]`

### 描述

**spkac** 命令处理 Netscape 签名的公钥和挑战（SPKAC）文件。它可以打印出其内容，验证签名，并根据提供的私钥生成自己的 SPKAC。

### 命令选项

- `**-in** *文件名*`
  指定读取的输入文件名，如果未指定此选项，则默认为标准输入。如果使用了 **-key** 选项，则此选项被忽略。

- `**-out** *文件名*`
  指定写入的输出文件名，默认为标准输出。

- `**-key** *密钥文件*`
  使用 **密钥文件** 中的私钥创建一个 SPKAC 文件。如果存在 **-in**、**-noout**、**-spksect** 和 **-verify** 选项，则这些选项将被忽略。

- `**-passin** *参数*`
  输入文件的密码源。有关 **参数** 格式的更多信息，请参阅 (1) 中的 **PASS PHRASE ARGUMENTS**（密码短语参数）部分。

- `**-challenge** *字符串*`
  在创建 SPKAC 时指定挑战字符串。

- `**-spcac** *spkac名称*`
  允许使用包含 SPKAC 的变量的替代名称。默认值为‘**SPKAC**’。此选项影响生成的和输入的 SPKAC 文件。

- `**-spksect** *节*`
  允许使用包含 SPKAC 的节的替代名称。默认值为默认节。

- `**-noout**`
  不输出 SPKAC 的文本版本（在创建 SPKAC 时不使用）。

- `**-pubkey**`
  输出 SPKAC 的公钥（在创建 SPKAC 时不使用）。

- `**-verify**`
  验证提供的 SPKAC 上的数字签名。

- `**-engine** *标识符*`
  通过其唯一的 **标识符** 字符串指定引擎将导致 **spkac** 尝试获取指定引擎的功能引用，从而在必要时初始化它。然后，该引擎将被设置为所有可用算法的默认引擎。

### 示例

打印 SPKAC 的内容：

```
openssl spkac -in spkac.cnf
```

验证 SPKAC 的签名：

```
openssl spkac -in spkac.cnf -noout -verify
```

使用挑战字符串“hello”创建一个 SPKAC：

```
openssl spkac -key key.pem -challenge hello -out spkac.cnf
```

### 备注

将适当 **DN** 组件附加到创建的 **SPKAC** 后，可以将其输入 **ca** 工具。

**SPKAC** 通常由 Netscape 在提交包含 **KEYGEN** 标签的表单时生成，作为证书注册过程的一部分。

挑战字符串允许原始形式的私钥持有证明。通过检查 **SPKAC** 签名和一个随机挑战字符串，可以保证用户知道与正在认证的公钥对应的私钥。这在某些应用中非常重要。如果没有这一点，可以使用之前的 **SPKAC** 进行“重放攻击”。

## 另请参阅

(1)

## SPLAIN

### 名称

diagnostics, splain - 生成冗长的警告诊断信息

### 概要

使用 diagnostics pragma：

```
use diagnostics;
use diagnostics -verbose;
enable diagnostics;
disable diagnostics;
```

使用 splain 独立过滤器程序：

```
perl program 2>diag.out
splain [-v] [-p] diag.out
```

使用 diagnostics 从运行异常的脚本中获取堆栈跟踪：

```
perl -Mdiagnostics=-traceonly my_script.pl
```

### 描述

#### diagnostics Pragma

此模块扩展了 Perl 编译器和 Perl 解释器（通过带 -w 开关运行 perl 或使用 use warnings）通常发出的简短诊断信息，并用 perldiag 中更详细的解释性描述进行补充。与其他 pragma 一样，它影响程序的编译阶段，而不是执行阶段。

要在程序中使用此 pragma，只需在程序开始处（或接近开始处）调用

```
use diagnostics;
```

（注意这会*启用* Perl 的 *-w* 标志。）然后，您的整个编译过程将（编辑：;）受到增强诊断信息的约束。这些信息仍然输出到 STDERR。

由于运行时问题和编译时问题之间的相互作用，以及这本来可能就不是一个好主意，您在编译时不能使用 *no diagnostics* 来关闭它们。但是，您可以使用 *disable() 和 enable()* 方法在运行时控制其行为，分别关闭和打开它们。

**\-verbose** 标志会在任何其他诊断信息之前首先打印出 perldiag 的介绍。*​$diagnostics::PRETTY* 变量可以为分页器生成更美观的转义序列。

由 Perl 本身发出的警告（或者更准确地说，与 perldiag 中找到的描述匹配的警告）只显示一次（没有重复的描述）。由用户代码生成的 *warn()* 类型的警告不受影响，允许显示重复的用户消息。

当 Perl 终止（die）时，此模块还会在错误消息中添加堆栈跟踪。这对于定位导致终止的原因非常有用。**\-traceonly**（或仅 **-t**）标志关闭警告消息的解释，只留下堆栈跟踪。因此，如果您的脚本正在终止，请用以下命令再次运行

```
perl -Mdiagnostics=\-traceonly my\_bad\_script
```

以查看终止时的调用堆栈。通过提供 **\-warntrace**（或仅 **-w**）标志，发出的任何警告也将附带堆栈跟踪。

#### splain 程序

虽然看起来是一个全新的程序，*splain* 实际上只不过是 *diagnostics.pm* 模块（可执行）的链接，以及 *diagnostics.pod* 文档的链接。**-v** 标志类似于 *use diagnostics \-verbose* 指令。**​-p** 标志类似于 *​$diagnostics::PRETTY* 变量。既然您正在使用 *splain* 进行后处理，能够 *enable()* 或 *disable()* 处理就没有意义了。

*splain* 的输出指向 **STDOUT**，这与 pragma 不同。

### 示例

以下文件肯定会在运行时和编译时触发一些错误：

```
use diagnostics;
print NOWHERE "nothing\n";
print STDERR "\n\tThis message
should be unadorned.\n";
warn "\tThis is a user warning";
print "\nDIAGNOSTIC TESTER: Please enter a <CR> here: ";
my $a, $b = scalar <STDIN>;
print "\n";
print $x/$y;
```

如果您更喜欢先运行程序，然后再查看其问题，请执行以下操作：

```
perl -w test.pl 2>test.out
./splain < test.out
```

请注意，这在更不可靠的 shell 中通常是不可能实现的，因为理论上

```
(perl -w test.pl >/dev/tty) >& test.out
./splain < test.out
```

您只是将现有的 `stdout` 移到了其他地方。

如果您不想修改源代码，但仍希望进行即时警告，请执行以下操作：

```
exec 3>&1;
perl -w test.pl 2>&1 1>&3 3>&- | splain 1>&2 3>&-
```

很酷，不是吗？

如果您想即时控制警告，请执行类似以下操作的操作。请确保先执行 use，否则您将无法访问 *enable()* 或 *disable()* 方法。

```
use diagnostics; # 检查整个编译阶段
print "\nnti for 1st bogus diag: SQUAWKINGS\n";
print BOGUS1 'nada';
print "done with 1st bogus\n";

disable diagnostics; # 仅关闭运行时警告
print "\nti for 2nd bogus: (squelched)\n";
print BOGUS2 'nada';
print "done with 2nd bogus\n";

enable diagnostics; # 重新打开运行时警告
print "\nti for 3rd bogus: SQUAWKINGS\n";
print BOGUS3 'nada';
print "done with 3rd bogus\n";

disable diagnostics;
print "\nti for 4th bogus: (squelched)\n";
print BOGUS4 'nada';
print "done with 4th bogus\n";
```

