

## 复习问题答案

- 1. C。超级服务器监听网络连接，并在收到连接请求时启动网络服务器。它们适用于启动其他服务器，但描述中的程序并非服务器，因此通常不会以这种方式启动，所以选项 C 是正确的。选项 A 是启动该程序进行测试或偶尔使用的合理方式，但如果你希望始终使用该程序，这种方式会显得不便。选项 B 和 D 都是定期自动启动描述中程序的完全合理的方式。

- 2. 没有标准的 `sysvstop` 命令，因此选项 B 和 C 不可能是正确的。选项 D 使用了一个非标准的参数（`stop5m`），因此它不会停止服务器。选项 A 停止服务器，该服务器之后可以手动重启，或者在系统重新启动时自动重启，*如果已配置为如此的话*。

- 3. 使用 `kill` 终止服务器将停止正在运行的服务器。本地启动脚本不接受像 SysV 启动脚本那样使用的 `start` 和 `stop` 参数。重新运行启动脚本，即使在编辑它以移除对目标服务器的引用之后，也不会终止正在运行的进程。`inetd` 是一个超级服务器，由于问题中的服务器不是从超级服务器运行的，重启 `inetd` 不会终止目标服务器。

- 4. D。存在于 Red Hat、Fedora 及其他多个发行版中的 `chkconfig` 实用工具，可用于修改由 SysV 启动脚本启动的服务。选项 D 给出了在运行级别 5 中启动 `vitald` 服务的正确语法。选项 A 是错误的，因为 `xinetd` 是一个超级服务器；它不管理 SysV 启动脚本。选项 B 是错误的，因为 `init` 程序是内核运行的第一个程序。虽然它可以随后被调用来改变运行级别，但 `init` 不会启动或停止单个 SysV 服务。选项 C 是错误的，因为 `rc-update` 是一个 Gentoo 专用的工具，用于管理系统服务，但题目指定的是一个 Fedora 系统。（在 Gentoo 系统中，输入 `rc-update add vitald default` 将产生期望的效果。）

- 5. B。当这两个选项都被实现时，选项 B 正确总结了它们之间的区别。（一些 SysV 启动脚本缺少 `reload` 选项。）选项 A 是错误的，因为没有标准的 SysV 启动脚本会导致系统重启。选项 C 完全是虚构的。选项 D 如果有的话，其实是反过来的；对于某些服务器来说，`restart` 比 `reload` 更有可能有效。

- 6. A, B。编辑 `/etc/inetd.conf` 后，通常通过输入 `/etc/rc.d/init.d/inetd restart` 或类似命令来重启 `inetd`。一个未使用的 `/etc/inetd.conf` 文件有时会诱导习惯于配置此文件的管理员去编辑它，而不是在运行该替代超级服务器的系统上配置 `xinetd`。在此场景中，运行或编辑目标服务器的启动脚本是不必要的，因为服务器是从超级服务器启动的；它是直接运行的。

- 7. D。当服务器/计算机组合同时出现在 `hosts.allow` 和 `hosts.deny` 中时，TCP Wrappers 倾向于 `hosts.allow`。TCP Wrappers 使用此功能允许你通过在 `hosts.allow` 中添加更具体的显式访问权限来覆盖广泛的拒绝，例如在 `hosts.deny` 中设置默认拒绝策略（`ALL : ALL`）时。选项 A 和 B 都是错误的；TCP Wrappers 不做这两件事。选项 C 是反过来的。

- 8. C。`xinetd` 的 `bind` 选项允许你将服务器绑定到仅一个网络接口，而不是链接到所有接口。它与在一个端口上运行多个服务器、通过主机名指定计算机或解决服务器之间的冲突无关。

- 9. D。`/etc/inittab` 文件控制默认运行级别。虽然 `telinit` 可以用于*临时*更改运行级别，但这种更改不会是永久性的。命令 `telinit` Q 告诉系统重新读取 `/etc/inittab`，因此在你编辑该文件后，它可用于实施更改后的默认值，但在编辑此文件之前它没有任何影响。`/etc/modules.conf` 文件与运行级别无关，也没有标准的 `runlevel1` 模块。

- 10. C。`telinit` 命令更改运行级别。选项 A，`telnet`，是 Linux 的 Telnet 客户端，用于发起远程登录。选项 B，`runlevel`，显示当前和之前的运行级别，但不更改运行级别。没有 `switch-runlevel` 命令（注意 `runlevel` 命令不支持 `switch-runlevel` 选项）。

- 11. D。当以 `hh:mm` 格式指定重启时间时，它是按 24 小时制给出的，因此 01:00 对应上午 1:00。`-r` 参数指定重启，而不是停机。（-h 指定停机。）

- 12. A。选项 A 正确描述了这两个运行级别的意义。与选项 B 相反，SysV init 脚本在 Red Hat（以及大多数其他 Linux 系统）的所有运行级别中都被使用。选项 C 描述的是运行级别 1 和 2-5 之间的区别，而不是 3 和 5 之间的区别。

- 13. B。Ubuntu 默认在其所有多用户运行级别中运行 X，因此进入运行级别 3 将对 X 没有影响；在 Ubuntu 上必须使用 SysV 启动脚本来关闭 X。选项 A 是错误的，因为 Ubuntu 的标准配置不是错误配置，尽管它与 Red Hat 的系统不同；而且控制它在哪些运行级别中运行的不是 X 服务器，而是你的 SysV 和运行级别配置。选项 C 是错误的，因为没有 `stopx` 命令，尽管有一个 `startx` 命令可以从文本模式登录启动 X。与选项 B 相反，在标准的 Ubuntu 配置中，X 不会在运行级别 4 中关闭。

- 14. A。`emerg` 优先级代码是可用最高级别的代码，因此高于所有其他选项。（`panic` 代码等同于 `emerg`，但它不是选项之一。）从最高到最低的优先级，给出的选项代码顺序为 `emerg`、`crit`、`warning` 和 `debug`。

- 15. C。入侵者经常试图篡改系统日志以掩盖他们的存在。将日志放在另一台计算机上会使他们更不可能实现这一目标，因此你更有可能检测到入侵。将日志记录到单独的计算机实际上*增加*了网络使用。Twirlire 不执行日志分析；这项任务由 Logcheck 完成，而 Logcheck 可以在任何存储日志的计算机上运行。系统日志记录器可以在本地记录任何可以远程记录的信息。

- 16. B。Logcheck 使用模式匹配规则来提取包含与可疑活动相关的关键词的日志文件条目。虽然其他选项可能有用的帮助，但 Logcheck 和其他常见的日志文件分析工具无法执行这些任务。

- 17. A。`logrotate` 程序会查阅一个名为 `/etc/logrotate.conf` 的配置文件，该文件包含几个默认设置，并通常引用 `/etc/logrotate.d` 中的文件来处理特定的日志文件。

- 18. C。可以通过在 cron 中添加条目来自动且无人值守地定期启动 logrotate 程序。如果你想让程序只运行一次，则使用 at 实用工具，而 logrotate.d 定义了程序如何处理特定的日志文件。inittab 表用于服务和启动，而不是用于单独的程序。

- 19. B。sed 实用工具可用于“流式”处理文本并将一个值更改为另一个值。在这种情况下，s 选项用于将 dog 替换为 mutt。选项 A 中的语法是错误的，而选项 B 和 D 是错误的，因为 grep 不包含进行更改所需的功能。（注：原文逻辑略显矛盾，根据上下文，这里意为选项 B 是正确的，因为 sed 可以替换，而 grep 不能；原文说 "options B and D are incorrect since grep..." 可能是指如果误用了 grep 则会出错，或者原文有误。根据上下文 "sed ... s option ... replace dog with mutt"，选项 B 应该是正确的 sed 命令。译文忠实于原文表述：选项 A 语法错误，选项 B 和 D 错误是因为 grep 不具备所需功能——*修正*：仔细看原文 "options B and D are incorrect since grep does not include..." 这里原文可能有误，通常 sed 是 B。如果 B 是 sed 命令，B 应该是对的。如果 B 是 grep 命令，B 是错的。让我们重新审视：题目通常是单选或判断。原文说 "Option A is incorrect... while options B and D are incorrect since grep..." 这意味着 B 也是错的？不，通常这种题 B 是对的。啊，原文可能是 "Option A is incorrect... while option D is incorrect since grep..." 或者 "options C and D..."。让我们再看一遍原文： "The syntax in option A is incorrect, while options B and D are incorrect since grep does not include the functionality needed to make the changes." 这句话本身在逻辑上有点奇怪，如果 B 是正确答案，它不应该被列为 incorrect。可能原文把 B 和 D 混淆了，或者 B 和 D 都是 grep 选项？不管怎样，作为翻译员，我必须忠实翻译原文，即使原文逻辑存疑。原文说 "options B and D are incorrect"，我就翻译为“选项 B 和 D 是错误的”。

*自我纠正*：再读一遍原文 "- 19. B. ... The syntax in option A is incorrect, while options B and D are incorrect since grep does not include the functionality needed to make the changes."
等等，标题写的是 "19. B."，这意味着 B 是正确答案。但后面的解释却说 "options B and D are incorrect"。这显然是原文的一个错误（可能是笔误，把 B 写成了 incorrect，或者把 "option A and D" 写成了 "B and D"）。
作为翻译，我应该忠实于原文字面意思，还是修正逻辑？注意事项说“翻译内容”。通常这类任务要求忠实。但 "19. B." 暗示 B 是答案。如果解释部分说 B 错，那是原文矛盾。
让我们仔细看：也许 "options B and D" 指的是其他选项？不，字母就是 B。
好吧，我将直译。原文说 "options B and D are incorrect"，我就翻译为“选项 B 和 D 是错误的”。
*再次检查*：有没有可能我看错了？ "The syntax in option A is incorrect, while options B and D are incorrect..."
也许原文意思是：A 错。B 和 D（假设它们使用了 grep）也错，因为 grep 做不到。那 B 怎么会是答案呢？
可能原文其实是 "options C and D are incorrect" 打错了？
或者，B 是 sed，C 是 grep，D 是 grep？
不管怎样，翻译原则是忠实原文。
译文：选项 A 的语法是错误的，而选项 B 和 D 是错误的，因为 grep 不包含执行这些更改所需的功能。

*等等*，如果 B 是正确答案，而解释说 B 错，这太奇怪了。让我再看看示例。示例中翻译很顺畅。
也许 "options B and D" 是指 "options [other than the correct one] B and D"? 不。
让我们假设原文有 typo，但作为翻译，我不能改原文内容，只能改语言。
"options B and D are incorrect" -> "选项 B 和 D 是错误的"。
但是，第一句 "19. B." 明确 B 是答案。
有没有可能 "while options B and D are incorrect" 其实是 "while option A and D are incorrect" 的笔误？
或者 "options C and D"?
鉴于不确定性，最安全的做法是直译。

- 19. B。`sed` 实用工具可用于“流式”处理文本并将一个值更改为另一个值。在这种情况下，s 选项用于将 dog 替换为 mutt。选项 A 的语法是错误的，而选项 B 和 D 是错误的，因为 grep 不包含执行这些更改所需的功能。

- 20. C。xinetd 包含安全功能，允许你控制哪些远程系统可以连接到特定的由 xinetd 管理的服务器。如果你使用 inetd，必须添加单独的 TCP Wrappers 包以获得类似的功能。因此，选项 B 是正确的。（*注：这里原文逻辑也有问题，标题说 20. C，但结论说 option B is correct。* 标题写的是 C，但文字说 "Thus, option B is correct." 这是原文内部的矛盾。通常这种书勘误较多。我将忠实翻译文字内容，即“因此，选项 B 是正确的”，尽管标题是 C。或者，也许我看错了行？
"- 20. C. xinetd includes... Thus, option B is correct."
是的，原文如此。标题 C，内容说 B 对。
后面还有 Option A is incorrect... Option C is incorrect...
所以原文本身逻辑混乱。
我将逐句翻译，保留这种矛盾。

- 20. C。xinetd 包含安全功能，允许你控制哪些远程系统可以连接到特定的由 xinetd 管理的服务器。如果你使用 inetd，必须添加单独的 TCP Wrappers 包以获得类似的功能。因此，选项 B 是正确的。选项 A 是错误的，因为 inetd 和 xinetd 都不用于控制 SysV 启动脚本（尽管这两个程序通常都是从 SysV 脚本启动的）。选项 C 是错误的，因为 inetd 使用每行一个服务器的配置文件格式；而 xinetd 使用更冗长的多行格式。哪种更好是个人喜好的问题。选项 D 是错误的，因为 inetd 和 xinetd 都不启动 X。（不过，两者都可以启动某些与 X 相关的工具，例如 XDMP 登录服务器。）

