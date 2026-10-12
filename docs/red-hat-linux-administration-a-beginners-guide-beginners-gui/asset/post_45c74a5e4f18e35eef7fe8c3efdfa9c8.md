
## Controlling Access to FTP

Being able to control who may and who may not enter your FTP server is a crucial aspect of server management. You may want to allow users with an account on the box to log in as themselves. You may want to allow only anonymous, password-less logins. Perhaps you want both. There are options to control whether new files can be uploaded or only downloads can be performed. You can even limit actions based on certain lists of users.

### Anonymous Access

Under the UNIX model, every process must have an owner. In the case of an anonymous FTP user, this owner should have minimal file access rights and only be able to see the files in the designated public FTP area. Even though this setup is taken care of by the **anonftp** package under Red Hat, it’s still something to keep in mind when deciding which options and permissions to set. Also keep in mind that so-called anonymous access still requests a username and password, but the server recognizes the username of **anonymous** or **ftp** as being special and will accept any password for them. Customarily, the user’s e-mail address is requested as the password on anonymous access, but no real validation is performed.

- **anonymous_enable** This is obviously the most important of the options related to an anonymous setup. The default for this option is “yes,” so you really only have to worry about it if you want to disable anonymous access.

- **anon_world_readable_only** This option defaults to “yes” under the assumption that from time to time the anonymous FTP user may own files that you don’t want the world to have access to. When enabled, anonymous users will only be allowed to download files that are world readable. Change the value to “no” if you want to allow downloading of all files readable by the FTP user.

![](img/ec2066d370d3af1a767664d36aa7ddfe_375_0.png)

### Ask the Expert

> **Q:** How can we ensure that anonymous users enter their real e-mail addresses?
>
> **A:** You cannot ensure that anonymous users enter their real e-mail addresses because FTP only provides authentication for users with accounts. Anonymous users can be truly anonymous. If you need gated access for users who do not have real accounts, you will probably need to use something fancier than FTP.

- **anon_upload_enable** This is set to “no” by default. If you change this to “yes” and also have the write_enable option set, anonymous users will be able to upload files. The anonymous FTP user must still have write permissions in the desired location.

- **anon_mkdir_write_enable** This will allow anonymous users to create new directories if the write_enable option is also on. The anonymous FTP user must have write permissions in the parent directory. The default is “no.”

- **anon_other_write_enable** This controls deleting and renaming of files by anonymous users. You probably don’t want to change this from its default value of “no.”

- **chown_uploads** This option will allow you to have all anonymous uploads automatically changed to be owned by a certain user. This can be useful for security.

- **chown_username** This is the user to whom files are chowned to if you enabled the previous option. The default is root, so you may want to change that to a dedicated user.

### Authenticated User Access

Here’s where we get into the issue of allowing users with accounts on the server to log in as themselves. The lack of general security in the FTP protocol means that the server usually tries to compensate with features like user ID remapping and chrooted jails. This makes configurations potentially trickier than you might expect.

- **local_enable** This is the primary option to allow logins from people with local accounts. You have to change this to “yes” to make most of the following options relevant.

- **guest_enable** This will remap all nonanonymous logins to a specified “guest” user account. This can be a useful security option for some configurations.

- **guest_username** This is the username to map as guest if you enable the previous option. The default is ftp.

- **userlist_enable** Turn this option to “yes” if you want to limit who can log in based on a list in a file. You can either allow only those names listed, or you can deny those listed, depending on the following option.

- **userlist_deny** This option is only consulted if the previous option is enabled. It defaults to “yes,” which will deny user accounts that are listed in the file. Changing this option to “no” reverses the meaning of the list so that only those listed can log in.

- **userlist_file** And this option specifies the file referred to by the preceding two options. The default is */etc/vsftpd.user_list*. It is instructive to at least examine the accounts that Red Hat has listed here by default.

### Configuring Host Access

While some FTP daemons will provide direct support for blocking certain hosts, the proper place for that kind of activity is in the access control files **hosts.allow** and **hosts.deny**. Place an entry in either or both of these files to adjust the access according to your needs. An example configuration might be:

```text
/etc/hosts.allow
vsftpd: LOCAL 10.1.42.0/24 *.my.domain.com
```

```text
/etc/hosts.deny
vsftpd: ALL
```

The access control files are very flexible, but if they don’t quite meet your needs for some reason, you can also adjust the settings in **xinetd.conf**. For more information on the **hosts.allow** and **hosts.deny** files, see Module 8.

## CRITICAL SKILL

### 11.4 Configuring a Virtual FTP Server

Even though the FTP protocol doesn’t support name-based virtual servers the way the Hypertext Transfer Protocol (HTTP) does, you can still set up multiple FTP servers on the same host so long as each server has its own IP address. To distinguish between the different “servers,” we’ll be taking advantage of **xinetd** once again. This section assumes that you have already configured an IP alias and fudged the Address Resolution Protocol (ARP) table correctly. (This is discussed later in this book in Part V, “Advanced Linux Networking.”) This quick jumpstart on the process assumes you have one Ethernet card and want to add a single virtual IP address:

- 1. Make sure your new IP address exists in both the local host table (**/etc/hosts**) and your DNS table. (In this example, we’ll call the host “earth.”)
