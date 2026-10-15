
在此例中，我们发现了 SUID 二进制文件。SUID 二进制文件的利用利用取决于多个因素。例如，如果 `/bin/cp`（复制命令）具有 SUID 权限，我们可以复制并覆盖像 `/etc/passwd` 敏感文件。

权限提升技术的全面列表可以在 g0tm1lk 编写的汇编 848 以及其他更新的资源中找到。

在手动操作 Linux 系统权限提升并理解了这一概念后，我们将在接下来的章节中学习如何自动化这一过程。

# 17.1.3 自动化枚举

如上一节所学，Linux 系统包含了大量可用于进一步攻击的信息。然而，手动收集这些详细信息可能非常耗时。幸运的是，我们可以使用各种脚本来自动化此过程。

为了获取目标系统的初始基准，我们可以在 Linux 等 UNIX 变体系统上使用 `unix-privesc-check`。这个 bash 脚本预装在我们的本地 Kali 机器的 `/usr/bin/unix-privesc-check` 路径，它会执行许多检查以寻找任何可以被用于本地权限提升的系统配置错误。我们可以通过在不带任何参数的情况下运行脚本来查看该工具的详情。

> 848 (G0tm1lk, 2021), https://g0tm1lk.com/2011/08/basic-linux-privilege-escalation
> 849 (Swissy, 2022).
> 850 https://github.com/swissyre/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-Privileges-Escalation.md
> 851 (Carlos Polop, 2022), https://hacktricks.xyz/linux-hardening/privilege-escalation
> 852 (Pentest Monkey, 2019), http://pentestmoney.net/tools/audit/unix-privesc-check

PWK - 版权所有 2023 OffSec Services Limited. 保留所有。

# OffSec

使用 Kali Linux 进行渗透测试

```
kali@kali:~$ unix-privesc-check
```

```
unix-privesc-check v1.4 ( http://pentestmonkey.net/tools/unix-privesc-check )
```

```
用法: unix-privesc-check { standard | detailed }
```

`"standard"` 模式：对许多安全设置进行速度优化检查。

`"detailed"` 模式：与标准模式相同，但还会检查每个打开的文件和调用的文件（例如从 shell 脚本解析的、链接的 .so 文件）。此模式速度较慢且容易产生误报，但可能帮助你发现第三方程序中更微妙的缺陷。

此脚本检查文件权限和其他允许本地用户提升权限的设置。

...

如上所示，脚本支持 `"standard"` 和 `"detailed"` 模式。根据提供的信息，标准模式似乎执行了速度优化的过程，并且应该提供更少的误报。因此，在接下来的示例中，我们在目标系统上运行脚本，并使用标准模式将整个输出重定向到名为 `output.txt` 的文件中。

```
joe@debian:-$ /unix-privesc-check standard > output.txt
```

脚本会对常用文件的权限进行检查。例如，除了非 root 用户可写的配置文件外：

```
Checking for writable config files
################################################
Checking if anyone except root can change /etc/passwd
WARNING: /etc/passwd is a config file. World write is set for /etc/passwd
Checking if anyone except root can change /etc/group
Checking if anyone except root can change /etc/fstab
Checking if anyone except root can change /etc/profile
Checking if anyone except root can change /etc/sudoers
Checking if anyone except root can change /etc/shadow
```

此输出显示任何人都可以编辑 `/etc/passwd`。这是非常重要的，因为允许攻击者轻松地提升自己的权限或在目标机器上创建用户账户。我们将在模块稍后演示这一点。

还有许多值得提到的其他工具，它们专门为 Linux 权限提升收集而设计，包括 LinEnum 和 LinPeas，这些工具在近几年中得到了活跃的开发和增强。

> 852 (Raj Chandel, 2018), https://www.hackingarticles.in/editing-etc-passwd-file-for-privilege-escalation

> 853 (Rebootuser, 2022), github.com/LinEnum

> 854 (Polop, 2022), github.com/linpeas/tree/master/PEAS

PWK - 版权所有 2023 OffSec Services Limited. 保留所有。

尽管在手动操作 Linux 系统权限提升并理解了这一概念后，我们将在接下来的章节中学习如何自动化这一过程。

# 17.2 敏感信息

在本 单元中，学习目标：

- 收集用户信息
- 内核信息
- 目标（目标）
- 敏感信息

# 17.2 敏感信息

如上一节所学，Linux 系统包含了大量可用于进一步攻击的信息。然而，手动收集这些详细信息可能非常耗时。幸运的是，我们可以使用各种脚本来自动化此过程。

为了获取目标系统的初始基准，我们可以在 Linux 等 UNIX 变体系统上使用 `unix-privesc-check`。这个 bash 脚本预装在我们的本地 Kali 机器的 `/usr/bin/unix-privesc-check` 路径，它会执行许多检查以寻找任何可以被用于本地权限提升的系统配置错误。我们可以通过在不带任何参数的情况下运行脚本来查看该工具的详情。

> 848 (G0tm1lk, 2021), https://g0tm1lk.com/2011/08/basic-linux-privilege-escalation
> 849 (Swissy, 2022).
> 850 https://github.com/swissyre/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-Privileges-Escalation.md
> 851 (Carlos Polop, 2022), https://hacktricks.xyz/linux-hardening/privilege-escalation
> 852 (Pentest Monkey, 2019), http://pentestmoney.net/tools/audit/unix-privesc-check

PWK - 版权所有 2023 OffSec Services Limited. 保留所有。

# OffSec

使用 Kali Linux 进行渗透测试

```
kali@kali:~$ unix-privesc-check
unix-privesc-check v1.4 ( http://pentestmonkey.net/tools/unix-privesc-check )
```

```
用法: unix-privesc-check { standard | detailed }
```

`"standard"` 模式：对许多安全设置进行速度优化检查。

`"detailed"` 模式：与标准模式相同，但还会检查每个打开的文件和调用的文件（例如从 shell 脚本解析的、链接的 .so 文件）。此模式速度较慢且容易产生误报，但可能帮助你发现第三方程序中更微妙的缺陷。

此脚本检查文件权限和其他允许本地用户提升权限的设置。
...

如上所示，脚本支持 `"standard"` 和 `"detailed"` 模式。根据提供的信息，标准模式似乎执行了速度优化的过程，并且应该提供更少的误报。因此，在接下来的示例中，我们在目标系统上运行脚本，并使用标准模式将整个输出重定向到名为 `output.txt` 的文件中。

```
joe@debian:-$ /unix-privesc-check standard > output.txt
```

脚本会对常用文件的权限进行检查。例如，除了非 root 用户可写的配置文件外：
