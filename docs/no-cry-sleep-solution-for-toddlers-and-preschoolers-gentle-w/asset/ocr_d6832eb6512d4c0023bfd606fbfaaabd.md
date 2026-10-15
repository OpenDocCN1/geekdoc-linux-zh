you can force the download with the -f option. For example, to download upgrades for Red Hat manually, you can connect to the Red Hat upgrade directory in the Red Hat FTP site and then issue the following get command:

```
get *
```

> Tip If you were interrupted during a download, you can restart the download from where you left off. This feature is built into NcFTP. (On other FTP programs, it can be invoked with the reget command.) NcFTP checks to see if you have already started to download a file and then continues from where you left off.

Certain features require you to enter an option on the command line after the get command. For example, adding the -r command specifies a recursive capability, enabling you to download and create subdirectories and their files. This command is particularly helpful in downloading upgrade directories, such as Red Hat's, which contain several subdirectories. The following example downloads the i386 directory and all its subdirectories:

```
get -R i386
```

If you want to give a file a different name on your local system, use the -z option. Enter the local filename you want after the remote filename. The following example downloads the readme file and renames it calinfo. If you did not use the -z option, both names would be taken as files to be downloaded, instead of only the first.

```
get -z readme calinfo
```

To obtain recent files only, you can use the -n option, which takes as its argument a number of days. Files older than the specified number of days are not retrieved. The following example downloads files posted within the last 30 days:

```
get -n 30 *
```

# Bookmarks and Macros

When you disconnect (close) from a site, NcFTP automatically saves information about it. This includes the site address, the directory you were in, and the login information. This information is placed in a file called bookmarks in your .ncftp directory. The site information is given a bookmark name you can use to access the site easily again. The bookmark name is usually the key name in the site's address. You can use this name to connect to the site. For example, ftp.redhat.com could be named redhat. You could then connect to it with the following command:

```
open redhat
```

You can edit your bookmark entries using the bookmark editor. Enter the command bookmarks to bring up the editor. Remote systems you have accessed are listed on the right side of the screen. Bookmark commands are listed on the left. You can change the bookmark name or edit login information, such as the username or password, the remote directory, or the transfer mode.