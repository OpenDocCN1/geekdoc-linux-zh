# To list the files and directories of a specified directory:

+   ls /bin

Here, you type the ls command plus the name of a directory. As shown in Code Listing 1.3, this command lists the files and directories in the /bin directory, in which you’ll find system commands and programs.

# Tips

+   You can list the files and directories of the root directory at any time and in any place by typing ls /.

+   Can’t remember that pesky filename? Just use ls to help jog your memory. Or, refer to Finding Forgotten Files with find in Chapter 2, which can also help you remember filenames.

+   Many other ls options are available to control the amount of information about your files that you see and the format in which they appear onscreen. See Chapter 2’s Listing Files and Directories with ls (More Goodies) section for details.

```
[jdoe@frazZ jdoe]$ ls /bin
arch*    domainname@  ipcalc*    open*    tar*
awk@     echo*        ipv6c     eys*     red@     unlink*
chmod*   fbresolution* login*    rm*      usleep*
chown*   fgrep@       ls*       rmdir*   vi@
consolechars* find*   lsb_release* rpm*     vim@
cp*      gawk*        mail*     rvi@     vim@
cpio*    gawk-3.1.6@  mkdir*    rview@
date*    gtar@        more*     sleep*   zcat*
dd*      gunzip*      mount*    sort*    zsh*
df*      gzip*        mv*       stat* 
dmesg*   hostname*    netstat*  stty*
dnsdomainname@ id@      nice*     su*
doexec*  gawk*        nisdomainname@ sync*
[jdoe@frazZ jdoe]$
```

Code Listing 1.3 Use ls with the name of a directory to list the contents of that directory (/bin, in this case).