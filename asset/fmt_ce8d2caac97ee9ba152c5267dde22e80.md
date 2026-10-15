
## 项目 15-3

在这个动手项目中，你将启用 `telnet` 服务并使用 `telnet` 工具连接它。

1. 按 `Ctrl-Alt-F2` 切换到命令行终端 (`tty2`)，并使用用户名 `root` 和密码 `secret` 登录终端。
2. 在命令提示符输入 `telnet localhost` 并回车。你收到了什么错误？为什么？
3. 使用 `vi` 等编辑器编辑 `/etc/xinetd.d/telnet` 文件，删除行：
   ```
   disable = yes
   ```
   完成后保存更改并退出编辑器。
4. 在命令提示符输入 `telnet localhost` 并回车。你可以使用 `telnet` 工具吗？为什么或为什么不？
5. 在命令提示符输入 `/etc/init.d/xinetd restart` 并回车启动守护进程。
6. 在命令提示符输入 `telnet localhost` 并回车。为什么成功？接下来，使用用户名 `root` 和密码 `secret` 登录系统。你成功了吗？收到了什么错误信息？等待 1 分钟让 `telnet` 关闭。
7. 在命令提示符输入 `cat /etc/security` 并回车。文件中的每个条目代表什么？接下来，输入 `rm -f /etc/security`。
8. 在命令提示符输入 `telnet localhost` 并回车。为什么成功？接下来，使用用户名 `root` 和密码 `secret` 登录系统。你成功了吗？收到了什么错误信息？等待 1 分钟让 `telnet` 关闭。

（注：项目 15-3 的 OCR 文本非常混乱，已提供清理后的逻辑流程）。

## 动手项目 741

12. 在 `ftp>` 提示符下，输入 `dir` 并按回车。`initab` 文件在那里吗？接下来，在 `ftp>` 提示符下输入 `bye` 并按回车退出 FTP 实用。
13. 在命令提示符下，输入 `ls -F` 并按回车。你的家目录下包含什么？`initab` 文件传输成功了吗？
14. 在命令提示符下，输入 `cp initab /var/ftp` 并按回车将 `initab` 文件复制到匿名FTP目录。接下来，在命令提示符下输入 `ls -F /var/ftp` 并按回车。存在哪些文件和子目录？`initab` 文件复制成功了吗？
15. 在命令提示符下，输入 `ftp localhost` 并按回车。在提示时使用用户名 `anonymous` 和密码 `user@sample.com` 登录。你成功了吗？
16. 在 `ftp>` 提示符下，输入 `dir` 并按回车。你看到了什么？`initab` 文件在那里吗？
17. 接下来，在 `ftp>` 提示符下输入 `lcd .` 并按回车将本地目录更改为当前目录。现在在 `ftp>` 提示符下输入 `mget *` 并按回车。当提示“mget initab?”时，输入 `y` 然后按回车。
18. 在 `ftp>` 提示符下，输入 `cd lib` 并按回车。接下来，在 `ftp>` 提示符下输入 `pwd` 并按回车。你正在使用哪个目录？
19. 接下来，在 `ftp>` 提示符下输入 `mget libs` 并按回车。当提示“mget libs.md5?”时，输入 `y` 然后按回车。你收到了什么错误信息？为什么？提示：查看屏幕输出中的文件权限。
20. 接下来，在 `ftp>` 提示符下输入 `get-2*` 并按回车。当提示“get ld-2.2.4.so?”时，输入 `y` 然后按回车。传输了吗？为什么？
21. 在 `ftp>` 提示符下输入 `bye` 并按回车退出 FTP 实用。
22. 在命令提示符下，输入 `ls -F /` 并按回车查看 `/` 目录的内容。`initab` 和 `ld-2.2.4.so` 文件在那里吗？
23. 输入 `exit` 并按回车退出 shell。

## 项目 15-5

在这个动手项目中，你将学习 `rcp`、`rsh`、`login` 和 `ssh` 实用程序，以受信任的方式访问你的计算机。

1. 按 `Ctrl-Alt-F2` 切换到命令行终端 (`tty2`)，并使用用户名 `root` 和密码 `secret` 登录 `term`。
2. 在命令提示符下，输入 `login localhost` 并按回车。发生了什么？按下 `Ctrl-c` 组合键返回提示符。
3. 使用如 `vi` 等文本编辑器编辑 `/etc/xinetd.d/rlogin` 文件，并删除如下行：
   ```
   disable = yes
   ```
   完成后，保存更改并退出编辑器。

## 第 15 章 Linux 网络

4. 在命令提示符下，输入 `/etc/init.d/xinetd restart` 并按回车重启互联网超级守护进程（Internet Super Daemon）。
5. 在命令提示符下，输入 `login localhost` 并按回车。你被提示输入密码了吗？输入 `secret` 并按回车。
6. 在命令提示符下，输入 `who` 并按回车。你以什么身份登录？你正在使用哪个终端？如何判断的？
7. 在命令提示符下，输入 `exit` 并按回车。你收到了什么消息？
8. 使用如 `vi` 等文本编辑器编辑 `/etc/hosts.equiv` 文件。有条目吗？添加一行：
   ```
   localhost
   ```
   完成后，保存更改并退出编辑器。
9. 在命令提示符下，输入 `login localhost` 并按回车。你被提示输入密码了吗？输入 `secret` 并按回车。
10. 在命令提示符下，输入 `exit` 并按回车。
11. 使用如 `vi` 等文本编辑器编辑 `/root/.hosts` 文件。有条目吗？添加一行：
    ```
    localhost
    ```
    完成后，保存更改并退出编辑器。
12. 在命令提示符下，输入 `login localhost` 并按回车。你被提示输入密码了吗？为什么没有？
13. 在命令提示符下，输入 `exit` 并按回车。
14. 在命令提示符下，输入 `rcp localhost:/etc/hosts localhost:/root/rcptest` 并按回车。你需要传递密码吗？为什么？接下来，在命令提示符下输入 `ls -F /root` 并按回车。`/etc/hosts` 文件是否成功复制到 `/root/rcptest` 文件？
15. 在命令提示符下，输入 `rsh localhost date` 并按回车在 `localhost` 计算机上执行 `date` 命令。发生了什么？按下 `Ctrl-c` 组合键返回你的 shell 提示符。
16. 使用如 `vi` 等文本编辑器编辑 `/etc/xinetd.d/rsh` 文件，删除如下行：
    ```
    disable = yes
    ```
