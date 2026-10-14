
# Unix 秘籍

![](img/01a10e500e9d28f7d728bbecf2ffd29c_0_0.png)

http://kickme.to/tiger/

本文档总结了 Mizou 可用 Unix 系统最通用的命令。有关更多详细信息，请参阅所有 Unix 操作系统上的 Unix 手页（man pages）。特定单元除了 Unix 手页外通常还有大量的在线文档。请查阅特定系统的文档。此外，在 SHOWME 上，gopher 也有也有大量信息。

本指南中的示例将显示 showme.missouri.edu 上的命令。简称为 SHOWME。

命令的描述遵循使用 Courier 字体显示的习惯。对于 Unix 命令和文件名：大小写是敏感的！命令和文件名将以适当的大小显示。

# Unix 操作系统对大小写敏感！

以下 Unix 系统可以通过公共计算机站点、拨号连接或通过 `telnet` 或 `ftp` 访问。

| Unix 系统 | MU 主机名 | 可用站点 |
| --- | --- | --- |
| AIX (IBM RS/6000) | showme.missouri.edu | 大多数站点；通过 `telnet` |
| Silicon Graphics | sgi*.missouri.edu | 127 Physics<br>124 GCB |
| NeXT | muebnx*.missouri.edu<br>mugenx*.missouri.edu<br>muphnx*.missouri.edu | 17 Engineering Complex West<br>222 GCB<br>127 Physics |

- * 每个工作站都有一个关联编号，它是主机名的一部分。

# 关于计算的大学规则

仅允许当前在读任何 MU 课程的学生或教职员工访问。

MU 规定计算的适当使用通常节约资源，未经适当许可不使用任何资源。除具有相应学号的学生外，无人可使用用户 ID。发现滥用计算资源的人将被拒绝访问，并可能面临停学或其他警告。

有关 MU 用户 ID 策略、计算规则和计算伦理的更多详细信息，请参阅 gopher 中的 3. Guidelines/section。

# 登录

1. `Telnet` 连接到你选择的机器。如果你需要帮助，请向主要计算站点之一的用户顾问咨询。

2. SHOWME 登录提示看起来如下：

```
showme.missouri.edu
login: _
```

如果你是学生，你的登录用户 ID 将是小写字母 'c' 后跟你的学号。如果你有教职员工用户 ID，请查阅校园计算帮助台邮件给你的文档以获取用户 ID 和默认密码。

系统会提示你输入登录密码。

```
showme.missouri.edu
login: c123456
c123456's Password: _
```

如果你有学生用户 ID，则默认密码将是 yymmd 格式的生日。例如：如果你的出生日期是 1974 年 6 月 7 日，则为 740607。第一次登录系统时，系统会提示你设置新密码。系统将提示你输入两次密码（以防止输入错误），以便计算机和人都都认为密码是相同的。在你输入密码时，屏幕不会显示密码。

```
showme.missouri.edu
login: c123456
c123456's password:
You are required to change your password.
Please choose a new one.
c123456's New Password: _
```

选择一个你容易记住但别人不容易记住的密码。

- 请使用包含数字或标点符号的密码。
- 请使用易记的密码。千万不要在任何地方写下密码！
- 请使用你可以快速输入而无需看键盘的密码。
- 不要以任何形式使用你的登录名。
- 不要使用你配偶、孩子或宠物的名字。
- 不要使用易于获取的其他信息。这包括车牌号、电话号码、社会安全号码、汽车品牌、你居住的街道名称等。
- 不要使用全数字密码，或全英文或外语字典的密码。
- 不要使用短于 6 个字符的密码。

Unix 指南 - 1999年5月7日 - mrg - 版本 1.0

记住 Unix 是大小写敏感的。密码：`truman99` 不等于：`Truman99`，甚至不同于：`TRUM99`。关于密码选择的更多信息请见 gopher。

```
showme.missouri.edu
login: c123456
c123456's password:
You are required to change your password.
Please choose a new one.
c123456's New Password: _
```

showme.missouri.edu

login: c123456

c123456's password:

You are required to change your password.

Please choose a new one.

c123456's New Password: _

提示

你需要更改密码。

请选择一个新的。

c123456's New Password: _

星符

showme.missouri.edu

登录

提示

显示密码。

星号提示

showme.missouri.edu

login:

********************

提示

登录后会显示信息。

```
showme.missouri.edu
login: c123456
c123456's password:
You are required to change your password.
Please choose a new one.
c123456's New Password: _
星符
showme.missouri.edu
login: c123456
c123456's password:
你需要更改你的密码。
请选择一个新的。
c123456's New Password: _
星符
showme.missouri.edu
login: c123456
c123456's password:
你需要更改你的密码。
请选择一个新的。
c123456's New Password: _
星符
提示
登录后会显示信息。
提示。
```

showme.missouri.edu

login: c123456

c123456's password:

You are required to change your password.

Please choose a new one.

c123456's New Password: _

```

# 会话控制与作业管理

单词周围的括号 `[ ]` 表示这是该命令的一个选项。斜体单词表示你需要提供斜体中的内容。

| | |
|---|---|
| `clear` | 清除终端屏幕。 |
| `jobs` | 列出停止和后台的作业。仅在 C Shell 中有效。 |
| `bg [%job]` | 在后台继续作业。[默认：当前作业]。仅在 C Shell 中有效。 |
| `fg [%job]` | 在前台继续作业。[默认：当前作业]。仅在 C Shell 中有效。 |
| `stop [%job]` | 停止后台运行的作业。[默认：当前作业]。仅在 C Shell 中有效。 |
| `%job [&]` | 继续作业，[如果有 & 则在后台运行]。仅在 C Shell 中有效。 |
| `nice command &` | 以低优先级在后台运行作业。另见 `command` 命令。 |
| `time command` | 显示命令消耗 CPU 和实际时间。 |
| `history [n]` | 列出最近的 n 个命令。如果你想执行此操作，必须预设 `history = m`，其中 m 是你想要记住的命令数。仅在 C Shell 中有效。 |
| `ps [options]` | 显示进程。默认仅显示你自己的。 |
| `-a` | 所有由终端控制的进程。 |
| `-g` | 显示组组（顶层进程）。 |
| `-tx` | 在 tty x 上的进程，例如 `-pt2` 或 `-tty2` |
| `-u` | 面向用户的输出。特定用户的进程。 |
| `-x` | 甚至显示没有终端的进程。 |
| `kill 123` | 杀死进程 123 [系统范围编号，使用 "`ps`"]。 |
| `kill %1` | 杀死作业 1 [你的进程 1，使用 "`jobs`"]。 |
| `at time [commandfile]` | 在稍后的时间运行程序/脚本。例如：`0300 0300 friday 0300 jan 25` |

每个文件名可以包含任何 ASCII 字符，长度可达 255 个字符。

**大小写敏感！** `file`（文件）和 `file Stuff`（文件内容）是不同的。

如果文件名包含对 shell 特定的字符（如：`>` `|` `&` `?` 或空格），你必须将其包含双引号或单引号中。例如：

```
'My #1 File' or "tmp/huh?" or 'Read Me\!'
```
