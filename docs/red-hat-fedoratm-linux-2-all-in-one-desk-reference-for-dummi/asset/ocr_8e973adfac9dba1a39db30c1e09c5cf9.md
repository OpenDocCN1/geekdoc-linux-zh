Core and already installed on your system. However, you do no harm in downloading and rebuilding the XMMS package again.

Download the source files for XMMS from www.xmms.org/download.php. The files are packed in the form of a compressed tar archive. Click the ftp link for the source files and then save them in the /usr/local/src directory in your Fedora Core system (be sure to log in as root; otherwise you cannot save in the /usr/local/src directory).

After downloading the compressed tar file, examine the contents with the following tar command:

```
tar ztf xmms*.gz | more
```

You see a listing similar to the following:

```
xmms-1.2.10/
xmms-1.2.10/intl/
xmms-1.2.10/intl/ChangeLog
xmms-1.2.10/intl/Makefile.in
xmms-1.2.10/intl/config.charset
xmms-1.2.10/intl/locale.alias
xmms-1.2.10/intl/ref-add.s
xmms-1.2.10/intl/ref-del.s
xmms-1.2.10/intl/gmo.h
xmms-1.2.10/intl/gettextP.h
xmms-1.2.10/intl/hash-stri
ng.h
xmms-1.2.10/intl/loadinfo.h
... rest of the output not shown ...
```

The output of this tar command shows you what's in the archive and gives you an idea of the directories that are created after you unpack the archive. In this case, a directory named xmms-1.2.10 is created in the current directory, which, in my case, is /usr/local/src. From the listing, you also learn the programming language used to write the package. If you see .c and .h files, the source files are in the C programming language used to write many open-source software packages.

To extract the contents of the compressed tar archive, type the following tar command:

```
tar zxvf xmms*.gz
```

You again see the long list of files as they extract from the archive and copy to the appropriate directories on your hard drive.

Now you're ready to build the software.