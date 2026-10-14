
本节描述的变量控制远程过程控制 (RPC) 设置。RPC 被 NFS、PCFS 和 `dbbind` 等系统使用。更多信息请咨询 `/etc/rc.config` 文件。

- `USE_KERNEL_NFSD_NUMBER` - 指定 NFS 服务器线程数（默认 = `"4"`）

- `NFS_SERVER_UGID` - 将用户和组 ID (UID 和 GID) 映射到 NFS 服务器（默认 = `"no"`）

- `REEXPORT_NFS` - 决定导入的 NFS 目录是否导出（重导出）到其他客户端（默认 = `"no"`）

- `START_PCFSD` - 启动 PCNFS 守护进程，Windows、MS-DOS 和其他操作系统（非 UNIX）使用它来挂载 NFS 文件系统（默认 = `"no"`）

- `START_BWNFSD` - 由 PCNF 系统使用（默认 = `"no"`）

- `PCNFSD_LPSPOOL` - 设置 PCNFS 缓存目录（默认 = `/var/spool/lpd`）

- `START_RWHOD` - 在启动时启动 `rhod` 守护进程。`rhwod` 通常是一个安全隐患，在大多数情况下你不应该开启它（默认 = `"no"`）

- `RUN_UPDATEDB` - 设置后，`cron` 系统定期运行 `updatb` 系统。这可以使 `locate` 系统（用于在你的 SuSE Linux 盒上查找文件）保持最新（默认 = `"yes"`）

## 系统维护设置

以下守护进程更新或清理与系统相关的守护进程。

- `REINIT_MAND` - 设置后，`cron` 每天运行 `mand` 次（默认 = `"yes"`）

- `RUN_UPDATEDB_AS` - 如果运行 `updatb`可能会创建一个安全漏洞，因为它泄露了 root 之外任何人无法访问的目录和文件信息。如果不是 root，则 `locatedb` 不创建完整的数据库（默认 = `"nobody"`）

- `UPDATEDB_NETPATHS` - 此变量告诉 `updatb` 跳过列出的文件系统。设置此变量允许其扫描 NFS 挂载的文件系统（默认 = `""`）

- `UPDATEDB_PRUNEPATHS` - 此变量告诉 `updatb` 跳过列出的目录（默认 = `/usr /mnt /cdrom /tmp /usr/tmp /var/spool/proc`）（注：根据标准路径将 OCR 错误 `/S.u.S.E.` 修正为 `/usr`）

- `UPDATEDB_NEWUSER` - `RUN_UPDATEDB_AS`。设置远程守护进程的用户（默认 = `""`）

- `DELETE_OLD_CORE` - 设置后，允许 `cron` 删除旧的 `core` 文件。如果设置了此项，则必须设置 `RUN_UPDATEDB`（默认 = `"no"`）

- `MAX_DAYS_FOR_CORE` - 决定什么是“旧”`core` 文件（单位：天，默认 = `"7"`）

- `DELETE_OLD_CATMAN` - 设置后，`cron` 删除旧的格式 pages (`/var/catman`)（默认 = `"yes"`）

- `CATMAN_ATIME` - 决定什么是“旧”`catman` 文件（单位：天，默认 = `"7"`）

- `CREATE_INFO_DIR` - 设置后，Perl 脚本生成 `usr/info/dir` 文件（默认 = `"yes"`）

- `CHECK_PERMISSIONS` - 设置后，`SuSEConfig` 使用 `chstat` 实用检查 `/etc/permissions` 配置文件中设置的文件和目录的所有权。`"set"` 选项告诉 `chstat` 将所有权和权限改回 `/etc/permissions` 文件中设置的值。`"warn"` 选项让 `chstat` 提供有关异常文件/目录的信息（默认 = `"set"`）

- `PERMISSION_SECURITY` - 告诉 `chstat` 使用哪个版本的 `/etc/permissions` 文件。版本有：`permission`,`permission.easy`,`permission.local`,`permission.paranoid` 和 `permission.secure`。这些值应该是自俗易懂的（默认 = `"easy"`）

- `MAX_DAYS_FOR_LOG` - 设置保留的日志数量（默认 = `"365"`）

- `RPMDB_BACKUP_DIR` - 设置后，对 `rpm` 数据库进行备份（默认 = `/var/adm`）

- `MAX_DAYS_BACKUPS` - 设置备份的最大数量（默认 = `"5"`）

- `TMP_DIRS_TO_CLEAR` - 告诉 `cron` 删除什么（默认 = `/tmp`）

- `MAX_DAYS_KEEP` - 告诉 `cron` 保留什么（默认 = `"0"`）

