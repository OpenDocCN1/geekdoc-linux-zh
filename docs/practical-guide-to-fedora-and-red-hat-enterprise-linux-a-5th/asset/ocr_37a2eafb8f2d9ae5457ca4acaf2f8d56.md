Use **userlist_file** to change the name of the file that this parameter consults. This parameter is checked only when **userlist_enable** is set to **YES**.
Default: **YES**

**userlist_file** The name of the file consulted when **userlist_enable** is set to **YES**.
Default: /etc/vsftpd/user_list

**local_enable** YES permits local users (users listed in /etc/passwd) to log in on the server.
Default: NO
Fedora/RHEL: YES

# **ANONYMOUS USERS**

**anonymous_enable**
YES allows anonymous logins.
Default: YES

**no_anon_password**
YES skips asking anonymous users for passwords.
Default: NO

**deny_email_enable**
YES checks whether the password (email address) that an anonymous user enters is listed in /etc/vsftpd/banned_emails or other file specified by **banned_email_file**. If it is, the user is not allowed to log in on the system. NO does not perform this check. Using **iptables** (page 819) to block specific hosts is generally more productive than using this parameter.
Default: NO

**banned_email_file**
The name of the file consulted when **deny_email_enable** is set to **YES**.
Default: /etc/vsftpd/banned_emails

# **WORKING DIRECTORY AND THE CHROOT JAIL**

When a user logs in on a **vsftpd** server, standard filesystem access permissions control which directories and files the user can access and how the user can access them. Three basic parameters control a user who is logged in on a **vsftpd** server:

+   - User ID (UID)
+   - Initial working directory
+   - Root directory

By default, the **vsftpd** server sets the user ID of a local user to that user's username and sets the user ID of an anonymous user to **ftp**. A local user starts in her home directory and an anonymous user starts in /var/ftp.