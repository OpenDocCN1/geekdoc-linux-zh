
前面为 pdksh 和 bash 展示的“输入数字显示月份”的示例，用 tcsh 可以写成如下形式：

```
#!/bin/tcsh

set month = 5
switch ( $month )
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
    default: echo "Oops! Month is Octember!" ; breaksw
endsw
```

每个条件下的语句后面都必须加上 `breaksw`。如果不加，下一个条件下的语句也会被执行。

## break 和 exit 语句

你还需要了解另外两个语句：`break` 语句和 `exit` 语句。

`break` 语句可用于终止迭代循环，例如 `for`、`until` 或 `repeat` 命令。

`exit` 语句可用于退出 shell 程序。你可以在 `exit` 后面加一个数字。如果当前 shell 程序是被另一个 shell 程序调用的，调用程序可以检查该退出码（根据 shell 不同，可能是 `$?` 或 `$status` 变量），并据此作出决策。

## 在 Shell 脚本中使用函数

与其他编程语言一样，shell 程序也支持函数。函数是 shell 程序中执行特定过程的一段代码；你可以在 shell 程序内多次复用同一个函数。函数有助于在编写 shell 程序时避免重复代码。

下面是 pdksh 和 bash 中函数的格式：

```
```sh
func(){
    Statements
}
```
```

可以这样调用函数：

```
```sh
func param1 param2 param3
```
```

参数 *param1*、*param2* 等是可选的。你也可以将参数作为单个字符串传递，例如 `$@`。函数可以像解析从命令行作为命令行参数传递给 shell 程序的位置参数一样解析这些参数，只不过这里使用的是脚本内部传入的值。例如，下面的脚本使用了一个名为 `Displaymonth()` 的函数，如果传入的月份数字超出 1 到 12 的范围，它会显示月份名称或错误信息。这个示例适用于 pdksh 和 bash：

```
```sh
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
```

上述程序显示以下输出：

```
```text
Month is August
```
```

## 相关的 Ubuntu 和 Linux 命令

在使用 shell 或编写 shell 脚本时，可以使用以下命令和工具：

-   `chsh` — 用于更改登录 shell 的命令
-   `kbitz` — 允许多人共享同一个 shell 进行交互
-   `mc` — 名为 GNU Midnight Commander 的视觉化 shell
-   `nano` — 控制台上易用的文本编辑器
-   `shar` — 用于创建 shell 归档文件的命令
-   `vi` — vi（实际上是 vim）文本编辑器

## 参考

http://www.linuxgazette.com/issue70/gosh.html — Linux Gazette 上关于“Bootstrapping Linux”的文章，其中详细介绍了启动过程中的 BIOS 和 MBR 相关内容。

http://www.lostcircuits.com/advice/bios2/1.shtm — LostCircuits BIOS 指南；详细解释了所有 BIOS 设置的含义。

http://www.rojakpot.com/default.aspx?location=1 — BIOS 优化指南；详细介绍如何随心所欲地调整 BIOS 设置。

http://www-106.ibm.com/developerworks/linux/library/l-slack.html — 通过 IBM 网站链接到一篇关于启动 Slackware Linux 的文章，旁边还有关于 System V 与 BSD init 脚本历史的补充说明。

`/usr/src/linux/init/main.c` — 了解 Linux 启动过程的最佳去处。读起来确实引人入胜。从源码中获取吧！

http://sunsite.dk/linux-newbie/ — Linux 新手管理员指南的主页 —— Linux 系统管理的温和入门。

GRUB 手册——这部仍未完成的手册可以在 http://www.gnu.org/software/grub/manual/ 找到。在你的 Ubuntu 系统上，`info grub` 会提供大量信息，并且可以在 `/usr/doc/grub` 中找到示例 `grub.conf` 文件（`/boot/grub/menu.lst` 是指向 `/boot/grub/grub.conf` 的符号链接；两个名称都可以使用）。

“LILO 用户指南”—— Werner Almesberger 撰写的关于 Linux Loader（即 LILO）及其在 Intel 架构 PC 上工作原理的权威技术著作。请在 `/usr/share/doc/lilo*/doc` 目录下查找 `User_Guide.ps` 文件，可使用 `gv` 客户端查看。LILO 已被 Ubuntu 弃用；GRUB 现在是该发行版支持的默认引导加载程序。

“Grub, Glorious Grub”—— Hoyt Duff，*Linux Format*，2001 年 8 月；第 58–61 页。一篇关于 GRUB 引导加载程序的教程。

http://www.linuxbase.org/spec/refspecs/LSB_1.0.0/gLSB/sysinit.html — Linux 标准库对系统初始化的描述；这是标准文档。
