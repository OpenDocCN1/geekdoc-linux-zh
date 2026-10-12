
samba-common, samba, samba-client, samba-swat, and redhat-config-samba. If you’re only looking for a server installation, you’ll need at least samba and samba-common. If you’re only interested in acting as a client, then you’ll want samba-common and samba-client. And if you don’t want to set up the config files by hand, you’ll want either samba-swat or redhat-config-samba if not both.

## CRITICAL SKILL

### 18.3 Performing Samba Administration

This section describes some of the issues of administering Samba. We’ll see how to start and stop Samba, how to do common administrative tasks with SWAT or redhat-config-samba, and how to use smbclient. Finally, we’ll examine the process of using encrypted passwords.

### Starting and Stopping Samba

If you want to manually control Samba, you can use the `/etc/init.d/smb` script to start and stop the services. This will handle both the smbd and nmbd services. For example, to explicitly start the service using this script, you would run:

```
[root@picard /root]# /etc/init.d/smb start
```

And to stop the service using this script, you would run:

```
[root@picard /root]# /etc/init.d/smb stop
```

To ensure that it starts at boot time, you can bring up the services GUI tool by selecting the Services tool from the Server Settings submenu, or type redhat-config-services on the command line. As you may have surmised from the previous example, the smb option will take care of both smbd and nmbd. The swat option can be turned on if you want to use the web-based configuration, or it can be left off if you only installed SWAT for the extra documentation.

![](img/ec2066d370d3af1a767664d36aa7ddfe_530_0.png)

If you’re looking to set this all up from the command line, you’ll want to make sure you have the appropriate symlinks in the /etc/rc3.d and /etc/rc5.d directories pointing to the /etc/init.d/smb script. See Module 7 for details on checking for this and setting up the symlinks if you don’t have them already. SWAT is typically started from xinetd, so you’ll want to edit /etc/xinetd.d/swat if you want to enable it. SWAT runs on port 901 by default, so you’ll want to look at /etc/services if you really need to change that for some reason.

> **NOTE**
> If you make a change to the configuration of Samba, you’ll need to stop and then restart Samba in order for those changes to take effect. It’s the client’s responsibility to reestablish the connection. This is part of the SMB protocol and not a limitation of Samba.

### Progress Check

- 1. What is PAM?
- 2. What is one difference between smbd and nmbd?

## CRITICAL SKILL

### 18.4 Administering Samba with SWAT

Prior to version 2 of Samba, the official way to configure it was by editing the smb.conf file. Though verbose in nature and easy to understand, this file was rather large and cumbersome. It also meant that setting up shares under Windows was still easier than setting up shares with Samba. Many individuals developed graphical front ends to the editing process. Many of these tools are still being maintained and enhanced—you can read more about them by visiting Samba’s web site at http://www.samba.org. As of version 2, however, Samba ships with the Samba Web Administration Tool (SWAT).

Using SWAT is remarkably easy. All configuration is done via a web browser. SWAT then takes the information from the browser and builds an smb.conf file. For those who are used to editing configuration files, this may be a bit annoying because SWAT doesn’t preserve comments in the configuration file itself. Therefore, server configuration documentation must remain external to Samba rather than embedded in the configuration file in the form of comments.

- 1. PAM (Password Authentication Module) allows you to authenticate users against a PDC.
- 2. nmbd handles name server requests from master browsers, domain, and WINS servers, whereas smbd handles the actual file sharing systems and printers.

> **NOTE**
> If you prefer maintaining comments in your configuration file or if you need to write some of your own tools to automate certain administration chores, you should not use SWAT. Herein lies the beauty of text-based configuration files. You have a choice: you don’t have to use the GUI if you don’t want to, and since the file format is public, anyone can write their own administration tool if they want to.

### Setting Up SWAT

You can use SWAT to manage Samba through a browser interface. It’s an excellent alternative to editing the Samba configuration files by hand, but don’t let it make you believe that the configuration files are complex!

