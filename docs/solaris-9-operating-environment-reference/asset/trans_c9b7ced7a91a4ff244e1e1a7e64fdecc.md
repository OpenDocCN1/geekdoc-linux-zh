

# 配置文件

# 1127

```
/usr/sbin/lpsut uid=lp
/usr/bin/cancel uid=0
/usr/bin/disable uid=lp
/usr/sbin/reject uid=lp
/usr/sbin/lpforms uid=lp
/usr/ucb/lprm uid=0
/usr/bin/enable uid=lp
/usr/sbin/lusers uid=lp
Cron 管理:
/etc/init.d/cron uid=0, gid=sys
/usr/bin/crontab uid=0
设备管理:
/usr/sbin/allocate uid=0
/usr/sbin/deallocate uid=0
文件系统管理:
/usr/sbin/mount uid=0
/usr/sbin/dfshares uid=0
/usr/sbin/format uid=0
/usr/sbin/devinfo uid=0
/usr/sbin/mkfs uid=0
/etc/init.d/standardmounts uid=0, gid=sys
/usr/sbin/shareall uid=0, gid=root
/usr/sbin/clir uid=0
/usr/bin/rmdir uid=0
/usr/lib/autofs/automountd uid=0
/usr/sbin/unshare uid=0, gid=root
/etc/init.d/buildmtab uid=0, gid=sys
/usr/lib/fs/autofs/automount uid=0
/usr/sbin/share uid=0, gid=root
/usr/bin/mkdir uid=0
/usr/lib/fs/ufs/tunef uid=0
/usr/sbin/fstype uid=0
/usr/sbin/ff uid=0
/usr/sbin/fuser uid=0
/usr/sbin/fsck uid=0
/usr/bin/eject uid=0
/usr/sbin/umountall uid=0
/usr/sbin/mountall uid=0
/usr/sbin/unshare uid=0, gid=root
/etc/init.d/ufs_quota uid=0, gid=sys
/usr/sbin/fsdb uid=0
/usr/lib/fs/ufs/newfs uid=0
/usr/lib/fs/ufs/fsirand uid=0
/usr/sbin/swap uid=0
/usr/sbin/umount uid=0
/etc/init.d/autofs uid=0, gid=sys
/usr/lib/bin/nfs/showmount uid=0
/usr/sbin/mkfile uid=0
/usr/sbin/dfmounts uid=0
邮件管理:
/usr/bin/mconnect uid=0
/usr/bin/sendmail uid=0
/usr/bin/mailq uid=0
/usr/bin/newaliases uid=0
```

/etc/init.d/sendmail uid=0, gid=sys
维护与修复:
/etc/init.d/syslog uid=0, gid=sys
/usr/sbin/syslogd de=0
/usr/sbin/init de=0
/usr/sbin/halt de=0
/usr/sbin/prtconf de=0
/usr/sbin/poweroff uid=0
/usr/bin/ldd de=0
/usr/sbin/eeprom de=0
/usr/sbin/adb de=0
/usr/sbin/reboot uid=0
/usr/bin/date de=0
/etc/init.d/syset uid=0, gid=sys
/usr/bin/vmstat de=0
/usr/sbin/crash de=0
媒体备份:
/usr/sbin/mt de=0
/usr/sbin/tar de=0
/usr/lib/fs/ufs/ufsdump uid=0, gid=sys
媒体恢复:
/usr/sbin/tar de=0
/usr/sbin/cpio de=0
/usr/sbin/mt de=0
/usr/lib/fs/ufs/ufsrestore uid=0
名称服务管理:
/usr/lib/nis/nisping de=0
/usr/lib/nis/nishowcache de=0
/usr/sbin/nscd de=0
/usr/sbin/nislin de=0
/usr/lib/nis/nisctl de=0
/usr/bin/nischttl de=0
/usr/lib/nis/nisstat de=0
网络管理:
/usr/sbin/in.named de=0
/usr/sbin/nscd de=0
/etc/init.d/init uid=0, gid=sys
/etc/init.d/inetvsc uid=0, gid=sys
/usr/sbin/ruptime de=0
/usr/sbin/spray de=0
/usr/sbin/ifconfig de=0
/usr/bin/rup de=0
/etc/init.d/ducp uid=0, gid=sys
/etc/init.d/inetinit uid=0, gid=sys
/etc/init.d/rpc de=0
/usr/sbin/netstat de=0
/etc/init.d/asppd uid=0, gid=sys
/etc/init.d/sysid uid=0, gid=sys
/usr/sbin/asppp2ppd de=0
/etc/init.d/sysid.sys uid=0, gid=sys
/usr/sbin/route de=0
/usr/bin/setname de=0
对象访问管理:
/usr/bin/chmod de=0
```

profiles

```
/usr/bin/getfacl   =0
/usr/bin/chgrp      =0
/usr/bin/setfacl    =0
/usr/bin/chown       =0
进程管理:
/usr/bin/crontab     =0
/usr/bin/pmap        =0
/usr/bin/truss       =0
/usr/bin/psig        =0
/etc/init.d/perf     uid=0, gid=sys
/usr/bin/pstop       =0
/usr/bin/prun        =0
/usr/bin/nice        =0
/usr/bin/renice      =0
/etc/init.d/power    =0
/etc/init.d/cvc       uid=0, gid=root
/usr/bin/pfiles      =0
/usr/bin/pstack      =0
/usr/bin/fuser       =0
/usr/bin/pdwx        =0
/usr/bin/pldd        =0
/usr/bin/pcred       =0
/usr/bin/plags       =0
/usr/bin/ps          =0
/usr/bin/kill        =0
/etc/init.d/cron      uid=0, gid=sys
/usr/bin/pwait       =0
/usr/bin/ptime       =0
/usr/bin/ptree       =0
软件安装:
/usr/bin/pkgprogram   uid=0
/usr/bin/pkgtrans    =0
/usr/bin/install     =0
/usr/bin/pkgm        =0
/usr/bin/pkgkgrm       uid=0, gid=bin
/usr/bin/pkginfo     =0
/usr/bin/pkgadd      uid=0, gid=bin
/usr/bin/pkgmv       uid=0, gid=bin
/usr/bin/ccs/make    =0
/usr/bin/pkgchk      =0
/usr/bin/admintool  uid=0, gid=bin
/usr/bin/pkgchk      =0
/usr/bin/admintool  uid=0, gid=bin
/usr/bin/pkgchk      =0
/usr/bin/pkgtrans    =0
/usr/bin/pkgm       =0
/etc/init.d/cron      uid=0, gid=sys
All:
```

