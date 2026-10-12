
## Part IV: Fedora Network and Server Setup

Other settings in the *netatalk.conf* file let you set which daemons run.

### Defining specific AppleTalk servers settings

Your netatalk server can appear as multiple file servers, each with different attributes. You can set up these "virtual" servers in the */etc/atalk/afpd.conf* file. Within each file server entry, you name the server, and then assign a variety of options to set how it is accessed. A few examples of how to do this are shown as comments in the *afpd.conf* file itself:

```
"Guest Volume" -uamlist uams_guest.so -loginmsg "Welcome guest!"
"User Volume" -uamlist uam_clixtcl.so -port 12000
```

The "Guest Volume" example causes a "Welcome guest!" message to appear when a user logs into the server. Because it is a guest server (uams_guest.so), no password is required. In the "User Volume" example, clear-text passwords and valid user accounts are needed for the volume. The service is provided on port number 12000. Guest Volume and User Volume appear as the names of the two servers, respectively, in the Mac's chooser window.

If your Linux computer is a router, with one or more network interfaces connected to public networks, you should use the *-ipaddr IPaddress* option. With that option, you can restrict access to the netatalk server from a particular network interface (probably one that only allows access from your local LAN). There are more than 30 options listed in *afpd.conf* that you can consider.

### Setting up users

As mentioned earlier, the netatalk server (by default) allows users with valid user names and passwords to log in to the server with clear-text (unencrypted) passwords and gain access to (at least) their own home directories. See the "Securing netatalk volumes" section later in this chapter to see how to set up the server to use encrypted passwords.

### Sharing netatalk volumes

You use the *AppleVolumes.default* file to indicate which volumes from the netatalk server are made available to your Mac clients. This file is located in */etc/atalk/AppleVolumes.default*.

> NOTE: See the "File- and directory-level security" section for detailed information on hidden files and directories, as well as user and group permissions issues related to sharing volumes.

Look at the last line in the *AppleVolumes.default* file. The single tilde (~) on a line by itself tells the AppleTalk daemon to make all Linux home directories (usually in the */home* directory) available as AppleTalk shared directories. When a user logs into the netatalk server, the user's own home directory appears as an available shared directory. A user who chooses to open that directory has the same rights to change, add, and delete files that he has when logged in directly to Linux.

A common practice is to add the text “Home Directory” to the line that contains the single tilde (~) so that it appears as follows:

```
~  *Home Directory*
```

Sharing additional directories can be done by simply adding a full path name to the directory you want to share and the volume name you want to assign to it. For example:

```
/var/toyprojects “Linux Toys”
```

As you can see in this example, /var/toyprojects is shared under the name “Linux Toys”. The volume name is limited to 27 characters and cannot contain the ":" character. In this simple case, access permissions to the volume are determined by the user, host, and folder-level security that is set up for the volume (see the “Securing netatalk volumes” section for more information).

You can also add options directly to each listing in the AppleVolumes.default file. On the same line, after the path (/var/toyprojects) and volume name (“Linux Toys”) options as shown in the previous example, you can add some options. Here are a few options that might interest you (look inside the AppleVolumes.default file for others):

- **casefold:option** — Normally, when a shared volume appears on the Mac client's screen, file and directory names appear in upper- and lowercase as they exist on the Linux system. By replacing *option* in the casefold option with *tolower* or *toupper*, you can have lowercase or uppercase appear in both directions, respectively. Or, you can have case translated (*xlatelower* or *xlatupper*) to set what the client sees.
- **allow:users/@groups** or **deny:users/@groups** — You could add specific users or groups to an *allow* or *deny* option to have those users or groups allowed or denied access to the shared *volume*. (Separate each with a comma; indicate a group with an @ sign.)
- **password:pwd** — Replace *pwd* with a password (up to eight characters) to define a password that is specific to the *volume*.
- **rolist:users/@groups** or **rwlist:users/@groups** — Use *rolist* or *rwlist* options to allow read-only or read/write access, respectively, to the users or groups you add to the list. (Separate each with a comma; indicate a group with an @ sign.)

By opening these shared volumes and creating files and folders in them, Mac clients automatically create some files and folders that are invisible to the Mac client. These files and folders hold resource fork information and other features that would not normally be in a Linux file system. The “File- and directory-level security” section describes these files and folders.

> **NOTE:** Although most of the files and folders described in the following section are invisible to Mac clients, if you share the same directories using Samba or some Linux file-sharing feature (such as NFS), they will be visible. You can use the veto feature of Samba to hide these files from Windows users.

## Securing netatalk volumes

Some Linux and netatalk features can be used to secure your volumes from unwanted access or misuse. The following sections describe how to protect your netatalk servers at the user, host, and file and directory levels.

### User-level security

When you create a shared volume (in AppleVolumes.default), you can indicate which users can access that volume. Users can be authenticated using clear-text passwords (to log in to their basic Linux user accounts) or by setting up a special encrypted password file using netatalk.

Users can be assigned to particular volumes when you define those volumes in the AppleVolumes.default file as described earlier. Here’s an example where the users mike and jojo and anyone in the group wheel are allowed access to a volume:

```
/var/homework "History homework" allow:mike,jojo,@wheel
```

To use the default clear-text passwords, you need only set up user accounts as you normally would in Linux (see Chapter 11). However, to use encrypted passwords for users (on a server configured to use encrypted passwords at the afpd.conf file as described earlier), you must create an AppleTalk password file (/etc/afpap/afppasswd). As root, type the following:

```
# afppasswd -c
```

This command gathers all regular users (UID 500 and above) and the guest user (nobody) and adds them to the afppasswd file. After you create afppasswd initially, you can later add individual users manually to that file (provided they also have valid Linux accounts).

Next, you need to add proper passwords for each of the users that will be allowed access to your netatalk shares. For example:

```
# afppasswd -a jake
Enter NEW APP password: ********
Enter NEW APP password again: ********
```

Issues related to choosing a good password (see Chapter 14) are true for setting AppleTalk passwords as well. If the passwords match, the user will be able to log in using the assigned user name and password when he tries to mount the AppleTalk volume from the netatalk server, provided the netatalk service is using encrypted authentication (uams_dhx.so).

### Host-level security

You can restrict which computers on your network have access to your netatalk services using the /etc/hosts.allow and /etc/hosts.deny files. These files are described in the “Using TCP wrappers” section of Chapter 14. These are the same files you use to allow or restrict access to other Linux networking services.
