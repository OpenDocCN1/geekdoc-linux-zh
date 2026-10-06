# 92 | Master of Linux Commands

There are two basic commands in linux system we use to copy and move files. These are cp and mv commands. Cp command is used for copying, the mv command is used for moving.

# Cp

As the copy command, using the form of cp command is as cp <source> <target>. So, for example, to copy the fileA to another location on the fileB name file we use the cp fileA fileB command.

Let's see it with an application. For example, I want to copy testA under zeyno directory (folder) to use /home directory as testB name. For this I need to use cp zeyno/testA /home/testB

```
root@kemal:~# cp zeyno/testA /home/testB
root@kemal:~# cd /home
root@kemal:/home# ls -l testB
-rw-r--r-- 1 root root 0 Kas 15 23:42 testB
```

If you think that you are not careful, you can use cp command -i. So if you have an old file of the same name, you receive a warning before writing on it (interactive). Data copying occurs with your confirmation.

```
root@kemal:~# cp -i zeyno/testA /home/testB
cp: `/home/testB' üzerine yazılsın mı?n
root@kemal:~# _
```

For example, when working in zeyno directory, to copy sample, test and testA files under /home/zeynep directory, we can use cp sample test testA /home/zeynep command.

![](bbox=[0.487, 0.923, 0.503, 0.943])