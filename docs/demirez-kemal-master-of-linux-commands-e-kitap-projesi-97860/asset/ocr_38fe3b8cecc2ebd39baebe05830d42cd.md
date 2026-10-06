```
root@kemal:-# file /var/run/utmp
/var/run/utmp: data
root@kemal:-# strings /var/run/utmp
reboot
4.0.0-kali-686-pae
tty1
tty1LOGIN
runlevel
4.0.0-kali-686-pae
root
pts/0
root
,;RV;
pts/1
root
(unknown)
ARV
root@kemal:-# _
```

Above we've listed string expressions in the the utmp file. Likewise, to see strings in the wtmp file strings /var/log/wtmp command can be used.