- `CWD_IN_ROOT` - 设置当前工作路径（默认 = `/root`）

- `ROOT_LOGIN_REMOTE` - 允许远程登录 root（默认 = `"no"`）

- `PASSWD_USE_CRLIB` - 设置后，所有密码通过 `cracklib` 处理（默认 = `"no"`）

- `HOW_TO_HANDLE_LIBS` - 使用动态链接程序（默认 = `"link"`）

- `CHECK_INITAB` - 允许 `SuSEConfig` 修改 `itittab` 文件（默认 = yes）

- `DISPLAYMANAGER` - 设置显示管理器为 KDM、XDM 或控制台（非图形）（默认 = `"*"`）

- `CONSOLE_SHUTDOWN` - 设置 Ctrl+Alt+Del 的动作。选项有 `ignore`、`reboot` 或 `halt`（默认 = `"reboot"`）

- `START_NSCD` - 在启动时启动缓存进程。名称缓存会在内存中保留解析以便快速访问（默认 = `"no"`）

- `umask` - 设置系统 `umask`。`umask` 决定文件或目录继承的权限。更多信息请参 `man` 页（默认 = `"022"`）

- `PATH` - 用于 `/etc/init.d` 脚本和 `SuSEConfig` 的内部路径。不用于用户或 root 账户（默认 = `"/sbin:/bin:/usr/sbin:/bin"`）

## 启动脚本消息

以下变量格式启动过程中看到的输出。更多信息请查看 `/etc/rc.config` 文件中的注释。

- `UPDATE_GROFF_CONF` - 更新 `groff` 配置（默认 = `"yes"`）

- `GROFF_PAGES` - 设置 `groff` 页面大小（默认 = `"*"`）

- `CREATE_PERLLOCAL_POD` - 允许 `SuSEConfig` 修改 `perlocal.pod`（默认 = `"yes"`）

- `GENERATE_PERL_SYSTEM_INCLUDES` - 允许 `SuSEConfig` 运行。当你更改内核源码时，这是必要的（默认 = `"yes"`）

- `KERNEL_LOGLEVEL` - 设置 `klogd` 使用级别（默认 = `"1"`）

- `SYSLOG_PARAMS` - 设置 `syslog` 参数。有关 `syslog` 的更多信息请查看 `man` 页（默认 = `"*"`）

- `DHCLIENTEP` - 设置 DHCP 客户端的延迟。有时需要允许系统正确设置（默认 = `"1"`）

- `CONSOLE_FONT` - 在启动时设置控制台字体（默认 = `"*"`）

- `CONSOLE_SCREENMAP` - 为给字体设置屏幕映射（默认 = `"*"`）

- `CONSOLE_UNICODEMAP` - 为某些字体设置 Unicode 映射（默认 = `"*"`）

# 附录 D：`/etc/rc.config` 文件

- `DEFAULT_WM` – 设置默认窗口管理器为 KDE 或 GNOME（默认 = `"kde"`）

- `GMT` – 如果设置为 `"-u"`，则将系统时钟设为 GMT（默认 = `""`）

- `GPM_PARAM` – 设置 GPM 使用的鼠标类型，GPM 是基于文本的鼠标系统（默认 = `"-t ps2 -m /dev/mouse"`）

- `INITRD_MODULES` – 设置启动时的 `initrd` 模块（默认 `"usbcore"`）

- `KEYTABLE` – 设置控制台键盘映射的国家代码（默认 `"us.map.gz"`）

- `LANGUAGE` – 设置“旧版”YaST 的语言（默认 = `"english"`）

- `MOUSE` – 设置鼠标设备文件（默认 = `"/dev/psauxx"`）

- `NFS_SERVER` – 启动时启动 NFS 服务器（默认 = `"yes"`）

- `RC_LANG` – 设置“旧版”YaST 的语言（默认 = `"en_US"`）

- `START_GPM` – 启动时启动 GPM（默认 = `"yes"`）

- `START_INETD` – 当系统进入多用户运行级别 2 或以上时，启动 `inetd` 守护进程（默认 = `"yes"`）

- `START_PORTMAP` – 启动时启动 `portmap` 守护进程。对于 NIS 和 NFS 等 RPC 服务是必须的（默认 = `"yes"`）

- `START_USB` – 启动时启动通用总线（USB）（默认 = `"yes"`）

- `TIMEZONE` – 设置时区（默认 = `"US/Mountain"`）

# 本地配置变量

此节控制本地配置设置。详情请参阅 `"/etc/rc.config"` 注释。
