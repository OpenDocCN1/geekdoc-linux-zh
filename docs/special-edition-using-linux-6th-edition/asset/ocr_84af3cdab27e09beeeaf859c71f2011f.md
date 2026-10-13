The problem is not the password, but the line in `/etc/pam.d/login` that calls `pam_security.so`. This line enables root to only login from those terminals listed in `/etc/security`. If you want to enable root to log using telnet (a uniformly bad idea), you’ll need to comment out or remove that line. One way around this restriction is to telnet in as an ordinary user and then use the `su` command to become root. This is just as bad as enabling a root login using telnet. A better way would be to install and use openssh, which encrypts the entire session, including the login.

*I need to upload some files as root, but I can’t log in.*

This is a very similar problem to the previous telnet problem. Again, this is not a good idea, but if you insist on doing it, you’ll need to do one of two things: Remove the `pam_list-file.so` line in `/etc/pam.d/ftp`, or remove root from the file `/etc/ftpusers`. A better idea would be to use scp to transfer the files using an encrypted channel where your root password is safe from prying eyes running tcpdump. You can transfer files to any server running sshd using the following command:

```
scp xferfile [user@]remotehost:/path/to/save/xferfile
```