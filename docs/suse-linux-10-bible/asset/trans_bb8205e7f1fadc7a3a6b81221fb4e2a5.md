

# 第 14 章 ◆ 使用系统 407

## Perl 版本
为了在 Perl 中实现我们的目标，我们编写以下脚本：

```perl
#! /usr/bin/perl
use Date::Calc::Object qw(:all);
Date::Calc->date_format(2);
open (LOG, "access.log");
while (<LOG>) {
    @bits = split(/\s+/,);
    if ($bits[2]==="192.168.2.4") {
        $date = Date::Calc->gettime(@bits[0]);
        print $date, ",", @bits[6];
        print "\n";
    }
}
```

在这里我们定义解释器为 Perl。以 `use` 开头的行导入了格式化日期所需的适当模块，接下来的行指定了日期的特定格式以及将打印的字符串。我们随后创建一个文件句柄 `(LOG)`，`while` 语句遍历文件的每一行。下一行通过空白符分割行，再次，如果第三个元素匹配所需的地址，我们就打印所需的信息。

输出如下：

15-Jul-2003 11:50:43
15-Jul-2003 11:50:47
15-Jul-2003 11:50:48
15-Jul-2003 11:50:48

再次，脚本使日志更具可读性，提供了我们需要的信息。

注意以下两个示例：

- 在每种情况下，我们导入了与计算和显示日期相关的模块，提供了原本不可用的函数（`from time import localtime, strftime, Date::Calc::Object qw(:all));`）。
- 在每种情况下，我们定义了一个文件句柄来读取日志（`infile = open('access.log', 'r'), open (LOG, "access.log"));`）。
- 在每种情况下，通过分割行获取的数据不需要任何特殊符号来表示其类型。在 Perl 中，我们必须使用 `@bits`（数组）和 `$date`（简单变量）。
- 在每种情况下，以 `#!` 开头的行告诉解释器使用系统。输出在时区方面有所不同。

## 注释与资源

对于我们来说，Python 更加整洁、易读且易于编写。Perl 与 shell 和 awk 共享许多约定，并以非常优雅处理正则表达式。Perl 较老，拥有更广泛的用户群和强大的自动化系统（CPAN），让你可以使用单个命令获取并安装模块。

## Python 资源

如果你对追求脚本感兴趣，请查看以下网站：

