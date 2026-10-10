
As you can see in this example, `/var/toyprojects` is shared under the name "Linux Toys." The volume name is limited to 27 characters and cannot contain the ":" character. In this simple case, access permissions to the volume are determined by the user, host, and folder-level security that is set up for the volume (see the “Securing netatalk volumes” section for more information).

You can also add options directly to each listing in the `AppleVolumes.default` file. On the same line, after the path (`/var/toyprojects`) and volume name (“Linux Toys”) options as shown in the previous example, you can add some options. Here are a few options that might interest you (look inside the `AppleVolumes.default` file for others):

- `casefold:option` — Normally, when a shared volume appears on the Mac client’s screen, file and directory names appear in upper- and lowercase as they exist on the Linux system. By replacing `option` in the casefold option with `tolower` or `toupper`, you can have lowercase or uppercase appear in both directions, respectively. Or, you could have case translated (`xlatelower` or `xlateupper`) to set what the client sees.
- `allow:users/@groups` or `deny:users/@groups` — You could add specific users or groups to an `allow` or `deny` option to have those users or groups allowed or denied access to the shared `volume`. (Separate each with a comma; indicate a group with an `@` sign.)
- `password:pwd` — Replace `pwd` with a password (up to eight characters) to define a password that is specific to the volume.
- `rolist:users/@groups` or `rwlist:users/@groups` — Use `rolist` or `rwlist` options to allow read-only or read/write access, respectively, to the users or groups you add to the list. (Separate each with a comma; indicate a group with an `@` sign.)

By opening these shared volumes and creating files and folders in them, Mac clients automatically create some files and folders that are invisible to the Mac client. These files and folders hold resource fork information and other features that would not normally be in a Linux file system. The “File- and directory-level security” section describes these files and folders.

> **NOTE:** Although most of the files and folders described in the following section are invisible to Mac clients, if you share the same directories using Samba or some Linux file-sharing feature (such as NFS), they will be visible. You can use the `veto files` feature of Samba to hide these files from Windows users.

## Securing netatalk volumes

Some Linux and netatalk features can be used to secure your volumes from unwanted access or misuse. The following sections describe how to protect your netatalk servers at the user, host, and file and directory levels.

### User-level security

When you create a shared volume (in AppleVolumes.default), you can indicate which users can access that volume. Users can be authenticated using clear-text passwords (to log in to their basic Linux user accounts) or by setting up a special encrypted password file using netatalk.

Users can be assigned to particular volumes when they define those volumes in the AppleVolumes.default file as described earlier. Here’s an example where the users mike and jojo and anyone in the group wheel are allowed access to a volume:

```
/var/homework "History homework" allow:mike,jojo,@wheel
```

To use the default clear-text passwords, you need only set up user accounts as you normally would in Linux (see Chapter 11). However, to use encrypted passwords for users (on a server configured to use encrypted passwords in the afpd.conf file as described earlier), you must create an AppleTalk password file (/etc/atalK/afppasswd). As root, type the following:

```
# afppasswd -c
```

This command gathers all regular users (UID 100 and above) and the guest user (nobody) and adds them to the afppasswd file.

Next, you need to add proper passwords for each of the users just added to the afppasswd file that will be allowed access to your netatalk shares. For example:

```
# afppasswd jake
Enter NEW AFP password: ********
Enter NEW AFP password again: ********
```

After you create afppasswd initially, you can later add individual users manually to that file (provided they also have valid Linux accounts). Do that using -a option to afppasswd:

```
# afppasswd -a cindy
Enter NEW AFP password: ********
Enter NEW AFP password again: ********
```

Issues related to choosing a good password (see Chapter 14) are true for setting AppleTalk passwords as well. If the passwords match, the user will be able to log in using the assigned user name and password when he tries to mount the AppleTalk volume from the netatalk server, provided the netatalk service is using encrypted authentication (uams_dxh.so).

### Host-level security

You can restrict which computers on your network have access to your netatalk services using the /etc/hosts.allow and /etc/hosts.deny files. These files are described in the “Using TCP wrappers” section of Chapter 14. These are the same files you use to allow or restrict access to other Linux networking services.

