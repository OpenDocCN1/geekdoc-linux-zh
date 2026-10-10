
### A. FontSection

- B. Fonts
- C. FontLoc
- D. FontPath

34. 使用哪种辅助技术为无法使用指针（如鼠标）的用户提供输入法？

- A. Keyboard（键盘）
- B. Sticky keys（粘滞）
- C. Mouse keys（鼠标键）
- D. On-screen keyboard（屏幕键盘）

35. 哪种辅助技术会忽略连续按下或按住的键？

- A. Sticky keys（粘滞）
- B. Mouse keys（鼠标键）
- C. Bounce keys（弹跳键）
- D. On-screen keyboard（屏幕键盘）

36. 使用 `LightDM` 时，使用哪个组合键返回终端？

- A. `Alt+Ctrl+F2`
- B. `Alt+Ctrl+F1`
- C. `Ctrl+F1`
- D. `Ctrl+Esc`

37. `LightDM` 配置中的哪种选项启用了特定用户的自动登录？

- A. `auto login`
- B. `auto user`
- C. `login auto`
- D. `user auto`

38. 哪种辅助技术会忽略连续按下或按住的键？

- A. Sticky keys（粘滞）
- B. Mouse keys（鼠标键）
- C. Bounce keys（弹跳键）
- D. On-screen keyboard（屏幕键盘）

39. 使用 `LightDM` 时，使用哪个组合键返回终端？

- A. `Alt+Ctrl+F2`
- B. `Alt+Ctrl+F1`
- C. `Ctrl+F1`
- D. `Ctrl+Esc`

40. `LightDM` 配置中的哪种选项启用了特定特定自动自动登录？

- A. `auto login`
- B. `auto user`
- C. `login auto`
- D. `user auto`

41. 假设启动时已禁用了显示管理器。登录后可以使用哪个命令启动 `X` 服务器？

- A. `xs`
- B. `xstart`
- C. `X -start`
- D. `startx`

42. `xorg.conf` 配置文件中的哪种选项配置了屏幕进入空闲模式但但不进入待机模式，并且在不支持 `DPMS` 的显示器上可用？

- A. `StandbyTime`
- B. `BlankTime`
- C. `SuspendTime`
- D. `OffTime`

43. 以下哪个命令可以帮助你确定 `X` 会话中给定窗口的信息，包括窗口大小和位置信息？

- A. `xkbinfo`
- B. `xdxpy`
- C. `xwininfo`
- D. `xver`

44. `GOK` 内部的哪个选项/按钮用于显示替代鼠标的按键？

- A. `Mouse`
- B. `MouseKeys`
- C. `Movement`
- D. `Compose`

45. 以下哪个命令允许名为 `cwa` 的主机连接到 `X` 服务器？

- A. `xconnect cwa`
- B. `xterm +cwa`
- C. `xhost +cwa`
- D. `xf cwa`

46. `ssh` 配置文件中的以下哪项选项需要启用，以便会话可以通过 `ssh` 连接发送？

- A. `X11Connect yes`
- B. `ForwardX11 yes`
- C. `ForwardX yes`
- D. `XForward yes`

47. `xorg.conf` 配置文件中 `Files` 部分的哪种配置选项可以添加服务器搜索字体的路径？

- A. `FontSection`
- B. `Fonts`
- C. `FontLoc`
- D. `FontPath`

48. 使用哪种辅助技术为无法使用指针（如鼠标）的用户提供输入法？

- A. Keyboard（键盘）
- B. Sticky keys（粘滞）
- C. Mouse keys（鼠标键）
- D. On-screen keyboard（屏幕键盘）

49. 哪种辅助技术会忽略连续按下或按住的键？

- A. Sticky keys（粘滞）
- B. Mouse keys（鼠标键）
- C. Bounce keys（弹跳键）
- D. On-screen keyboard（屏幕键盘）

# 第 7 章

# 管理任务（领域 107）

本章涵盖以下 `CompTIA LINUX+`/`LPIC-1` 考试目标：

- `107.1` 管理用户账户和相关文件
    - 添加、修改和删除用户和组
    - 管理密码/组数据库中的用户信息
    - 创建特殊目的和受限账户
    - 以下是使用的文件和工具列表：
        - `/etc/passwd`
        - `/etc/shadow`
        - `/etc/group`
        - `/etc/skel`
        - `chage`
        - `getent`
        - `groupadd`
        - `groupdel`
        - `groupmod`
        - `passwd`
        - `useradd`
        - `userdel`
        - `usermod`

