

## 使用 sudo 模拟 root

正如你现在所知，以 root 身份登录会赋予你修改整个 Unix 系统的能力，而不仅仅是你个人有权限访问、读取或修改的目录和文件。当然，拥有如此大的权力也伴随着责任——不要搞砸整个系统就是其中之一。特别是在你学习系统管理时，你可能想通过以 sudo 登录来尝试这些技能。使用 sudo 工具，你可以像 root 一样运行某些命令，但风险没有成为 root 那么大。真正的 root 用户必须授予使用 sudo 的权限，有时权限仅限于使用特定的实用程序——你需要自行尝试。

```
[jdoe@frazz jdoe]$ cd /var/log
[jdoe@frazz log]$ tail messages
tail: messages: Permission denied
[jdoe@frazz log]$ sudo tail messages

We trust you have received the usual lecture from the local System Administrator. It usually boils down to these two things:

#1) Respect the privacy of others.
#2) Think before you type.

Password:
Jan 25 06:01:01 frazz CROND[22809]: (root) CMD (nice -n 19 run-parts /etc/cron.hourly)
Jan 25 06:01:01 frazz CROND[22818]: (mail) CMD (/usr/bin/python -S /usr/lib/mailman/cron/qrunner)
Jan 25 06:01:01 frazz su(pam_unix)[22814]: session opened for user news by (uid=0)
Jan 25 06:01:01 frazz su(pam_unix)[22814]: session closed for user news
Jan 25 06:01:02 frazz msec: unable to run chage: chage: unknown user: ejray
Jan 25 06:01:03 frazz msec: changed mode of /var/log/news/nntpsend.log from 660 to 640
Jan 25 06:02:00 frazz CROND[22865]: (mail) CMD (/usr/bin/python -S /usr/lib/mailman/cron/qrunner)
Jan 25 06:03:00 frazz CROND[22867]: (mail) CMD (/usr/bin/python -S /usr/lib/mailman/cron/qrunner)
Jan 25 06:04:00 frazz CROND[22872]: (mail) CMD (/usr/bin/python -S /usr/lib/mailman/cron/qrunner)
Jan 25 06:04:17 frazz sudo: jdoe : TTY=pts/1 ; PWD=/var/log ; USER=root ; COMMAND=/usr/bin/tail messages
[jdoe@frazz log]$
```

代码清单 16.1 sudo 命令让你能够做普通用户无法做的事情，但风险没有成为 root 那么大。

```
1001 jdoe@foo $ sudo ls
Password:
My mind is going. I can feel it.
Password:
Take a stress pill and think things over.
Password:
He has fallen in the water!
1002 jdoe@foo $
```

代码清单 16.2 更令人惊讶的是，sudo 还有幽默感。

请注意，所有 sudo 的使用都会被记录。如果你的系统管理员不希望你尝试以 root 身份操作，不要在除自己系统之外的任何系统上使用 sudo。在代码清单 16.2 中，我们展示了普通用户与拥有权限操作之间的区别。

### 使用 sudo 模拟 root：

1. cd /var/log; tail messages

   以普通用户的身份，尝试查看 /var/log 中的系统日志文件。在 Linux 系统上，通常是 /var/log/messages；在 Solaris 系统上，通常是 /var/log/syslog。其他 Unix 变体会有其他但类似的位置。

   请注意，其中一些文件需要 root 权限才能查看，而另一些则不需要。如果你能以自己的身份查看文件，请选择另一个文件来看看 sudo 如何提供帮助。

2. sudo tail messages

   在上一次尝试被拒绝权限后，在命令前加上 sudo 以尝试以 root 权限发出相同的命令。

3. ********

   在有趣的警告之后输入你的密码，然后注意这次命令成功了（参见代码清单 16.1）。

- 如果你没有获得使用 sudo 的权限（不仅仅是技术上的权限，而是实际的“你可以这样做”的许可），不要使用。所有使用 sudo 的操作都会被记录，你很可能会为自己的行为负责。

- 只要可能，最好只在需要时使用 sudo，而不是成为 root。任何拼写错误都可能带来问题，有意识地在想要以 root 权限操作时加上 sudo 是件好事。

- 使用 sudo 一次后，你可以在一段时间内（通常为五分钟）再次使用它而无需再次输入密码。

- 一些版本的 sudo 在密码输入错误时会显示相当有趣的提示（代码清单 16.2）。不过，如果你故意去查看这些提示，很可能会极大地惹恼你的系统管理员。

