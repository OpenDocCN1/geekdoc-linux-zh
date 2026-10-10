

7. **密码：** ISS316Security

8. 按 `:` 键进入 **插入** 模式。

9. 找到并取消注释以下行（删除 `#`）
    ```text
    # SModLoad imudp.so
    # $UDPSPerverRun 514
    ```

10. 向下滚动并找到该行：`*.* @@remote-host:514`。在下一行下方，添加新的一行：`*.* @<教师服务器IP地址>:514`

**注意：** 不要使用 `<教师服务器IP地址>`。请替换为教师的虚拟机 IP 地址。例如，如果教师的虚拟机 IP 地址为 `172.30.0.40`，该行应显示为：`*.* @@172.30.0.40:514`

11. 保存更改并退出文件。按 `escape` 键退出插入模式，然后按 "shift" 和 `:` 键进入命令模式。在命令模式的冒号提示符下，输入 `wq` 以退出并保存更改。

### 搜索日志文件

12. 启动 openssh 服务器。输入命令：`sudo service sshd start` 并按 `<enter>`。如果提示，请输入学生账户的密码（**ISS316Security**）。

13. 使用无效账户通过安全外壳（SSH）连接到本地主机。输入命令：`ssh nonexist@localhost` 并按 `<enter>`。

**注意：** 该账户在服务器上不存在。但无论如何请尝试登录，以生成一条日志记录。当出现消息“Are you sure you want to continue connecting(yes/no)?”时，输入：`yes` 并按 `<enter>`。接下来，输入任意密码。三次尝试失败后，连接将断开。

14. 从安全日志中读取日志信息。输入命令：`su -c ' cat /var/log/secure | grep nonexist '` 并按 `<enter>`。

15. **密码：** ISS316Security

16. 查找最后安装的包或软件。输入命令：`su -c ' tail /var/log/yum.log '` 并按 `<enter>`

17. **密码：** ISS316Security

18. 在日志中查找系统启动时是否启动了 sshd 服务。输入命令：`su -c ' cat /var/log/boot.log | grep sshd'` 并按 `<enter>`。

19. **密码：** ISS316Security

### 安装和配置 Tripwire

20. 安装 Tripwire 软件。输入命令：`sudo yum install tripwire -y` 并按 `<enter>`。如果提示输入密码，请输入学生用户的密码（ISS316Security）。

21. 配置 tripwire。输入命令：`su -c 'tripwire-setup-keyfiles'`

22. **密码：** ISS316Security

23. 按照步骤创建站点和本地密钥文件密码短语。
    - a) 站点密码短语输入 'is418lab09'
    - b) 本地密码短语输入 'is418lab09'。

**注意：** 该过程将要求输入站点和本地密码短语以生成加密的策略和配置文件。当被提示时，请输入之前过程中创建的密码，即 'is418lab09'

24. 初始化 Tripwire 数据库。输入命令：`su -c 'tripwire --init'` 并按 `<enter>`。

25. **密码：** ISS316Security

26. 请输入您的本地密码短语：is418lab09