- `107.2` 通过调度任务自动化管理任务
    - 管理 `cron` 和 `at` 任务
    - 配置用户对 `cron` 和 `at` 服务的访问
    - 配置 `anacron`
    - `/etc/cron.{d,daily,hourly,monthly,weekly}`
    - `/etc/at.deny`
    - `/etc/at.allow`
    - `/etc/crontab`
    - `/etc/cron.allow`
    - `/etc/cron.deny`
    - `/var/spool/cron/*`
    - `crontab`
    - `at`
    - `atq`
    - `atrm`
    - `anacron`
    - `/etc/anacrontab`

- `107.3` 本地化和国际化
    - 配置本地设置和环境变量
    - 配置时区设置和环境变量
    - 以下是使用的文件和工具列表：
        - `/etc/timezone`
        - `/etc/localtime`
        - `/usr/share/zoneinfo`
        - `LC_*`
        - `LC_ALL`
        - `LANG`
        - `TZ`
        - `/usr/bin/locale`
        - `tzselect`
    - `tzconfig`
    - `date`
    - `iconv`
    - `UTF-8`
    - `ISO-8859`
    - `ASCII`
    - `Unicode`

![](img/84990579543ce21a46ac6dc5014.png)

1. 哪个文件包含用户信息（如用户名和真实姓名），并对所有用户可见？

- A. `/etc/pass`
- B. `/etc/shadow`
- C. `/etc/passwd`
- D. `/etc/user-info`

2. 下列哪个命令会在每天上午12:15 和 下午12:15 通过 `cron` 执行任务？

- A. `0,12 * *`
- B. `15 0,12 * *`
- C. `15 * * 0/12`
- D. `*/12 * * 15`

3. 哪个文件用于指示服务器的本地时区？

- A. `/etc/time`
- B. `/etc/timezoneconfig`
- C. `/etc/localtime`
- D. `/etc/localtz`

4. 哪个文件用于提供可以添加和删除 `cron` 任务的用户列表？

- A. `/etc/cron.job`
- B. `/etc/cron.allow`
- C. `/etc/cron.users`
- D. `/etc/crontab`

5. 下列哪个命令移除账户过期时间？

- A. `sudo chage -l username`
- B. `sudo chage -E -1`
- C. `sudo chage -E username`
- D. `sudo chage --noexpire username`

6. 在哪个目录下找到不同地区的时区文件？

- A. `/etc/timezoneinfo`
- B. `/etc/zoneinfo`
- C. `/var/zoneinfo`
- D. `/usr/share/zoneinfo`

## 第 7 章 管理任务 (Domain 107)

7. 下列哪个命令从现在开始调度一系列命令？

- A. `at +1hr`
- B. `at now + 1 hour`
- C. `atq`
- D. `at -1`

8. 你需要从系统中删除一个用户，包括其家目录。下列哪个命令可以完成此任务？

- A. `userdel`
- B. `userdel -r`
- C. `userdel -R`
- D. `deluser`

9. 在创建用户时，应该在哪个目录下放置文件以便将其复制到用户的家目录？

- A. `/etc/skel`
- B. `/etc/homedir`
- C. `/home/useplate`
- D. `/etc/template`

10. 如果你需要的计算机在不同时间关机，应该使用哪种任务调度器？

- A. `cron.d`
- B. `cron.hourly`
- C. `anacron`
- D. `at`

11. 下列哪个命令以自 `epoch` 秒的格式提供当前日期和时间？

- A. `date %+seconds`
- B. `date +%s`
- C. `date --seconds`
- D. `date --now`

12. `iconv` 命令的哪个选项显示特定系统中可用的字符集？

- A. `--show-char`
- B. `--show`
- C. `--list`
- D. `--all`

13. 哪个环境变量控制日期时间的格式（例如 12 小时或 24 小时时钟）？

- A. `LOCALE_DATE`
- B. `DATE_FORMAT`
- C. `LC_TIME`
- D. `LC_DATE`

14. 哪个命令显示当前通过 `at` 调度的任务列表？

- A. `atlist`
- B. `atq`
- C. `atl`
- D. `at --jobs`

15. 如果用户不允许交互式地登录计算机，应该将用户设置为哪个 shell？

- A. `/bin/bash`
- B. `/bin/tcsh`
- C. `/bin/zsh`
- D. `/bin/false`

16. 下列哪种编码提供了字符的多字节表示？

- A. `ISO-8859`
- B. `UTF-8`
- C. `ISO-L`
- D. `UFTMulti`

17. 下列哪个命令将名为 `DomainAdmins` 的组改为 `DomainUsers`？

- A. `groupmod -n DomainAdmins DomainUsers`
- B. `groupch DomainAdmins DomainUsers`
- C. `chgroup DomainAdmins DomainUsers`
- D. `group -N DomainAdmins DomainUsers`

18. 在哪个目录下你会找到对应于系统中当前 `cron` 任务的用户文件列表？

- A. `/var/spool/cron/crontabs`
- B. `/var/spool/jobs`
- C. `/etc/cron`
- D. `/etc/cron.users`

