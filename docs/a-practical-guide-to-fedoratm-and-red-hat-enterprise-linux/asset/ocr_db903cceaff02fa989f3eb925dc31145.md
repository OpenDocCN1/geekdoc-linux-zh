max_per_ip Specifies the maximum number of clients from the same IP address. Zero (0) indicates unlimited clients from the same IP address.
Default: 0

# LOGGING IN

Three classes of users can log in on a vsftpd server: anonymous, local, and guest. The guest user is rarely used and is not covered in this chapter. A local user logs in using his system username and password. An anonymous user logs in using **anonymous** or **ftp** and his email address as a password. You can control whether each of these classes of users can log in on the server and what they can do once they log in. You can also specify what a local user can do on a per-user basis; for more information refer to user_config_dir on page 736.

# LOCAL USERS

userlist_enable The */etc/vsftpd/user_list* file (page 737), or another file specified by userlist_file, contains a list of zero or more users. YES consults this list and takes action based on **userlist_deny**, either granting or denying users in the list permission to log in on the server. To prevent the transmission of cleartext passwords, access is denied immediately after the user enters her username. NO does not consult the list. Set to NO for a more secure system.
Default: NO
Fedora/RHEL: YES

userlist_deny YES prevents users listed in */etc/vsftpd/user_list* (page 737) from logging in on the server. NO allows *only* users listed in */etc/vsftpd/user_list* to log in on the server. Use **userlist_file** to change the name of the file that this parameter consults. This parameter is checked only when **userlist_enable** is set to YES.
Default: YES

userlist_file The name of the file consulted when **userlist_enable** is set to YES.
Default: */etc/vsftpd/user_list*

local_enable YES permits local users (users listed in */etc/passwd*) to log in on the server.
Default: NO
Fedora/RHEL: YES

# ANONYMOUS USERS

anonymous_enable YES allows anonymous logins. NO disables anonymous logins.
Default: YES

no_anon_password YES skips asking anonymous users for passwords.
Default: NO