- [www.python.org](https://www.python.org)
- [www.python.org/psf/](https://www.python.org/psf/)
- [://python.org](https://python.org)

你还可以检查 `/usr/share/doc/packages/python` 目录下的可用信息。此外，你可以参考以下关于该主题的书：

- 《Python Bible》Dave Bueck 和 Stephen Tanner (Wiley, 2001)
- 《Making Use of Python》Rashi Gupta (Wiley, 2002)
- 《Python Essential Reference》David Beasley (New Riders, 2001)
- 《Learning Python》Mark Lutz 和 David Asher (O'Reilly, 2003)
- 《Programming Python》Mark Lutz (O'Reilly)

## Perl 资源

如果你想研究 Perl，请查看以下网站：

- [www.cpan.org](https://www.cpan.org)
- [www.perl.com](https://www.perl.com)
- [www.perl.org](https://www.perl.org)
- [www.perlfoundation.org](https://www.perlfoundation.org) 是一个为你的 Perl 安装添加功能的模块搜索网站。更好的是，可以通过单个命令从 CPAN 下载并安装模块，只要你知道模块名称。`/usr/share/doc/packages/perl/` 目录下也有可用信息。

你也可以使用 `perldoc` 获取更多关于 Perl 信息。例如，你可以使用 `perldoc Date::Calc` 查看示例使用的模块文档。最后，你可以找到以下书籍：

- 《Perl Dummies》Joe Hoffman (Wiley, 2003)
- 《Weekend Crash Course》Joe Merlini (Wiley, 2001)
- 《Beginning Perl》Simon Cozens 与 Peter Wainwright (Wrox Press, 2000)
- 《Learning Perl》Randal L. Schwartz 和 Tom Phoenix (O'Reilly, 2001)
- 《Programming Perl》Larry Wall, Tom Christiansen 和 Jon Want (O'Reilly, 2000)

如果本章中的某些工具对你来说是新的，请不要遗憾，只需将其作为需要时会回头的参考即可。将其视为一次游戏的邀请。设置一个无关紧要的系统并尝试一些具有潜在破坏性的工具。尝试对其造成一些破坏并修复它。当需要它来时，这种经验将是无价的。如果你没有用过 shell 脚本或脚本语言，请以这里的介绍作为起点，并利用列出的一些资源尝试一些想法。

## Linux 网络

在网络化环境中使用 Linux（无论是提供数据还是提供服务）都是该操作系统在企业市场的主要驱动力。当你安装 SUSE 时，提供了使用系统配置来配置网络的选项。在本章中，我们将深入探讨使用命令行工具配置网络。了解如何直接使用工具而不是使用 SUSE 管理工具始终是学习你的系统如何工作的最佳方法。

### 交叉引用
我们在第 1 章中讨论过配置网络。SUSE 安装后的网络配置与安装期间的网络配置完全相同。有关如何使用 YaST 工具访问网络配置的更多信息，请参见第 9 章。

此外，在本章中我们还讨论了 `ping` 和 `traceroute`，你可以它们在排查网络故障时让生活变得简单。

最后，使用有线网卡时配置网络与使用无线网卡大不同，我们在本章中讨论了这个问题。由于 Linux 对蓝牙的支持，我们讨论了它的用途以及可用于与蓝牙设备配对的应用程序。

## 配置 IP 网络

正如我们在前面的章节中所提到的，在 Linux 中有许多方法实现相同的操作。你可以通过 YaST、使用 `ifconfig`、使用 SUSE 网络配置文件以及使用 `ip` 命令来配置网络。接下来的章节将讨论如何从命令行配置你的 IP 网络。在本章的剩余部分中，你需要以 root 身份登录以完成网络。

# 第 15 章

## 本章内容

- 配置 IP 网络
- 地址解析协议
- 使用网络工具
- 排查网络
- 设置无线网络和蓝牙

### ifconfig

如果你需要查看网络配置，`ifconfig` 命令是一个简单快速的方法。作为 root，只需输入 `ifconfig` 即可显示所有端口的配置（见列表 15-1），包括物理和虚拟（我们稍后将在章节中讨论虚拟接口）。

## 列表 15-1: ifconfig 的输出

```
# ifconfig
eth0          Link enc:Ethernet HWaddr:00:03:ff:69:68:12
       inet addr:192.168.1.130 Bcast:192.168.1.255 Mask:255.255.255.0
       inet6 addr:fe80::203f:ff69:68d1/64 Scope:Link
      UP BROADCAST RUNNING MULTICAST  Metric:1 MTU:1500
  rx packets:30256 errors:0 dropped:0 overflows:0 frame:0
  tx packets:36509 errors:0 dropped:0 overflows:0 carrier:0
  collisions:0 txuellen:1000
  rx bytes:4048565 (3.8 Mb) TX bytes:34473633 (32.8 Mb)
  Interrupt:1 Base address:0x1080
lo            Link enc:Loopback
       inet addr:127.0.0.1 Mask:255.255.0.0
       inet6 addr ::/128 Scope:Host
      UP LOOPBACK MTU:16384 Metric:1
  rx packets:3162 errors:0 dropped:0 overflows:0 frame:0
  tx packets:3162 errors:0 dropped:0 overflows:0 carrier:0
  collisions:0 txuellen:0
  rx bytes:11507333 (1.0 Mb) TX bytes:11507333 (1.0 Mb)
```

表 15-1 显示了 ifconfig 输出的分解。

你可能会遇到附加网络接口上的其他标志，常见的是 `PROMIS` 标志。这意味着你的以太网适配器会监听经过其链路的所有数据包，而不是只监听目标是为你自己的站的数据包。

