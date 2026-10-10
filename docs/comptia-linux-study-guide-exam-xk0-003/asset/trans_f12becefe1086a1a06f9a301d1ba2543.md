
5. 在修改服务器配置文件后，为什么在 SysV 启动脚本中你可能使用 `reload` 而不是 `restart` 作为参数？

- A. `reload` 选项重新加载单个服务器，而 `restart` 选项会导致 Linux 关闭并重启。
- B. 对于某些服务器，`reload` 使服务器在不关闭的情况下重新加载配置文件，而 `restart` 则完全关闭并重启服务器，这可能会断开用户连接。
- C. `reload` 选项使用现有的文件句柄重新读取配置文件，而 `restart` 创建新的文件句柄，增加了磁盘上文件损坏的风险。
- D. 对于某些服务器，`reload` 工作更可靠，因为它对配置的更改比 `restart` 更完整。

6. 一名新的 Linux 系统管理员编辑了 `/etc/inetd.conf` 以添加一个服务器。进行此更改后，管理员测试了新服务器，但远程系统无法访问该新服务器。原因可能是什么？（选择所有适用项。）

- A. 管理员可能忘记重启 `inetd`。
- B. 系统可能正在使用 `xinetd` 而不是 `inetd`。
- C. 管理员可能忘记编辑新服务器的 `/etc/rc.d/init.d` 脚本。
- D. 管理员可能忘记第一次手动启动新服务器。

7. 某个服务器/计算机组合同时出现在 `hosts.allow` 和 `hosts.deny` 中。当 TCP Wrappers 运行时，这种配置的结果是什么？

- A. TCP Wrappers 拒绝运行并在 `/var/log/messages` 中记录错误。
- B. 系统管理员会被呼叫以决定是否允许访问。
- C. `hosts.deny` 优先；客户端被拒绝访问服务器。
- D. `hosts.allow` 优先；客户端被授予访问服务器的权限。

8. 什么时候 `xinetd` 的 `bind` 选项最有用？

- A. 当你想在同一个端口上运行两个服务器时
- B. 当你想通过名称而不是 IP 地址指定计算机时
- C. 当 `xinetd` 运行在具有两个网络接口的系统上时
- D. 当解决不同服务器之间的冲突时

9. 若要更改 Linux 系统的默认运行级别，你会怎么做？

- A. 发出 `telinit x` 命令，其中 x 是所需的运行级别。
- B. 编辑 `/etc/modules.conf`，并将运行级别作为 `runlevel` 模块的选项输入。
- C. 发出 `telinit 0` 命令，让系统询问你新的运行级别。
- D. 编辑 `/etc/inittab`，并在 `initdefault` 行中输入正确的运行级别。

10. 以下哪个命令将正在运行的系统切换到运行级别 3？

- A. telnet 3
- B. runlevel 3
- C. telinit 3
- D. switch-runlevel 3

11. 以下命令由系统管理员在中午输入，它会完成什么操作？
`# shutdown -r 01:00 "Up again soon."`

- A. 在下午 1:00（一小时后）重启计算机，并显示消息 "Up again soon" 作为对用户的警告
- B. 在下午 1:00（一小时后）关闭（停止）计算机，并显示消息 "Up again soon" 作为对用户的警告
- C. 在凌晨 1:00（13小时后）关闭（停止）计算机，并显示消息 "Up again soon" 作为对用户的警告
- D. 在凌晨 1:00（13小时后）重启计算机，并显示消息 "Up again soon" 作为对用户的警告

12. 在标准的 Red Hat 系统上，运行级别 3 和 5 之间的区别是什么？

- A. 运行级别 3 不启动 X，但运行级别 5 会启动。
- B. 运行级别 3 不启动 SysV 初始化脚本，但运行级别 5 会启动。
- C. 运行级别 3 启动单用户模式，而运行级别 5 是多用户模式。
- D. 以上所有。

13. 你想在 Ubuntu 系统上关闭 X，因此你进入运行级别 3；然而，X 没有关闭。为什么？

- A. 你的 X 服务器配置错误，导致它在所有运行级别中运行。
- B. Ubuntu 不使用运行级别来控制 X 的运行时间。
- C. 你还必须输入 stopx 来停止 X。
- D. 在 Ubuntu 上，你必须进入运行级别 4 才能关闭 X。

14. 以下哪个系统日志代码代表最高优先级？

- A. emerg
- B. warning
- C. crit
- D. debug

15. 指定一台保护完善的计算机来记录多台其他计算机的日志文件有哪些优势？

- A. 以这种方式记录日志信息可以最小化网络使用。
- B. 日志系统可以使用 Tripwire 分析日志。
- C. 存储在单独计算机上的日志被入侵者破坏的可能性较小。
- D. 你可以将信息记录到一台单独的计算机上，而该信息无法在本地记录。

16. 为什么 Logcheck 这样的日志文件分析工具很有用？