```
[student@TargetFedora01 yum.repos.d]$ su -c 'tripwire --init'
Password:
Please enter your local passphrase:
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_98_0.png)

**注意：** Tripwire 将根据默认策略文件中的指定内容对计算机上的所有文件建立索引。会出现几次“No such file or directory.”（没有该文件或目录）的警告。由于实验中使用默认配置文件引用了 Fedora 中未找到的许多文件位置，因此可以忽略这些警告。完成索引后，将出现一条消息“The database was successfully generated.”（数据库已成功生成。）。

27. 对 `/bin/ls` 文件强制进行时间戳更改。输入命令：`su -c 'touch /bin/ls'` 并按 `<enter>`。

28. **密码：** ISS316Security

![](img/73be0eef2ceb12f43f3eb92c420134f5_99_0.png)
图 50 – 更改 `/bin/ls` 文件的时间戳

29. 使用 Tripwire 执行文件完整性检查。输入命令：`su -c 'tripwire --check'` 并按 `<enter>`。

30. **密码：** ISS316Security

![](img/73be0eef2ceb12f43f3eb92c420134f5_99_1.png)
图 51 – 运行 tripwire 文件完整性检查器

> **注意：** Tripwire 现在将检查默认策略文件中指定的已索引文件。与之前步骤一样，“No such file or directory”（没有该文件或目录）警告可以忽略。报告生成后，向上滚动查看报告结果。至少应该有针对已修改的 `/bin/ls` 文件的违规项。

### 安装和计划 rkhunter

31. 安装 rkhunter rootkit 检查器。输入命令：`sudo yum install rkhunter -y` 并按 `<enter>`。如果提示输入密码，请输入学生用户的密码（ISS316Security）。

32. 输入命令：`su -c 'rkhunter --update'` 并按 `<enter>` 以确保 rkhunter 软件已使用最新的签名进行更新。当被提示时，请输入 root 的密码（ISS316Security）。

![](img/73be0eef2ceb12f43f3eb92c420134f5_99_2.png)
图 52 – 更新 rkhunter 数据库

33. **输入命令：** `su -c 'vi /etc/rkhunter.conf'` 并按 `<enter>`。当被提示时，请输入 root 的密码（ISS316Security）。

34. **向下滚动并找到该行：** `MAIL-ON-WARNING="root"`

35. 按 “`i`” 键进入 **插入模式**。

36. 将 `MAIL-ON-WARNING="root"` 更改为 `MAIL-ON-WARNING="student"`。

37. **保存更改并退出文件。** 按 `escape` 键退出插入模式，然后按 “`shift`” 和 “`:`” 键进入命令模式。在命令模式的冒号提示符下，输入 `wq` 以退出并保存更改。

38. 使用 cron 计划程序，计划 rkhunter 每天早上 2:30 am 运行。

39. 使用 `vi` 编辑器创建一个空文本文件。**输入命令：** `vi rkhunter.txt` 并按 `<enter>`。

40. 按 “`i`” 键进入 **插入模式**。

41. 将以下行添加到 rkhunter.txt 文件
    ```
    30 2 * * * /usr/bin/rkhunter -c -q >/dev/null 2>&1
    ```

42. 保存更改并退出文件。按 `escape` 键退出插入模式，然后按 “`shift`” 和 “`:`” 键进入命令模式。在命令模式的冒号提示符下，输入 `wq` 以退出并保存更改。

43. 为 root 用户计划 cron 任务。**输入命令：** `su -c 'crontab rkhunter.txt'` 并按 `<enter>`。

44. **密码：** ISS316Security

45. 列出已安装的 cron 任务。**输入命令：** `su -c 'crontab -l'` 并按 `<enter>`

46. **密码：** ISS316Security

47. **输入命令：** `su -c 'rkhunter -c'` 并按 `<enter>`。

48. **密码：** ISS316Security

```
[student@TargetFedora01 ~]$ su -c 'crontab rkhunter.txt'
Password:
[student@TargetFedora01 ~]$ su -c 'crontab -l'
Password:
30 2 * * * /usr/bin/rkhunter -c -q >/dev/null 2>&1
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_100_0.png)

## 交付物

完成实验 #9：实施安全日志记录与监控的最佳实践后，学生需要提供以下交付物：

- 1. 学生需提交以下文件的截图：
    - a. /etc/rsyslogd.conf 文件的输出
    - b. /var/log/secure、/var/log/yum.log 和 /var/log/boot 日志文件的输出
    - c. tripwire 和 rkhunter 两者成功的 yum install 命令输出
- 2. 实验 #9 - 评估工作表，包含评估问题的答案

## 评估标准和评分细则

以下是学生必须执行的实验 #9 的评估标准和评分细则：

- 1. 学生是否能够在 Fedora Linux 服务器中配置远程日志记录，并将 syslogs 和其他事件发送到远程主机以进行安全的二级日志记录？ – [20%]
- 2. 学生是否能够在 Fedora Linux 服务器中搜索不同的日志文件，以识别特定类型的日志存储位置及其回收频率？ – [20%]
- 3. 学生是否能够安装并配置 Tripwire 文件完整性工具，以便快速识别并正确记录（本地和远程）对重要系统文件的修改？ – [20%]
- 4. 学生是否能够安装并计划 rkhunter 使用 cron 子系统在指定间隔运行，从而在可能的情况下正确且快速地识别 rootkit？ – [20%]
- 5. 学生是否能够配置日志文件的自动搜索以及重要安全应用程序的自动运行，以正确监控 Fedora Linux 服务器的恶意活动？ – [20%]

