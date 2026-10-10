
![](img/48eec858cce7dfb89da36a4d40b7daf3_151_0.png)

**FIGURE 6.9** xmixer when invoked with the 1 command as xgmixer. The functionality remains the same, but the appearance is different because this version uses the GTK toolkit instead of the Athena toolkit.

## Networking Applications

Numerous networking applications are available for FreeBSD. This section will concentrate on Web browsers, e-mail, FTP, and so on.

### Configuring Netscape

The Netscape Communicator Web browser is available for FreeBSD. The latest version available for FreeBSD is 4.8. If you want to run Netscape 7, you will need to run the Linux version of Netscape in FreeBSD. In addition, you will also need to run the Linux version if you want to use most plug-ins, such as Flash and Shockwave. These plug-ins are available only for Linux versions of Netscape. Running the Linux version of Netscape in FreeBSD allows you to use these plug-ins.

All the Netscape browsers, including the Linux versions, are available as ports in the www directory. This allows you to install and run the Linux versions just like they were normal FreeBSD applications.

Once Netscape has been installed, you can start it with the command `netscape` for Netscape 4.8 or with the command `netscape7` for Netscape 7. This section will cover Netscape 4.8, but Netscape 7 is similar.

Most users have probably used Netscape before, and the configuration in FreeBSD is the same as the configuration in Windows. To change Netscape options, click Edit in the menu bar and then click Preferences. This brings up a configuration dialog box like the one in Figure 6.10.

To configure the various Netscape settings, click the plus sign (+) by the desired category of options to expand it. Then, click the item you wish to configure to bring up its configuration dialog box in the right side of the window.

### Lynx Web Browser

Lynx is a Web browser that runs in text mode and has no graphical capabilities. Although it can still be used, it is getting more and more difficult to navigate the Web with Lynx because it does not support images, frames, or Java. Because many sites are using images as links and not making use of ALT tags, this can cause navigational problems in Lynx that are difficult or impossible to get around. Figure 6.11 shows Lynx with the FreeBSD Web site loaded into it.

![](img/48eec858cce7dfb89da36a4d40b7daf3_152_0.png)

**FIGURE 6.10** The configuration dialog box for Netscape. It is similar to configuring Netscape in Windows.

![](img/48eec858cce7dfb89da36a4d40b7daf3_152_1.png)

**FIGURE 6.11** The FreeBSD Web site in Lynx.

Lynx can still work on quite a few sites, although navigation is not always easy. Use the arrow keys to move between links in the browser window. The spacebar will advance to the next page. Type **G** to change to a different Web site. You will be asked to enter a URL after typing **G**. **Q** quits Lynx after asking whether you are sure you want to quit.

For more information on Lynx, including customization options, see the Lynx man page by typing `man lynx`.

## FTP

FTP (*File Transfer Protocol*) is a method of transferring files between systems. Although it is not commonly used directly anymore (often, files are downloaded from FTP by clicking Web site links), it is still handy to know if you need to move files to another server.

To start an FTP session, type **ftp** followed by the name of the server you wish to connect to at the shell prompt or X-terminal. For example, to connect to the FreeBSD FTP server, you would type the following:

```
ftp ftp.freebsd.org
```

Once you have done this, and assuming the connection is successful, you will eventually see something like the following:

```
Connected to ftp.beastie.tdk.net.
220 ftp.beastie.tdk.net FTP server (Version DG-4.1.73 983302105) ready.
Name (ftp.freebsd.org:murban):
```

At the **Name** prompt, you need to enter your login name for the FTP server. If your login name is the same as your login name for the system you are currently on, you can simply press Enter without entering a name here, and your local login name will be used.

If you do not have a login name for the system, you can log in to public FTP servers with the name **anonymous**. For example, this is how you would log in to the FreeBSD FTP server. Once you have entered anonymous as the username and pressed Enter, the remote host will respond with something like the following:

