you do see an error, don't panic. Most error messages don't reflect a problem with the program itself, but usually with the system in some way or another. Typically, these messages are the result of inappropriate file permissions (see the chmod command in Chapter 6), or files that cannot be found. In the latter case, make sure your path has at the very least the /bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, /usr/local/sbin, and /usr/X11R6/bin directories in it. You can echo your path by issuing the command

```
(root@ford esh-2.0.13)# echo $PATH
```

See Chapter 6 for information on the **env** command so that you can set your path correctly.

In general, slow down and read the error message. Even if the format is a little odd, it may explain what is wrong in plain English, thereby allowing you to quickly fix it. If the error is still confusing, look at the documentation that came with the package to see if there is a mailing list or e-mail address you can contact for help. Most developers are more than happy to provide help, but you need to remember to be nice and to the point. (In other words, don't start an e-mail with a one-paragraph rant about why their software is terrible!)

# ## Installing the Package

Similar to the compile stage, the installation stage typically goes smoothly. In most cases, all you need to run, once the compile is done, is

```
(root@ford esh-2.0.13)# make install
```

This will start the *installation script* (which is usually embedded in the Makefile). Because make displays each command as it is executing it, you will see a lot of test fix by. Don't worry about it—it's perfectly normal. Unless you see an error message, the package is installed.

If you do see an error message, it is most likely because of permissions problems. Look at the last file it was trying to install before failure and then go check on all the permissions required to place a file there. You may need to use the chmod, chown, and chgrp commands for this step; see Chapter 6 for additional details.

# ## Clean Up

Once the package is installed, you can do some cleanup to get rid of all the temporary files created during the installation. Since *we* have the original source code tarball, it is okay to simply get rid of the entire directory from which you compiled the source code. In the case of SSH, you would get rid of /usr/local/ssh-2.0.13. Begin by going one directory level above the directory you want to remove. In this case, that would be /usr/local/src.

```
(root@ford esh-2.0.13)# cd /usr/local/src
```