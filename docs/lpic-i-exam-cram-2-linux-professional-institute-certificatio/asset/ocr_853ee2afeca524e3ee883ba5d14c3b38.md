# # Setting Up a Simple Samba Server

To show how easy Samba is to configure, the next section is a quick setup of Samba to share a single directory for a user, including setting up the user for access. Follow these steps:

+   1. Edit the /smb.conf file and add the following share to the end of the file:

```
```
# A share usable only the user snuffy
[snuffydir]
    comment = a private share for snuffy
    path = /usr/share/snuffy
    valid users = snuffy
    public = no
    writable = yes
    printable = no
```
```

![](bbox=[0.08, 0.35, 0.18, 0.45])

The comment is just that—the path is a valid path that **snuffy** has access to, the valid users are **snuffy**, the **public** keyword keeps other users out of that directory, the **writable** keyword allows **snuffy** to change the files therein, and **printable** being set to no means that no print job will be accepted into the directory.

+   2. Save and exit the file.

+   3. Run testparm to check the file.

+   4. Start Samba with /etc/rc.d/init.d/smb start (on Red Hat).

+   5. Confirm the service's start.

+   6. Add the user snuffy with the following command:

```
```
useradd -m snuffy
```
```

+   7. Set the password for snuffy with the following command:

```
```
passwd snuffy
```
```

(Enter the password twice.)

+   8. Add the existing user to the Samba password files with the command shown here:

```
```
smbadduser snuffy:snuffy
```
```

(Enter the password twice.)

![](bbox=[0.08, 0.88, 0.18, 0.98])

The first instance of the name **snuffy** represents the Linux user **snuffy**; the second **snuffy** after the colon represents the Samba user or the connecting Windows client user.