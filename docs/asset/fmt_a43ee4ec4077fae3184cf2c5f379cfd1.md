
> 注意：文本邮件客户端可以读取由其他客户端下载的邮件。例如，你可以通过输入 `mail -f $HOME/.evolution/mail/loc/Inbox` 来打开你的 Evolution 邮件信箱。

# 使用 mail 管理电子邮件

最老、且当你只想快速检查远程服务器上 root 用户的邮箱内容时最简单的命令是 `mail` 命令 (`/bin/mail`)。虽然 `mail` 可以以交互方式使用，但它经常用于发送基于脚本的电子邮件。这里是一些示例：

```
$ mail -s 'My Fedora version' chris@example.com < /etc/redhat-release
$ ps aux | mail -s 'My Process List' chris@example.com
```

刚刚显示的邮件示例提供了快速发送文本的方案，而无需打开图形界面邮件应用程序。第一个示例发送了内容的

## 第 12 章：访问网络资源

将 `/etc/redhat-release` 文件发送给用户 chris@example.com。主题 (`-s`) 设置为 'My Fedora Version'。在第二个示例中，将当前运行的进程列表 (`ps aux`) 发送到同一个用户，主题为 'My Process List'：

以交互方式使用时，默认情况下 `mail` 命令会打开由当前 shell 的 `$MAIL` 值设置的邮箱。例如：

```
# echo $MAIL
# /var/spool/mail
# mail
mail 8.1 6/6/93. Type ? for help.
*/var/spool/root*: 25 messages 25 new
U logwhatab.1 Fri Jun 15 00:03 44/167 * "Logwhat for ab (Linux)"
U logwhatab.1 Sat 16 04:32 87/256 * "Logwhat for ab (Linux)"
3 logwhatab.1 Sun 17 04:28 92/269 * "Logwhat for ab (Linux)"
N logwhatab.1 Fri Jun 22 09:28 44/167 * "Logwhat for ab (Linux)"
N 5 MAILER-DAEMON@ Fri Jun 22 09:28 93/3348 * "Warning: could not send "
```

当前消息旁边有一个大于号 (`>`)。新消息有开头（但没有））标记，未读消息标记为 `U`，如果没有字母，则表示该消息已读。底部的提示符 (`&`) 准备好接收消息。

此时，你处于命令模式。你可以使用简单的命令进行移动并执行基础的邮件功能。输入 `?` 查看命令列表，或者更改你使用的消息数量。输入 `7` 查看一条消息。输入 `v3` 在 `vi` 编辑器中打开第三条消息。输入 `h18` 查看以 18 开头的的消息头列表。输入 `t` 回复消息，输入 `r7`（输入你的消息，在行尾输入一个点来发送消息）。输入 `d4` 删除第四条消息（或使用 `d4–9` 删除第 4 到 9 条消息）。输入 `!bash` 退出到 shell（然后退出即可返回 `mail`）。

在退出 `mail` 之前，请注意，退出时你查看的任何消息都会从你的邮箱文件复制到 `$HOME`，除非你保留了它们 (`pre`)。要让所有消息留在你的邮箱中，输入 `x` 退出。要保存对邮箱的更改，输入 `q` 退出。

你可以打开任何 MBOX 格式的文件。例如，如果你以 root 用户身份登录，但想打开用户 chris 的邮箱，输入以下命令：

```
mail -f /var/spool/mail/chris
```

### 使用 mutt 管理邮件

如果你想持续使用命令行邮件客户端，我们建议你使用 `mutt` 而不是 `mail`。`mail` 命令有很多局限性，例如无法在不预先对其进行编码（如使用 `uuencode` 命令）的情况下发送附件，而 `mutt` 具有许多处理现代电子邮件需求的功能。`mutt` 命令是 `mutt` 软件包的一部分。

像 `mail` 一样，`mutt` 也可以用于从脚本中弹出消息。`mutt` 还增加了发送附件的能力。例如：

```
$ mutt -s "My Fedora Version" -a /etc/redhat-release \
chris@example.com < email-body.txt
$ mutt -s "My Fedora Version" -a /etc/redhat-release \
chris@example.com < /dev/null
```

