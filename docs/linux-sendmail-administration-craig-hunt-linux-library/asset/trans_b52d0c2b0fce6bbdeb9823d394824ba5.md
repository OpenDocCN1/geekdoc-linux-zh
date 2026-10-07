
wren.foobirds.org。如果该系统不可用，它将尝试 parrot.foobirds.org。在 ibis 的情况下，Sendmail 将将邮件投递到 ibis.foobirds.org。`/mx` 命令允许你预测投递过程。

列表 10.12 中的第二个命令 `/canon` 会向 DNS 查询规范名称（canonical name）。在示例中，`/canon` 命令的主机名为 `redbreast`，它被传递给 DNS。DNS 为主机 `redbreast` 返回规范名称 `robin.foobirds.org`。

列表 10.12 中的最后一个命令在数据库中查找值。在示例中，数据库是 `generics`，它是 `genericstable` 的标准内部名称。用于查找的键是 `kathy`。在列表 10.12 中，键 `kathy` 返回 `genericstable` 中的值 `kathy.mcafferty`。系统上配置的任何数据库都可以使用 `/map` 命令进行搜索。

查询 DNS 或搜索数据库的命令在本文早期运行的测试中均未使用。通常，你并不关心这些值对 DNS 或数据库返回的地址所产生的影响；你查询 DNS 或数据库的唯一时刻是你想确定这些系统向 Sendmail 提供了什么内容。由于地址模式通常用于调试或完善 Sendmail 配置，你更有可能使用地址模式命令，让你检查 `sendmail.cf` 文件的内容。列表 10.13 显示了这两个命令的执行情况。

# 列表 10.13 在地址测试模式下查看配置文件

```
=M
mail 0 (prog): P=/usr/bin/smush S=EnvFromML/HdrFromLREvTol/HdrTol M=0 U=0 F=DFMetoloqu L=0 E=
T-Unix/X-Unix/X-Unix A=n A-smush -c u
mail 1 (*file*): P=[FILE] S=parse/parse R=parse M=0 U:0:
F=9DFMetoloqu L=0 T-Unix/X-Unix/X-Unix A=FILE S=u
mail 2 (*include*): P=/dev/null S=parse/parse R=parse/parse
M=0 U=0 F=s E=
T=<undefined>=<undefined>
A=Include S=u
mail 3 (smtp): P=[IPC] S=EnvFromSMTP/HdrFromSMTP
REvTol/EnvSMTP M=0 U=0 F=DFMXamu L=90 E=\r\n
TNS/RFC822/SMTP A=TCP $h
mail 4 (smtp): P=[IPC] S=EnvFromSMTP/HdrFromSMTP
REvTol/EnvSMTP M=0 U=0 F=DFMXamu L=90 E=\r\n
TNS/RFC822/SMTP A=TCP $h
```

# 在测试模式下运行 Sendai 291

```
mailer 5 (smtp8): M=[IPC] S=EnvFromSMTP/HdrFromSMTP
R=EnvToSMTP/EnvToSMTP M=U=0 F=%DFMXamu L=990 E=\r\n	DNS/RFC8222/ A=TCP C$
mailer 6 (smtp): M=[IPC] S=EnvFromSMTP/HdrFromSMTP
R=EnvToSMTP/EnvToSMTP M=U=0 F=%DFMXamu L=990 E=\r\n	DNS/RFC8222/ A=TCP C$
mailer 7 (relay): M=[IPC] S=EnvFromSMTP/HdrFromSMTP
R=MasqSMTP/MasqSMTP M=U=0 F=8DFMXamu L=2040 E=\r\n	DNS/RFC8222/ A=TCP C$
mailer 8 (promail): P=/usr/bin/promail S=EnvFromSMTP/HdrFromSMTP
R=EnvToSMTP/EnvToSMTP M=U=0 F=DFMXamu L=90 E=\r\n	DNS/RFC822/X-Unix A=n -Y -m $d
mailer 9 (local): P=/usr/bin/promail S=EnvFromL/HdrFromL
R=EnvTol/HdrTol M=U=0 F=/59;ADMFPSfhlnsq L=0 E=\r\n	DNS/RFC822/X-Unix A=n -a -h $d
```
=Final
RS$ < "@LOCAL" > $\$	$1 < $2 foobirds . org > $2
RS$ < + $+	$1 , @2 : $3
RS+ @ -$0 @ $$
+ $1 @ $2

