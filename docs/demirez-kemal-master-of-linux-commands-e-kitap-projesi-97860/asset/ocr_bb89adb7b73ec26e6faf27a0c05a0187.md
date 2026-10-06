# 206 | Master of Linux Commands

```
root@kemal:~# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:~# awk '{print $1}'
Linux
Kali
Ethical
CentOS
RedHat
root@kemal:~# _
```

If there is ": between the expressions in lieu of space, we should use awk -F point:

```
root@kemal:~# cat personal
Ali:312:Ankara
Veli:212:İstanbul
Kemal:232:İzmir
root@kemal:~# awk '{print $1}' personal
Ali:312:Ankara
Veli:212:İstanbul
Kemal:232:İzmir
root@kemal:~# awk -F: '{print $1}' personal
Ali
Veli
Kemal
root@kemal:~# _
```

As you can see, '{print $1}' personal could not get the result we wanted. We used awk -F: '{print $1}' personal since ":" is used as seperator.

To see the phrases in reserved areas, for example to see the phrases in first and third areas, '{print $1,$S3}' command should be used, If you forgot to put comma between $1 and $3, all the expressions will be showed alongside eachother.