第一个示例将文件 `email-body.txt` 作为消息正文，并将 `/etc/redhat-release` 文件作为附件。第二个示例发送了附件，但消息正文为空 (`< /dev/null`)。

你可以通过简单输入 `mutt` 来开启你的 `mutt` 会话（假设你的默认邮箱是 `$MAIL`）：

```
$ mutt
/home/chris Mail does not exist. Create it? ([yes]/no): y

q:Quit d:El u:Unde s:Save m:Mail r:Reply g:Group r?:Help

1 0 Jun 16 logwatch@ab (69) Logwach for ab (Linux)
2 0 Jun 18 logwatch@ab (171) Warning for ab (Linux)
3 0 Jun 18 Mail Delivery S (219) Warning: could not send message
4 0 Jun 19 logwatch@ab (33) Warning for ab (Linux)
```

```
--Mutt:/var/pool/mail/root [Msgs:22 New:0 Old:20 63K]--(date)/(time)--(all)--
```

由于 `mutt` 是面向屏幕的，因此使用 `mutt` 更加方便。一常地，在 `mutt` 中使用 `mail` 快捷键命令来移动。输入 `t` 获取帮助。顶部栏会显示提示，帮助你处理邮件。使用上、下方向键来高亮你想读的消息。按回车键查看高亮的消息。使用 `PageUp` 和 `PageDown` 翻阅每条消息。按 `p` 返回消息头。

使用斜杠 (`/`) 搜索文本，或使用 `Esc` 键 (`Esc/`) 反向搜索。输入 `n` 搜索。按 `Tab` 键跳转到下一个新消息或未读消息。使用 `Esc-Tab` 回到上一个。输入 `s` 将当前消息发送到文件。输入 `d` 删除消息，输入 `u` 取消删除。

要发送新邮件，输入 `m`。输入 `r7` 回复（输入你的消息，在行尾输入一个点来发送消息）。输入 `d4` 删除第四条消息（或 `d4–9` 删除第 4 到 9 条消息）。输入 `!bash` 退出到 shell（然后退出即可返回 `mail`）。

在退出 `mail` 之前，请注意，退出时你查看的任何消息都会从你的邮箱文件复制到 `$HOME`，除非你保留了它们 (`pre`)。要让所有消息留在你的邮箱中，输入 `x` 退出。要保存对邮箱的更改，输入 `q` 退出。

（注：此处部分翻译原文似乎存在重复或乱码，已根据语意进行逻辑对齐）

（注：此处部分翻译原文似乎存在重复或乱码，已根据语意进行逻辑对齐）

# 第 13 章：执行远程系统管理

| 使用 SSH 工具 |

| :--- |

| 使用 SSH 隧道 |

| 使用 SSH 密钥 |

| 使用 SSH 远程桌面 |

| 使用 SSH 共享 |

| 使用 VNC 使用 SSH |

| 远程登录使用 SSH |

尽管 SSH 提供了更好的工具，但许多过时的 Unix 命令在处理远程通信时仍然被使用。

## SSH 总结

尽管 SSH 提供了更好的工具，但许多过时的 Unix 命令在处理远程通信时仍然被使用。

（注：原文部分存在存在重复内容）

尽管 SSH 提供了更好的工具，但许多过时的 Unix 命令在处理远程通信时仍然被使用。

## 第 13 章：进行远程系统管理

`OpenSSH` 同时提供了客户端和服务器组件。以下是关于 SSH 的一些事实：

- 对于 Windows，你可以在 Cygwin (`www.cygwin.com`) 内使用 Linux SSH 工具。除非你已经在使用 Cygwin（一个适用于 Windows 的类 Linux 环境），否则我们推荐使用 PuTTY (`www.chiark.greenend.org/uk/sgatatham/putty`)。PuTTY 是一个免费开源 Telnet/SSH 客户端。

- 尽可能使用 SSH 版本 2，因为它最安全。某些启用 SSH 的网络设备可能只支持旧的、不安全的版本。OpenSSH 支持所有版本。旧版本的 Fedora 和 RHEL 接受 SSH v1 和 v2。新版本默认接受版本 2。

- 在 Fedora 和 RHEL 中，使用 `systemctl start sshd` 来启动 SSH 服务（ssh daemon）。要配置该服务，请编辑 `/etc/ssh/ssh_config` 文件。
