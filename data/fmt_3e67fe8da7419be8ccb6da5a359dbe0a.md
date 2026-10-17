
a. 打印队列不接受作业并向用户发送消息，说明打印机不可用

b. 打印队列接受作业进入打印队列并将其保留在那里，直到打印机再次启用

c. 当发送 `lp` 请求时，打印机显示为离线

d. 打印队列将发送给的所有打印作业重定向到 `/dev/null`

## 复习题 509

1. 在引用 `/etc/syslog.conf` 文件时，________ 指定了某区域信息，而 ________ 是重要性。

a. 部分 (section)

b. 服务 (service)

c. 进程 (process)

d. 设施 (facility)

2. 大多数日志文件位于哪个目录？

a. `/etc/log`

b. `/log`

c. `/var/log`

3. 什么文件包含 UID 和 GID 范围等默认信息？

a. `/etc/skel`

b. `/etc/passwd`

c. `/etc/defs`

d. `/default`

4. 负责 Linux 打印的后台进程是什么？

a. `lp`

b. `cupsd`

c. `lpd`

d. `lpstat`

5. 使用哪个命令解锁用户账户？

a. `lock username`

b. `open username`

c. `usermod -U username`

d. `useradd -U username`

6. 除了用户列表外，`etc/passwd` 文件还包含账户过期信息。对或错？

19. 你使用 `lstat` 确定 User1 在 Printer1 队列中放置了两个尚未打印的大作业。ID 为 17 和 21。使用哪个命令从打印队列中删除这两个作业？

a. `cancel 17 21`

b. `cancel -u 17 21`

c. `cancel -a 17 21`

d. `cancel 17 21`

20. 使用哪个命令删除用户账户？

a. `usermod -d username`

b. `del username`

c. `userdel`

d. `rm`

## 实验项目

这些项目应按照给顺序完成。本章介绍的实验项目总共需要三小时完成。实验室的要求包括：

- 根据实验项目 7-2 安装了 Red Hat Core 2 的计算机

### 实验 11-1

![](img/8fe037bf1ed016dccb79dbd1a27184f2_527_0.png)

在这个实验中使用打印机配置工具创建一个本地打印机。

1. 开启计算机。Linux 系统加载后，使用用户名 root 和密码 secret 登录图形终端 (tty7)。

2. 在 Gnome 桌面加载后，导航到 Red Hat 按钮、系统设置、打印机。

3. 选择 New 按钮创建新打印机。

4. 在 Add 界面点击 Forward，在 Name 框中输入 pi，在 Short description 框中输入 sample text-only printer。完成后点击 Forward。

5. 在 Queue type 界面，确保 Locally-connected 被选为队列类型

6. 在 Queue type 界面，确保选中了-selected并点击 Custom device 按钮。在 Custom device 对话框中输入 `/dev/null`，以指定打印作业将发送到特殊设备 `/dev/null` 并点击 OK。点击 Forward。

特殊设备 `/dev/null` 代表空设备；发送到此设备的任何打印作业将被丢弃。

- 7. 在打印机模型界面上，向下滚动通用打印模型列表，直到看到 Text Only Printer（仅文本打印机）并选中它。点击 Forward（前进）。

- 8. 在 Finish 和创建新打印队列的界面上，点击 Finish（完成）。在提示打印测试页时，选择 No（否）。

- 9. 观察代表你的打印机的行。它是默认打印机吗？点击 Apply（应用）按钮重启 cups 守护进程。

- 10. 关闭打印机配置工具并在 GNOME 桌面中打开终端。

- 11. 在终端提示符处，输入 `cat /etc/cups/printers.conf` 并按回车。将此文件中打印机的条目与你在本次实验项目中指定的设置进行比较。

- 12. 输入 `exit` 并按回车关闭终端界面。

- 13. 退出 GNOME 桌面。

## 项目 11-2

在本次实验项目中，你将控制打印过程、创建打印作业并在打印队列中管理它们。

- 1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并使用用户名 `root` 和密码 `secret` 登录终端。

