
structure from one Linux partition to another without losing the connection between the files and their attributes.

Here are a few tips to think about before you start using netatalk:

- Use Mac clients to create, move, and copy files on the Mac volume whenever possible. This is the best way to keep your volumes clean and working properly.
- If you must move netatalk files and folders from a Linux shell, use the `apple_mv`, `apple_cp`, and `apple_rm` commands (described later in this chapter).
- You can share the same volumes with both your Mac clients (using netatalk) and Windows clients (using Samba), but this involves certain risks and caveats as well. See the "Sharing files with netatalk and Samba" section later in this chapter for ways to avoid trouble.
- Mac users expect permission on files and directories to be more open than many Linux administrators are comfortable with. Check the "Securing netatalk volumes" section for information on the best ways to securely provide the necessary access.
- Tools for tracking down network services and troubleshooting problems for AppleTalk networks are different than those used for pure TCP/IP networks. Refer to the "Troubleshooting netatalk" section for information on the tools you can use for tracking down network problems.

## Setting up the netatalk server

The following steps provide a high-level overview of how to set up your netatalk server. (The sections that follow contain details on how to do these steps.)

- 1. **Start netatalk** — Like most Linux network services, netatalk can be set to start automatically from a start-up script, in this case `/etc/init.d/atalk`. (You can do some limited file sharing with the default configuration, as described in the next section.)
- 2. **Configure general settings** (`/etc/atalk/netatalk.conf` file) — Use the `netatalk.conf` file to add your own general netatalk server settings. The default settings for the general netatalk configuration are:
  - **Clients** — Up to 20 Mac clients can connect to your server at a time.
  - **AppleTalk host name** — Your computer's host name (type `hostname -s` to see it) is used as your computer's AppleTalk server host name.
  - **Authentication** — Netatalk will allow users to connect using a guest login (*nobody* user) with no password, a clear-text password, or an encrypted password (Diffie-Hellman style authentication).
  - **Guest user** — A guest user can connect without entering a password and access shared volumes that are open to the world. This guest user is assigned to the Linux *nobody* user name. (By default, no guest shares are set up.)
  - **Daemon processes** — Netatalk starts daemon processes to manage your AppleTalk network interface (atalkd daemon), start the AppleTalk print sharing service (papd daemon), and start the AppleTalk filing protocol (afpd daemon) for sharing volumes.
- 3. **Configure server settings** (*/etc/atalk/afpd.conf file*) — Configuring afpd.conf lets you set up specific settings for your netatalk server (you can even have multiple, virtual servers configured that each look different to the outside world). The contents of the afpd.conf file affect how the AppleTalk filing protocol daemon (afpd) shares its volumes with Mac clients.
- 4. **Set up users** — The netatalk server can rely on the Linux users you add to the computer (using clear-text passwords), then limit access to your shared volumes based on those permissions. Or, you can configure netatalk to use encrypted passwords to validate users.
- 5. **Share volumes** (*/etc/atalk/AppleVolumes.default file*) — When netatalk starts, each user with a valid Linux login to your computer, by default, access his or her own home directory as an AppleTalk share from a Mac client. You can (and probably will) have more shared volumes by configuring them in the AppleVolumes.default file.
- 6. **Securing shared volumes** — Netatalk can take advantage of Linux security features to protect shared volumes. You can secure volumes at the host, user, and file/directory level.
- 7. **Share printers** (*/etc/atalk/papd.conf file*) — Netatalk can share any printer you have connected to Linux (or otherwise configured locally) by adding a definition to the papd.conf file. No printers are shared until you add them.

As you work with your shared volumes and printers, you will find that maintenance issues arise from time to time. In particular, you should refer to the following sections:
"File/directory-level security" (for dealing with hidden attribute files and directories), "Sharing files with netatalk and Samba" (to share the same directories from netatalk and Samba), and "Troubleshooting netatalk" (for general troubleshooting tips).

### Starting netatalk

Start up netatalk as you would most Linux network services: from a start-up script. The netatalk script is called atalk (*/etc/init.d/atalk*). To turn it on, type the following as root user:

