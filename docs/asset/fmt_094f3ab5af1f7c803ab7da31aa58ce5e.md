
In Fedora and SUSE, you can turn stand-alone servers on and off by using the `systemctl` command. You can get the names of the service scripts by typing `ls /etc/init.d`. Then you can turn off a service (such as Samba) by typing `sudo systemctl stop smb`. If the service was already running, type `/etc/init.d/smb stop` to stop the service. You can run scripts from the `/etc/init.d` directory with the `stop` argument to stop any service in a similar manner.

### Configuring the Internet super server

In addition to stand-alone servers such as web and mail servers, the servers `inetd` and `xinetd` servers have to be configured separately. These servers are *Internet super servers* because they can start other servers on demand.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_414_1.png)

Type `ps ax | grep inetd` to see which Internet super server — `inetd` or `xinetd` — your system runs.

Debian and Ubuntu use `inetd`, and Fedora and SUSE use `xinetd`.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_414_2.png)

The `inetd` server is configured through the `/etc/inetd.conf` file. You can disable a service by locating the appropriate line in that file and commenting it out by placing a pound sign (`#`) at the beginning of the line. After saving the configuration file, type `/etc/init.d/inetd restart` to restart the `inetd` server.

Configuring the `xinetd` server is a bit more complicated. The `xinetd` server reads a configuration file named `/etc/xinetd.conf` at startup. This file in turn refers to configuration files stored in the `/etc/xinetd.d` directory. The configuration files in `/etc/xinetd.d` tell `xinetd` which ports to listen to and which server to start for each port. Type `ls /etc/xinetd.d` to see a list of the files in the `/etc/xinetd.d` directory on your system. Each file represents a service that `xinetd` can start. To turn off any of these services, edit the file in a text editor, and add a `disable = yes` line in the file. After you make any changes in the `xinetd` configuration files, you must restart the `xinetd` server; otherwise, the changes don’t take effect. To restart the `xinetd` server, type `/etc/init.d/xinetd restart`. This command stops the `xinetd` server and then starts it again. When the server restarts, it reads the configuration files, and the changes take effect.

### Configuring TCP wrapper security

A common security feature of `inetd` and `xinetd` is their use of the TCP wrapper to start various services. The *TCP wrapper* is a block of code that provides an access-control facility for Internet services, acting like a protective package for your message. The TCP wrapper can start other services, such as FTP and Telnet, but before starting a service, it consults the `/etc/hosts.allow` file to see whether

请求服务的 主机 允许使用该服务。如果 `/etc/hosts.allow` 中没有关于该主机的任何内容，TCP 包装器会检查 `/etc/hosts.deny` 文件以查看是否拒绝该服务。如果两个文件都为空，TCP 包装器会提供对所请求服务的访问。

以下是收紧 `inetd` 或 `xinetd` 配置启动的服务访问权限需要遵循的步骤：

- 1. **使用文本编辑器编辑 `/etc/hosts.deny` 文件，并向该文件添加以下行：**

```
ALL : ALL
```

此设置拒绝所有主机访问系统上的任何 Internet 服务。

- 2. **编辑 `/etc/hosts.allow` 文件并向其中添加可以访问系统上服务的 主机名称。**

若要仅允许来自 192.168.1.0 网络和本地主机（IP地址 127.0.0.1）的 主机访问系统上的服务，请在 `/etc/hosts.allow` 文件中放置以下行：

```
ALL : 192.168.1.0/255.255.255.0 127.0.0.1
```

- 3. **如果您想允许特定远程主机访问特定 Internet 服务，请使用以下语法作为 `/etc/hosts.allow` 中的一行：**

`server_program_name: hosts`

这里，`server_program_name` 是服务器程序的名称，而 `hosts` 是可以访问该服务的 主机的以逗号分隔的列表。您也可以将 `hosts` 输入为网络地址或整个域名，例如 `.mycompany.com`。

## 使用安全 Shell 进行远程登录

Linux 附带 Open Secure Shell（OpenSSH）软件，这是一套程序，提供对 Berkeley r 命令的 安全替代：`rlogin`（远程登录）、`rsh`（远程 shell）和 `rcp`（远程复制）。OpenSSH 使用公钥加密来验证用户身份并加密两个主机之间的通信，以便用户可以安全地从远程系统登录并安全地复制文件。

本节简要描述了在 Linux 中使用 OpenSSH 软件的方法。要了解有关 OpenSSH 的更多信息并阅读其最新新闻，请访问 `www.openssh.com` 或 `www.openssh.org`。

OpenSSH 软件在 Linux 安装期间安装。表 2-2 列出了 OpenSSH 软件的主要组件。

### 表 2-2 OpenSSH 软件的组件

| 组件 | 描述 |
|---|---|
| `/usr/sbin/sshd` | 如果希望远程系统上的用户能够使用 ssh 客户端安全登录，则此 SSH 守护进程必须在主机上运行。当来自 ssh 客户端的连接到达时，`sshd` 使用公钥加密进行身份验证并与 ssh 客户端建立加密通信链路。 |