- 2. 在命令提示符处，输入 `lpstat -t` 并按回车。cups 守护进程正在运行吗？p1 是否启用了缓冲打印？

- 3. 在命令提示符处，输入 `disable -“To pause print jobs in the print queue” p1` 并按回车，防止 lp 打印机打印。

- 4. 在命令提示符处，输入 `lpstat -t` 并按回车。验证 p1 已启用缓冲但已禁用。

- 5. 接下来在命令提示符处输入 `lp -n 2 -d p1` 并按回车，向 p1 打印两份 `/etc/hosts`。你收到了什么打印作业 ID？

- 6. 在命令提示符处，输入 `lpstat` 并按回车。你的打印机在队列中吗？

- 7. 在命令提示符处，输入 `sort /etc/hosts | lp` 并按回车，对文件 `/etc/hosts` 进行排序并将输出发送 p1。注意你不需要为 `lp` 命令使用 `-d`选项，因为它是默认打印机。你收到了什么打印作业 ID？

- 8. 在命令提示符处，输入 `lpstat` 并按回车。验证两个打印作业都在队列中。

## 第 11 章常见管理任务

- 9. 在命令提示符处，输入 `cancel p1-p2`（如果屏幕上的打印作业数字不同，请使用相应的数字）从队列中移除两个作业。输入 `lpstat` 并按回车验证它们已被移除。

- 10. 在命令提示符处，输入 `ipadmin -u allow:none -u deny:all -d p1` 并按回车，防止所有用户向 p1 打印。

- 11. 在命令提示符处，输入 `lp /etc/hosts` 并按回车。你成功了吗？

- 12. 在命令提示符处，输入 `ipadmin -u allow:all -u deny:none -d p1` 并按回车，允许所有用户向 p1 打印。

- 13. 在命令提示符处，输入 `lp /etc/hosts` 并按回车。你成功了吗？

- 14. 在命令提示符处，输入 `cancel -a` 并按回车从队列中移除任何打印作业。

- 15. 输入 `exit` 并按回车退出 shell。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_529_0.png)

## 项目 11-3

在本次实验项目中，你将查看系统日志守护进程（System Log Daemon）和 logrotate 工具的配置。

- 1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并使用用户名 `root` 和密码 `secret` 登录终端。

- 2. 在命令提示符处，输入 `ls -l /dev/cron` 并按回车。文件类型是什么？哪个守护进程使用该文件？它的用途是什么？

- 3. 在命令提示符处，输入 `less /etc/syslog.conf` 并按回车查看系统日志守护进程的配置文件。观察条目。为什么 cron 守护进程的所有信息都会记录在这些文件中？完成后按 `q` 退出工具。

- 4. 在命令提示符处，输入 `tail /var/log/cron` 并观察条目。写下你在文件中看到的最后一条目。

- 5. 在命令提示符处，输入 `killall -9 cron` 并按回车停止 cron 守护进程。

- 6. 在命令提示符处，输入 `cron` 并按回车启动 cron 守护进程。

- 7. 在命令提示符处，输入 `tail /var/log/cron` 并观察条目。将步骤 4 的输出与终端屏幕上的输出进行比较。最后一条目是什么？为什么？

- 8. 在命令提示符处，输入 `cat /etc/cron.daily/logrotate` 并按回车观察每天运行的 logrotate 命令。接下来在命令提示符处输入 `cat /etc/crontab` 并按回车。`/etc/cron.daily` 目录的内容每天在什么时候运行？

- 9. 在命令提示符处，输入 `less /etc/logrotate.conf` 并按回车查看 logrotate 命令的配置文件。日志文件何时轮转？

5. 在命令提示符下，输入 `usermod -l bozobo2` 并按回车，将用户 bozo2 的登录名改回 bozo。

6. 在命令提示符下，输入 `usermod -u 666 bozo` 并按回车，将用户 bozo 的 UID 改为 666。接下来在命令提示符下输入 `cat /etc/passwd` 并按回车。UID 改变了吗？
