
1 profiles are in complain mode.

Out of 69 processes running:

5 processes have profiles defined.

5 processes have profiles in enforce mode.

0 processes have profiles in complain mode.

为了强调一点，即在重启 AppArmor 后，进程需要重启才能再次被限制，请看以下示例：

```
dal0:~# rcapparmor stop

Unloading AppArmor profiles                     done

dal0:~# rcapparmor start

Loading AppArmor profiles                       done

dal0:~# rcapparmor status

apparmor module is loaded.

50 profiles are loaded.

49 profiles are in enforce mode.

1 profiles are in complain mode.

Out of 62 processes running:

0 processes have profiles defined.

0 processes have profiles in enforce mode.

0 processes have profiles in complain mode.
```

重启其中一个有配置文件的进程会改变 `rcapparmor status` 的输出：

```
dal0:~# rcnscd restart

Shutting down Name Service Cache Daemon          done

Starting Name Service Cache Daemon               done

dal0:~# rcapparmor status

apparmor module is loaded.

50 profiles are loaded.

49 profiles are in enforce mode.

1 profiles are in complain mode.

Out of 62 processes running:

1 processes have profiles defined.

1 processes have profiles in enforce mode.

0 processes have profiles in complain mode.
```

AppArmor 的输出不包含有关被限制的配置文件或进程的具体数据。

已加载的配置文件列表保存在 `/sys/kernel/security/apparmor/profiles` 中。它可能如下所示：

```
dal0:~# cat /sys/kernel/security/apparmor/profiles

/usr/sbin/traceroute (enforce)

/usr/sbin/squid (enforce)

/usr/sbin/sendmail (enforce)

/usr/sbin/postqueue (enforce)

...

/usr/lib/postfix/bounce (enforce)

/usr/lib/firefox/firefox.sh (complain)

/usr/bin/ld (enforce)

...
```

命令 `unconfined` 列出具有绑定套接字但未加载配置文件的进程：

```
dal0:~# unconfined

2659 /sbin/portmap not confined

2659 /sbin/portmap not confined

2694 /usr/lib/zmd/zmd-bin not confined

2756 /usr/sbin/slpd not confined

2756 /usr/sbin/slpd not confined

2756 /usr/sbin/slpd not confined

2756 /usr/sbin/slpd not confined

2756 /usr/sbin/slpd not confined

2756 /usr/sbin/slpd not confined

2756 /usr/sbin/slpd not confined

2831 /usr/sbin/cuped not confined

2831 /usr/sbin/cuped not confined

2874 /usr/sbin/sshd not confined

2905 /usr/sbin/sshd not confined

2905 /usr/sbin/sshd not confined

3040 /usr/lib/postfix/master not confined

3040 /usr/lib/postfix/master not confined
```
