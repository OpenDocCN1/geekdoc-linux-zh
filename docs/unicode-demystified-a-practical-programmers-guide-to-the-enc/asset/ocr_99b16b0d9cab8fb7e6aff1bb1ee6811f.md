the techniques of authenticating users stay the same from application to application. PAM permits a system administrator to change the authentication mechanism for a given application without touching the application.

PAM provides authentication for a variety of system-entry services (login, ftp, and so on). You can take advantage of PAM's ability to authenticate system-entry services with different authentication mechanisms, such as RSA, DCE, Kerberos, and smart cards.

From login using us su to shutting the system down, whenever you are asked for a password (or not asked for a password because the system trusts that you are who you say you are), PAM makes it possible for systems administrators to configure the authentication process and makes the configuration process exactly the same for all applications that PAM use to do their authentication.

The configuration files stored in /etc/pam.d describe the authentication procedure for each application. These files usually have names that are the same as similar to the name of the application they configure. For example, authentication for login is configured in /etc/pam.d/login. The name of the file is the name of the PAM service that the files configure. Occasionally one file may serve two programs.

# Do Not Lock Yourself Out of Your System

Editing PAM configuration files correctly takes care and attention. It is easy to lock yourself out of your computer with a single mistake. To avoid this type of problem, always keep backup copies of the PAM files you edit, test every change thoroughly, and make sure that you can still log in once the change is installed. Keep a Superuser session open until you are done. When a change fails and you cannot log in, use the Superuser to replace the newly edited files with your backup copies.

PAM warns you about any errors it encounters, logging them to the /var/log/messages or /var/log/secure files. Look inside these files if you are trying to figure out why a changed PAM file is not working properly. In order to prevent possibly giving unnecessary information to a malicious user, PAM sends error messages to a file rather than to the screen.

There is no relationship between PAM services and the /etc/services files. The name of the PAM service is an arbitrary string that each application gives to PAM; PAM then looks up the configuration file with that name and uses it to control how it authenticates. There is no central registry of PAM service