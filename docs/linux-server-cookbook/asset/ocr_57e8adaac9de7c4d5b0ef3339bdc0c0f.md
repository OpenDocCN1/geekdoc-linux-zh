| nice | max nice priority allowed to raise to values: [-20, 19] |
| --- | --- |
| rtprio | max realtime priority |

![](bbox=[0.32, 0.15, 0.68, 0.17])

A user can check the limits applied using the command **ulimit**, as is shown in [figure 6.56:]:

```
agonzalez@ubuntu:~$ ulimit -a
    real-time non-blocking time  (microseconds, -R) unlimited
    core file size          (blocks, -c) 0
    data seg size           (kbytes, -d) unlimited
    scheduling priority             (-e) 0
    file size               (blocks, -f) unlimited
    pending signals             (-i) 15251
    max locked memory       (kbytes, -l) 502268
    max memory size         (kbytes, -m) unlimited
    open files                   (-n) 1024
    pipe size            (512 bytes, -p) 8
    POSIX message queues     (bytes, -q) 819200
    real-time priority             (-r) 0
    stack size              (kbytes, -s) 8192
    cpu time               (seconds, -t) unlimited
    max user processes              (-u) 15251
    virtual memory          (kbytes, -v) unlimited
    file locks                      (-X) unlimited
```

![](bbox=[0.33, 0.6, 0.67, 0.62])

In [figure 6.57:], an administrator limits the number of user processes can have. Users can set their own limits with the built-in shell command called **ulimit**, but always set a value lower than the default or the specific one for that user:

```
root@ubuntu:~# echo "agonzalez          hard  nproc     10" >> /etc/security/limits.conf
root@ubuntu:~# su - agonzalez
agonzalez@ubuntu:~$ ulimit -u
10

agonzalez@ubuntu:~$
agonzalez@ubuntu:~$ ulimit -u 5
agonzalez@ubuntu:~$ ulimit -u
5
```

![](bbox=[0.29, 0.83, 0.71, 0.84])

If the user, after setting its own limit to five processes, tries to run more than that number, they will receive the error, as shown in [figure 6.58:]: