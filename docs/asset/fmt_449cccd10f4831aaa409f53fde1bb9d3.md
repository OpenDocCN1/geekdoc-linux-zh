
- A. `/etc/init.d/proftpd stop`

- B. `sysvstop /etc/init.d/proftpd`

- C. `sysvstop proftpd`

- D. `/etc/init.d/proftpd stop`

3. 你通过编译源代码安装了一个服务器。源代码中不包含 SysV 启动脚本，而你又不想通过超级服务器运行它，所以你在本地启动脚本（`/etc/rc.d/rc.local`）中启动了它。你需要暂时关闭该服务器。你应该怎么做？

- A. 输入 `/etc/rc.d/rc.local stop`。

- B. 编辑启动脚本以移除该服务器，并重新运行脚本。

- C. 从 `/etc/inetd.conf` 中移除该服务器的条目，然后输入 `/etc/rc.d/init.d/inetd restart`。

- D. 使用 `ps` 找到该服务器的进程 ID 号（`pid`），然后输入 `kill` `pid`。

4. 你发现你的 Fedora 系统上安装了 VitalServer 软件包，但在启动计算机进入运行级别 5 时它没有自动运行。假设该软件包附带一个名为 `vitald` 的 SysV 启动脚本，为了在运行级别 5 中启用此服务器，你可能会输入什么？

- A. `xined 5 vitald add`

- B. `init vitald 5`

- C. `rc-update add vitald 5`

- D. `chkconfig --level 5 vitald on`

5. 在对服务器配置文件做出更改后，为什么可能会在 SysV 启动脚本中使用 reload 而不是 restart 作为参数？

- A. reload 选项重新加载单个服务器，而 restart 选项会导致 Linux 关闭并重新启动。

- B. 对于某些服务器，reload 导致服务器在不关闭的情况下重新加载配置文件，而 restart 则完全关闭并重新启动服务器，这可能会断开用户连接。

- C. reload 选项使用现有的文件句柄重新读取配置文件，而 restart 创建新的文件句柄，增加磁盘上文件损坏的风险。

- D. 对于某些服务器，reload 更可靠，因为它对配置进行的更改比 restart 更完整。

6. 一位新的 Linux 系统管理员编辑 `/etc/inetd.conf` 以添加一个服务器。做出此更改后，管理员测试了新服务器，但远程系统无法访问该新服务器。原因可能是什么？（选择所有适用项。）

- A. 管理员可能忘记重启 `inetd`。

- B. 系统可能使用的是 `xinetd` 而不是 `inetd`。

- C. 管理员可能忘记为新服务器编辑 `/etc/rc.d/init.d` 脚本。

- D. 管理员可能忘记首次手动启动新服务器。

7. 某个服务器/计算机组合同时出现在 `hosts.allow` 和 `hosts.deny` 中。当 TCP Wrappers 运行时，这种配置的结果是什么？

- A. TCP Wrappers 拒绝运行并在 `/var/log/messages` 中记录错误。

- B. 系统管理员会被呼叫以决定是否允许访问。

- C. `hosts.deny` 优先；客户端被拒绝访问服务器。

- D. `hosts.allow` 优先；客户端被授予访问服务器的权限。

8. 在什么情况下，`xinetd` 的 `bind` 选项最有用？

- A. 当你希望在一个端口上运行两个服务器时

- B. 当你希望按名称而不是 IP 地址指定计算机时

- C. 当 `xinetd` 运行在具有两个网络接口的系统上时

- D. 在解决不同服务器之间的冲突时

9. 要更改 Linux 系统的默认运行级别，你会怎么做？

- A. 发出 `telinit x` 命令，其中 `x` 是所需的运行级别。

- B. 编辑 `/etc/modules.conf`，并将运行级别作为运行级别模块的一个选项输入。

- C. 发出 `telinit 0` 命令，让系统询问你新的运行级别。

- D. 编辑 `/etc/inittab` 并在 `initdefault` 行中输入正确的运行级别。

10. 以下哪个命令将正在运行的系统切换到运行级别 3？

- A. `telnet 3`

- B. `runlevel 3`

- C. `telinit 3`

- D. `switch-runlevel 3`

11. 当系统管理员在中午输入以下命令时，它会实现什么功能？

```
# shutdown -r 01:00 "Up again soon."
```

- A. 在下午 1:00（一小时后）重新启动计算机，并显示信息 `Up again soon` 作为对用户的警告

- B. 在下午 1:00（一小时后）关闭（halt）计算机，并显示信息 `Up again soon` 作为对用户的警告

- C. 在凌晨 1:00（13 小时后）关闭（halt）计算机，并显示信息 `Up again soon` 作为对用户的警告

- D. 在凌晨 1:00（13 小时后）重新启动计算机，并显示信息 `Up again soon` 作为对用户的警告

12. 在标准的 Red Hat 系统上，运行级别 3 和 5 之间有什么区别？

- A. 运行级别 3 不启动 X，但运行级别 5 会启动。

