Next comes the CD directory search path. With this option, you can configure any number of directories that can be in the search path. For example, if a client enters cd bin, and there is no bin directory in the current directory, then the server will check the directories in the search path. If the directory requested exists in one of those directories, the client will be directed there.

# Anonymous FTP

WU-FTPD provides a number of capabilities for serving anonymous (i.e., non-authenticated) users. And anonymous user generally has very limited capabilities on the server, and is often unable to upload files, or modify any content on the server. This page provides access to many of the features related to anonymous users on your FTP server.

# Anonymous FTP root directories

This option allows you to configure the root directory for anonymous users of a given class. So setting this to /home/ftp for the all class, will cause the server to chroot to the directory specified for any anonymous user. The initial directory (somewhere above the chrooted directory) will then be the home directory indicated in /etc/passwd for the user ftp. Using this option, it becomes possible for local network users to be chrooted to a different directory than users from the Internet, for example. This option configures the anonymous-root directive.

# Guest root directories

This option, much like the previous option, configures the chroot behavior of the server. In this case, however, it configures for guest users who have logged in with a valid user name and password. So, it is possible to set the chroot environment to /home, causing users to be unable to traverse the directory tree below that point. The initial working directory, unless otherwise specified, will be the users home directory specified in the /etc/passwd. This option configures the guest-root directive.

# Unix groups for anonymous users

Here you may configure the default UNIX group whose permissions will apply to anonymous users of a given class. This option configures the autogroup directive.

# Anonymous FTP password check

The server always performs a user name and password authentication check, before permitting access. The convention is to accept a blank user name, and the valid email address of the user. Here you can configure how strict the checking of the given email address is, and whether to issue a warning, but still allow the login, or deny access, if the email address is invalid for some reason. This option configures the passwd-check directive.