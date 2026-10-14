# Home Directory Options

When creating a new home directory for a user, or when modifying an existing user's home directory, Webmin can be customized to suit many different environments. The following options specify details about home directory creation and modification:

# Permissions on new home directories

New directories for users will be created with the permissions specified here. The default is 0755, which means the owner of the file can read, write, and execute files in the directory assuming permission on the file itself, while the group and all other users on the system, can read and execute within the directory. In a web hosting environment, this looseness is often necessary to permit the web server to have access to a user's document root. However, in most business environments, these permissions are unacceptably lax. A better choice would be 0700 or 0711. The former disallows all users, other than UID 0, from being able to list the contents of the directory or read anything within the directory, while the latter permits other users to change directory into the directory, but not necessarily to read or execute files within it. It is useful to permit other users to pass through the current directory to a directory within which is intended to be shared with other users.

# Copy files into new home directories from

When creating new UNIX users, it is customary to provide a base set of configuration files to set up sensible defaults for the shell, desktop settings, path and other environment variables, and any local configuration details that would make the user's life more convenient. For example, on a machine used primarily for development, it is likely that the CVSROOT environment variable will be set on login. Similarly, a desktop machine will have icons to make it easier for the user to locate the files they need to use in day-to-day work. This file is usually called /etc/skel, where skel is short for skeleton, but it can be any directory name.

# Automatic home directory base

Webmin can automatically set the home directory path for you if automatic directory creation is selected. This option allows you to specify the location of the home directory. There is rarely a good reason to stray from the tradition of using /home for this purpose.

# Automatic home directory style

In most environments, the traditional home directory naming scheme of /home/username is perfectly acceptable, but in some large-scale networks, the number of users would make managing such a directory cumbersome. So administrators have resorted to breaking down the username distribution in various ways to permit easier home directory maintenance. Webmin supports several such alternate name distributions, specifically: /home/u/username, /home/u/us/username, and /home/us/username.