What makes SWAT a little different from other browser-based administration tools is that it does not rely on a web server (like Apache). Instead, SWAT performs all the needed web server functions without implementing a full web server. This is mostly accomplished by running through the xinetd daemon.

Simply point your web browser to your Samba server at port 901 to get a login prompt for entering SWAT. Note that the default configuration only allows you to connect to SWAT from the same machine on which you are running Samba. This was done for the purpose of security, since you don’t want to allow random people to be able to probe at your machine remotely. If you have a web browser installed on the server, simply point it at http://localhost:901/. If you don’t have a web browser installed on the local system, then you have to choose between using a different administration tool or enabling SWAT to be used across the network. If you want to use a local web browser but don’t have X Window System installed on the Samba server, you can still use any of a number of text-based web browsers as well.

> **CAUTION**
> Logging in as root through SWAT causes the root password to be sent from the web browser to the Samba server. Therefore, avoid doing administration tasks across an untrusted network. Preferably, run a web browser on the server itself, or set up an SSH tunnel between the client host and the Samba server host.

### Using SWAT from Other Hosts

If you used xinetd, then you already have TCP Wrappers functionality built into the configuration file. Changing the only_from option in /etc/xinetd.d/swat will allow you to add additional hosts with the ability to connect. Take a look at Module 8 for more information on how to limit which hosts can connect to your server.

### The SWAT Menus

When you connect to SWAT and log in as root, you’ll see the main menu shown in Figure 18-1. From here, you can find almost all the documentation you’ll need for Samba’s configuration files, daemons, and related programs. None of the links point to external web sites, so you can read them at your leisure without connecting to the Net. You’ll also be able to access the Samba How-To collection and the book *Using Samba*.

At the top of the window are buttons for the following menu choices:

| Button Name | Description |
| :--- | :--- |
| Home | The main menu page |
| Globals | Configuration options that affect all operational aspects of Samba |
| Shares | For setting up disk shares and their respective options |
| Printers | For setting up printers to be accessible to NT clients |
| Status | The status of the smbd and nmbd processes, including a list of all clients connected to these processes and what they are doing (the same information that’s listed in the smbstatus command-line program) |
| View | The resulting smb.conf file |
| Password | Password settings |

![](img/ec2066d370d3af1a767664d36aa7ddfe_533_0.png)

### Globals

The Globals page lists all settings that affect all aspects of Samba’s operation. These settings are divided into seven groups: Base, Security, Logging, Tuning, Printing, Browse, and WINS. To the left of each option is a link to the relevant documentation of the setting and its values. If you’re planning to share UNIX printers through Samba, you’ll want to make sure you have your printing option set to use LPRng or Common Unix Printing System (CUPS), as appropriate.

### Shares

Under Windows, setting up a *share* means creating a new folder, right-clicking it, and allowing it to be shared. Additional controls can be established by right-clicking the folder and selecting Properties.

Using SWAT, these same actions are accomplished by creating a new share. You can then select the share and click Choose Share. This brings up all the configurable parameters for the share.

### Printers

Samba automatically makes all printers listed in your local printing setup—that is the /etc/printcap file, in the case of LPRng, or /etc/cups/printers.conf, in the case of CUPS (see Module 19), available for use via SMB to Windows clients. Through this series of menus, you can modify Samba’s treatment of these printers or even add additional printers. The one thing you cannot do here is add printers to the main system. See Module 19 for more information on that process.

### Status

The Status page shows the current status of the smbd and nmbd daemons, including information about what clients are connected and their actions. The page automatically updates every 30 seconds by default, but you can change this rate if you like (it’s an option on the page itself). Along with status information, you can turn Samba on and off or ask it to reload its configuration file. This is necessary if you make any changes to the configuration.

### View

As you change your Samba configuration, SWAT keeps track of the changes and figures out what information it needs to put into the smb.conf file. Open the View page, and you can see the file SWAT is putting together for you.

### Password

Use the Password page if you intend to support encrypted passwords. You’ll want to give your users a way to modify their own passwords without having to log in to the Linux server. This page allows users to do just that.