```
331 Guest login ok, send your e-mail address as password.
Password:
```

Simply do what it says, and enter your e-mail address as your password. Note that the password will not echo to your screen.

After you have logged in, you may get a welcome message and finally something that looks similar to the following:

```
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

At the prompt, you can use many of the same shell commands that you use at your local shell to navigate through the FTP server. See Chapter 7 for details on how to work with shell commands. Table 6.9 provides a list of some of the most commonly used commands in an FTP session.

**TABLE 6.9** Commonly Used FTP Commands

| Command | Action |
| :--- | :--- |
| ls | Lists the directory contents of the remote host. |
| cd | Changes the directory on the remote host. |
| pwd | Displays the current directory you are in on the remote host. |
| lcd | Changes the directory on the local host. |
| binary | Transfers files in binary mode (this mode should be used for anything other than plain-text). |
| ascii | Transfers files in ASCII mode (this mode should be used *only* for plain-text). Note that plain-text can also be transferred in binary mode, in most cases, with no problems. |
| put *filename* | Copies *filename* to the remote host. *filename* is assumed to be in the current directory unless a path is specified. If no destination file is specified, the file will be placed in the current directory in the remote host and have the same name as the local file. (This command works only if you have permission to write to the directory on the remote machine.) |
| mput *file1 file2* | Copies multiple files in a list to the remote host. The files will be placed in the current directory on the remote host. (This command works only if you have permission to write to the directory on the remote machine.) |
| get *filename* | Copies a file from the remote host to the local system. If no path is specified, the file is assumed to be located on the current directory on the remote host. If no destination file is specified, the file will be copied to the local system using the same filename. |
| mget *file1 file2* | Gets multiple files in a list from the remote host. The files will be placed in the current directory on the local system. |
| mkdir *dirname* | Creates a directory called *dirname* on the remote machine (assuming you have permission to do so). |
| rmdir *dirname* or rm *dirname* | Removes the directory called *dirname* on the remote machine (assuming you have permission to do so). |
| del *filename* | Deletes the file *filename* from the remote machine (assuming you have permission to do so). |
| bye or quit | Closes the connection with the remote host and quits the FTP program, returning you to the shell prompt. |

You can also type **help** at the `ftp>` prompt to get a list of available commands. Type **help** followed by one of the commands in the list to get a short description of what that command does. Here’s an example:

```
ftp> help
Commands may be abbreviated. Commands are:

!  disconnect  mdelete    preserve   runique
$  edit       mkdir      progress   send
   account    exit       get        prompt     sendport
   append     form       mkdir      proxy      site
   ascii      ftp        mls        put        size
   bell       get        mode       pwd        status
   binary     gate       mdtimes    quit       struct
   bye        glob       more       quote      sunique
   case       hash       mput       recv       system
   cd         help       msand      reget      tenex
   cdup       idle       newer      rename     trace
   chmod      image      nlist      reset      type
   close      lcd        nmap       restart    umask
   cr         less       ntrans     restrict   user
   debug      lpwd       open       rhelp      verbose
   delete     ls         page       rmdir      ?
   dir        macdef     passive    rstatus
```

```
ftp> help mdir
mdir list contents of multiple remote directories
ftp>
```

For more information on using FTP, read the manual pages for FTP by typing `man ftp` at the shell prompt. You might also want to read the sections in Chapter 7 on file-manipulation commands because the commands used in FTP are similar.

The following shows what a sample FTP session might look like:

```
bash$ ftp ftp.freebsd.org
Connected to ftp.beastie.tdk.net.
220 ftp.beastie.tdk.net FTP server (Version DG-4.1.73 983302105) ready.
Name (ftp.freebsd.org:murban): anonymous
331 Guest login ok, send your e-mail address as password.
Password:
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
227 Entering Passive Mode (62,243,72,50,88,26)
150 Opening ASCII mode data connection for 'file list'.
total 2
```
