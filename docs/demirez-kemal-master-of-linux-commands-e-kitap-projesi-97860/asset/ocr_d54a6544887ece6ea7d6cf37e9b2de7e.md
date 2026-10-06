```
root@kemal:~# cat sample.txt
Linux commands
linux commands
LiNu commands
linuxX commands
root@kemal:~# sed "s/com/(COM)/g" sample.txt
Linux (COM)mands
linux (COM)mands
LiNu (COM)mands
linuxX (COM)mands
root@kemal:~# _
```

Let's see what we can use to delete all uppercase characters in a file. For example to delete all the uppercase characters from our file with named list we need to use sed "s/[A-Z]//g" list command.

```
root@kemal:~# cat list
AnKARA, IStanBUL, NewYork, HACKEr
root@kemal:~# sed "s/[A-Z]//g" list
nra, tanu, ework, r
root@kemal:~# _
```

To delete everything except uppercase letters, we can use sed "s/[^A-Z]//g" list command.

```
root@kemal:~# cat list
AnKARA, IStanBUL, NewYork, HACKEr
root@kemal:~# sed "s/[^A-Z]//g" list
AKAISBLNYHACKE
root@kemal:~# _
```

If you want to delete everything except lowercase letters and numbers in the file, this time we use sed "s/[^1-9a-z]//g" list command.