# 994 Part IV: Fedora RHEL Network and Server Setup

```
# chkconfig talk on
```

The previous command causes lasts the next time you reboot. To start it now (it may take a few minutes to complete), type:

```
# service talk start
```

Here’s what happens when you start the AppleTalk service:

+   - The AppleTalk daemon (atalkd) starts from the contents of the /etc/talk/atalkd.conf file.
- The papd daemon registers printers using the contents of the /etc/talk/papd.conf file.
- The afpd daemon registers volumes from the contents of the /etc/talk/AppleVolumes.default file (using settings from the AppleVolumes.system file).

To check that the nettalk service started properly, as root type one from the following Linux system on the network (the output may take a minute or two to appear):

```
# nbp1kup
toys:AFFServer 65280.115:128
toys:netalk 65280.115:4
toys:Workstation 65280.115:4
```

To check whether your nettalk service is available from a Mac client, go to the Mac client and perform the appropriate procedure:

+   - For a pre-Mac OS X client — Click the Apple Chooser. From the Chooser window, click AppleShare. The nettalk service should appear in the Select a server pane. Click it and click OK, and then use any user login and password from Linux to use that’s home directory.
- For a Mac OS X client — From the Finder bar, go To, Connect to server. The URL of the nettalk shared directory. For example, for the home directory on the computer named toys for the user named chris, you could type the following:

```
afp://toys/chris
```

You can use an IP address instead of a computer name. By default, your user’s home directory (in this case, /home/chris) is offered as an AppleTalk volume. When prompted, typed the password for that user and select the volume representing the home directory. If you can’t find and open the nettalk service from your Mac, see the “Troubleshooting nettalk” section in this chapter for some suggestions.