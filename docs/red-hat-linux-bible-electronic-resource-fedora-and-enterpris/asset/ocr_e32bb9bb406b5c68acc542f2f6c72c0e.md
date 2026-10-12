+   - `password:pwd` — Replace `pwd` with a password (up to eight characters) to define a password that is specific to the volume.
+   - `rolist:users/@groups` or `wrolist:users/@groups` — Use `rolist` or `wrolist` options to allow read-only or read/write access, respectively, to the users or groups you add to the list. (Separate each with a comma; indicate a group with an @ sign.)

By opening these shared volumes and creating files and folders in them, Mac clients automatically create some files and folders that are invisible to the Mac client. These files and folders hold resource fork information and other features that would not normally be in a Linux file system. The "File/directory-level security" section describes these files and folders.

> NOTE: Although most of the files and folders described below are invisible to Mac clients, if you share the same directories using Samba or some Linux file-sharing feature (such as NFS), they will be visible. You can use the veto feature of Samba to hide these files from Windows users.

# Securing netatalk volumes

Some Linux and netatalk features can be used to secure your volumes from unwanted access or misuse. The following sections describe how to protect your netatalk servers at the user, host, and file/directory levels.

# User-level security

When you create a shared volume (in `AppleVolumes.default`), you can indicate which users can access that volume. Users can be authenticated using clear-text passwords (to log in to their basic Linux user accounts) or by setting up a special encrypted password file using netatalk.

Users can be assigned to particular volumes when you define those volumes in the `AppleVolumes.default` file as described earlier. Here’s an example where the users *mike* and *jojo* and anyone in the group *wheel* are allowed access to a volume:

```
/var/homework "History homework" allow:mike,jojo,@wheel
```

To use the default clear-text passwords, you need only set up user accounts as you normally would in Linux (see Chapter 11). However, to use encrypted passwords for users (on a server configured to use encrypted passwords in the `afpd.conf` file as described earlier), you must create an AppleTalk password file (`/etc/atalc/afppasswd`). As root, type the following:

```
# afppasswd -c
```

This command gathers all regular users (UID 500 and above) and the guest user (*nobody*) and adds them to the `afppasswd` file. After you create `afppasswd` initially, you can later add individual users manually to that file (provided they also have valid Linux accounts).

Next, you need to add proper passwords for each of the users that will be allowed access to your netatalk shares. For example: