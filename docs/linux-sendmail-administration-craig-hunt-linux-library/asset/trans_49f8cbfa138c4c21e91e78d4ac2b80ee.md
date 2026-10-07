
本章将详细检查每个章节。除非进行极细小的更改，否则你不太可能直接修改 **sendmail**.cf** 文件。更改宏配置并重新构建一个新的 sendmail.cf 是进行配置更改的首选技术。然而，理解 sendmail.cf 文件的结构，以及它包含的配置命令的语法和用途，是每位 Sendmail 员员的一项基本技能。理解 **sendmail**.cf** 文件可以帮助你理解宏配置命令的作用，并让你观察到这些更改对底层配置的影响。更重要的是，Sendmail 测试工具是与 sendmail.cf 配置文件协同工作的。为了有效地监控测试，你需要理解测试输出，而这些输出通常基于 **sendmail**.cf** 文件的结构。

我们对 sendmail.cf 文件的分析从开头的第一个部分——本地信息（Local Info）开始，然后逐节遍历整个文件。Local Info 部分包含了种类最丰富的配置语句，也是系统管理员经常修改的 sendmail.cf 文件部分。

## Local Info 部分 (The Local Info Section)

sendmail.cf 文件中的第一个部分包含特定本地主机的信息：例如主机名、任何中继主机名以及域名。它还包含了特定于你的 Sendmail 副本的信息，例如 Sendmail 在返回错误消息时使用的名称，以及你运行的 Sendmail 分发版本号。此外，Local Info 部分还包含了 Sendmail 使用的可选数据库的定义。这些多样化的信息汇集在 **sendmail**.cf 文件的开头，以便在需要手动编辑时更容易定位。

列表 7.1 显示了为 redhat.nc 文件生成的 Sendmail 8.11 sendmail.cf 的 Local Info 部分。它经过了编辑以减少未使用行的数量。它与你 Linux 系统上的 Local Info 部分几乎相同，但不会完全一样。不用担心这些差异；它们都与注释和空行数有关。命令本身没有。

## 列表 7.1 完整的 Local Info 部分

```
####################
# local info #####################
\Cwlocalhost
# 包含我们接收邮件的主机名称的文件
```
```
Fw/etc/mail/local-host-names
# 我的官方域名
#Dj$w.Foo.COM
```
CP.

# '智能'中继主机（可能为空）
DS
# 不可以出现在本地用户名中的操作符
CO @ %!
# 仅包含点的类（用于识别标准名称）
C..
# 仅包含左括号的类（用于识别域字面量）
C[
# access_db 接受类
C(Accept)OK RELAY
# 允许 relay($R) 的主机
FR-o /etc/mail/relay-domains
# 算术映射
Karith ar
# access map 中 tls_connect 的可能值
C(tls)VERIFY ENCR
# 我将未指定的名称发送给谁（null 表示本地投递）
DR
# 谁接收所有本地邮件流量
DH
# 去引号奉留
Kdequote devote
# 类 E: 应该从此主机暴露的名称，即使
# 我们进行了伪装
# 类 L: 应该在本地投递的名称
# 类 M: 应该转换为 $M 的域名
# 类 N: 不应该转换为 $M 的域名
#CL root
# 我 伪装成谁（null 表示不进行伪装）（另见 $=M）
DM
# 我在错误消息中的名称
DnMAIL-DAEMON
# 邮件器表（覆盖域名）
Kmailertable hash -o /etc/mail/mailertable
```

# 第 7 章 sendmail.cf 文件

```
# 虚拟用户表（映射传入的用户）
Kvirtuser hash -o /etc/mail/virtusertable

CP

# 访问列表数据库（用于垃圾邮件拦截）
Kaccess hash hash /etc/mail/access
# 配置版本号
DZ8.11.0
```

空行会被忽略。以 # 注释开头的行是理解晦涩 sendmail.cf 文件的宝贵帮助。以大写字母开头的行是配置命令。列表 7.1 包含了 D、C、F 和 K 命令。

本地信息由 D 命令定义，它定义宏变量；C 命令定义类变量；F 命令从文件中加载类值；K 命令定义信息数据库。sendmail.cf 的命令语法非常简洁。命令只有一个字符长，许多变量的名称也只有一个字符。再加上赋值给变量的值紧挨着变量名挤，这使得你拥有一了既简练又难以阅读的配置命令。让我们仔细查看 D、C、F 和 K 命令，以便我们能够破密 Local Info 部分发生了什么。

## Define宏命令 (The Define Macro Command)

define 命令 D 定义一个变量并为其赋值。一旦定义了该变量，存储的值就会被其他 sendmail.cf 命令以及 Sendmail 本体直接使用。变量提供了灵活性，使得通过修改特定系统的宏变量，相同的相同的 sendmail 配置运行在许多不同的系统上。

传统的变量名是单个 ASCII 字符，用户创建的宏变量使用大写字母，而 Sendmail 内部宏使用小写字母和特殊字符作为名称。这些规则已经改变。现在 Sendmail 定义了几个大写名称变量的含义，在 Sendmail 版本 8.11 中，变量名不再限于单个字符。长变量名被包含在大括号中，例如，{WebHost} 是一个有效的变量名。然而，快速检查 sendmail.cf 显示没有使用长变量名。列表 7.2 显示了 sendmail.cf 中的所有 D 命令。

## 列表 7.2 sendmail.cf 中的 D 命令

```
DS
DR
DH
DM
DnMAIL-DAEMON
D8M
```

列表 7.2 显示了一些有趣的内容。首先，大多数变量都没有设置。前三个 D 命令为 S、R 和 H变量设置了值。这些每个变量识别一个外部中继。

- S 变量存储 m4 配置中 SMART_HOST 变量定义的中继主机。SMART_HOST 中继是处理所有输出邮件的中央邮件服务器。
- R 变量持有处理本地邮件的中继主机名称。m4 配置中的 LOCAL_RELAY 命令设置了 R 的值。当设置 R 时，本地计算机不处理自己的本地邮件。针对本地用户 kathy 的邮件不在处理，而是通过 R变量指定的服务器中继。
- H 变量存储 m4 配置中 MAIL_HUB 命令定义的邮件服务器名称。MAIL_HUB 处理所有接收地址包含本地主机名的本地邮件。此外，虽然发给 kathy 的邮件可能由 LOCAL_RELAY 处理，但来自 foobirds.org 的任何用户的邮件都会通过 MAIL_HUB 服务器中继。

很容易理解为什么这些系统中没有设置这些变量。这些外部中继仅用于，例如在客户端配置中。

第四个没有设置的是 M。它与中继无关。M 变量持有伪装值。我们在本章稍后会讨论邮件，并在第9 章“特殊较4 配置”中会有更多关于伪装的内容。

