
在 `-L` 选项之后，我们列出了想要转发的本地端口、远程服务器名称以及我们想要转发到远程服务器上的端口。

### 图 7.18. 为 PuTTY 设置 SSH 隧道。

![](img/9ba05966cc0c98b5830dd68d51d157c1_268_0.png)

## 启动 VNC 服务器守护进程

现在我们已经打开了 SSH 会话，通过在命令行提示符输入 `vncserver` 来启动 VNC 服务器守护进程：

```
[kermit@swinetrek ~]$ vncserver
```

你需要一个密码来访问桌面。

```
Password:
Verify:

New 'swinetrek:1 (kermit)' desktop is swinetrek:1

Creating default startup script /home/kermit/.vnc/xstartup

Starting applications specified in /home/kermit/.vnc/xstartup

Log file is /home/kermit/.vnc/swinetrek:1.log
```

```
$[kermit@swinetrek ~] $
```

如果你是第一次运行 `vncserver`，它会要求你输入用于此次及未来 VNC 连接的密码。稍后可以使用 `vncpasswd` 命令更改此密码。

`vncserver` 会在 `~/.vnc` 目录中为当前登录的用户创建配置文件。在我们第一次使用 VNC 之前，我们需要修改这些文件之一，以确保在登录时启动 GNOME 桌面环境。在文本编辑器中打开 `~/.vnc/xstartup` 文件，找到显示“Uncomment the following two lines for normal desktop”的行，并取消其后两行的注释。完成后，文件应该看起来像这样：

File: `~/.vnc/xstartup`

```
#!/bin/sh

# Uncomment the following two lines for normal desktop:

unset SESSION_MANAGER

exec /etc/X11/xinit/xinitrc

[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup

[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources

xsetroot -solid grey

vncconfig -iconic &

xterm -geometry 80x24+10+10 -ls -title "VNCDESKTOP Desktop" & 

twm &
```

## 连接到 VNC 服务器

下一步——连接到 VNC 服务器——也很简单。使用你的 VNC 客户端，将 `localhost:1` 输入为服务器名称。这可能看起来有点反直觉，但它是正确的：通过连接到 `localhost:1`，你实际上连接到了远程机器上的 5901 端口，该连接通过 SSH 隧道传输到远程机器的 5901 端口，那里 VNC 服务器正在等待连接。你现在拥有了一个安全的 VNC 连接，因为它是通过你设置的 SSH 隧道传输的。

在 VNC 运行时不要关闭 SSH 会话，否则你的 VNC 会话将被突然中断！完成工作后，通过关闭窗口断开 VNC 连接。你必须停止服务器上的 VNC 守护进程：在与服务器的 SSH 连接中，输入 `vncserver -kill :1` 来停止 VNC 服务器守护进程。然后你可以退出 SSH 会话，这将关闭 SSH 隧道。

## 总结

能够远程操作服务器是一件非常有用的事情。无论你是否直接坐在服务器面前，都可以对你的 LAMP 服务器进行操作。

## 偶尔管理

与日常工作相比，这些任务是“偶尔”的。创建备份越容易，你执行备份的可能性就越高。

### 备份

执行备份最简单的方法是将文件写入 CD。你的备份策略可以根据你的意愿变得复杂——但一个简单的备份策略比一个无法实施的复杂策略要好。

第一次运行脚本时，你将选择要备份的文件；此后，运行脚本（每天）只需将这些文件备份到 CD 即可。该脚本也是书中代码的一部分。

```
"$HOME/.simple-cd-backup/FilesToBackup"

zenity --title "Simple CD Backup" --question-question-text \

"Burn files in the directory?"

if [ $? == 1 ]; then exit; fi

mkisofs -f -l -o $ISO -A "$BACKUPDIR" \

zenity --progress-text="Creating backup" \

--title "Simple CD Backup" --progress --pulsate -auto-close

cdrecord -v speed=4 --dev/$CDDEVICE $ISO \

zenity --progress-text="Burning CD" \

--title "Simple CD Backup" --progress --pulsate -auto-close

rm $ISO

zenity --info-infotext burned to CD.
```

将此脚本保存为 `~/Desktop/simple-cd-backup.sh`，然后设置为可执行文件：可以右键点击文件设置相应的权限，或者在命令行输入 `chmod +x ~/Desktop/simple-cd-backup.sh`。

你可以双击此文件来查看图 8.1 所示的 Run or Display? 对话框。点击 Run 运行脚本；点击 Display 在文本编辑器中打开文件。

图 8.1. Run or Display? 对话框。

![](img/9ba05966cc0c98b5830dd68d51d157c1_274_0.png)

如果你运行脚本，它将创建 `~/.simple-cd-backup/FilesToBackup` 目录，在 Nautilus 中打开该目录，最后弹出如图 8.2 所示的确认窗口。

