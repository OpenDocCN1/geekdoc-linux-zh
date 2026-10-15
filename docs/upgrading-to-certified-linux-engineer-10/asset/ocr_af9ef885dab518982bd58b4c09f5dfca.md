# Objective 1 Configure User Authentication with PAM

User authentication plays a central role in IT security. Linux uses PAM (Pluggable Authentication Modules) in the authentication process as a layer between users and applications. A Linux system administrator can use these modules to configure the way programs should authenticate users.

By providing system-wide access to applications through authentication modules, authentication does not have to be part of each application requiring authentication. The Pluggable Authentication Modules take care of that task for applications.

For example, when a user logs into a Linux system on a virtual terminal, a program called login is usually involved in this process.

Login requires a user's login name and the password. The password is encrypted and then compared with the encrypted password stored in an authentication database. If the encrypted passwords are identical, login grants the user access to the system by starting the user's login shell.

If other authentication procedures are used, such as smart cards, all programs that perform user authentication must be able to work together with these smart cards. Before PAM was introduced all applications that handle authentication, like login, FTP, or SSH, had to be extended to support a smart card reader.

PAM makes things easier. PAM creates a software level with clearly defined interfaces between applications (such as login) and the current authentication mechanism. Instead of modifying every program, a new PAM module can be enable authentication with a smart card reader. After adjusting the PAM configuration for an application this application can make use of this new authentication method.