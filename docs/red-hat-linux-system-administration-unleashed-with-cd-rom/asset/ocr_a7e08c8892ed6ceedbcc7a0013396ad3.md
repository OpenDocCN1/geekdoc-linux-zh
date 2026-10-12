# Installing X-Chat

At the time of this writing, the latest release is version 1.2.1. If you have an earlier version (such as is installed with Red Hat 6.0), it is well worth upgrading. X-Chat 1.2.1 offers an improved user interface as well as several other changes.

Download the RPM binary from the download page and place it into an appropriate directory. Move to that directory and install using the Red Hat Package Manager,

```
rpm -ivh xchat-1.2.1-1.1386.rpm.
```

Note that if you have a previously installed version of X-Chat, you should use the command

```
rpm -Uvh xchat-1.2.1-1.1386.rpm instead.
```

# Running X-Chat

If you are using the GNOME interface and had a previously installed version of X-Chat, X-Chat can be run from the GNOME menu. It appears in the Internet sub-menu.

If you had no previous version of X-Chat installed and installed the latest version using RPM, the binary executable is in /usr/bin. This is in the default shell search path for all users.

Of course, if you installed from source, you need to read the makefile and if you installed from a tarball, the binary will usually appear in a directory of the same name as the program underneath the directory in which the tarball was placed.

Having started X-Chat, the first thing to do is to select a nickname—the default is your username—and then choose a server to connect to. X-Chat very helpfully provides a comprehensive list of servers for you to choose from so you shouldn't need to go looking on the WWW. If you know what server you require and it doesn't appear on the list, you can add it using the New Server button.

Clicking on Connect after choosing a server connects you to the server and you will normally see the message of the day. Nickname conflicts will be advised at this point.

# BitchX

According to the home page (http://www.bitchx.com), "BitchX is a modified clone of the popular ircII client, and is available for almost all UNIX OS's...".

BitchX is another console-based IRC client that offers an alternative to ircII. Because it is console based, you don't need to worry about getting X up and running—just use that old 386 in the garage that only has a mono video card capable of 80 × 25 display!

Note that documentation is not installed with the program but you can find an FAQ list at http://scripts.bitchx.com/bxf... .