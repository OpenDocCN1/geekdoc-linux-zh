
列表9-2 显示我从 Red Hat 系统登录我的 Windows PC。我被提示输入密码，然后获得了有关 Windows 系统的信息。你可以在提示符处输入`help`来获取可能的命令列表。`smb`提示符下的命令与命令行`ftp`命令非常相似。要退出连接，输入`exit`。

另一种让 Samba 客户端上的文件在你的 Red Linux 系统上可访问的方法是将客户端文件系统挂载到你的文件系统上。你可以使用`smbmount`命令执行此操作。该命令的语法为：

```
smbmount //computer name/directory /system_mount_point
```

该命令及其输出示例如下：

```
[root@terry]# smbmount //terry/c /mnt/windows
Password:
[root@terry]# cd /mnt/windows
```

## 第 9 章：使用 Samba 连接 Windows PC

```bash
[root@terry windows]# ls
aclder.exe MSDOS.SYS quicktime
arcset.exe Muhnlet Setup QuickTimeInstaller.zip
AUTOEXEC.BAT My Download Files Recycled
boot.ini My Music rhss
camatia NALCache W2K.CD
CONFIG.SYS netplus Windows Update System Files
Documents and Settings Novell WINNT
Drivers NTDTECT.COM WSMOREITE.ID
fgc ntdlr WT61CE.OWL
hyberfil.sys 2.pdf WT6102.OWL
IO.SYS pagefile.sys WT6103.OWL
config.aat Program Files WT61US.OWL
Local Mhunt PUTTTY,.ND
```

在这个示例中，我正在连接到与上一个示例中相同的 Windows PC。但是，通过使用`smbount`命令，我正将 Windows 文件系统挂载到我的 Red Hat Linux 系统上。在输入 Windows PC 的密码并返回命令行提示符后，我切换到刚刚挂载的目录并运行`ls`命令以获取所挂载的 Windows 共享目录的目录列表。现在，我可以通过常规的文件系统工具在两个系统之间轻松移动文件。我可以将这些信息放入`/etc/fstab`文件中，这样在需要时系统启动时就会挂载这些目录。

要卸载客户端文件系统，请输入`smbount`命令和要卸载的目录路径，如下：

```bash
# smbount /mnt/windows
```