The following is an example of an entry in the hosts.allow file.

```
ALL:.linuxtoys.com EXCEPT abc.linuxtoys.com
```

This example allows access to netatalk (and all other services) from all computers in the linuxtoys.com domain except for the computer named abc.linuxtoys.com. See Chapter 14 for details about other ways to indicate services (instead of ALL) and hosts.

## File- and directory-level security

Netatalk creates hidden files and directories to handle Mac features that are not in Linux. Understanding those files and directories and working with standard Linux ownership and permissions are the best ways to refine access to the AppleTalk volumes you share.

### Understanding hidden Mac files and directories

Netatalk creates special files and directories that you can’t see from the Mac Finder. Because these files begin with a dot (.), they are hidden from normal directory listings (ls) in Linux as well. The following descriptions should help you understand these files and directories.

> **NOTE:** To see hidden files from a folder window (from the GNOME desktop), click Edit → Preferences. Then from the Views tab, select the “Show hidden and backup files” check box. Type **ls -a** to see them from a Terminal window.

- **`.AppleDouble`** — Every directory within your shared netatalk volume contains a `.AppleDouble` directory. This directory is created automatically as soon as you create a file or directory from a Mac client on the netatalk server. Within this directory are separate files representing attributes of each file in the associated directory. For example, creating a text file in `/var/toyprojects` called `mytext.txt` would create a file called `/var/toyprojects/.AppleDouble/mytext.txt` that contained attributes about that file.

You can create an Icon directory within any `.AppleDouble` directory for a shared volume (`/var/toyprojects/.AppleDouble/Icon` for example), enabling you to add custom icons to the shared volume. Permissions of those directories must be open to writing (for anyone you want to be able to add and change icons), and reading (to anyone you want to allow to see icons).

- **`.AppleDouble/.Parent`** — This directory within each `.AppleDouble` directory contains information about the shared directory.
- **`.AppleDesktop`** — For each shared volume, this directory is located in the top-level directory. This directory contains information about the applications that created the data stored on the volumes and the icons used to represent that data.
- **Network Trash Folder** — This folder, in the top-level shared directory, holds deleted files from the client. (Note spaces in the directory name, which must be preceded with a backspace to access the folder from the Linux shell.)
- **Temporary Items** — Some applications need this folder (located in the top-level directory) to create temporary files.

Other directories may also appear because applications that work on files in a volume need special directories to get their work done.

### Setting file and directory permissions

Permissions on shared netatalk volumes tend to be more wide open than would typically be the case on shared Linux directories in order to match the expectations that Mac users generally have about permissions.

In particular, the set-GID (group) bit is often turned on for directories. By using the set GID feature, any file or directory created in the directory would be owned by the associated group. For example, follow these steps as root user from the shell (creating any directory name you want to share):

```
# mkdir /var/toyprojects
# chown chris /var/toyprojects
# chgrp toypgroup /var/toyprojects
# chmod 2775 /var/toyprojects
# ls -ld /var/toyprojects
drwxrwxr-x 2 chris toypgroup 4096 Mar 16 13:32 /var/toyprojects
```

In this example, I prepared a directory to be shared by netatalk called /var/toyprojects. I made the owner of the directory the user chris (use your own user name). I created a group (see Chapter 11 for creating groups) and called it toypgroup. Then I set the permission to 2775 on the directory, which means that the group set-GID bit is on (2), the owner (chris) has full read/write/execute permission (7), the group (toypgroup) has full read/write/execute permission (7), and other has only read and execute permissions (5).

Turning on the group set-GID bit causes all files and directories created in /var/toyprojects (and its subdirectories) to be assigned to the toypgroup group, regardless of who created it. Because I set group permissions wide open (7), anything created in /var/toyprojects and its subdirectories will be under the complete control of anyone assigned to toypgroup. This is a nice technique for sharing files in a group project.

After the top-level directory is created, netatalk will create the files and directories it needs (such as .AppleDouble and Network Trash Folder) as the Mac clients add files and folders. Netatalk should also propagate the correct permissions to those items.

Here are some tips about setting permissions:

- A user must have write permission to the .AppleDesktop directory (and subdirectories) to create an application in a shared directory.
