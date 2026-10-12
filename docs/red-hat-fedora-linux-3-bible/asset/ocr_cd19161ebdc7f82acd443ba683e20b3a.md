# # 936 Part IV: Fedora Network and Server Setup

Other settings in the *netatalk.conf* file let you set which daemons run.

# ## Defining specific AppleTalk servers settings

Your netatalk server can appear as multiple file servers, each with different attributes. You can set up these "virtual" servers in the */etc/atalk/afpd.conf* file. Within each file server entry, you name the server, and then assign a variety of options to set how it is accessed. A few examples of how to do this are shown as comments in the *afpd.conf* file itself:

```
"Guest Volume" -uamlist uams_guest.so -loginmsg "Welcome guest!"
"User Volume" -uamlist uam_clixtcl.so -port 12000
```

The "Guest Volume" example causes a "Welcome guest!" message to appear when a user logs into the server. Because it is a guest server (uams_guest.so), no password is required. In the "User Volume" example, clear-text passwords and valid user accounts are needed for the volume. The service is provided on port number 12000. Guest Volume and User Volume appear as the names of the two servers, respectively, in the Mac's chooser window.

If your Linux computer is a router, with one or more network interfaces connected to public networks, you should use the *-ipaddr IPaddress* option. With that option, you can restrict access to the netatalk server from a particular network interface (probably one that only allows access from your local LAN). There are more than 30 options listed in *afpd.conf* that you can consider.

# ## Setting up users

As mentioned earlier, the netatalk server (by default) allows users with valid user names and passwords to log in to the server with clear-text (unencrypted) passwords and gain access to (at least) their own home directories. See the "Securing netatalk volumes" section later in this chapter to see how to set up the server to use encrypted passwords.

# ## Sharing netatalk volumes

You use the *AppleVolumes.default* file to indicate which volumes from the netatalk server are made available to your Mac clients. This file is located in */etc/atalk/AppleVolumes.default*.

> NOTE: See the "File- and directory-level security" section for detailed information on hidden files and directories, as well as user and group permissions issues related to sharing volumes.

Look at the last line in the *AppleVolumes.default* file. The single title (-) on a line by itself tells the AppleTalk daemon to make all Linux home directories (usually in the */home* directory) available as AppleTalk shared directories. When a user logs into the netatalk server, the user's own home directory appears as an available shared directory. A user who chooses to open that directory has the same rights to change, add, and delete files that he has when logged in directly to Linux.