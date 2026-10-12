
## Shell 控制结构

```
else if (expression) then
    Statements
else
    Statements
endif
```

if 条件可以嵌套，即一个 if 条件内部可以包含另一个 if 条件。if 条件不强制要求有 else 部分。如果所有 if 语句中指定的表达式均为假，则执行 else 部分。语句中可选的 if 部分（`else if (expression) then`）在其后的条件为真且前一个 if 语句为假时执行。关键字 `endif` 用于指示 if 语句的结束，这在存在嵌套 if 条件时非常有用。在这种情况下，你应能够将 `endif` 与 `if` 匹配，以确保所有 if 语句都正确编码。

使用变量 `var` 仅有 Yes 和 No 两个值作为示例，以下是使用 tcsh 的编码方式：

```
if ($var == "Yes") then
    echo "Value is Yes"
else if ($var == "No") then
    echo "Value is No"
else
    echo "Invalid value"
endif
```

tcsh 中 if 条件的第二种形式如下：

```
if (expression) command
```

在这种格式下，如果表达式求值为真，只能执行单个命令。

## case 语句

case 语句用于根据与指定变量匹配的离散值或值范围来执行语句。在大多数情况下，如果你有很多条件，可以使用 case 语句代替 if 语句。

pdksh 和 bash 中 case 语句的格式如下：

```
case str in
    str1 | str2)
        Statements;;
    str3 | str4)
        Statements;;
    *)
        Statements;;
esac
```

你可以为每个条件指定若干离散值——例如 `str1`、`str2` 等，或者使用通配符指定一个值。最后一个条件应为 `*`（星号），如果在其他条件都不满足时执行。对于每个指定的条件，执行关联的语句直到双分号（`;;`）。

你可以编写一个脚本，如果你提供月份数字作为参数，它将回显月份名称。如果你提供的数字不在 1 到 12 之间，你将收到一条错误消息。该脚本如下：

```
#!/bin/sh
case $1 in
  01 | 1) echo "Month is January";;
  02 | 2) echo "Month is February";;
  03 | 3) echo "Month is March";;
  04 | 4) echo "Month is April";;
  05 | 5) echo "Month is May";;
  06 | 6) echo "Month is June";;
  07 | 7) echo "Month is July";;
  08 | 8) echo "Month is August";;
  09 | 9) echo "Month is September";;
  10) echo "Month is October";;
  11) echo "Month is November";;
  12) echo "Month is December";;
  *) echo "Invalid parameter";;
esac
```

你需要在每个条件下的语句末尾加上双分号（`;;`）。如果不这样做，下一个条件下的语句也会被执行。

tcsh 中 case 语句的格式如下：

```
switch (str)
  case str1;str2:
    Statements
    breaksw
  case str3;str4:
    Statements
    breaksw
  default:
    Statements
    breaksw
endsw
```

你可以为每个条件指定若干离散值——例如 `str1`、`str2` 等，或者使用通配符指定一个值。最后一个条件应为 `default`，如果在其他条件都不满足时执行。对于每个指定的条件，执行关联的语句直到 `breaksw`。

前面为 pdksh 和 bash 展示的回显给定数字对应月份的示例，可以按如下方式用 tcsh 编写：

```
#!/bin/tcsh
set month = 5
switch ($month)
    case 1: echo "Month is January" ; breaksw
    case 2: echo "Month is February" ; breaksw
    case 3: echo "Month is March" ; breaksw
    case 4: echo "Month is April" ; breaksw
    case 5: echo "Month is May" ; breaksw
    case 6: echo "Month is June" ; breaksw
    case 7: echo "Month is July" ; breaksw
    case 8: echo "Month is August" ; breaksw
    case 9: echo "Month is September" ; breaksw
    case 10: echo "Month is October" ; breaksw
    case 11: echo "Month is November" ; breaksw
    case 12: echo "Month is December" ; breaksw
    default: echo "Oops! Month is October!" ; breaksw
endsw
```

你需要在每个条件下的语句末尾加上 `breaksw`。如果不这样做，下一个条件下的语句也会被执行。

## break 和 exit 语句

你应该了解另外两个语句：break 语句和 exit 语句。

break 语句可用于终止迭代循环，例如 for、until 或 repeat 命令。

Exit 语句可用于退出 shell 程序。你可以选择在 exit 后使用一个数字。如果当前 shell 程序是由另一个 shell 程序调用的，调用程序可以检查代码（取决于 shell 是 `$?` 或 `$status` 变量）并据此做出决定。

