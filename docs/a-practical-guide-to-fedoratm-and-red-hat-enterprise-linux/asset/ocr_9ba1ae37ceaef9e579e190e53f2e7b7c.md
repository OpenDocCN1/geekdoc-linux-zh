**deny_email_enable**

YES checks whether the password (email address) that an anonymous user enters is listed in `/etc/vsftpd/banned_emails` or another file specified by **banned_email_file**. If it is, the user is not allowed to log in on the system. NO does not perform this check. Using `firewall-cmd` (page 906) to block specific hosts is generally more productive than using this parameter.

Default: NO

**banned_email_file**

The name of the file consulted when **deny_email_enable** is set to YES.

Default: `/etc/vsftpd/banned_emails`

# The working directory and the chroot jail

When a user logs in on a **vsftpd** server, standard filesystem access permissions control which directories and files the user can access and how the user can access them. Three basic parameters control a user who is logged in on a **vsftpd** server:

+   * The user ID (UID)
+   * The initial working directory
+   * The root directory

By default, the **vsftpd** server sets the UID of a local user to that user's UID and sets the UID of an anonymous user to that of the user named **ftp**. A local user starts in her home directory and an anonymous user starts in `/var/ftp`.

By default, anonymous users are placed in a `chroot` jail for security; local users are not. For example, when an anonymous user logs in on a **vsftpd** server, his home directory is `/var/ftp`. All that user sees, however, is that his home directory is `/.` The user sees the directory at `/var/ftp/upload` as **/upload**. The user cannot see or work with, for example, the **/home**, **/usr/local**, or **/tmp** directory because the user is in a `chroot` jail. For more information refer to “Setting Up a `chroot` Jail” on page 487.

You can use the **chroot_local_user** parameter to put each local user in a `chroot` jail whose root is the user's home directory. You can use **chroot_list_enable** to put selected local users in `chroot` jails.

**chroot_list_enable**

Upon login, YES checks whether a local user is listed in `/etc/vsftpd/chroot_list` (page 737) or another file specified by **chroot_list_file**.

When a user is in the list and **chroot_local_user** is set to NO, the user is put in a `chroot` jail in his home directory. Only users listed in `/etc/vsftpd/chroot_list` are put in `chroot` jails.

When a user is in the list and **chroot_local_user** is set to YES, that user is not put in a `chroot` jail. Users not listed in `/etc/vsftpd/chroot_list` are put in `chroot` jails.

Default: NO