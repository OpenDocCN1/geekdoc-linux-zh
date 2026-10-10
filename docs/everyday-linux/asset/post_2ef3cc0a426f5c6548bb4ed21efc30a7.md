
# Some Internet Applications

## Opera

The makers of Opera have not released a stable version of Opera for Linux at the time of this printing. It is worth noting, however, that Opera is a very small and fast alternative to the huge browsers available now.

There are tech preview releases of Opera available at their web site (which can be found in the reference section in the back of the book). It’s well worth checking out, and it will be a force to be reckoned with when completed.

## Lynx

Lynx is a text-only browser, frequently used to avoid loading images and scripting. Since it’s completely text-based, it is incredibly fast. However, web page makers rarely design their pages to work well with text browsers, so Lynx usually doesn’t render web pages very well. Fortunately, the makers of Lynx have steadily increased support for features such as tables and frames.

Lynx comes with Linux and almost all UNIX operating systems. It has been around for a long time and remains the choice of some systems administrators. People who are blind or cannot see well sometimes prefer to use Lynx; it cuts out much non-textual information and Braille keyboards work better.

## FTP Programs

FTP programs allow you to connect to what are known as FTP servers. FTP stands for file transfer protocol. There are several programs which use the file transfer protocol to send and receive files over the Internet. Among these are favorites such as NCFTP and GFTP.

### NCFTP

NCFTP is a program run from the command line, generally used because it allows download recovery. Just like a regular highway, the information superhighway is subject to traffic jams and crashes. Your download may be terminated or suspended before completion, and NCFTP will allow you to start where you left off.

To run NCFTP, open a terminal window by clicking on the terminal icon on your panel. When the terminal screen comes up, type ncftp. A window will appear that looks a little like this:

```
[root@exter /root]# ncftp

NcFTP 3.0.0 beta 21 (October 04, 1999) by Mike Gleason (nccftp@nccftp.com). Copyright (c) 1992-1999 by Mike Gleason. All rights reserved.

nccftp> help

Commands may be abbreviated. 'help showall' shows hidden and unsupported commands. 'help <command>' gives a brief description of <command>.

ascii  cat help lpage open quote site
bgget cd jobs lput page rename type
bgput chmod lcd lrename pdir rhp umask
bgstart close lchmod lrm plis rm version
binary debug lls lmdir put rmdir
bookmark dir lmkdir ls pwd set
bookmarks get lookup mkdir quit show
nccftp> _
```

