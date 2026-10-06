```
root@kemal:~# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:~# sed "y/ieg/IEG/" test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
REdHat SystEm Mng.
root@kemal:~# _
```

Finally, let's make an example taking commands from a file
 work on them. Let's type y/ieg/IEG/ and in a text file and
save it as change.sed. Then use sed -f change.sed test
command to make changes in our test file.

```
root@kemal:~# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:~# cat change.sed
y/ieg/IEG/
root@kemal:~# sed -f change.sed test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
REdHat SystEm Mng.
root@kemal:~# _
```