```
root@kemal:~# runlevel
N 5
root@kemal:~# _
```

Each work level has a folder where the scripts located to launch of the service and terminate the services. These directories found in /etc directory and have rcX.d format (X = operating level).

```
rc0.d
rc1.d
rc2.d
rc3.d
rc4.d
rc5.d
rc6.d
rc.local
rc5.d
```

Files in this directory beginning with K, indicate the services which will stop working when switching to this level. The files starting with S indicates the services which will be executed when switching to operational levels.

```
root@kemal:/etc/rc5.d# ls
K1apache S01openven2
K1atftpd S01redsocks S01rsyslog
K1beef-wss S01whod S01thin
K1bluetooth S01samba-ad-dc S01luuid
K1darkstat S01mbd S02anacron
K1dns2tcp S1nmspd S02arpwatch
K1oldradis S1ssh S02atd
K1lexim4 S1lsh S02cron
K1lined S02avahi-daemon S02dbus
K1miredo K2mysql S02gdom
K1nmbd K2postgresql S02irqbalance
K1ntp README
K1openbsd-inetd S01binfmt-support S02redis-server
root@kemal:/etc/rc5.d#
```