19. 哪个命令删除 `ID` 为 3 的 `at` 任务？

- A. `atq`
- B. `at -l`
- C. `atm 3`
- D. `rmat`

20. 哪个命令可以查看系统上可用的时区并获取可用于脚本设置时区的输出？

- A. `tzd`
- B. `/etc/locale`
- C. `tzdata`
- D. `tzselect`

21. 你需要确定 `LDAP` 集成是否工作。为了实现这一点，你想通过 `/etc/nconf` 获取用户列表？

- A. `get`
- B. `getent`
- C. `usermod`
- D. `userlist`

22. 在添加用户和组时，哪个文件的名称包含最大和最小用户 `ID` 信息？

- A. `/etc/groupinfo`
- B. `/etc/login.defs`
- C. `/etc/login.info`
- D. `/etc/loginlist`

23. 下列哪个被用作全局 `cron` 文件？

- A. `/etc/cron.d`
- B. `/etc/cron.sys`
- C. `/etc/crontab`
- D. `/etc/cron.tab`

24. 添加到用户家目录下的 `.profile` 中的下列哪行会将时区设置为 `America/Chicago`？

- A. `TZ=/Central; export TZ`
- B. `TIMEZONE='America/Chicago'; export TIMEZONE`
- C. `set TZ=/Central`
- D. `TZ='America/Chicago'; export TZ`

25. 在哪个目录下你会找到每 24 小时通过 `cron` 的脚本？

- A. `/etc/cron.daily`
- B. `/etc/cron.weekly`
- C. `/etc/cron.hourly`
- D. `/etc/crontab`

26. 下列 `LANG` 变量的哪个会让系统跳过本地化（locale）？

- A. `LANG=COMPAT`
- B. `LANG=NONE`
- C. `LANG=C`
- D. `LANG=END`

27. 运行 `useradd` 时，需要指定哪个选项以创建家目录？

- A. `-h`
- B. `-m`
- C. `-x`
- D. `-a`

28. 下列哪个命令锁定用户的密码登录，但不阻止其他形式的登录？

- A. `usermod L`
- B. `userdel -r`
- C. `useradd -h`
- D. `userlock`

29. 如果你需要重新配置特定会话的所有本地变量和设置，可以使用哪个环境变量？

- A. `LC_LIST`
- B. `LC_GLOBAL`
- C. `LC_ALL`
- D. `ALL_LOCALE`

30. 下列哪个项在放在 `/etc/crontab` 中会以 `www-data` 用户身份运行名为 `/usr/local/bin/changehome.sh` 的命令？

- A. `1 1 * * www-data /usr/local/bin/change.sh`
- B. `www-data changehome.sh`
- C. `*/1 www-data changehome.sh`
- D. `* * */www-data /usr/local/bin/changehome.sh`

31. 下列哪个命令产生列系统中所有用户最后密码更改时间的报告？

- `passwd -a`
- `passwd -S`
- `passwd a -S`
- `passwd --all`

32. 假设密码每 60 天必须更改一次。哪个命令会更改用户的最后密码更改日期，而不实际用户更改账户？

- `chage -f`
- `chage -w`
- `chage -l`
- `chage -d`

33. 下列哪个文件被 `anacron` 用于读取任务相关的配置信息？

- `/etc/anacron.d`
- `/etc/anacrontab`
- `/etc/anacron.config`
- `/etc/anacron.conf`

34. 下列哪个命令将系统级时区设置为 `America/Los_Angeles`？

- `-sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime`
- `-sf America/Los_Angeles; /etc/localtime`
- `-sd /etc/localtime /usr/share/timezone/America/Los_Angeles`
- `-sf /etc/localtime /usr/share/zoneinfo/America/Los_Angeles`

35. 哪个文件包含不允许创建 `cron` 调度任务的用户列表？

- `/etc/cron.users`
- `/etc/cron.deny`
- `/etc/cron.allow`
- `/etc/cron.userlist`

36. 哪个文件包含用户名、`UID` 和加密密码的列表？

- `/etc/passwd`
- `/etc/shadow`
- `/etc/encpass`
- `/etc/grouppass`

37. 下列哪项最符合 Linux 系统上 `UID` 和 `GID` 之间的关系？

- A. 对于特定用户，`UID` 和 `GID` 在系统中是相同的。
- B. 每个用户都有相同的 `UID` 和 `GID`，并且在用户创建时创建。
- C. `UID` 代表用户，而 `GID` 是一个全局唯一的用户 ID。
- D. `UID` 和 `GID` 之间没有直接关系。

38. 在基于 Debian 的系统中，哪个命令可以使用包的工具更改时区？

- A. `dpkg-reconfigure time`
- B. `dpkg-reconfigure tzdata`
- C. `apt-select tzdata`
- D. `apt-config timezone`
