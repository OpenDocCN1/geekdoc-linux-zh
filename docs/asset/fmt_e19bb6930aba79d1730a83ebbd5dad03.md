
## 编辑 exports 文件

编辑 `/etc/exports` 文件（`vi /etc/exports`）并添加：

示例：

```
/dir/export host1.mydomain.com(ro, squash)

/dir/export host2.mydomain.com(ro, squash)
```

`dir/to/export` 是你想要导出的目录，`host#.mydomain.com` 是允许登录该目录的机器，`<ro>` 选项意味着只读，`<root_squash>` 选项表示在该目录下不允许 root 写入。

要使此更改生效，你需要在终端上运行以下命令：

```
[root@deep]# /usr/sbin/exportfs -a
```

注意：请注意，在系统上提供 NFS 服务可能会带来安全风险。个人而言，我不推荐使用它。

## 8. 禁用控制台程序访问

© Copyright 1999-2000 Gerhard Maurani and Open Network Architecture ®

80

关于本书的意见和建议请邮寄至 `gmourani@videotron.ca`

在一个安全的环境中，如果我们确定控制台是（因为设置了 BIOS 和 LILO 密码，并且系统上所有的物理电源和重启开关都可用），那么对于服务器上的普通用户，完全禁用控制台等程序的访问是有益的。

要这样做，请运行以下命令：

```
root@deep]$# rm -f /etc/security/console.apps/<servicename>
```

其中 `<servicename>` 是你想要禁用控制台等访问的程序名称。但是，除非你使用 x，否则请不要删除 xserver 文件，否则将人无法启动 X server。（如果你使用 xdm 启动 X server，那么它是唯一需要启动 x 的用户，在这种情况下，你可能真的想删除 xserver 文件）。

示例：

```
root@deep]$# rm -f /etc/security/console.apps/halt

root@deep]$# rm -f /etc/security/console.apps/poweroff

root@deep]$# rm -f /etc/security/console.apps/reboot

root@deep]$# rm -f /etc/security/console.apps/shutdown

root@deep]$# rm -f /etc/security/console.apps/xserver
```
如果删除，root 将是唯一能启动 X 的用户。

这将禁用 `halt`、`poweroff`、`reboot` 和 `shutdown` 程序的控制台等访问。再次强调，如果你遵循我们的设置，你的服务器上没有安装 Xwindow 界面，且上述所有文件将不会出现在 `/etc/security/` 目录中，因此请忽略上述步骤。

## 9. 禁用控制台访问

以下脚本将为你解决问题。以“root”身份创建一个 `disabling.sh` 文件（`touch disabling.sh`）并添加以下行：

```bash
#!/bin/sh
for i in /etc/pam.d/* do
sed '/^.*/pam_console.so/#/' $i
done
```

使用以下命令使脚本具有可执行权限并执行它：

```
root@deep]$# chmod 700 disabling.sh

root@deep]$# ./disabling.sh
```

这将注释掉 `"/etc/pam.d/"` 下所有文件中引用 `"pam_console.so"` 的行。脚本已执行，你可以从系统中将其删除。

## 10. "/inetd.conf" 文件

关于本书的意见和建议请邮寄至 `gmouraani@videotron.ca`

Inetd，也称为“超级服务器”，它会根据请求加载网络程序。`inetd.conf` 文件告诉 `inetd` 监听哪些端口以及为每个端口启动什么。当你的 Linux 系统连接到任何网络时，首先要查看的是你需要提供哪些服务。不需要的服务应该被禁用，这样你就会少担心。查看 `"/inetd.conf"` 文件，通过注释掉（在行开头添加 `#`）你不需要的服务，并向 `inetd` 发送 `SIGHUP` 命令来更新 `inetd.conf`。

### 第 1 步

将文件的权限更改 600。

```
[root@deep]$# chmod 600 /etc/inetd.conf
```

### 第 2 步

确保所有者是 root。

```
[root@deep]$# stat /etc/inetd.conf
File: inetd.conf
Size: 2869 Filetype: File
Mode: 0600(rw----) Uid: (0/ root) Gid: (0/ root)
Device: 8,0 Inode: 18219 Links: 1
Access: Sep 22 10:24 1999
Modify: Mon 20 10:22 1999
Change: Mon 20 10:22 1999
```

### 第 3 步

编辑 `inetd.conf` 文件（`vi /etc/inetd.conf`）并禁用你计划使用的服务：`ftp`, `telnet`, `talk`, `imap`, `pop-2`, `pop-3`, `finger`, `auth` 等。

要重新读取此文件的更改，只需执行 `killall -HUP inetd`。
