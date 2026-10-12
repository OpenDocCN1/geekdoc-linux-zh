
David Laight 补充道：担心 Rust 可能会增加更多测试。我们只需要确保构建时间并使用大量的内存。

在**不遥的未来**。`Linus` 的担忧一点也不严重，基本上是不同类型的担忧。他注意到，人们要么支持添加 Rust，要么有可以随时间推移而解决的担忧。而 `Josh` 和他的团队愿意适应我“‘如果编译器变了，我需要进行完整测试——以防万一它编译了……Linux 发行版倾向于总是 htat Linux 依赖于 Rust，Firefox 依赖于 Rust，这意味着某些‘可疑’的代码处理方式不同。……与最近版本的 Rust 一起发布。如果这意味着内核也将依赖 Rust 语言本身来满足……内核的需求。与此同时，`Adrian Bunk` 有一个 con- 此同时，`Arnd Bergmann` 推测了一个不断更新的版本“‘虽然 Linux 过去使用 12 年前的……构建。可能也没有坏处。Q Q Q

`LINUX-MAGAZINE.COM` | `LINUXPROMAGAZINE.COM`

第 241 期

2020年12月

13

![](img/56e7a0f7bfb6321f705dd064cbb9793e_77_0.png)

![](img/56e7a0f7bfb6321f705dd064cbb9793e_77_1.png)

![](img/56e7a0f7bfb6321f705dd064cbb9793e_77_2.png)

![](img/56e7a0f7bfb6321f705dd064cbb9793e_77_3.png)

**良好的声誉并保护你的 Linux 系统免受攻击。我们将为你展示一些检测和防御入侵者的技巧。**

作者：`Charly Kühn`

对于任何面对互联网的计算机来说，安全都是问题，而解决方案可以根据你的需要变得尽可能大且全面。防火墙、渗透测试和入侵防御系统（IPS）都是重要的，但在开始添加这些关键安全层之前，你就可以为保护系统做很多工作。本文强调了一些非常简单以至于经常被忽视的基础安全步骤。

如果你正在管理一个可以从头安装的 Linux 系统，请记住，系统上的服务越少意味着攻击途径越少，因此一种值得的方法是忽略所有你并不需要的东西。许多发行版提供了专门设计的精简版版本，以减少攻击面。然后你可以设置一个微型 Linux 并仅导入你真正需要的包。

系统运行后，请保持其最新状态。特别是安全更新，需要每天检查并立即安装。许多发行版都有安装安全更新的自动化过程。例如，在 Debian 和 Ubuntu 上，术语是“无人升级（unattended upgrades）[1]

除了安装更新和只使用你需要的服务等老生常谈之外，一些额外的操作确实可以帮助减少你的受攻击风险。继续读下了解你现在可以采取的一些简单步骤。

`root` 账户属于最高权限的用户，其密码对于攻击者来说是一个极具价值的目标。一些现代 Linux 替代方案（如 Ubuntu）默认禁用 `root` 登录，但其他 Linux 发行版仍允许它。如果系统可以通过互联网通过 SSH 访问，你将会发现列表 1：`/var/log/auth.log`

01

```
$ egrep -i fail /var/log/auth.log
```

02

[...]

03

`Jul 16 13:28:47 ubuntu sshd[21717]: pam_unix(sshd:auth): authentication failure; gnome= uid=0 euid=0`

04

`tty=sshA= rhost=222.186.180.223 user=root` 05

`Jul 16 13:28:48 ubuntu sshd[21717]: Failed password for root from 222.186.180.223 port 4141 ssh2`

06

```
$ journalctl _SYSTEMD_UNIT=sshd.service | egrep -i fail 07
```

[...]

`Jul 24 13:02:18 ontario sshd[10311]: pam_unix(sshd:auth): authentication failure; gnome= uid=0`

09

`eid=0 tty=ssh ruser= rhost=222.186.180.223 user=root` 10

`Jul 24 13:02:20 ontario sshd[10311]: Failed password for root from 222.186.180.223 port 48972 ssh2`

![](img/56e7a0f7bfb6321f705dd064cbb9793e_81.png)

| 位置 | 描述 |
| :--- | :--- |
| `inet` | `222.184.0.0` |
| `name` | 江苏-江苏省 |
| `descr` | 中国 |
| `descr` | 电信 |
| `descr` | 北京 |
| `inet` | `222.191.255.255` |
| `country` | CN |
| `inet` | `222.186.180.223` |
| `country` | AI |
| `inet` | `222.186.180.223` | 江苏 |
| `inet` | `222.186.180.223` | 1000 |
| `inet` | `222.186.180.223` | |
| `inet` | `222.186.180.223` | | |
| `inet` | `222.186.180.223` | | |
| `descr` | `222.186.180.223` | | |
| `descr` | `222.186.180.223` | | |
| `descr` | `222.186.180.223` | | |
| `descr` | `222.186.180.223` | | |
| `descr` | `222.186.180.223` | | |

使用 `usermod -a -G sudo bob` 命令。（请检查您发行版的文档：Ubuntu 以及其他某些发行版会自动将安装时创建的第一个用户账户添加到 Sudo 组。）

要测试一切是否工作正常，请注销并重新以 `bob` 的身份登录。然后执行以下命令：

`sudo ls /root`