## 第 8 章：偶发管理

图 8.2. `simple-cd-backup` 脚本显示的窗口。

![](img/9ba05966cc0c98b5830dd68d51d157c1_275_0.png)

将确认对话框移到侧边（但不要点击“取消”），并向此目录创建你想要备份的文件的符号链接（symlinks）。将文件链接到目录中是至关重要的：不要直接复制它们。有时，你可以右键点击文件来创建链接，但如果你没有权限向该文件目录写入，则该选项将不可用。在这些情况下，请使用 `ln -s` 命令。例如，如果你想备份包含所有系统配置的 `/etc` 目录，可以输入以下内容：

```
[kermit@swinetrek ~]$ ln -s /etc \
> ~/.simple-cd-backup/FilesToBackUp/etc

[kermit@swinetrek ~]$
```

或者，如果你有一个三键鼠标，可以按照以下步骤操作：

- 双击桌面上的“计算机”图标，或者选择“位置” > “计算机”。
- 双击“文件系统”，显示根目录。
- 使用中间键将 `cd` 文件夹切换到 `FilesToBackup` 文件夹中。
- 点击菜单上的“在此处创建链接”。

一旦你已经在 `FilesTo-Backup` 文件夹中为你想要备份的每个文件建立了链接，请关闭 `FilesToBackup` 窗口。插入一张空白 CD，当你在对话框中看到“刻录目录中链接的文件吗？”时，点击“确定”。文件将被链接到一张 CD 镜像，该镜像将被刻录到 CD 中。将弹出对话框，报告这两个步骤的进度，因此你需要在进程完成后点击“确定”。

下次你运行备份时（例如在第二天），你创建的链接仍然会在那里。这意味着，要运行每日备份，你只需点击 `simple-cd-backup`，然后在“刻录目录中链接的文件吗？”提示处点击“确定”：它会将你的文件刻录到备份 CD 中。

### 释说明

让我详细解释一下该脚本的工作原理。使用该脚本不需要了解这些信息，但它是展示 Shell 脚本如何像强大的应用程序一样运行的良好示例，且只需要少量的编码工作。如果脚本在你的系统上没有完全按预期运行，此说明也可能帮助你调试脚本。

脚本中实际执行工作的是最后几行，它们使用了 `mkisoofs`（“make ISO filesystem”的缩写）和 `drecord`。脚本的其他部分侧重于以用户友的方式设置备份。

首先，`simple-cd-backup` 使用一小段 Python 解析 `/proc/sys/dev/cdrom/info` 文件检查系统是否具有 CD 刻录机。该文件列出了系统中所有的 CD-ROM 驱动器，并提供了每个驱动器能力的指示。在我的机器上，显示如下：

| 驱动器名称: hdc |
| :--- | :--- |
| 驱动器速度 | 24 |
| 驱动器槽数 | 1 |
| 可以关闭托盘 | 1 |
| 可以打开托盘 | 1 |
| 可以锁定托盘 | 1 |
| 可以更改速度 | 1 |
| 可以选择磁盘 | 0 |
| 可以读取多段模式 | 1 |
| 可以读取 MCN | 1 |
| 报告介质更改 | 1 |
| 可以播放音频 | 1 |
| 可以写入 CD-R | 1 |
| 可以写入 CD-RW | 1 |
| 可以读取 DVD | 1 |
| 可以写入 DVD-R | 1 |
| 可以写入 DVD-RAM | 0 |
| 可以读取 MRW | 1 |
| 可以写入 MRW | 1 |
| 可以写入 RAM | 1 |

上面的文件列出了一个名为 "hdc" 的 CD 驱动器，可以通过 `/dev/hdc` 访问。如果有更多 CD 驱动器，会在文件中增加列。我们的脚本使用单行 Python 代码在该文件中查找“Can CD-R”且后跟一个 `1` 的行。如果找不到这样的列，它将显示错误（使用下文介绍的 `zenity`）并退出。

`FilesToBackup` 是一个 Nautilus 窗口，显示目录 `~/.simple-cd-backup/FilesToBackup`，该目录由脚本创建（如果它还尚不存在）。若要查看它，请使用此命令运行 Nautilus：

```
[kernit@swinetrek ~]$nautilus --no-desktop --browser \
> "$HOME/.simple-cd-backup/FilesToBackup"
```

脚本大量使用了 `zenity`，这是一个用于从 shell 脚本中弹出各种类型 GNOME 警告框和对话框的命令。例如，脚本使用以下代码显示一个包含“确定”和“取消”按钮的对话框：

```
[kernit@swinetrek ~]$ zenity --title "Simple CD Backup" \
> --question --question-text "刻录目录中链接的文件吗?"
```

这会显示如图 8.3 所示的对话框。

