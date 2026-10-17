
`BROADCAST RUNNING MULTICAST MTU:1500 Metric:1`

`Interrupt:11 Base address:0xde0`

```
- 6. 惯例是在基础接口名称（`eth0`）后面使用数字作为 IP 别名，但你可以使用任何你喜欢的字符。输入 `ifconfig eth0:abc 1.2.3.5`。输入 `ifconfig eth0:abc`。你看到：
```

```
eth0:abc

Link encap:Ethernet Haddr 00:07:95:BB:A3:6A

inet addr:1.2.3.5 Bcast:1.255.255.255 Mask:255.0.0.0

 BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

Interrupt:11 Base address:0xde0
```

- 7. 现在为本地环回接口（`lo`）创建两个 IP 别名。输入 `ifconfig lo:0 127.0.0.2`，然后输入 `ifconfig lo:1 127.0.0.3`。现在输入 `ifconfig|more`。你会看到你到为止为止创建的所有接口。

- 8. 你可以关闭这些 IP 别名的任何一个。输入 `ifconfig eth0:5 down`。现在输入 `ifconfig|more`。你会发现 `eth0:5` 接口不再列出。

- 9. 如果你尝试启用已关闭的 IP 别名，必须在关闭后重新创建 IP 别名。输入 `ifconfig eth0:5 up`。你会看到类似这样的错误信息：
`SIOCSIFFLAGS: Cannot assign requested address`

- 10. 要返回你的原始网络设置，请重启电脑。

### 认证目标

Linux* 考试目标：

- 配置基础网络服务和设置 (`3.4`)
- 以 root 身份登录或使用 `su` 命令执行管理任务 (`4.7`)
- 运行并解释 `ifconfig` (`5.4`)

### 复习题

- 1. 下面由哪个命令配置了 IP 别名？
    - a. `ifconfig -alias 192.168.0.50`
    - b. `ifconfig eth0-alias 192.168.0.50`
    - c. `ifconfig eth0:0 192.168.0.50`
    - d. `ifconfig eth0:0 127.0.0.5`
- 2. 你可以为本地环回接口（`lo`）分配 IP 别名吗？是/否
- 3. 可以创建多少个 IP 别名？
    - a. `64`
    - b. `256`
    - c. 接口
    - d. `256`
- 4. 在关闭 IP 别名后，必须指定地址和子码来重新启用吗？是/否
- 5. 启用 IP 别名时，必须指定地址和子码吗？是/否

### 实验 15.3 安装与配置 vsftpd

`vsftpd` 用于在网络上传输文件。大多数 Linux 发行版都包含它。

#### 所需材料

- 以 root 权限访问
- 浏览器

预计完成时间：40 分钟

#### 活动

1. 在浏览器中访问 `vsftpd.com`。
2. 查看关于 `vsftpd` 的信息。
3. 安装 `vsftpd`。
4. 在浏览器中查看安全设置。
5. 查看 `vsftpd` 的版本。
6. 下载压缩包。
7. 切换到第二个控制台（`Ctrl+Alt+2`）。
8. 进入目录。
9. 解压压缩包。
10. 进入子目录。
11. 运行 `./install_vsftpd`。你会看到：

```
Created /etc/ftpusers

No FTP server is running.

/etc/xinetd.conf does not appear to be handling "ftp" service.

/etc/xinetd.d does not appear to be handling "ftp" service.

vsftpd is not currently running.

Installing configuration files.

Installing new vsftpd config.

Looking up IP address and hostname.

Created /usr/local/etc/vsftpd/domain.conf.

Installing programs.

Configuring your system so vsftpd starts at boot.

Starting vsftpd: OK

Checking if the FTP service has started.
```

恭喜！`vsftpd` 已成功完成。下一步是自定义你的安装：

```
/usr/local/etc/vsftpd/general.conf

/usr/local/etc/vsftpd/domain.conf
```

完成后运行 `/usr/local/sbin/restart_vsftpd`。
安装日志保存为 `/usr/local/etc/vsftpd/install_vsftpd.log`。

上面的文本告诉你，每当你对 `vsftpd` 进行更改时，必须运行 `restart_vsftpd`。通常，进程在向它们发送 `SIGHUP` 信号时会重新配置。

12. 你可以通过显示进程来查看 `vsftpd` 是否正在运行。输入 `ps ax| grep vsftpd`。你会看到类似下面的行：

```
15108 S< 0:00 vsftpd -d /usr/local/etc/vsftpd/general.conf /usr/local

15109 S< 0:00 vsftpd -d /usr/local/etc/vsftpd/general.conf /usr/local

15110 S< 0:00 vsftpd -d /usr/local/etc/vsftpd/general.conf /usr/local

15111 S< 0:00 vsftpd -d /usr/local/etc/vsftpd/general.conf /usr/local
```

## 第 15 章 Linux 网络

21. 现在以你的用户账户登录。首先，通过输入 `open localhost` 连接到 FTP 服务器。系统提示你输入用户名。输入你的用户名。（该用户账户必须已存在于系统中。）如果你的用户名是 `john`，你会看到以下内容：

```
User join okay, need password.

Password:
```

22. 输入用户账户的密码。如果你输入正确，你会看到以下内容：
```
- 你是允许的 50 个并发用户中的第 1 个。

- 匿名登录。

远程系统类型为 UNIX。

正在使用二进制模式传输文件。

ftp>
```

23. 因为你是以普通用户身份登录的，目录应该是用户的家目录。如果属的话，输入 `ls`。你会看到你在第 13 步中创建的 `save_the_whales` 文件。

```
-rw-r--r-- 1 john 0 Nov 17 10:20 save_the_whales
```