I have taken the liberty of showing you all of the commands that NCFTP can use. (To do this yourself, type help while you're using the program.) Here is a brief synopsis of some of the commands:

- **open (-u) [server]** The open command will open an FTP connection to the server that you specify. For instance, you can use open ftp.ccil.org to open an FTP connection to that server. The -u option tells NCFTP that you want to specify your own username instead of using the anonymous user. This is useful if you're connecting to an FTP server on which you have an account.
- **close** When you're done with the FTP session, you can close it. This won't close the program itself, just the connection, so you can connect to other FTP sites with the open command.
- **quit** When you're completely done with all of your FTP sessions, use the quit command to close the program. If you are connected when you type in quit, NCFTP will disconnect you.
- **get, mget [filename]** The get command will download files from a server. If you want to get more than one file at once, you must use the mget (multiple get) command.
- **ls** When you need a file listing, use the *ls* command. It will display all of the files in the current directory.
- **cd [directory]** You will probably need to change directories when you're using NCFTP; use the *cd* command to do it.

Once you've finished using NCFTP, you can type *exit* to exit the terminal window. You'll notice that many of these commands are the same as we use for the command-line interface.

### GFTP

GFTP is the GNU FTP program.

![](img/92fb6d8ad19de3b3470ba95c7b71b82e_172_0.png)

**Figure 9-4**  
*This is what GFTP looks like.*

GFTP is easy to use, but it may require a little getting used to. It makes use of a variety of services. They aren’t complicated, but there are a lot of them, so it can take a little while to become accustomed to using GFTP. After you do, though, you’ll be able to use an incredibly versatile and powerful FTP program. We are first going to concern ourselves with the menu bar at the top of the GFTP screen. We’ll then look at the rest of the GFTP screen.

#### FTP

The first menu is the FTP menu. When you click on this menu, you are presented with four different options: ascii, binary, options, and quit. The last one is obvious—click on it to exit the program.

The first two, ascii and binary, refer to the *transfer method*, that is, how GFTP is going to attempt to transfer the files that you download and upload. All text files should be transferred using the ascii mode; other files should be transferred in binary mode. You may not encounter problems if you attempt to transfer binary files in ascii mode, but it’s best to be on the safe side. The mode that you’re currently transferring in is listed on the left side.

You’ll probably spend some time in the options menu.

There are four tabs in the options section. The first is the general tab. Following it are the FTP proxy and HTTP proxy tabs and finally the Local Hosts tab. The general tab is probably the only one you’re going to change. The final three are used for network purposes, so if you’re not on a network, you should leave these tabs alone. If you are on a network, you should only fill in this information as directed by a network administrator.

In the General section, you will be able to put in your e-mail address, the program you use to view files (the “view program”), the program you use to edit files (the “edit program”), and other miscellaneous details.

Your e-mail address is the password sent when you log in as an anonymous user. Many people don’t like to type their real e-mail addresses because some sites will collect the addresses and put them in mailing lists. These lists are sold and used by commercial companies to send unsolicited commercial e-mail (UCE), or “spam.” I usually give a false address.

The view and edit programs should be specified with their full path and file-name, unless the program is already in the path. (Such as gedit.)

The other checkboxes that are available are fairly self-explanatory. These options will not change any of the files that you download or set formats that could restrict your use of GFTP, so you can experiment with these safely.

![](img/92fb6d8ad19de3b3470ba95c7b71b82e_174_0.png)

**Figure 9-5**  
The options menu in GFTP.

One of the fill-in boxes does deserve some special attention. The “Max KB/S” will allow you to specify the maximum transfer rate possible during transfers. On occasion, when you transfer files between your computer and local servers, files may be transferred so quickly that errors in the transfer occur, damaging the contents of your file. If you find that this happens to you, you should set this according to the speed of your modem. If you have a 56k bps modem, you would set the “Max KB/S” rate to 5.6. Generally, you can always divide your modem speed by ten and put it into this box.

#### Local

The next menu item is labeled “Local.” Local means that you’re dealing with the computer that you’re working on, not the computer to which you’re connected. (As you’ll see shortly, the computer you’re connected to is called the “remote” computer.)

All of the options under this menu are performed on files or directories on your home computer. Fortunately, most of them are self-explanatory. There are a few of note, however:

- **Change Filespec** This option will change what files you view in your directory. To view all files, use the file specification `*`. If you wanted to find all files that begin with the letters “pin”, you would type in `pin*`. If you just wanted to find files with four character filenames that begin with “pin,” you would type in `pin?`. The asterisk and question mark are called *wildcard characters*, and they tell the computer to list any filenames with additional characters. Question marks are used for single characters and are cumulative. So `pin??` stands for five-letter filenames that start with “pin.” `pin?` is just four letters. The asterisk is used to indicate that the filenames can be of any length.
- **Chmod** You can change permissions of files locally if you wish. To do so, highlight the file you wish to make changes to by clicking on it. Then click on local, and then click on chmod.
- **Refresh** If you make changes to the directory structure or some files, you may need to refresh the file list before you can see that the changes were made. Click on local and then refresh to update the list.

#### Remote

The remote menu is the same as the local menu but for three exceptions—open URLs, disconnect, and send SITE command. This menu controls what actions you can take on the computer that you’re connected to (otherwise known as the remote computer). Like on your own computer, if you have an FTP account on another computer, you’ll be able to change filenames and file permissions, add or delete directories, and so on.

The open URL remote option allows you to input an FTP web address, in the form ftp://ftp.sitename.com. Most web browsers come with their own rud-
