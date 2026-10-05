

# 网络与互联网服务

# 第二部分

YaST 还会检测是否与其他软件包存在冲突，例如 proftpd 或 in.ftptd。

# 图 10.2
高亮显示了 wuftpd FTP 器的 YaST 工具。

![](img/cbac72550c7126a22162e94d91a0c360_355_0.png)

软件包 wuftpd 被高亮显示了，按 `i` 键安装该软件包。YaST 可能会向你发出警告，提示 proftpd 或 in.ftptd 已经安装。你可以按 `Return`（回车）键继续安装 wu-ftptd。在安装 wu-ftptd 的过程中，会弹出一系列系列对话框和消息。软件包安装完成后，SuSEConfig 的输出将运行，并在你退出 YaST 时执行一系列命令。proftpd 和 in.ftptd 软件包可以以类似的方式加载，或者已经作为 "n" 系列的软件包加载了。

wu-ftptd 同时也以 RPM（红帽软件包管理器）的形式提供，并在初始设置期间作为安装选项出现。如果你决定运行 FTP 服务器但未安装 RPM，请从 CD-ROM 中获取 `wu-ftptd-2.4.2vr17-3.i386.rpm`，或者检查 http://www.suse.com 获取最新版本。要安装 RPM，请挂载你的 SuSE CD-ROM 或在系统中下载服务器的路径。为了说明之便，该文件的位置位于 `/root` 目录。

```
# -ivv /root/wu-ftptd-2.4.2vr17-3.i386.rpm
```

如果你计划安装一个匿名访问的站点，请务必也从 CD-ROM 安装 `anonftpd-2.8-1.i386.rpm`。你始终可以在 http://www.suse.com 检查最新版本。

要安装匿名 FTP 文件，请以 root 身份登录并运行以下命令：

```
# -ivv anonftpd-2.8-1.i386.rpm
```

# 释

尽管 anonftp 软件包包含了设置匿名 FTP 服务所需的文件，且 wu-ftpd rpm 文件包含了 FTP 守护进程，但你会在 ftp rpm 软件包中找到 FTP 客户端程序。安装所有三个 RPM 以获得完整服务。匿名 FTP 服务器应仅由经验丰富的用户安装。

你应该定期检查 SuSE 网站以获取 Linux FTP 软件的更新，特别是如果你允许通过互联网访问你的计算机。许多较新版本的 Linux 网络或通信软件包含了安全修复程序或其他增强功能，旨在保护你的计算机免受入侵者的攻击。

要测试安装是否成功，只需使用 FTP 客户端并连接到你的机器即可。对于示例 FTP 服务器 aptiva，你将对以下内容做出响应：

```
# ftp aptiva
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version-wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva): anonymous
331 Guest login, send your complete e-mail address as password.
Password: willie@thinkpad.home.org
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for /bin/ls.
total 6
drwxr-xr-x 6 root 1024 Feb 17 13:21 .
drwxr-xr-x 6 root 1024 Feb 17 13:22 ..
--x--x--x 2 root 1024 Feb 17 13:21 bin
--x--x--x 2 root 1024 Feb 17 13:21 etc
drwxr-xr-x 2 root 1024 Feb 17 13:21 lib
drwxr-xr-x 2 ftp 1024 Sep 11 1998 pub
226 Transfer complete.
ftp>
```

如你所见，登录后你将位于 `/home/ftp` 目录。要退出 FTP 客户端软件，只需在 `ftp>` 提示符下输入 `bye` 或 `quit`。如果你想测试私有 FTP

![](img/cbac72550c7126a22162e94d91a0c360_356_0.png)

# 网络与互联网服务 第二部分

服务器，重新运行 FTP 客户端但使用你的登录名而不是匿名登录。以下是一个示例：

# ftp aptiva

```
Connected to aptiva.home.org.
220 aptiva.home.org FTP server (Version-wu-2.4.2-academ[BETA-18])(1)
Mon Aug 3 19:17:20 EDT 1998) ready.
Name (aptiva): anonymous
331 Guest login, send your complete e-mail address as password.
Password: willie@thinkpad.home.org
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful.
150 Opening ASCII mode data connection for /bin/ls.
total 6
drwxr-xr-x 6 root 1024 Feb 17 13:21 .
drwxr-xr-x 6 root 1024 Feb 17 13:22 ..
--x--x--x 2 root 1024 Feb 17 13:21 bin
--x--x--x 2 root 1024 Feb 17 13:21 etc
drwxr-xr-x 2 root 1024 Feb 17 13:21 lib
drwxr-xr-x 2 ftp 1024 Sep 11 1998 pub
226 Transfer complete.
ftp>
```

