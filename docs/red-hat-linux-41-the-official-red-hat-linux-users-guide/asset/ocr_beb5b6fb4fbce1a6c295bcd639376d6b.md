which is the function you use in a C program to turn swap on. Unless you are writing your own program to do it, this probably isn't what you want. So, using the chart above, you can see that what you want is probably a “system command” and is located in section 8. You can then do man 8 swapon. All of this is because man searches the man directories in order, and then returns when it finds the first match.

You can also search the man pages for strings. You do this using man -k string-to-search-for. This won't work, however, unless the makewhatis database has been created. Under Red Hat Linux, this is done by a cron job overnight. If you don't leave your system running overnight the database won't get created. If that is the case, just run:

```
/etc/cron.weekly/makewhatis.cron
```

Note: This must be done as root.

Once you've done that, you could enter man -k swapon. That command would return:

```
```
# man -k swapon
swapon, swapoff (2) - start/stop swapping to file/device
swapon, swapoff (8) - enable/disable devices and files for paging and swapping
```
```

So you can see that there are pages in section 2 and 8 both referring to swapon (and swapoff in this case).

# 6.1.2 Package Documentation

Many packages of software have READMES and other documentation as part of the source package. Red Hat Linux uses a standard place to install those documents so that you don't have to install the sources to look at the documents. All of those documents are stored in subdirectories of /usr/doc. The subdirectory depends on the package. Each package that has extra documentation will create a directory called packagename-version-releasenumber. For example, the tin package might be version 1.22 and release number 2. The path to its documentation would be /usr/doc/tin-1.22-2.