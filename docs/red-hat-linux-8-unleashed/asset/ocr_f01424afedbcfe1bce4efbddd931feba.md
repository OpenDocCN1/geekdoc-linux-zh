This creates the /var/ftp directory and places necessary libraries and binaries in this directory structure, which is used by the FTP server.

# The FTP User

During the rpm installation, an FTP user was added to the /etc/passwd file. This user is not a normal user per se, but a name for anonymous FTP users. The FTP user entry in /etc/passwd looks like this

```
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
```

The FTP user, as discussed here, applies to anonymous FTP configurations and server setup. The RPM package creates an entry for the FTP user, but it doesn't set a default shell or create the /var/ftp directory.

Also, note that other Linux distributions use a different default directory, such as /usr/local/ftp, for FTP files and anonymous users.

This entry follows the standard /etc/passwd format: username, password, password, user id, group id, comment field, home directory, and shell.

To learn more about /etc/passwd, see the section "The Password File" in Chapter 9, "Managing Users."

Each of the items in this entry is separated by colons. In the preceding example, you can see that the Red Hat system hosting the server has the shadow-utils package installed because it has an x in the password field. The shadow password system is important because it adds an additional level of security to Red Hat Linux; the shadow password system normally is installed during the Red Hat Linux installation.

The FTP server software uses this account to assign permissions to users connecting to the server. By using a default shell of /sbin/nologin for anonymous FTP users versus /bin/bash or some other standard, interactive shell, an anonymous FTP user, will be unable to log in as a regular user. /sbin/nologin isn't a shell, but program usually assigned to an account that has been locked. As root inspection of the /etc/shadow file shows (see Listing 18.1), it's impossible to log into this account, denoted by the * as the password.

# LISTING 18.1 Shadow Password File ftp User Entry

```
# cat /etc/shadow
bin:*:11899:0:99999:7::
daemon:*:11899:0:99999:7::
adm:*:11899:0:99999:7::
```