- A. Logcheck 将日志文件条目从晦涩的注释翻译成英文。
- B. Logcheck 筛选大型日志文件并提醒你最令人怀疑的条目。
- C. Logcheck 比较几天或几周的活动模式并发现异常。
- D. Logcheck 使用日志文件中的信息帮助识别黑客。

17. `logrotate` 程序会查阅以下哪个配置文件来获取其设置？

- A. `/etc/logrotate.conf`
- B. `/usr/sbin/logrotate/logrotate.conf`
- C. `/usr/src/logrotate/logrotate.conf`
- D. `/etc/logrotate/.conf`

18. 你的经理要求你配置 `logrotate` 以定期无人值守的方式运行。你应该配置什么实用工具/功能来实现这一点？

- A. at
- B. `logrotate.d`
- C. cron
- D. `inittab`

19. 以下哪个命令会将文件 animals.txt 中所有出现的 dog 在屏幕显示中更改为 mutt？

- A. `sed -s "dog" "mutt" animals.txt`
- B. `grep -s "dog|mutt" animals.txt`
- C. `sed 's/dog/mutt/' animals.txt`
- D. `cat animals.txt | grep -c "dog" "mutt"`

20. 以下哪一项是 xinetd 相对于 inetd 的优势？

- A. xinetd 可以控制 SysV 启动脚本；inetd 不能这样做。
- B. xinetd 比 inetd 包含更多内置的安全功能。
- C. xinetd 提供更简洁的每服务器一行的配置文件格式。
- D. xinetd 启动 X；使用 inetd 的系统必须单独启动 X。

## 复习题答案

- 1. C. 超级服务器监听网络连接并根据连接尝试启动网络服务器。它们对于启动其他服务器很有用，但描述的程序不是服务器，因此通常不会以这种方式启动，所以选项 C 是正确的。选项 A 是启动该程序进行测试或偶尔使用的合理方式，尽管如果你希望始终使用该程序，这样会很麻烦。选项 B 和 D 都是在常规和自动基础上启动所描述程序的完全合理的方式。
- 2. A. 没有标准的 `sysvstop` 命令，因此选项 B 和 C 不可能是正确的。选项 D 使用了一个非标准的参数 (`stop5m`)，因此它不会停止服务器。选项 A 停止服务器，该服务器可以稍后手动重新启动，或者如果已配置为自动重启，则在系统重启时自动重启。
- 3. D. 使用 `kill 11` 杀死服务器将停止正在运行的服务器。本地启动脚本不接受像 SysV 启动脚本那样使用的 `start` 和 `stop` 参数。即使编辑启动脚本以删除对目标服务器的引用，重新运行启动脚本也不会杀死正在运行的进程。`inetd` 是一个超级服务器，由于相关服务器不是从超级服务器运行的，重启 `inetd` 不会杀死目标服务器。
- 4. D. `chkconfig` 实用工具存在于 Red Hat、Fedora 和其他几个发行版中，可用于修改由 SysV 启动脚本启动的服务。选项 D 提供了在运行级别 5 中启动 `vitald` 服务的正确语法。选项 A 不正确，因为 `xinetd` 是一个超级服务器；它不管理 SysV 启动脚本。选项 B 不正确，因为 `init` 程序是内核运行的第一个程序。虽然可以随后调用它来更改运行级别，但 `init` 不会启动或停止单独的 SysV 服务。选项 C 不正确，因为 `rc-update` 是 Gentoo 特有的用于管理系统服务的工具，但问题指定了 Fedora 系统。（在 Gentoo 系统中，输入 `rc-update add vitald default` 会产生所需的效果。）
- 5. B. 当两个选项都实现时，选项 B 正确总结了这两个选项之间的区别。（一些 SysV 启动脚本缺少 `reload` 选项。）选项 A 不正确，因为没有标准的 SysV 启动脚本会导致系统重启。选项 C 完全是虚构的。选项 D 如果有的话是反过来的；对于某些服务器，`restart` 比 `reload` 更有可能起作用。
- 6. A, B. 编辑 `/etc/inetd.conf` 后，应该重启 `inetd`，通常通过输入 `/etc/rc.d/init.d/inetd restart` 或类似命令。未使用的 `/etc/inetd.conf` 文件有时可能会引诱习惯配置此文件的管理员去编辑它，而不是配置在运行此替代超级服务器的系统上的 `xinetd`。在此场景中，运行或编辑目标服务器的启动脚本是不必要的，因为服务器是从超级服务器启动的；它不是直接运行的。
- 7. D. 当服务器/计算机组合同时出现在 `hosts.allow` 和 `hosts.deny` 中时，TCP Wrappers 偏向于 `hosts.allow`。TCP Wrappers 使用此功能允许你通过向 `hosts.allow` 添加更具体的显式访问权限来覆盖广泛的拒绝，例如在 `hosts.deny` 中设置默认拒绝策略 (`ALL : ALL`) 时。选项 A 和 B 都是错误的；TCP Wrappers 不会做其中任何一件事。选项 C 是反过来的。

