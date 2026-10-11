This is not to say that the missing file problem is solved, just that no file verification was performed.

# 6.3.9. -v: Display Additional Information

Although RPM won’t report an error with the command syntax if you include the -v option, you won’t see much in the way of additional output:

```
# rpm -Vv bash
#
```

Even if there are verification errors, adding -v won’t change the output:

```
# rpm -Vv apmd
S.5....T /etc/rc.d/init.d/apmd
S.5....T /usr/X11R6/bin/xapmd
#
```

The only time that the -v option will produce output is when the package being verified has a verification script. Any normal output from the script won’t be displayed by RPM when run without -v (note that failure messages will always be displayed):

```
# rpm -V bother
#
```

But when -v is added, the script’s non-error-related output is displayed:

```
# rpm -Vv bother
This is the bother 3.5 verification script
#
```

# 6.3.10. -vv: Display Debugging Information

Sometimes it’s necessary to have even more information than we can get with -v. By adding another v, that’s just what we’ll get:

```
# rpm -Vvv rpm
D: opening database in /var/lib/rpm/
D: verifying record number 2341208
D: dependencies: looking for libz.so.1
D: dependencies: looking for libdb.so.2
D: dependencies: looking for libc.so.5
#
```

The lines starting with D: have been added by using -vv. We can see where the RPM database is located and what record number contains information on the rpm-2.3-1 package. Following that is the list of dependencies that the rpm package requires.

In the vast majority of cases, it will not be necessary to use -vv. It is normally used by software engineers working on RPM itself, and the output can change without notice. However, it’s a handy way to gain insights into RPM.