```
# chkconfig atalk on
```

The previous command causes netatalk to start the next time you reboot. To start it now, type:

```
# service atalk start
```

Here's what happens when you start the AppleTalk service:

- The AppleTalk daemon (atalkd) starts from the contents of the */etc/atalk/atalkd.conf* file.
- The papd daemon registers print services using the contents of the `/etc/atalk/papd.conf` file.
- The afpd daemon registers volumes from the contents of the `/etc/atalk/AppleVolumes.default` file (using settings from the `AppleVolumes.system` file).

To check that the netatalk service started properly, as root user type the following from any Linux system on the network (the output may take a minute or two to appear):

```
# nbplkup
toys:APPServer			65280.115:128
toys:netatalk			65280.115:4
toys:Workstation			65280.115:4
```

To check if your netatalk server is available from a Mac client, go to the Mac client and perform the appropriate procedure:

- **For a pre-Mac OS X client** — Click the Apple Chooser. From the Chooser window, click AppleShare. The netatalk server should appear in the "Select a file server" pane. Click on it and click OK, then use any valid user login and password from Linux to open that user's home directory.
- **For a Mac OS X client** — From the Finder bar, click Go, then Connect to server. Type the URL of the netatalk shared directory. For example, for the home directory on the computer named `toys` for the user named `chris`, you could type the following:

```
afp://toys/chris
```

If you can't find and open the netatalk server from your Mac, see the "Troubleshooting netatalk" section in this chapter for some suggestions.

## Defining general AppleTalk server settings

Settings in the `/etc/atalk/netatalk.conf` file define information related to the general operation of your netatalk server. Step 2 of "Setting up the netatalk server" describes the default settings in this file. The following code lines illustrate a few things you might want to change (as root user).

```
AFPD_MAX_CLIENTS=100
```

Instead of limiting the number of Mac clients who can simultaneously use your netatalk server to 20, you can use any number you like (100 is shown above). To change the zone and server name, you could change the following settings:

```
ATALK_ZONE=GSTREET
ATALK_NAME="History 101"
```

This example sets the zone name to GSTREET and the server name to History 101. To change how authentication is performed, you could use one of the following two AFPD_UAMLIST examples:

```
AFPD_UAMLIST="-U uams_guest.so"
AFPD_UAMLIST="-U uams_clrtxt.so"
```

The first example makes netatalk a guest-only server. The second line allows only valid users from the Linux system using clear-text passwords. The following line lets you change the guest user account:

```
AFPD_GUEST=nobody
```

You could change nobody to any valid user account on Linux, and that account will be used as your guest user. Other settings in the netatalk.conf file let you set which daemons run.

### Defining specific AppleTalk servers settings

Your netatalk server can appear as multiple file servers, each with different attributes. You can set up these "virtual" servers in the /etc/afpd.conf file. Within each file server entry, you name the server, and then assign a variety of options to set how it is accessed. A few nice examples of how to do this are shown as comments in the afpd.conf file itself:

```
"Guest Volume" -uamlist uams_guest.so -loginmsg "Welcome guest!"
"User Volume" -uamlist uams_clrtxt.so -port 12000
```

The "Guest Volume" example causes a "Welcome guest!" message to appear when a user logs into the server. Because it is a guest server (uams_guest.so), no password is required. In the "User Volume" example, clear-text passwords and valid user accounts are needed for the volume. The service is provided on port number 12000. Guest Volume and User Volume appear as the names of the two servers, respectively, in the Mac's chooser window.

If your Linux computer is a router/firewall, with one or more network interfaces connected to public networks, you should use the -ipaddr IPaddress option. With that option, you can restrict access to the netatalk server from a particular network interface (probably one that only allows access from your local LAN). There are more than 30 options listed in afpd.conf that you can consider.

### Setting up users

As mentioned earlier, the netatalk server (by default) allows users with valid user names and passwords to log in to the server with clear-text (unencrypted) passwords and gain access to (at least) their own home directories. See the "Securing netatalk volumes" section later to see how to set up the server to use encrypted passwords.