一旦你确认想要刻录 CD，真正的工作就开始了。脚本使用 `mkisoofs` 创建一个包含目录中链接的所有文件的 ISO 镜像。它使用以下命令执行：

```
File: simple-cd-backup.sh (excerpt)

mkisoofs -f -l -o $ISO "$DISNAME" "$BACKUPDIR"
```

`$ISO` 定义为镜像，`$DISNAME` 是磁盘名称，`$BACKUPDIR` 是 `~/.simple-cd-backup/FilesToBackup`。脚本使用 `-f` 和 `l` 选项。一旦 ISO 镜像准备就绪，将使用 `drecord` 命令：

```
File: simple-cd-backup.sh (excerpt)

drecord -v /dev/hdc $ISO
```

该命令将 ISO 镜像刻录到 `/dev/hdc`。在刻录完成后，脚本会删除 `$ISO` 文件。

这将将 `/dev/hdc` 刻录到 `$ISO` 镜像。

最后，脚本会通过 `zenity` 告知用户操作已完成。

## 第 8 章：临时管理

所有这些日志都以纯文本文件的形式呈现。你不需要 GUI 视图工具，可以使用以下简单的命令在终端中查看日志。

```bash
@swinetrek kermit# cat /var/log/messages

Oct 11 06:14:59 swinetrek syslogd 1.4.1: restart.

Oct 11 06:14:59 swinetrek kernel: klogd 1.4.1,
log source /=proc/kmsg

Oct 11 06:14:59 swinetrek kernel: Linux version 2.6.11-1.1369_FC4
(bhcompileodebuild.redhat.com)
(gcc version 4.0.0 2005052) Red Hat 4.0.0-9)

#1 Thu Jun 22 22:55:56 EDT 2005

Oct 11 06:14:59 swinetrek kernel: BIOS-provided physical RAM map:

Oct 11 06:14:59 swinetrek kernel:
BIOS-e820:0000000000000000-0000000009fc00

Oct 11 06:14:59 swinetrek kernel:
BIOS-e820:0000000000000000-0000000000a0000 (reserved)
```

```bash
Oct 17 21:01:20 swinetrek sshd(pam_unix)[2989]: session closed for user kermit

Oct 17 21:16:25 swinetrek su(pam_unix)[2605]: session closed for user root

Oct 17 21:16:21 swinetrek su(pam_unix)[3060]: session opened for user root by (uid=0)#
```

当你使用 SSH 连接到其他机器时，日志的文本特性非常有用；你可以直接从命令行查看日志文件，而无需使用 VNC 或类似的图形化工具。

在命令行调查日志文件时，一个非常有用的命令是 `tail`。它可以列出任何文件的最后行。

```bash
@swinetrek kermit# tail /var/log/httpd/error_log

[client 192.168.69.36] PHP Warning: Division by zero in /var/www/html/div-zero-test.php on line 2

Mon Oct 17 23:07:59 2005 [error] client 192.168.69.36] File does not exist: /var/www/html/favicon.ico

Mon Oct 17 23:08:05 2005 [error] client 192.168.69.36] File does not exist: /var/www/html/favicon.ico

Tue Oct 17 01:27:22 2005 [error] client 69.20.162.232] File does not exist: /var/www/html/favicon.ico

Tue Oct 17 03:50:12 2005 [error] client 192.168.69.36] File does not exist: /var/www/html/favicon.ico

[client 192.168.69.36] PHP Fatal error: Call to undefined function blowup() in /var/www/html/blowup-test.php on line 2
```

### 日志轮转

```bash
[Tue Oct 17 03:52:47 2005] [error] [client 192.168.69.36] File does not exist: /var/www/html/favicon.ico

[Tue Oct 17 03:53:01 2005] [error] [client 192.168.69.36] File does not exist: /var/www/html/favicon.ico

[client 192.168.69.36] PHP Warning: Division by zero in /var/www/html/div-zero-test.php on line 20

[Tue Oct 17 03:57:26 2005] [error] [client 192.168.69.36] File does not exist: /var/www/html/favicon.ico

*root@swinetrek hermit]*
```

如果你正在调查一个发生的错误，`tail` 会非常方便；它能让你避免翻遍整个文件。如果你想查看文件的更多（或更少）内容，可以使用 `tail -n filename` 来显示 `filename` 的最后 `n` 行。`-f` 选项会指示 `tail` 在新行被添加到文件时实时显示它们。这对于“监控”日志文件非常有帮助。作为一个实验，运行 `tail -f /var/log/httpd/error_log`，然后尝试访问一个你服务器上不存在的文件 URL（例如 `http://localhost/foo.txt`）。你会看到 `tail` 立即输出了错误。按 Ctrl-C 退出 `tail`。

### 日志轮转

你可能会发现，随着时间的推移，日志文件的副本开始出现。例如：

```bash
[root@swinetrek hermit]# /var/log/httpd/
```
