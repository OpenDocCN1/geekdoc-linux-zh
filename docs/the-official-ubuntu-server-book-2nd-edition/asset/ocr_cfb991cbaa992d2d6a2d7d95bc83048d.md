installed on the system. To get a quick overview of what this might look like, you could run the following command:

```
$ dpkg -l most
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Cfg-files/Unpacked/Failed-cfg/Half-inst/
| Err?=(none)/Hold/Reinst-required/X/both-problems
|/ Err?=(none)/Hold/Reinst-required/X/both-problems
(Status,Err: uppercase=bad)
||/ Name           Version        Description
+++=+==============+==============+================================
ii most           5.0.0a-1       Pager program similar to more and less
```

Run without any arguments, dpkg -l will show this basic information on the installation status, name, version, and description of every package on your system.

Another simple task is to get a list of files contained within the package. If you have a DEB file that you have not installed, you can get this information by running dpkg --contents as in the example below:

```
$ dpkg --contents /var/cache/apt/archives/most_5.0.0a-1_i386.deb
drwrxr-xr-x root/root         0 2008-05-06 12:06 ./
drwrxr-xr-x root/root         0 2008-05-06 12:06 ./usr/
drwrxr-xr-x root/root         0 2008-05-06 12:06 ./usr/bin/
-rw-r--r-- root/root     59940 2008-05-06 12:06 ./usr/bin/most
drwrxr-xr-x root/root         0 2008-05-06 12:06 ./usr/share/
drwrxr-xr-x root/root         0 2008-05-06 12:06 ./usr/share/man/
drwrxr-xr-x root/root         0 2008-05-06 12:06 ./usr/share/man/man1/
-rw-r--r-- root/root      5912 2008-05-06 12:06 ./usr/share/man/man1/most.1.gz
drwrxr-xr-x root/root         0 2008-05-06 12:06 ./usr/share/doc/
drwrxr-xr-x root/root         0 2008-05-06 12:06 ./usr/share/doc/most/
-rw-r--r-- root/root      2989 2007-09-09 12:14 ./usr/share/doc/most/changelog.gz
-rw-r--r-- root/root      5544 2008-05-06 12:06 ./usr/share/doc/most/copyright
-rw-r--r-- root/root      3335 2007-09-06 10:15 ./usr/share/doc/most/README
-rw-r--r-- root/root      1386 2006-05-01 13:51 ./usr/share/doc/most/lesskeys.rc
-rw-r--r-- root/root       492 2006-05-01 13:51 ./usr/share/doc/most/most.fun.txt
-rw-r--r-- root/root      3086 2006-05-01 13:51 ./usr/share/doc/most/most.rc
```