
```sh
#!/bin/sh

# 这是一个为 root 用户提供每日报告的脚本 - rrc
# 头信息
SYS_LOG=`dmesg | tail`
UP_TIME=`uptime | awk -F: '{print $2}'`

echo "\n\n" > /export/home/scripts/report
echo "Good morning - Here's the news from `uname -n`" >> /export/home/scripts/report
echo for `date` >> /export/home/scripts/report
echo "\n*******\n" >> /export/home/scripts/report
echo "The last entries in the syslog are:\n \n$SYS_LOG" >> /export/home/scripts/report

# 体育
CPU_ACT=`uptime | awk -F: '{print $4}'`
RE_BOOT=`who -b`

echo "\n*******\n" >> /export/home/scripts/report
echo "The current CPU load over the last 1, 5 and 15 mins is:$CPU_ACT" >> /export/home/scripts/report
echo "The system was last rebooted:$RE_BOOT" >> /export/home/scripts/report

# 本地人员
CURRENT_USERS=`tail /var/adm/sulog`
echo "\n*******\n" >> /export/home/scripts/report
echo "The users currently logged in are:\n \n$CURRENT_USERS | cat" >> /export/home/scripts/report
echo "\n\n*******\n" >> /export/home/scripts/report
```

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_376_0.png)

# 检测与拒绝黑客攻击 • 第11章

```sh
The last 10 users of the su command were:\n$WHO_SU" | cat >>/export/home/scripts/report
echo "\n\n" >> /export/home/scripts/report
echo "If you were a Hacker, how would you break into this system?" >>/export/home/scripts/report
```

通过此部分中的信息，我们寻找一个不应该处于活跃状态的账户。例如，如果我们看到用户账户 `janeill` 在早上 7:00 登录，而我们知道该用户很少在早上 9:00 之前出现，我们就有理由怀疑。要么是 `janeill` 起早了，要么她昨晚忘记注出了——要么是其他人正在使用该账户。无论什么情况下，都需要进行调查。

此外，这还能告诉我们谁在使用 `su` 命令。如果我们看到用户 `janeill` 成功切换到了 `root` 账户，而我们知道该用户不应该这样做，我们就有了麻烦。

脚本的最后一行将报告发送到 `root` 电子邮件地址。通过使用 Sendmail 别名，我们可以将报告发送到任何电子邮件地址：

```sh
cat /export/home/scripts/report | mailx -s "Daily Report from `uname -n`" root
```

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_376_0.png)

# 检测与拒绝黑客攻击 • 第 11 章 353

## 开始行动！

以下是完整的脚本：

```sh
#!/bin/sh

# 这是一个为 root 用户提供每日报告的脚本 - rrc
# 头信息
SYS_LOG=`dmesg | tail`
UP_TIME=`uptime | awk -F: '{print $2}'`

echo "\n\n" > /export/home/scripts/report
echo "Good morning - Here's the news from `uname -n`" >> /export/home/scripts/report
echo for `date` >> /export/home/scripts/report
echo "\n*******\n" >> /export/home/scripts/report
echo "The last entries in the syslog are:\n \n$SYS_LOG" >> /export/home/scripts/report

# 体育
CPU_ACT=`uptime | awk -F: '{print $4}'`
RE_BOOT=`who -b`

echo "\n*******\n" >> /export/home/scripts/report
echo "The current CPU load over the last 1, 5 and 15 mins is:$CPU_ACT" >> /export/home/scripts/report
echo "The system was last rebooted:$RE_BOOT" >> /export/home/scripts/report

# 本地人员
CURRENT_USERS=`tail /var/adm/sulog`
echo "\n*******\n" >> /export/home/scripts/report
echo "The users currently logged in are:\n \n$CURRENT_USERS | cat" >> /export/home/scripts/report
echo "\n\n*******\n" >> /export/home/scripts/report
```

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_376_0.png)

通过此部分中的信息，我们寻找一个不应该处于活跃状态的账户。例如，如果我们看到用户账户 `janeill` 在早上 7:00 登录，而我们知道该用户很少在早上 9:00 之前出现，我们就有理由怀疑。要么是 `janeill` 起早了，要么她昨晚忘记注出了——要么是其他人正在使用该账户。无论什么情况下，都需要进行调查。

此外，这还能告诉我们谁在使用 `su` 命令。如果我们看到用户 `janeill` 成功切换到了 `root` 账户，而我们知道该用户不应该这样做，我们就有了麻烦。

脚本的最后一行将报告发送到 `root` 电子邮件地址。通过使用 Sendmail 别名，我们可以将报告发送到任何电子邮件地址：

```sh
cat /export/home/scripts/report | mailx -s "Daily Report from `uname -n`" root
```

## 总结

预测意外是不可能的。如果你可以预测，那么根据定义，它就不再是“意外”了。无论你如何加固围墙，总有人会进入。本章描述的概念将在有人突破围墙后为你提供帮助。

在本章中，我们涵盖了检测和拒绝针对我们系统的攻击的方法。不依赖任何单一方法来保护我们的系统是重要的。

我们讨论了创建自己的工具，例如自定义脚本。许多黑客对流行的入侵检测软件非常熟悉，正如你一样。他们知道这些软件的优缺点，或者如何绕过它们。获得优势的方法之一是创建自己的安全脚本。尝试不同的使用方法来监控受保护的系统。

我们还涵盖了构建我们的蜜罐系统。自制的蜜罐是一个强大的工具。由于没有固定的设置，黑客很难对其检测和规避。在构建蜜罐时，确保你像黑客一样思考。对其进行彻底测试。在将其投入生产环境之前，我经常挑战同事测试蜜罐。

## 解决方案快速通道

### 监控黑客活动

- 使用 `Tripwire` 是监控文件和目录更改的极佳方法。虽然商业版本提供了额外功能，但开源版本是在预算有限的情况下提供安全的理想解决方案。
- `tripwire.pol` 文件是策略文件，决定了 `Tripwire` 监控哪些内容以及何时发送警报。
- 商业版本提供了 `Tripwire Manager`，你可以用它来远程监控和配置多个系统。

### 使用 Shell 脚本提醒系统管理员

- 你可以使用自定义的 Shell 脚本来提供额外的监控。