## 在 Shell 脚本中使用函数

与其他编程语言一样，shell 程序也支持函数。函数是 shell 程序的一部分，执行特定过程；你可以在 shell 程序中多次重复使用同一个函数。函数有助于在编写 shell 程序时消除代码重复的需要。

pdksh 和 bash 中函数的格式如下：

```
func() {
   Statements
}
```

你可以按如下方式调用函数：

```
func param1 param2 param3
```

参数 `param1`、`param2` 等是可选的。你也可以将参数作为单个字符串传递——例如，`$@`。函数可以解析参数，就好像它们是作为命令行参数从命令行传递给 shell 程序的位置参数，但实际上使用脚本内部传递的值。例如，以下脚本使用名为 `Displaymonth()` 的函数，如果你传递一个不在 1 到 12 范围内的月份数字，它会显示月份名称或错误消息。此示例适用于 pdksh 和 bash：

```
#!/bin/sh
Displaymonth() {
   case $1 in
      01 | 1) echo "Month is January";;
      02 | 2) echo "Month is February";;
      03 | 3) echo "Month is March";;
      04 | 4) echo "Month is April";;
      05 | 5) echo "Month is May";;
      06 | 6) echo "Month is June";;
      07 | 7) echo "Month is July";;
      08 | 8) echo "Month is August";;
      09 | 9) echo "Month is September";;
      10) echo "Month is October";;
      11) echo "Month is November";;
      12) echo "Month is December";;
      *) echo "Invalid parameter";;
   esac
}
Displaymonth 8
```

前面的程序显示以下输出：

Month is August

## 相关的 Fedora 和 Linux 命令

使用 shell 或编写 shell 脚本时，你可以使用这些命令和工具：

- chsh—用于更改登录 shell 的命令
- kibitz—允许两人在单个 shell 中进行交互
- mc—名为 GNU Midnight Commander 的可视化 shell
- nano—适用于控制台的易用文本编辑器
- system-config-users—一个图形用户管理实用工具，可用于更改一个或多个用户的登录 shell
- shar—用于创建 shell 归档的命令
- vi—vi（实际上是 vim）文本编辑器

## 参考资料

- http://www.linuxgazette.com/issue70/gosh.html—一篇关于“引导 Linux”的 Linux Gazette 文章，其中包含关于启动过程中 BIOS 和 MBR 方面的许多细节。
- http://www.lostircuits.com/advice/bios2/1.shtml—the LostCircuits BIOS 指南；关于所有这些 BIOS 设置含义的许多细节。
- http://www.rojakpot.com/default.aspx?location=1—the BIOS 优化指南；关于随心所欲调整这些 BIOS 设置的细节。
- http://www-106.ibm.com/developerworks/linux/library/l-slack.html—通过 IBM 网站链接到一篇关于启动 Slackware Linux 的文章，以及一个关于 System V 与 BSD init 脚本历史的侧边栏。
- /usr/src/linux/init/main.c—了解 Linux 如何启动的最佳地点。阅读起来真的很有趣。从源代码获取！
- http://sunsite.dk/linux-newbie/—Linux Newbie 管理员指南主页——对 Linux 系统管理的温和介绍。
- GRUB 手册—这本尚未完成的手册可以在 http://www.gnu.org/software/grub/manual/ 找到。在你的 Fedora Core 系统上，`info grub` 提供大量信息和一个 `grub.conf` 文件示例（`/boot/grub/menu.lst` 是 `/boot/grub/grub.conf` 的符号链接；使用任一名称均可），可以在 `/usr/doc/grub` 中找到。
- “LILO User’s Guide”——Werner Almesberger 关于 Linux 加载器 LILO 及其在基于 Intel 的 PC 上工作原理的权威技术著作。在 `/usr/share/doc/lilo*/doc` 目录下查找文件 `User_Guide.ps`，可以使用 `gv` 客户端查看。LILO 已从 Fedora Core 中移除；GRUB 现在是该发行版支持的默认启动加载器。
- “Managing Initscripts with Red Hat’s chkconfig”——作者 Jimmy Ball，Linux Journal，2001 年 4 月；第 128–132 页。
- “Grub, Glorious Grub”——作者 Hoyt Duff，Linux Format，2001 年 8 月；第 58–61 页。关于 GRUB 启动加载器的教程。
- http://www.redhat.com/docs/manuals/linux/RHL-9-Manual/custom-guide/s1-services-serviceconf.html—Red Hat 关于使用 system-config-service 客户端（当时称为 redhat-config-service）的指南。

