
### b. 在 `/etc/vsftpd/vsftpd.conf` 文件中，确保变量如下：
`anonymous_enable=YES`
`write_enable=YES`
`local_enable=YES`

### c. 对于 Fedora 或 RHEL 7，打开防火墙配置窗口并勾选服务下的 FTP。对于早期的 RHEL 和 Fedora 系统，通过在 `/etc/sysconfig/iptables` 文件中的 `DROP` 或 `REJECT` 规则之前添加以下规则来配置 iptables 防墙允许 TCP 端口 21 的新请求：
```bash
-A INPUT -m state --NEW -m tcp -p tcp --dport 21 -j ACCEPT
```

### d. 通过将相应的模块加载 `/etc/sysconfig/iptables-config` 文件来配置 iptables 防墙连接跟踪：
`IPTABLES_MODULES="nf_conrack"`

### e. 为了让 SELinux 上传到目录，首先正确设置文件上下文：
```bash
# seman fcontext -a -t public_content_rw_t "/var/ftp/in/(.*)"
# restorecon -F -R -v /var/ftp/in
```

### f. 接下来，设置 SELinux 布尔值允许上传：
```bash
# setsebool -P allow_content_ftp_anon_write
```

## 附录 B：练习答案

- g. 重启 `vsftpd` 服务（`service vsftpd restart` 或 `systemctl restart vsftpd.service`）。

- 8. 要安装 `lftp` FTP 客户端（如果你没有第二个 Linux 系统，请在运行 FTP 服务器的宿主机上安装 `lftp`）并将 `/etc/hosts` 文件上传到服务器上的 `incoming` 目录，请以 `root` 用户身份运行以下命令：
```
# yum install lftp
# lftp localhost
lftp localhost:/> cd in
lftp localhost:/in> put /etc/hosts
89 bytes transferred
lftp localhost:/in> quit
```
你将无法直接看到你已将 `hosts` 文件复制到 `incoming` 目录。但是，在运行 FTP 服务器的宿主机 shell 中输入以下内容以确保 `hosts` 文件存在那里：
```bash
# ls /var/ftpd/in hosts
```
如果你无法上传文件，请按照练习 7 中的描述排查故障，检查你的 `vsftpd.conf` 设置，并检查 `/var/ftpd/directory` 的所有权和权限。

- 9. 使用你选择的任何 FTP 工具，访问 `ftp://kernel.org` site 上的 `/pub/linux/docs/man-pages` 目录并列出目录内容。使用 `lftp` 客户端的操作如下：
```bash
# lftp ftp://kernel.org/pub/linux/docs/man-pages
cd ok, cwd=/pub/linux/docs/man-pages
kernel.org/pub/linux/docs/man-pages> ls
drwxr-xr-x 2 536 24756 May 10 2022 Archive
-rw-r--r-- 1 536 536 1135808 Feb 09 2023 man-pages-3.34.tar.bz
-rw-r--r-- 1 536 536 1674738 Feb 09 2023 man-pages-3.34.tar.gz
-rw-r--r-- 1 536 536 543 Feb 09 2023 man-pages-3.34.tar.sign
```

- 10. 使用你选择的任何 FTP 工具，将你访问的 `kernel.org` 目录下的 `man-pages-3.78.tar.gz` 下载到本地系统的 `/tmp` 目录。
```bash
# lftp ftp://kernel.org/pub/linux/docs/man-pages
cd ok, cwd=/pub/linux/docs/man-pages
lftp kernel.org:man-pages> get man-pages-3.78.tar.gz
1739208 bytes transferred in 4 seconds (481.0K/s)
lftp kernel.org:man-pages> quit
```

## 第 19 章：配置 Windows 文件共享 (Samba) 服务器

- 1. 要安装 `samba` 和 `samba-client` 包，请在本地系统的 shell 中以 `root` 输入以下内容：
```bash
# install samba samba-client
```

- 2. 要启动并启用 `smb` 和 `nmb` 服务，请在本地系统的 shell 中以 `root` 输入以下内容：
```bash
# systemctl enable smb.service
# systemctl start smb.service
# systemctl enable nmb.service
# systemctl start nmb.service
```
或者
```bash
# chconfig smb on
# service smb start
# chconfig nmb on
# service nmb start
```

- 3. 要将 Samba 服务器的工作组（`workgroup`）设置为 `TESTGROUP`，`netbios` 名称设置为 `MYTEST`，服务器字符串（`server string`）设置为 `Samba Test System`，请以 `root` 用户身份使用编辑器打开 `/etc/samba/smb.conf` 文件并修改三行使其如下：
```ini
workgroup = TESTGROUP
netbios name = MYTEST
server string = Samba Test System
```

- 4. 要向你的系统添加 Linux 用户 `phil` 并为 `phil` 添加 Linux Samba 和 `samba` 密码，请在 shell 中以 `root` 输入以下内容（务必记住你设置的密码）：
```bash
# useradd phil
# password phil
New password: *****
Retype password: *****
# smbpasswd -a phil
New SMB password: *****
Retype new SMB password: *****
Added user phil.
```

- 5. 要设置 `[homes]`，使主目录是可浏览的（`yes`）且可写的（`yes`），且 `phil` 是唯一的有效用户，请以 `root` 用户打开 `/etc/samba/smb.conf` 文件并修改 `[homes]` 节使其如下：
```ini
[homes]
comment = Home Directories
browseable = yes
writable = yes
valid users = phil
```

- 6. 要设置必要的 SELinux Boolean 使 `phil` 通过 Samba 客户端访问其主目录，请在 shell 中以 `root` 输入以下内容：
```bash
# setsebool -P samba_enable_dirs
```

- 7. 从本地系统，使用 `smbclient` 命令列出可用的 `homes`：
```bash
# smbclient -L localhost
Enter root's password:
<ENTER> Anonymous login
Domain=DATAGROUP OS=Unix Server=Samba 4.1.15 Share=homes Comment=Home Directories
```
