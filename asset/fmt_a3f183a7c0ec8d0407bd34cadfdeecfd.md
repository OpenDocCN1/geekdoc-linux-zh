
# echo "Welcome to your vsftpd server" > /var/ftp/test

- 6. 在运行 FTP 服务器的系统上，使用浏览器从匿名 FTP 主目录打开 test 文件，在地址栏中输入以下内容并按回车：

打开浏览器，输入以下内容并按回车：

```
ftp://localhost/test
```

浏览器窗口中应该出现“Welcome to your vsftpd server”文本。

- 7. 要从匿名 FTP 主目录访问 test 文件，请执行以下操作。（如果你无法访问该文件，请检查你的防火墙、SELinux 和 TCP wrappers 是否已配置为访问该文件，如本文此处所示。）

- a. 在网络中可以到达 FTP 服务器的系统上，在浏览器地址栏中输入以下内容（将 *host* 替换为系统的完全限定主机名或 IP 地址）：

```
ftp://host/test
```

如果你在浏览器窗口中看不到欢迎信息，请检查是什么阻止了访问。要临时关闭防火墙（刷新你的 iptables 规则），请在 FTP 服务器的 shell 中以 root 用户身份输入以下命令，然后再次尝试访问站点：

```
# iptables -F
```

- b. 要临时禁用 SELinux，输入以下内容然后再次尝试访问站点：

```
# setenforce 0
```

在你确定了导致 FTP 服务器上的文件不可用的原因后，回到第 18 章的“保护你的 FTP 服务器”部分，并按照步骤确定可能阻止访问你文件的因素。这些是可能的情况：

- c. 对于 iptables，确保服务器上有一条规则打开了 TCP 21 端口。

- d. 对于 SELinux，确保文件上下文被设置为 `public_content_t`。

# 附录 B：练习答案

- 8. 要配置你的 vsftpd 服务器允许匿名用户向名为 `in` 的目录上传文件，请在 FTP 服务器上以 root 身份执行以下操作：

- a. 在 `/var/ftp/` 下创建 `in` 目录

```
# mkdir /var/ftp/in
# chown ftp:ftp /var/ftp/in
# chmod 777 /var/ftp/in
```

- b. 对于较新的 Fedora 或 RHEL，打开防火墙配置窗口并勾选服务下的 FTP 框以访问你的 FTP 服务。对于较早的 RHEL 和 Fedora 系统，通过在 `/etc/sysconfig/iptables` 中的某个 DROP 或 REJECT 规则之前的某处添加以下规则，来配置你的 iptables 防火墙允许在 TCP 21 端口上接收新请求：

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 21
-j ACCEPT
```

- c. 通过加载相应的模块到 `/etc/sysconfig/iptables-config` 来配置你的 iptables 防火墙连接：

```
IPTABLES_MODULE="nf_conntrack_ftp"
```

- d. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

- e. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

- f. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

- g. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

- h. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

- i. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

- j. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

- k. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

- l. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

- m. 对于 SELinux 允许上传到目录，首先使用以下命令：

```
semanage fcontext -a -t public_content_t "/var/ftp/in(/.*)?"
restorecon -Rv /var/ftp/in
```

# 第七部分：附录

d. 出现提示时，选择“注册用户”（Registered User），输入 phil 作为用户名，输入网域 (TESTGROUP)，并输入 phil 的密码。

e. 打开另一个 Nautilus（企文件管理器）窗口，并将一个文件拖入 phil 的家目录（homes folder）。

9. 要打开防火墙，以便任何可以访问服务器的人都能访问 Samba 服务（smbd 和 nmbd 进程），你只需打开“防火墙配置”（Firewall Configuration）窗口并勾选 samba 和 samba-client 复选框（针对“运行时”和“永久”设置）。如果你的系统使用 iptables，请修改 `/etc/sysconfig/iptables` 文件，使防火墙显示如下（你是在那些加粗部分中添加的内容）：

```
*filter
:INPUT [0:0]
:FORWARD [0:0]
:OUTPUT [0:0]
- INPUT -m state --state ESTABLISHED, RELATED -j ACCEPT
- INPUT -p icmp -j ACCEPT
- INPUT -i lo -j ACCEPT
- INPUT -m state --state NEW -m udp -p udp --dport 1377 -j ACCEPT
- INPUT -m state --state NEW -m udp -p udp --dport 1378 -j ACCEPT
- INPUT -m state --state NEW -m tcp -p tcp --dport 139 -j ACCEPT
- INPUT -m state --state NEW -m tcp -p tcp --dport 445 -j ACCEPT
- FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT
```

然后输入以下规则进行重新加载：

```
# service iptables restart
```

10. 要从网络上的另一个系统（Windows 或 Linux）以用户 phil 的身份再次打开 homes 共享，并确保你可以向其拖放文件，请执行以下操作：

+ a. 这一步只是重复之前描述的内容，或者是访问 Windows 资源管理器窗口并打开该共享（通过选择“网络”，然后选择 Samba 服务器）。技巧在于确保该服务已通过 Nautilus 服务器功能可用。

+ b. 如果你无法访问 Samba 共享，尝试禁用你的防火墙并禁用 SELinux。当你关闭其中任何一个服务时，共享将变为可访问，此时返回并调试无法工作的服务问题：

```
# setforce 0
# service iptables stop
```
