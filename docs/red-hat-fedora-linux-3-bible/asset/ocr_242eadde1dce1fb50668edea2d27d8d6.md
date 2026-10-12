+   • Allow access to everyone — Choose this option if you want to allow anyone to access this directory. (All users will have privileges assigned to the guest user when accessing the directory.)

After you click OK, Samba is started and the new directory is immediately available. You can close the Samba Server Configuration window.

+   13. Although Samba should be running at this point, you probably need to set Samba to start automatically every time you reboot Linux. To do that, type the following as root user in a Terminal window:

```
chkconfig smb on
```

You can repeat the steps for adding a Samba shared directory for every directory you want to make available on your network. At this point, you can either:

+   • Go through your Samba server settings in more detail (as described in the "Configuring Samba with SWAT" section) to understand how you might want to further tune your Samba server.

+   • Try accessing the shared directories you just created from a client computer on your network.

If you cannot open the shared directory you just configured from a Windows computer or other Linux computer on your LAN, you are probably experiencing one of the following problems:

+   • The client isn't supplying a valid user name and password.

+   • The client isn't supplying an encrypted password.

The quick way around these problems is to use only share-level security (which, of course, throws your security right out the window). The other solution is to get passwords up-to-date and make sure that clients are using encrypted passwords (as described in the "Setting up Samba clients" section later in this chapter).

# Configuring Samba with SWAT

The Samba Web Administration Tool (SWAT) is a Web-based interface for configuring Samba. While it's not quite as easy to use as the Samba Server Configuration window, it does offer more options for tuning Samba and Help descriptions for each option.

> **CAUTION:** Both SWAT and the Samba Server Configuration window configure Samba by modifying the `/etc/samba/smb.conf` file. Different GUI tools can overwrite each other's settings, sometimes in a way that causes the other tool not to work.

In general, it's best to make a backup copy of your files before switching GUI tools. Eventually, you should choose one tool and stick with it.