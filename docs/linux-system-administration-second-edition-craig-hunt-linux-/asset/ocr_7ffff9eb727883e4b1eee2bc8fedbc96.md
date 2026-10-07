$ sudo shutdown -r now

sudo first validates the user's identity by querying for a password. It thens the file /etc/sudoers to determine whether user has permission to execute a command as the specified user or as root if no other user is specified. The /etc/sudoers file looks like this:

```
# sudoers file.
# This file MUST be edited with the 'visudo' command as root.
# See the sudoers man page for the deails on how to write a sudoers file.
#
```

# # Host alias specification

# # User alias specification

# # Cmnd alias specification

```
# User privilege specification
root ALL=(ALL) ALL
someuser ALL=(ALL) ALL
```

If the user is listed in /etc/sudoers, a password prompt is issued. The referenced operation is performed and a five–minute timer will be set. During that five minutes, the authenticated user can perform sudo commands without re-authenticating.

sudo is a critical tool. Thanks to it, you can grant certain users and administrative staff access to perform some high–level tasks without actually giving them the password. (Of course, you'll do this only when the benefits of letting the user handle the tasks outweighs the potential risks. The user needs to be not only trustworthy but technically competent.) This tool is available on standard distributions of Linux and is available for most flavors of Unix. For more extensive descriptions of sudo, visit its home page at http://www.courtesan.com/sudo/man/sudo.html, and see Ramon Hantonen's Linux Security (Sybek, 2001).

# In Sum

This chapter has discussed many aspects of Linux system administration, but since the entire book is about administration, it has only scratched the surface. Use this chapter as a guide to future chapters. Next we will work through the installation process, using Red Hat Linux as a model.