`-M` 命令打印出当前 Sendmail 配置中的所有 mailer 定义。`-M` 显示的所有字段都是在第 7 章“Mailer 定义（Mailer Definitions）”部分讨论过的（注：原文此处对列表 10.13 之后的内容似乎存在乱码或重复逻辑错误，翻译时已根据上下文进行了逻辑对齐）。但 `-M` 命令也显示了一些非常有趣的内容：首先，你会注意到每个 mailer 都有一个标识数字以及一个名称。其次，更重要的是，有两个 mailer 并没有出现在 `sendmail.cf` 文件中：

- *file*：*file* mailer 是一个直接将邮件内容发送到文件的内部 mailer。
- *include*：*include* 是一个将邮件附加列表的内部 mailer。

`/S` 命令显示给定规则集的所有重写规则。在列表 10.13 中，我们要求 Sendmail 显示最终规则集的内容。当规则集由 `/S` 命令显示时，规则集中的任何变量都会被变量的值所替换。在列表 10.13 中，`/S` 命令的第三条规则似乎包含了 (img/963911aa446fb8976cb3d37f7aafdd_34_0.png)。

# 测试 Sendmail

字符串字符串 `wren.foobirds.org`。实际上，规则包含了 `$`，所以 `wren.foobirds.org` 必须是存储在变量中的。通常，`/S` 命令用于检查规则集，以查看你对规则集的修改是否符合预期，或者你正在试图弄清楚规则集为什么这样做。

要查看执行中的规则集的细节，你可以使用调试模式。使用 `-d` 命令在地址模式内选择调试级别。列表 10.14 显示了开启和未开启调试 `12` 的测试。

# 在地址测试期间使用调试设置

```
sendmail
地址测试模式（规则集未自动调用）
输入 <ruleset><address>
> final @foobirds.org
input: sara @foobirds.org
returns: sara @foobirds.org
-d21.12
> final @foobirds.org
input: sara @foobirds.org
-----trying rule: $* < $*
------rule fails
-----trying rule: $* < $+
------rule matches: $1 < $2
rewritten as: sara @foobirds.org
-----trying rule: $* < $+
------rule fails
-----trying rule: $* < %LOCAL >
------rule fails
-----trying rule: $* < $+
------rule matches: $1 $2 $3
rewritten as: sara @foobirds.org
-----trying rule: $* < $+
------rule fails
-----trying rule: @ + $+ ; $+
------rule fails
-----trying rule: $* @ $°
------rule fails
-----trying rule: $+ @ - UUCP
------rule fails
-----trying: $+ % @ $@
final returns: sara@foobirds.org
/quit
```

在列表 10.14 中，地址 `sara@foobirds.org` 通过规则集 `final` 产生了输出地址 `sara@foobirds.org`。这正是我们预期的，但地址模式只显示了进入规则集的值和输出的值；它没有显示任何中间的细节。通过列表 10.13 中的 `/S` 命令，我们知道最终规则集包含了八条单独的规则。在默认设置下，我们无法看到规则的具体执行。因此，我们使用 `-d21.12` 命令将调试级别设置为 `21.12`。

进行了第二次测试，地址 `sara@foobirds.org` 运行通过规则集 `final`。这一次，每个重写规则的操作都会显示出来。Sendmail 显示字符串 `trying:`，后面是规则的模式 (pattern) 字段。如果地址不匹配模式，Sendmail 显示 `rule fails` 并移动到下一条规则。如果地址匹配模式，Sendmail 打印字符串 `rule matches:`，后面是规则的模板 (template) 字段，然后打印重写后的地址。它会一直这样下去，直到整个规则集运行完毕，或者遇到了导致 Sendmail 执行规则集的规则。这种程度的细节可能在你调试一个编写的但运行不符合预期的规则集时才需要。

`21.12` 调试级别在地址模式内很有用，因为它影响了测试期间显示的细节程度。然而，大多数地址模式的调试级别是在命令行调用的，而不是在地址模式内。

# 使用调试级别

（注：此处原文文本似乎存在严重的重复和乱码，翻译时已根据上下文逻辑进行了整合处理）
