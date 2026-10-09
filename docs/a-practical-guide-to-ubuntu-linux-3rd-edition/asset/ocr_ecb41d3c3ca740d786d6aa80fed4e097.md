# If you can no longer use swat

tip If you can no longer use swat, you probably changed the **hosts allow** setting incorrectly. In this case you need to edit /etc/samba/smb.conf manually and fix the line with the words **hosts allow** in it:

```
```bash
$ grep hosts smb.conf
    hosts allow = 127.0.0.1, 192.168.0.8
    hosts deny = ALL
```
```

The preceding entries allow access from 192.168.0.8 only. They also allow swat to work. You do not need to restart Samba after changing **smb.conf**.

values for **hosts allow** and **hosts deny**, if any, are taken from the global parameters. Make sure **read only**, **guest ok**, and **browsable** are set as you desire. Set **available** to YES or you will not have access to the share. Click **Commit Changes** when you are done with the SHARES page. If you want to see how many parameters there really are, click **Advanced** near the top of the page. Switching between the Basic and Advanced views removes any changes you have not committed.

From a Windows machine, you should now be able to access the share you just created (page 814).

# You do not need to restart Samba when you change smb.conf

tip Samba rereads its configuration files each time a client connects. Unless you change the **security** parameter (page 810), you do not need to restart Samba when you change **smb.conf**.

# smb.conf: MANUALLY CONFIGURING A SAMBA SERVER

The /etc/samba/smb.conf file controls most aspects of how Samba works and is divided into sections. Each section begins with a line that holds some text between brackets ([...]). The text within the brackets identifies the section. Typical sections are

+   * [globals] Defines global parameters
+   * [printers] Defines printers
+   * [homes] Defines shares in the homes directory
+   * [share name] Defines a share (you can have more than one of these sections)

**smb.conf comments** As installed on an Ubuntu Linux system, the **smb.conf** sample configuration file contains extensive comments and commented-out examples. Comment lines start with either a hashtag (#) or a semicolon (;). The sample file uses hashtags to begin lines that are intended to remain as comments. Semicolons begin lines that you may want to mimic or use as is by removing the semicolons. The following segment of **smb.conf** contains three lines of true comments and three lines beginning with semicolons that you may want to uncomment and change:

```
```
# Un-comment the following (and tweak the other settings below to suit)
# to enable the default home directory shares.  This will share each
# user's home directory as \\server/username
:[homes]
;    comment = Home Directories
;    browsable = no
```
```