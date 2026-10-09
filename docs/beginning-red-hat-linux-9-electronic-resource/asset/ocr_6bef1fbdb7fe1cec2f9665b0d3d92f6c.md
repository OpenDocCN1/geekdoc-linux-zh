```
restore > ls
```
:  2 .        11 lost+found/ 32001 joe/
  2 ../     256009 postgres/
restore > add joe/.gnome2/acce

l
s Make node ./joe
Make node ./joe/.gnome2
Make node ./joe/.gnome2/acce

l
s restore > ls
:  2 .        11 lost+found/ 32001 *joe/
  2 ../     256009 postgres/

restore > extract
Extract requested files
You have not read any volumes yet.
Unless you know which volume your file(s) are on you should start
with the last volume and work towards the first.
Specify next volume # (none if no more volumes): 1
Add links
Set directory mode, owner, and times.
Set owner/mode for './? [yn] y
restore > quit
```
```

You might agree with me that dump is a very powerful tool for quickly and easily backing up entire filesystems. It serves a purpose that is not filled with either tar or cpio.

In summary, backing up and archiving files is very important. Linux comes with a vast assortment of applications and tools to make archiving a convenient process. There are tools available for mirroring partitions and files, performing network backups, such as Amanda, as well as backups to CD-ROM, ccdirecord. Once you decide on a backup strategy, you should investigate these tools to determine the application that is most suited for your purpose.

Next, we will shift gears a bit and talk about building applications from source code. Say, for example, you find a really powerful archival application. After looking at its documentation, you realize, to your disappointment, that it does not come with a pre-built binary for Linux, but only source code. How do you go about building it? Proceed to the next section to find out more.

# Building from Source

So far in this book, the applications we've been using have all been installed from pre-compiled binary RedHat Packet Manager (RPM) packages. We've seen how quick and easy it is to install, modify, and uninstall programs from pre-compiled binaries. However, there are also many applications available as (uncompiled) source code, typically in a compressed archive of some sort (i.e. .tar.gz or .tar.bz2).