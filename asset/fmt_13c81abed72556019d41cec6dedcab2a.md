
完成后保存更改并退出编辑器。
- 11. 在命令提示符下输入 `/etc/rc.d/init.d/smb restart` 并按回车。
- 12. 在命令提示符下输入 `smclient -L /server1` 并按回车，其中 X 是老师分配给你的唯一数字。在提示时输入 Samba 密码 secret。你看到新的共享目录了吗？
- 13. 在命令提示符下输入 `smclient \serverX/newshare` 并按回车，其中 X 是老师分配给你的唯一数字。在提示时输入 Samba 密码 secret。
- 14. 在 `smb:\>` 提示符下输入 `dir` 并按回车。你在 `/var/www/html` 目录吗？
- 15. 在 `smb:\>` 提示符下输入 `exit` 并按回车。
- 16. 输入 `exit` 并按回车退出你的 shell。

# 第15章 配置网络服务与安全

## 项目 15-5

在本次动手项目中，你将使用 `nmap` 工具和 `/etc/services` 文件检查本地计算机上运行的服务。

- 1. 按 Ctrl+Alt+F2 切换到命令行终端 (tty2)，并使用用户名 root 和密码 secret 登录终端。
- 2. 在命令提示符下输入 `/etc/rc.d/init.d/httpd stop` 并按回车。
- 3. 在命令提示符下输入 `/etc/rc.d/init.d/inetd stop` 并按回车。
- 4. 在命令提示符下输入 `/etc/rc.d/init.d/smb stop` 并按回车。
- 5. 在命令提示符下输入 `nmap -sT 127.0.0.1` 并按回车。列出的端口中有哪些是你认识？有未知端口吗？可以在哪里找到有关未知端口的信息？端口 `23/tcp` 关联的服务是什么？
- 6. 在命令提示符下输入 `grep 23 /etc/services` 并按回车。运行在端口 23的服务全名是什么？
- 7. 在命令提示符下输入 `/etc/rc.d/init.d/httpd start` 并按回车。
- 8. 在命令提示符下输入 `/etc/rc.d/init.d/inetd start` 并按回车。
- 9. 在命令提示符下输入 `/etc/rc.d/init.d/smb start` 并按回车。
- 10. 在命令提示符下输入 `nmap -sT 127.0.0.1` 并按回车。Apache 开启了哪些端口？
- 11. 输入 `exit` 并按回车退出你的 shell。

## 项目 15-6

在本次动手项目中，你将使用 `su` 和 `sudo` 工具获取 root 权限。

- 1. 按 Ctrl+Alt+F2 切换到命令行终端 (tty2)，并使用用户名 root 和密码 secret 登录终端。
- 2. 在命令提示符下输入 `su dailyuser` 并按回车。
- 3. 在命令提示符下输入 `passwd dailyuser` 并按回车。在提示时输入密码。
- 4. 在命令提示符下输入 `su - dailyuser` 并按回车。你需要输入密码吗？在命令提示符下输入 `whoami` 并按回车确保你现在是以 dailyuser 登录。
- 5. 在命令提示符下输入 `su - root` 并按回车。在提示时输入 root 密码。在命令提示符下输入 `whoami` 并按回车确保你现在是以 root 。
- 6. 在命令提示符下输入 `exit` 并按回车退出 root 会话。
- 7. 在命令提示符下输入 `exit` 并按回车退出 dailyuser 会话。
- 8. 运行命令 `visudo -f /etc/sudoers`。在文件末尾添加以下行：

```
dailyuser ALL=(root) /bin/touch
```
