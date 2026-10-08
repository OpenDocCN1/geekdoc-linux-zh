+   4. To list files with similar names but a field that covers a range,  
you could do the following:

```
$ ls libddd9873[5-6].sl
libddd98735.sl libddd98736.sl
```

+   5. To list files that start with "ux," and have the extension "300"
or "700," you could do the following:

```
$ ls ux*.\{700,300\}
uxboot1f.700 uxinstd.300
```

+   6. To list the files in your home directory, you could use ~:

```
$ ls -a ~
.	.cshrc.org .login	.shrc.org
..	.exrc	.login.org .cshrc
.history
```

+   7. To list the files in the home directory of a user, you can do the  
following:

```
$ ls -a ~gene
.	.history	.splinedat under.des
..	.login	traxl.txt xtra.part
.cshrc	.login.org ESP-File
.cshrc.org .profile Mail
.exrc	.shrc.org opt
```

![](bbox=[0.88, 0.11, 0.98, 0.19])

Many of these techniques are useful when writing shell scripts,  
so become familiar with file name expansion.