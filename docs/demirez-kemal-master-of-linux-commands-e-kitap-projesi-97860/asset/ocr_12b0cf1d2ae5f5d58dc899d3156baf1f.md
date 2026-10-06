Let's continue with another example. If you want to delete the first two letters on all the lines in the file we can use sed "s/../" test command such.

```
root@kemal:~# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:~# sed "s/../"
nux BackTrack 5
li Linux 2.0
hical Hacking
tntOS
dhat System Mng.
root@kemal:~# _
```

We can do multiple selection by using square brackets. There is a sample script to use about it below.

```
root@kemal:~# cat sample.txt
Linux commands
linux commands
LiNu commands
LiNu commands
root@kemal:~# sed "s/[Ll]inu[XX]/LINUX/g" sample.txt
LINUX commands
LINUX commands
LiNu commands
LINUX commands
root@kemal:~# _
```

We want to say with the command above: Replace all phrases start with L or l and end with x or X characters with LINUX.

If you want to specify the changes made to the text taking place between the parentheses, you can use sed "s/com/(COM)/g" sample.txt command. For example, if we will continue the previous example