- B. 运行级别 3 不启动 SysV init 脚本，但运行级别 5 会启动。

- C. 运行级别 3 启动到单用户模式，而运行级别 5 是多用户模式。

- D. 以上皆是。

13. 你想在 Ubuntu 系统上关闭 X，因此进入运行级别 3；然而，X 没有关闭。为什么？

- A. 你的 X 服务器配置错误，在所有运行级别中都会运行。

- B. Ubuntu 不使用运行级别来控制 X 何时运行。

- C. 你还必须输入 `stop` 来停止 X。

- D. 你必须在 Ubuntu 上进入运行级别 4 才能关闭 X。

14. 以下哪个系统日志代码代表最高优先级？

- A. `emerg`

- B. `warning`

- C. `crit`

- D. `debug`

15. 指定一台受良好保护的计算机来记录其他几台计算机的日志文件，有什么优势？

- A. 以这种方式记录信息可以最小化网络使用。

- B. 日志系统可以使用 `Tripwire` 分析日志。

- C. 存储在单独计算机上的日志不太容易被入侵者破坏。

- D. 你可以将信息记录到一台单独的计算机上，而本地无法记录。

16. 为什么像 Logcheck 这样的日志文件分析工具很有用？

- A. `Logcheck` 将日志文件条目从晦涩的注释翻译成通俗易懂的英文。

- B. `Logcheck` 筛选大型日志文件并提醒你那些最可疑的条目。

- C. `Logcheck` 比较几天或几周的活动模式并发现异常。

- D. `Logcheck` 使用日志文件中的信息来帮助识别黑客。

17. 以下哪个配置文件是 `logrotate` 程序咨询其设置的来源？

- A. `/etc/logrotate.conf`

- B. `/usr/sbin/logrotate/logrotate.conf`

- C. `/usr/src/logrotate/logrotate.conf`

- D. `/etc/logrotate/.conf`

18. 你的经理要求你配置 `logrotate` 以便在无人值守的情况下定期运行。你应该配置什么实用程序/功能来实现这一点？

- A. `at`

- B. `logrotate.d`

- C. `cron`

- D. `inittab`

19. 以下哪个命令将文件 `animals.txt` 中所有的 `dog` 更改为 `mutt` 并在屏幕显示中输出？

- A. `sed -s "dog" "mutt" animals.txt`

- B. `grep -s "dog||mutt" animals.txt`

- C. `sed 's/dog/mutt/' animals.txt`

- D. `cat animals.txt | grep -c "dog" "mutt"`

20. 以下哪项是 `xinetd` 相对于 `inetd` 的优势？

- A. `xinetd` 可以控制 SysV 启动脚本；`inetd` 不能这样做。

- B. `xinetd` 包含比 `inetd` 更多的内置安全功能。

- C. `xinetd` 提供更简洁的每行一个服务器的配置文件格式。

- D. `xinetd` 启动 X；使用 `inetd` 的系统必须单独启动 X。

## 复习问题答案

1. C。超级服务器监听网络连接，并在收到连接请求时启动网络服务器。它们适用于启动其他服务器，但描述中的程序并非服务器，因此通常不会以这种方式启动，所以选项 C 是正确的。选项 A 是启动该程序进行测试或偶尔使用的合理方式，但如果你希望始终使用该程序，这种方式会显得不便。选项 B 和 D 都是定期自动启动描述中程序的完全合理的方式。

2. 没有标准的 `sysvstop` 命令，因此选项 B 和 C 不可能是正确的。选项 D 使用了一个非标准的参数（`stop5m`），因此它不会停止服务器。选项 A 停止服务器，该服务器之后可以手动重启，或者在系统重新启动时自动重启，如果已配置为如此的话。

3. 使用 `kill` 终止服务器将停止正在运行的服务器。本地启动脚本不接受像 SysV 启动脚本那样使用的 `start` 和 `stop` 参数。重新运行启动脚本，即使在编辑它以移除对目标服务器的引用之后，也不会终止正在运行的进程。`inetd` 是一个超级服务器，由于问题中的服务器不是从超级服务器运行的，重启 `inetd` 不会终止目标服务器。

4. D。存在于 Red Hat、Fedora 及其他多个发行版中的 `chkconfig` 实用工具，可用于修改由 SysV 启动脚本启动的服务。选项 D 给出了在运行级别 5 中启动 `vitald` 服务的正确语法。选项 A 是错误的，因为 `xinetd` 是一个超级服务器；它不管理 SysV 启动脚本。选项 B 是错误的，因为 `init` 程序是内核运行的第一个程序。虽然它可以随后被调用来改变运行级别，但 `init` 不会启动或停止单个 SysV 服务。选项 C 是错误的，因为 `rc-update` 是一个 Gentoo 专用的工具，用于管理系统服务，但题目指定的是一个 Fedora 系统。（在 Gentoo 系统中，输入 `rc-update add vitald default` 将产生期望的效果。）

5. B。当这两个选项都被实现时，选项 B 正确总结了它们之间的区别。（一些 SysV 启动脚本缺少 `reload` 选项。）选项 A 是错误的，因为没有标准的 SysV 启动脚本会导致系统重启。选项 C 完全是虚构的。选项 D 如果有的话，其实是反过来的；对于某些服务器来说，`restart` 比 `reload` 更有可能有效。

6. A, B。编辑 `/etc/inetd.conf` 后，通常通过输入 `/etc/rc.d/init.d/inetd restart` 或类似命令来重启 `inetd`。一个未使用的 `/etc/inetd.conf` 文件有时会诱导习惯于配置此文件的管理员去编辑它，而不是在运行该替代超级服务器的系统上配置 `xinetd`。在此场景中，运行或编辑目标服务器的启动脚本是不必要的，因为服务器是从超级服务器启动的；它是直接运行的。

7. D。当服务器/计算机组合同时出现在 `hosts.allow` 和 `hosts.deny` 中时，TCP Wrappers 倾向于 `hosts.allow`。TCP Wrappers 使用此功能允许你通过在 `hosts.allow` 中添加更具体的显式访问权限来覆盖广泛的拒绝，例如在 `hosts.deny` 中设置默认拒绝策略（`ALL : ALL`）时。选项 A 和 B 都是错误的；TCP Wrappers 不做这两件事。选项 C 是反过来的。

8. C。`xinetd` 的 `bind` 选项允许你将服务器绑定到仅一个网络接口，而不是链接到所有接口。它与在一个端口上运行多个服务器、通过主机名指定计算机或解决服务器之间的冲突无关。

9. D。`/etc/inittab` 文件控制默认运行级别。虽然 `telinit` 可以用于临时更改运行级别，但这种更改不会是永久性的。命令 `telinit` Q 告诉系统重新读取 `/etc/inittab`，因此在你编辑该文件后，它可用于实施更改后的默认值，但在编辑此文件之前它没有任何影响。`/etc/modules.conf` 文件与运行级别无关，也没有标准的 `runlevel1` 模块。

10. C。`telinit` 命令更改运行级别。选项 A，`telnet`，是 Linux 的 Telnet 客户端，用于发起远程登录。选项 B，`runlevel`，显示当前和之前的运行级别，但不更改运行级别。没有 `switch-runlevel` 命令（注意 `runlevel` 命令不支持 `switch-runlevel` 选项）。

11. D。当以 `hh:mm` 格式指定重启时间时，它是按 24 小时制给出的，因此 01:00 对应上午 1:00。`-r` 参数指定重启，而不是停机。（-h 指定停机。）

12. A。选项 A 正确描述了这两个运行级别的意义。与选项 B 相反，SysV init 脚本在 Red Hat（以及大多数其他 Linux 系统）的所有运行级别中都被使用。选项 C 描述的是运行级别 1 和 2-5 之间的区别，而不是 3 和 5 之间的区别。

13. B。Ubuntu 默认在其所有多用户运行级别中运行 X，因此进入运行级别 3 将对 X 没有影响；在 Ubuntu 上必须使用 SysV 启动脚本来关闭 X。选项 A 是错误的，因为 Ubuntu 的标准配置不是错误配置，尽管它与 Red Hat 的系统不同；而且控制它在哪些运行级别中运行的不是 X 服务器，而是你的 SysV 和运行级别配置。选项 C 是错误的，因为没有 `stopx` 命令，尽管有一个 `startx` 命令可以从文本模式登录启动 X。与选项 B 相反，在标准的 Ubuntu 配置中，X 不会在运行级别 4 中关闭。

14. A。`emerg` 优先级代码是可用最高级别的代码，因此高于所有其他选项。（`panic` 代码等同于 `emerg`，但它不是选项之一。）从最高到最低的优先级，给出的选项代码顺序为 `emerg`、`crit`、`warning` 和 `debug`。

15. C。入侵者经常试图篡改系统日志以掩盖他们的存在。将日志放在另一台计算机上会使他们更不可能实现这一目标，因此你更有可能检测到入侵。将日志记录到单独的计算机实际上增加了网络使用。`Tripwire` 不执行日志分析；这项任务由 `Logcheck` 完成，而 `Logcheck` 可以在任何存储日志的计算机上运行。系统日志记录器可以在本地记录任何可以远程记录的信息。

16. B。`Logcheck` 使用模式匹配规则来提取包含与可疑活动相关的关键词的日志文件条目。虽然其他选项可能有用的帮助，但 `Logcheck` 和其他常见的日志文件分析工具无法执行这些任务。

17. A。`logrotate` 程序会查阅一个名为 `/etc/logrotate.conf` 的配置文件，该文件包含几个默认设置，并通常引用 `/etc/logrotate.d` 中的文件来处理特定的日志文件。

18. C。可以通过在 `cron` 中添加条目来自动且无人值守地定期启动 `logrotate` 程序。如果你想让程序只运行一次，则使用 `at` 实用工具，而 `logrotate.d` 定义了程序如何处理特定的日志文件。`inittab` 表用于服务和启动，而不是用于单独的程序。
