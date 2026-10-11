Use the previous line with the following /etc/limits.conf examples since you have used the configuration argument to change the default of /etc/security/limits.conf:

+   - The following line uses pam_limits to restrict the core file size to 0KB for all users:
+       *          soft          core                0
+   - The next two lines use pam_limits to restrict the maximum number of processes to 20 and the number of logins to 4 for members of the staff group:
+       @staff     hard        nproc               20
+       @staff     hard        maxlogins           4

+   - The next line imposes a soft rss limit of 10000KB for username alice:
+       alice      soft        rss                 10000

# The pam_pwdb Module

The pam_pwdb module provides a generic interface to the Password Database library (pwdb). The use of the pam_pwdb module varies according to the management group in question:

Account When used as an account function, the pam_pwdb module establishes the status of the user's account and password. In the case of the password, pam_pwdb may offer advice to the user on changing their password, and it may even delay giving service to the user until they have established a new password.

Authentication When used as an authentication function, the pam_pwdb module determines under what conditions the password provided by the user should be used to authenticate them to a requested service.

Password When used as a password function, the pam_pwdb module updates the user's password. Using libpwdb, this module can move the user's password from one database to another.

Session When used as a session function, the pam_pwdb module logs the username and the service type to syslog. Messages are logged at the beginning and at the end of the user's session.

The pam_pwdb module is typically used in services like /etc/pam.d/login, and its syntax is as follows:

```
module_type control_flag pam_pwdb.so arguments
```

The arguments you can use with the pam_pwdb module vary according to the management group in question.