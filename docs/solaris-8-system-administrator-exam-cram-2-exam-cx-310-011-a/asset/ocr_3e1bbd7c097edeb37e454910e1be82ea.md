# Initialization Files

Several initialization (or startup) files are associated with each user account home directory (identified by the **$HOME** environment parameter). These files specify commands to be executed when the associated event occurs. Depending on the login shell being used, a login initialization file, a shell startup file, or a logout file can exist. Table 6.5 lists the various initialization files.

| File | sh | csh | ksh |
|---|---|---|---|
| Login initialization file | `$HOME/.profile` | `$HOME/.login` | `$HOME/.profile` |
| Shell startup file | N/A | `$HOME/.cshrc` | User-defined |
| Logout file | N/A | `$HOME/.logout` | N/A |

Commands in the login initialization file are executed when the user logs in. All three common shells provide a login initialization file. Commands in the shell startup file are executed whenever the logged-in user starts a shell. Both csh and ksh provide this capability. The **ENV** parameter is used to define the name of the ksh shell startup initialization file. Only csh provides a file for automatic execution of commands when a user logs out.

![](bbox=[0.148, 0.561, 0.244, 0.63])

It is important to know the names of the initialization files and their uses for the Bourne, C, and Korn shells.

# The System Profile

For user accounts that use the Bourne (sh) or Korn shell (ksh) as a login shell, commands in the system profile are executed before the user’s login initialization file. This file is named /etc/profile and, when executed, it sets a default terminal type (TERM) and then calls **umask(1)** to set the default file permission mask to 022. If the user’s home directory does not include a file named .hushlogin, the user’s storage quota is displayed by using **quota(1M)**, the message of the day (if any) is displayed, and a notification message is displayed if new e-mail has arrived for the user.

The following example shows the default contents of /etc/profile for a Solaris 8 system: