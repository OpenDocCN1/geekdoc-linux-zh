
## Using the Macintosh's Chooser

MacOS uses the Chooser to mount volumes exported by networked computers, and you use the Chooser to mount your Linux files—at least in versions of MacOS through 8.6.

> NOTE
> 
> The upcoming MacOS X might abolish the Chooser, so you might need to use some other means of selecting your Linux exports in MacOS X.

To mount a Linux share from a Macintosh, follow these steps:

- 1. Select Apple, Chooser to open the Chooser, shown in Figure 12.1.

![](img/5d4d3092919d1d16884788127447cc6d_326_0.png)

FIGURE 12.1
You use the Chooser to access both shared files and printers (shared or local).

- 2. Click the AppleShare icon in the left portion of the Chooser. The Macintosh checks the network for AppleTalk servers, and if your Netatalk configuration is correct, you see your Linux computer among them.

> NOTE
> 
> These instructions presume that you've enabled AppleTalk support in your Macintosh. Examine the AppleTalk radio button near the bottom right of the Chooser. It should be set to Active. If it's set to Inactive, change that setting.

3. Select your Linux server from the list of computers and click OK. MacOS responds by displaying a connection dialog box, as shown in Figure 12.2. If you have enabled guest logins, you can elect to use the guest account, but you won’t have access to your home directories. If you want access to your user account files, select Registered User and type your Linux username and password, and then click Connect.

![](img/5d4d3092919d1d16884788127447cc6d_327_0.png)

# FIGURE 12.2

With the version of Netatalk included with this book’s CD-ROM, you are able to send only a cleartext password.

4. The Macintosh now displays the volume selection dialog box, shown in Figure 12.3. Select the volume you want to mount. If you want to mount this volume every time your Macintosh starts, check the box on the right of the list. You can tell the system to save only your username or your username and password. After you select the options you want, click OK, and the Macintosh mounts the volume.

![](img/5d4d3092919d1d16884788127447cc6d_327_1.png)

# FIGURE 12.3

You can select only one volume at a time in the volume selection dialog box; to open more than one, you need to select the server a second time from the Chooser.

After you mount a volume, a network drive icon appears on the Macintosh desktop. You can double-click that icon to manipulate the files on your Linux server as if they were local to the Macintosh, with some caveats.

Occasionally, there may be a problem with the AppleTalk portion of Netatalk's functioning. In this situation, you don't see your Linux server in the Chooser, but you might still be able to access it by clicking the Server IP Address button. The Macintosh then displays a dialog box asking for an IP address, which you must provide. (Note that this is a numerical IP address, not a TCP/IP machine name.) The login procedure can then proceed normally. The problem with a Linux server not appearing in the Chooser can sometimes be cured by restarting Netatalk, occasionally in conjunction with shutting down and rebooting all the Macintoshes on the network.

## Accessing Linux Files

For the most part, your networked Linux filesystem should work as you would expect any other Macintosh drive to behave. There are some caveats and a few bugs, though, particularly as relate to inter-OS interactions:

- As described earlier, Linux uses the contents of the /etc/atalk/AppleVolumes.system file to determine what files map to what application and file type. If the AppleVolumes.system file is misconfigured or if you lack critical applications, you may have difficulty accessing some files.
- Linux supports much longer filenames than does Macintosh—Macintosh is limited to 31 characters, whereas Linux can handle up to 255. If a file has more than 31 characters in its filename, Netatalk ignores it, so you can't access that file on the Macintosh.
- Linux is a case-sensitive OS (p. xxx), whereas MacOS is normally case-retentive (p. 230). Unless you adjust Netatalk's case-handling features using the casefold option in AppleVolumes.default, Netatalk forces the Macintosh to behave in a case-sensitive way.
- Macintosh aliases to files on Netatalk volumes might not work between sessions. Similarly, the lists of recently accessed files that many programs might not work between sessions.
- Multiuser access to individual files can be tricky. If several users need read-only access to a file, there's normally no problem; however, if two users try to gain write access to the same file, the results can be unpredictable. This is especially true when Macintosh users (using Netatalk) and Windows users (using Samba) try to access the same file, since Netatalk and Samba don't coordinate their file-locking procedures.
- Some Macintosh programs have problems creating large files on large volumes—the Macintosh claims there's not enough free disk space, though there is. The precise limits vary, but the problem normally doesn't appear on files measured in anything less than hundreds of megabytes. This therefore isn't a problem for the average word processing document, but it is when creating a CD-recordable (CD-R) image file or backing up a
